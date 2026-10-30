---
layout: Conceptual
title: SAML/WS-Fed identity provider federation - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/direct-federation-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about federation with an external organization's SAML/WS-Fed identity provider (IdP) for external user self-service sign-up and invitation redemption.
ms.topic: concept-article
ms.date: 2026-04-21T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1012
ms.collection: M365-identity-device-management
locale: en-us
document_id: a7a1f702-4e7b-f680-7773-94a6eee88e5c
document_version_independent_id: a7a1f702-4e7b-f680-7773-94a6eee88e5c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/direct-federation-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/direct-federation-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/direct-federation-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4c2cf1d2-34ee-137b-9f73-5402f12c0185
---

# SAML/WS-Fed identity provider federation - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In Microsoft Entra workforce and external tenants, you can set up federation with other organizations that use a SAML or WS-Fed identity provider (IdP). Users from the external organization can then use their own IdP-managed accounts to sign in to your apps or resources, either during invitation redemption or self-service sign-up, without having to create new Microsoft Entra credentials. The user is redirected to their IdP when signing up or signing in to your app, and then returned to Microsoft Entra once they successfully sign in.

You can associate multiple domains with a single federation configuration. The partner's domain can be either Microsoft Entra verified or unverified.

Note

Direct SAML/WS-Fed federation between two Microsoft Entra tenants is not a supported or recommended configuration. Even if a SAML trust is technically configured between two Entra tenants, Microsoft Entra still uses the native Entra-to-Entra B2B collaboration model and not SAML.

Setting up SAML/WS-Fed IdP federation requires configuration both in your tenant and in the external organization's IdP. In some cases, the partner needs to update their DNS text records. They also need to update their IdP with the required claims and relying party trusts.

## User authentication with SAML/WS-Fed IdP federation

Once you set up federation with a partner's SAML/WS-Fed IdP, users can sign up or sign in by selecting the **Sign up with** or **Sign in with** option. They're redirected to the identity provider, and then returned to Microsoft Entra once they successfully sign in.

For external tenants, a user's sign-in email doesn't need to match the predefined domains set up during SAML federation. If a user doesn't have an account in your external tenant and enters an email address on the sign-in page that matches a predefined domain in any of the external identity providers, they're redirected to authenticate with that identity provider.

### Verified and unverified domains

A user's sign-in experience depends on whether the partner's domain is Microsoft Entra verified.

- **Unverified domains** are domains that aren’t DNS-verified in Microsoft Entra ID. After federation, users can sign in using their credentials from the unverified domain.
- **Unmanaged (email-verified or “viral”) tenants** are created when a user redeems an invitation or performs self-service sign-up for Microsoft Entra ID using a domain that doesn’t currently exist. After federation, users can sign in using their credentials from the unmanaged tenant.
- **Microsoft Entra ID verified domains** are domains that are DNS-verified with Microsoft Entra, including domains where the tenant has undergone an [admin takeover](../identity/users/domains-admin-takeover). After federation:

    - For self-service sign-up, users can use their own domain credentials.
    - For invitation redemption, Microsoft Entra ID remains the primary IdP. In a workforce tenant, you can prioritize the federated IdP for invitation redemption by [changing the redemption order](cross-tenant-access-overview#configurable-redemption).

    Note

    Changing the redemption order isn't currently supported in external tenants or across clouds.

### How federation affects current external users

If an external user already redeemed an invitation or used self-service sign-up, their authentication method doesn't change when you set up federation. They continue using their original authentication method (for example, one-time passcode). Even if a user from an unverified domain uses federation, and their organization later moves to Microsoft Entra, they continue using federation.

For B2B collaboration in a workforce tenant, you don't need to send new invitations to existing users because they continue using their current sign-in method. But you can [reset a user's redemption status](reset-redemption-status). The next time the user accesses your app, they will repeat the redemption steps and can switch to federation.

### Sign-in endpoints in workforce tenants

When federation is set up in your workforce tenant, users from the federated organization can sign in to your multitenant or Microsoft first-party apps by using a [common endpoint](redemption-experience#redemption-process-and-sign-in-through-a-common-endpoint) (in other words, a general app URL that doesn't include your tenant context). During the sign-in process, the user chooses **Sign-in options**, and then selects **Sign in to an organization**. They type the name of your organization and continue signing in using their own credentials.

SAML/WS-Fed IdP federation users can also use application endpoints that include your tenant information, for example:

- `https://myapps.microsoft.com/?tenantid=<your tenant ID>`
- `https://myapps.microsoft.com/<your verified domain>.onmicrosoft.com`
- `https://portal.azure.com/<your tenant ID>`

You can also give users a direct link to an application or resource by including your tenant information, for example `https://myapps.microsoft.com/signin/X/<application ID?tenantId=<your tenant ID>`.

## Key considerations for SAML/WS-Fed federation

### Partner IdP requirements

Setting up SAML/WS-Fed IdP federation requires configuration both in your tenant and in the external organization's IdP. Depending on the partner's IdP, the partner might need to update their DNS records to enable federation with you. See [Step 1: Determine if the partner needs to update their DNS text records](direct-federation#step-1-determine-if-the-partner-needs-to-update-their-dns-text-records).

The partner must update their IdP with the required claims and relying party trusts. The Issuer URL in the SAML request sent by Microsoft Entra ID for external federations is now a tenanted endpoint, whereas previously it was a global endpoint. Existing federations with the global endpoint continue to work. But for new federations, set the audience of the external SAML or WS-Fed IdP to a tenanted endpoint. See the [SAML 2.0 section](direct-federation#to-configure-a-saml-20-identity-provider) and the [WS-Fed section](direct-federation#to-configure-a-ws-fed-identity-provider) for required attributes and claims.

### Signing certificate expiration

If you specify the metadata URL in the IdP settings, Microsoft Entra ID automatically renews the signing certificate when it expires. However, if the certificate is rotated for any reason before the expiration time, or if you don't provide a metadata URL, Microsoft Entra ID is unable to renew it. In this case, you need to update the signing certificate manually.

### Session expiration

If the Microsoft Entra session expires or becomes invalid, and the federated IdP has SSO enabled, the user experiences SSO. If the federated user's session is valid, the user isn't prompted to sign in again. Otherwise, the user is redirected to their IdP for sign-in.

### Partially synced tenancy

Federation doesn't resolve sign-in issues caused by a partially synced tenancy, where a partner’s on-premises user identities aren't fully synced to Microsoft Entra in the cloud. These users can’t sign in with a B2B invitation, so they need to use the [email one-time passcode](one-time-passcode) feature instead. The SAML/WS-Fed IdP federation feature is for partners with their own IdP-managed organizational accounts but no Microsoft Entra presence.

### B2B guest accounts

Federation doesn't replace the need for B2B guest accounts in your directory. With B2B collaboration, a guest account is created for the user in your workforce tenant directory regardless of the authentication or federation method used. This user object allows you to grant access to applications, assign roles, and define membership in security groups.

### Signed authentication tokens

Currently, the Microsoft Entra SAML/WS-Fed federation feature doesn't support sending a signed authentication token to the SAML identity provider.