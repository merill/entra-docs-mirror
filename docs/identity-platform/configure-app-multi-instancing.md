---
layout: Conceptual
title: Configure app multi-instancing - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/configure-app-multi-instancing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about multi-instancing, which is needed for configuring multiple instances of the same application within a tenant.
manager: pmwongera
ms.custom: 
ms.date: 2023-06-09T00:00:00.0000000Z
ms.reviewer: alamaral
ms.topic: how-to
locale: en-us
document_id: 1ad581e1-1779-511c-1dd5-22eb9eaaa9b0
document_version_independent_id: 66076cd9-0c2f-7b80-4911-b276673970cd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/configure-app-multi-instancing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/configure-app-multi-instancing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/configure-app-multi-instancing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9c04a76a-92ea-07ac-c21b-0ad22e72f320
---

# Configure app multi-instancing - Microsoft identity platform | Microsoft Learn

App multi-instancing refers to the need for the configuration of multiple instances of the same application within a tenant. For example, the organization has multiple accounts, each of which needs a separate service principal to handle instance-specific claims mapping and roles assignment. Or the customer has multiple instances of an application, which doesn't need special claims mapping, but does need separate service principals for separate signing keys.

## Sign-in approaches

A user can sign-in to an application one of the following ways:

- Through the application directly, which is known as service provider (SP) initiated single sign-on (SSO).
- Go directly to the identity provider (IDP), known as IDP initiated SSO.

Depending on which approach is used within your organization, follow the appropriate instructions described in this article.

## SP initiated SSO

In the SAML request of SP initiated SSO, the `issuer` specified is usually the app ID URI. Utilizing App ID URI doesn't allow the customer to distinguish which instance of an application is being targeted when using SP initiated SSO.

### Configure SP initiated SSO

Update the SAML single sign-on service URL configured within the service provider for each instance to include the service principal guid as part of the URL. For example, the general SSO sign-in URL for SAML is `https://login.microsoftonline.com/<tenantid>/saml2`, the URL can be updated to target a specific service principal, such as `https://login.microsoftonline.com/<tenantid>/saml2/<issuer>`.

Only service principal identifiers in GUID format are accepted for the issuer value. The service principal identifiers override the issuer in the SAML request and response, and the rest of the flow is completed as usual. There's one exception: if the application requires the request to be signed, the request is rejected even if the signature was valid. The rejection is done to avoid any security risks with functionally overriding values in a signed request.

## IDP initiated SSO

The IDP initiated SSO feature exposes the following settings for each application:

- An **audience override** option exposed for configuration by using claims mapping or the portal. The intended use case is applications that require the same audience for multiple instances. This setting is ignored if no custom signing key is configured for the application.
- An **issuer with application id** flag to indicate the issuer should be unique for each application instead of unique for each tenant. This setting is ignored if no custom signing key is configured for the application.

### Configure IDP initiated SSO

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Open any SSO enabled enterprise app and navigate to the SAML single sign-on blade.
4. Select **Edit** on the **User Attributes & Claims** panel.
5. Select **Edit** to open the advanced options blade.
6. Configure both options according to your preferences and then select **Save**.