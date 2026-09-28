---
layout: Conceptual
title: Azure Single Sign Out SAML Protocol - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/single-sign-out-saml-protocol
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This article describes the Single Sign-Out SAML Protocol in Microsoft Entra ID
manager: pmwongera
ms.custom: 
ms.date: 2024-04-10T00:00:00.0000000Z
ms.reviewer: 
ms.topic: reference
locale: en-us
document_id: 76d4eac0-25d3-b5d5-f58e-cdd1024f32b4
document_version_independent_id: 7771f280-3701-4f88-cb9f-add968d494de
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/single-sign-out-saml-protocol.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/single-sign-out-saml-protocol
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/single-sign-out-saml-protocol.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7fda2367-36b5-9042-6d83-448b7996aefb
---

# Azure Single Sign Out SAML Protocol - Microsoft identity platform | Microsoft Learn

Microsoft Entra ID supports the SAML 2.0 web browser single sign-out profile. For single sign-out to work correctly, the **LogoutURL** for the application must be explicitly registered with Microsoft Entra ID during application registration.

If the app is [added to the Azure App Gallery](../identity/enterprise-apps/v2-howto-app-gallery-listing) then this value can be set by default. Otherwise, the value must be determined and set by the person adding the app to their Microsoft Entra tenant. Microsoft Entra ID uses the **LogoutURL** to redirect users after they're signed out. Microsoft Entra ID supports redirect binding (HTTP GET), and not HTTP POST binding.

The following diagram shows the workflow of the Microsoft Entra single sign-out process.

[![Screenshot of the Microsoft Entra Single Sign Out Workflow.](media/single-sign-out-saml-protocol/saml-single-sign-out-workflow.png)](media/single-sign-out-saml-protocol/saml-single-sign-out-workflow.png#lightbox)

## LogoutRequest

The cloud service sends a `LogoutRequest` message to Microsoft Entra ID to indicate that a session has been terminated. The following excerpt shows a sample `LogoutRequest` element.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

The `LogoutRequest` element sent to Microsoft Entra ID requires the following attributes:

- `ID` - This identifies the sign-out request. The value of `ID` shouldn't begin with a number. The typical practice is to append **id** to the string representation of a GUID.
- `Version` - Set the value of this element to **2.0**. This value is required.
- `IssueInstant` - This is a `DateTime` string with a Coordinate Universal Time (UTC) value and [round-trip format ("o")](/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings). Microsoft Entra ID expects a value of this type, but doesn't enforce it.

Per section 3.7 of the [SAML 2.0 core specification](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf), there can be multiple participants (other applications) in a session besides your application. If one of the other participants sends a `LogoutRequest` to the Microsoft identity platform (the session authority), it will send a `LogoutRequest` back to all the session participants except the participant who sent the initial `LogoutRequest`. If another participant simultaneously initiated sign-out, there would be a race to see which `LogoutRequest` reaches Microsoft identity platform first. Therefore, an application should always be prepared to handle a `LogoutRequest`.

### Issuer

The `Issuer` element in a `LogoutRequest` must exactly match one of the **ServicePrincipalNames** in the cloud service in Microsoft Entra ID. Typically, this is set to the **App ID URI** that is specified during application registration.

### NameID

The value of the `NameID` element must exactly match the `NameID` of the user that is being signed out.

Note

During SAML logout request, the `NameID` value is not considered by Microsoft Entra ID. If a single user session is active, Microsoft Entra ID will automatically select that session and the SAML logout will proceed. If multiple user sessions are active, Microsoft Entra ID will enumerate the active sessions for user selection. After user selection, the SAML logout will proceed.

## LogoutResponse

Microsoft Entra ID sends a `LogoutResponse` in response to a `LogoutRequest` element. The following excerpt shows a sample `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>

```

Microsoft Entra ID sets the `ID`, `Version` and `IssueInstant` values in the `LogoutResponse` element. It also sets the `InResponseTo` element to the value of the `ID` attribute of the `LogoutRequest` that elicited the response.

### Issuer

Microsoft Entra ID sets this value to `https://login.microsoftonline.com/<TenantIdGUID>/` where &lt;TenantIdGUID&gt; is the tenant ID of the Microsoft Entra tenant.

To correctly identify the issuer element, use the value `https://login.microsoftonline.com/<TenantIdGUID>/` as shown in the sample LogoutResponse. This URL format identifies the Microsoft Entra tenant as the issuer, representing the authority responsible for issuing the response.

### Status

Microsoft Entra ID uses the `StatusCode` element in the `Status` element to indicate the success or failure of sign-out. When the sign-out attempt fails, the `StatusCode` element can also contain custom error messages.