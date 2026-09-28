---
layout: Conceptual
title: Microsoft Entra federation metadata - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/federation-metadata
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This article describes the federation metadata document that Microsoft Entra ID publishes for services that accept Microsoft Entra tokens.
manager: pmwongera
ms.custom: 
ms.date: 2024-10-01T00:00:00.0000000Z
ms.reviewer: ludwignick
ms.topic: concept-article
locale: en-us
document_id: a14a5b9b-be67-bdd5-cbcf-368f5c64c5d6
document_version_independent_id: f9bdda7e-ed83-00e0-8055-169f9bcab5d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/federation-metadata.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/federation-metadata
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/federation-metadata.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: b308c2f1-fd8c-cb05-bee9-40e32a330d7a
---

# Microsoft Entra federation metadata - Microsoft identity platform | Microsoft Learn

Microsoft Entra ID publishes a federation metadata document for services that are configured to accept the security tokens that Microsoft Entra ID issues. The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](https://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](https://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## Tenant-specific and tenant-independent metadata endpoints

Microsoft Entra ID publishes tenant-specific and tenant-independent endpoints.

Tenant-specific endpoints are designed for a particular tenant. The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information. Applications that restrict access to a single tenant use tenant-specific endpoints.

Tenant-independent endpoints provide information that is common to all Microsoft Entra tenants. This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants. Tenant-independent endpoints are recommended for multitenant applications, since they are not associated with any particular tenant.

## Federation metadata endpoints

Microsoft Entra ID publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:

- A registered domain name of a Microsoft Entra tenant, such as: `contoso.onmicrosoft.com`.
- The immutable tenant ID of the domain, such as `aaaabbbb-0000-cccc-1111-dddd2222eeee`.

For **tenant-independent endpoints**, the `TenantDomainName` is `common`. This document lists only the Federation Metadata elements that are common to all Microsoft Entra tenants that are hosted at login.microsoftonline.com.

For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. The tenant-independent endpoint is https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml. You can view the federation metadata document by typing this URL in a browser.

## Contents of federation metadata

The following section provides information needed by services that consume the tokens issued by Microsoft Entra ID.

### Entity ID

The `EntityDescriptor` element contains an `EntityID` attribute. The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token. It is important to validate the issuer when you receive a token.

The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.

```xml
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
entityID="https://sts.windows.net/00aa00aa-bb11-cc22-dd33-44ee44ee44ee/">
```

You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value. The resulting value will be the same as the token issuer. The strategy allows a multitenant application to validate the issuer for a given tenant.

The following metadata shows a sample tenant-independent `EntityID` element. Please note, that the `{tenant}` is a literal, not a placeholder.

```xml
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_aaaabbbb-0000-cccc-1111-dddd2222eeee"
entityID="https://sts.windows.net/{tenant}/">
```

### Token signing certificates

When a service receives a token that is issued by a Microsoft Entra tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document. The federation metadata includes the public portion of the certificates that the tenants use for token signing. The certificate raw bytes appear in the `KeyDescriptor` element. The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.

A federation metadata document published by Microsoft Entra ID can have multiple signing keys, such as when Microsoft Entra ID is preparing to update the signing certificate. When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.

The following metadata shows a sample `KeyDescriptor` element with a signing key.

```xml
<KeyDescriptor use="signing">
<KeyInfo xmlns="https://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
aB1cD2eF-3gH4i...J5kL6-mN7oP8qR=
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
```

The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section. The certificates published in both sections will be the same.

In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.

The following metadata shows a sample `RoleDescriptor` element.

```xml
<RoleDescriptor xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:fed="https://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType" protocolSupportEnumeration="https://docs.oasis-open.org/wsfed/federation/200706">
```

In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.

The following metadata shows a sample `IDPSSODescriptor` element.

```xml
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```

There are no differences in the format of tenant-specific and tenant-independent certificates.

### WS-Federation endpoint URL

The federation metadata includes the URL that is Microsoft Entra ID uses for single sign-in and single sign-out in WS-Federation protocol. This endpoint appears in the `PassiveRequestorEndpoint` element.

The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.

```xml
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="https://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.

```xml
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="https://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### SAML protocol endpoint URL

The federation metadata includes the URL that Microsoft Entra ID uses for single sign-in and single sign-out in SAML 2.0 protocol. These endpoints appear in the `IDPSSODescriptor` element.

The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.

The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.

```xml
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
  </IDPSSODescriptor>
```

Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.

```xml
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```