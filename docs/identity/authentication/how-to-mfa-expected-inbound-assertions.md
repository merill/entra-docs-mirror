---
layout: Conceptual
title: Satisfy Microsoft Entra ID multifactor authentication (MFA) controls with MFA claims from a federated IdP - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-mfa-expected-inbound-assertions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Explains Microsoft Entra ID multifactor authentication (MFA) SAML/WSFed assertions.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: bozbayburtlu
locale: en-us
document_id: 1b95d597-c0af-5996-363f-9a7f98f94ec5
document_version_independent_id: 1b95d597-c0af-5996-363f-9a7f98f94ec5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-mfa-expected-inbound-assertions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-mfa-expected-inbound-assertions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-mfa-expected-inbound-assertions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 64cd2f16-5966-422c-66ae-6fb95d66729a
---

# Satisfy Microsoft Entra ID multifactor authentication (MFA) controls with MFA claims from a federated IdP - Microsoft Entra ID | Microsoft Learn

This document outlines the assertions Microsoft Entra ID requires from a [federated identity provider (IdP)](../hybrid/connect/whatis-fed) to honor configured [federatedIdpMfaBehaviour](/en-us/graph/api/domain-post-federationconfiguration#federatedidpmfabehavior-values) values of acceptIfMfaDoneByFederatedIdp and enforceMfaByFederatedIdp for Security Assertions Markup Language (SAML) and WS-Fed federation.

Tip

Configuring Microsoft Entra ID with a federated IdP is **optional**. Microsoft Entra recommends [authentication methods](overview-authentication) available in Microsoft Entra ID.

- Microsoft Entra ID includes support for authentication methods previously only available via a federated IdP such as certificate/smartcards with [Entra Certificate Based Authentication](concept-certificate-based-authentication)
- Microsoft Entra ID includes support for integrating 3rd party MFA providers with [External Authentication Methods](how-to-authentication-external-method-manage)
- Applications integrated with a federated IdP can be [integrated directly with Microsoft Entra ID](/en-us/entra/architecture/migration-best-practices)

## Using WS-Fed or SAML 1.1 federated IdP

When an admin optionally configures their Microsoft Entra ID tenant to use a [federated IdP](../hybrid/connect/whatis-fed) using WS-Fed federation, Microsoft Entra redirects to IdP for authentication and expect a response in the form of a Request Security Token Response (RSTR) containing a SAML 1.1 assertion. If configured to do so, Microsoft Entra honors MFA done by the IdP if one of the following two claims is present:

- `http://schemas.microsoft.com/claims/multipleauthn`
- `http://schemas.microsoft.com/claims/wiaormultiauthn`

They can be included in the assertion as part of the `AuthenticationStatement` element. For example:

```xml
 <saml:AuthenticationStatement
    AuthenticationMethod="http://schemas.microsoft.com/claims/multipleauthn" ..>
    <saml:Subject> ... </saml:Subject>
</saml:AuthenticationStatement>
```

Or they can be included in the assertion as part of the `AttributeStatement` elements. For example:

```xml
<saml:AttributeStatement>
  <saml:Attribute AttributeName="authenticationmethod" AttributeNamespace="http://schemas.microsoft.com/ws/2008/06/identity/claims">
       <saml:AttributeValue>...</saml:AttributeValue> 
      <saml:AttributeValue>http://schemas.microsoft.com/claims/multipleauthn</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

### Using sign-in frequency and session control Conditional Access policies with WS-Fed or SAML 1.1

[Sign-in frequency](../conditional-access/concept-conditional-access-session#sign-in-frequency) uses UserAuthenticationInstant (SAML assertion `http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant`), which is AuthInstant of first factor authentication using password for SAML1.1/WS-Fed.

## Using SAML 2.0 federated IdP

When an admin optionally configures their Microsoft Entra ID tenant to use a [federated IdP](../hybrid/connect/whatis-fed) using [SAMLP/SAML 2.0](../hybrid/connect/how-to-connect-fed-saml-idp) federation, Microsoft Entra will redirect to the IdP for authentication, and expect a response that contains a SAML 2.0 assertion. The inbound MFA assertions must be present in the `AuthnContext` element of the `AuthnStatement`.

```xml
<AuthnStatement AuthnInstant="2024-11-22T18:48:07.547Z">
    <AuthnContext>
        <AuthnContextClassRef>http://schemas.microsoft.com/claims/multipleauthn</AuthnContextClassRef>
    </AuthnContext>
</AuthnStatement>
```

As a result, for inbound MFA assertions to be processed by Microsoft Entra, they **must** be present in the `AuthnContext` element of the `AuthnStatement`. Only one method can be presented in this manner.

### Using sign-in frequency and session control Conditional Access policies with SAML 2.0

[Sign-in frequency](../conditional-access/concept-conditional-access-session#sign-in-frequency) uses AuthInstant of either MFA or First Factor auth provided in the `AuthnStatement`. Any assertions shared in the `AttributeReference` section of the payload are ignored, including `http://schemas.microsoft.com/ws/2017/04/identity/claims/multifactorauthenticationinstant`.