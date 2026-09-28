---
layout: Conceptual
title: Add a SAML/WS-Fed identity provider - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/direct-federation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Set up direct federation with SAML 2.0 or WS-Fed identity providers so users can sign in with work accounts. Understand attributes and claims for federation.
ms.topic: how-to
ms.date: 2026-04-08T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, seo-july-2024, sfi-image-nochange, msecd-doc-authoring-1012
locale: en-us
document_id: 7b1d9428-2dbb-c80b-c2cd-b4841d3d8bd3
document_version_independent_id: 20af5f8d-479c-66ec-aacd-d3f9cb79c814
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/direct-federation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/direct-federation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/direct-federation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 322d779f-fa90-6721-fb17-5d613a626091
---

# Add a SAML/WS-Fed identity provider - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Your Microsoft Entra tenant can be directly federated with external organizations that use a SAML or WS-Fed identity provider (IdP). Users from the external organization can then use their own IdP-managed accounts to sign in to your apps or resources, either during invitation redemption or self-service sign-up, without having to create new Microsoft Entra credentials. The user is redirected to their IdP when signing up or signing in to your app, and then returned to Microsoft Entra once they successfully sign in.

## Prerequisites

- Review the configuration considerations in [SAML/WS-Fed identity providers](direct-federation-overview).
- A workforce tenant or an [external tenant](customers/how-to-create-external-tenant-portal).

Note

The Issuer value for the IdP must be a valid URI following RFC 3986 format (for example, `https://testdev.example.com` or `http://www.example.com/exk10l6w90DHM0yi`). Single-word or non-URI values (for example, `testdev`) aren't supported and are rejected by the portal. This aligns with Microsoft Entra ID's secure identifier patterns, as documented in [Restrictions on identifier URIs](../identity-platform/identifier-uri-restrictions). For SAML IdPs, the Issuer must uniquely identify the provider as a URI, per SAML 2.0 standards and [Microsoft Entra validation rules](../identity/hybrid/connect/how-to-connect-fed-saml-idp#required-attributes).

## How to configure SAML/WS-Fed IdP federation

### Step 1: Determine if the partner needs to update their DNS text records

Use the following steps to determine if the partner needs to update their DNS records to enable federation with you.

1. Check the partner's IdP passive authentication URL to see if the domain matches the target domain or a host within the target domain. In other words, when setting up federation for `fabrikam.com`:

    - If the passive authentication endpoint is `https://fabrikam.com` or `https://sts.fabrikam.com/adfs` (a host in the same domain), no DNS changes are needed.
    - If the passive authentication endpoint is `https://fabrikamconglomerate.com/adfs` or `https://fabrikam.co.uk/adfs`, the domain doesn't match the fabrikam.com domain, so the partner needs to add a text record for the authentication URL to their DNS configuration.
2. If DNS changes are needed based on the previous step, ask the partner to add a TXT record to their domain's DNS records, like the following example:

    `fabrikam.com.  IN   TXT   DirectFedAuthUrl=https://fabrikamconglomerate.com/adfs`

### Step 2: Configure the partner organization’s IdP

Next, your partner organization needs to configure their IdP with the required claims and relying party trusts. For federation to work properly, Microsoft Entra External ID requires the external IdP to send certain attributes and claims, which must be configured at the external IdP.

Note

To illustrate how to configure a SAML/WS-Fed IdP for federation, we use Active Directory Federation Services (AD FS) as an example. See the article [Configure SAML/WS-Fed IdP federation with AD FS](direct-federation-adfs), which gives examples of how to configure AD FS as a SAML 2.0 or WS-Fed IdP in preparation for federation.

#### To configure a SAML 2.0 identity provider

Microsoft Entra External ID requires the SAML 2.0 response from the external IdP to include specific attributes and claims. The necessary attributes and claims can be configured at the external IdP by either:

- Linking to the online security token service XML file, or
- Manually entering the values

Refer to the following tables for the required values.

Note

Ensure the value matches the cloud for which you're setting up external federation.

**Table 1. Required attributes for the SAML 2.0 response from the IdP.**

| Attribute | Value for a workforce tenant | Value for an external tenant |
| --- | --- | --- |
| AssertionConsumerService | `https://login.microsoftonline.com/login.srf` | `https://<tenantID>.ciamlogin.com/login.srf` Add `https://<tenantID>.ciamlogin.com/login.srf` as the callback/ACS URL on the external IdP if required by that provider. |
| Audience | `https://login.microsoftonline.com/<tenant ID>/` (Recommended) Replace `<tenant ID>` with the tenant ID of the Microsoft Entra tenant you're setting up federation with. In the SAML request sent by Microsoft Entra ID for external federations, the Issuer URL is a tenanted endpoint (for example, `https://login.microsoftonline.com/<tenant ID>/`). For any new federations, we recommend that all our partners set the audience of the SAML or WS-Fed based IdP to a tenanted endpoint. Any existing federations configured with the global endpoint (for example, `urn:federation:MicrosoftOnline`) continue to work, but new federations stop working if your external IdP is expecting a global issuer URL in the SAML request sent by Microsoft Entra ID. | `https://login.microsoftonline.com/<tenant ID>/`Replace `<tenant ID>` with the tenant ID of the Microsoft Entra tenant you're setting up federation with. |
| Issuer | The issuer URI of the partner's IdP, for example `http://www.example.com/exk10l6w90DHM0yi...` | The issuer URI of the partner's IdP, for example `http://www.example.com/exk10l6w90DHM0yi...` |

**Table 2. Required claims for the SAML 2.0 token issued by the IdP.**

| Attribute Name | Value |
| --- | --- |
| NameID Format | `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent` |
| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` | The user's email address |

#### To configure a WS-Fed identity provider

Microsoft Entra External ID requires the WS-Fed message from the external IdP to include specific attributes and claims. The necessary attributes and claims can be configured at the external IdP by either:

- Linking to the online security token service XML file, or
- Manually entering the values

Note

Currently, the two WS-Fed providers that have been tested for compatibility with Microsoft Entra ID are AD FS and Shibboleth.

##### Required WS-Fed attributes and claims

The following tables show requirements for specific attributes and claims that must be configured at the third-party WS-Fed IdP. To set up federation, the following attributes must be received in the WS-Fed message from the IdP. These attributes can be configured by linking to the online security token service XML file or by entering them manually.

Refer to the following tables for the required values.

Note

Ensure the value matches the cloud for which you're setting up external federation.

**Table 3. Required attributes in the WS-Fed message from the IdP.**

| Attribute | Value for a workforce tenant | Value for an external tenant |
| --- | --- | --- |
| PassiveRequestorEndpoint | `https://login.microsoftonline.com/login.srf` | `https://<tenantID>.ciamlogin.com/login.srf` |
| Audience | `https://login.microsoftonline.com/<tenant ID>/` (Recommended) Replace `<tenant ID>` with the tenant ID of the Microsoft Entra tenant you're setting up federation with. In the SAML request sent by Microsoft Entra ID for external federations, the Issuer URL is a tenanted endpoint (for example, `https://login.microsoftonline.com/<tenant ID>/`). For any new federations, we recommend that all our partners set the audience of the SAML or WS-Fed based IdP to a tenanted endpoint. Any existing federations configured with the global endpoint (for example, `urn:federation:MicrosoftOnline`) continue to work, but new federations stop working if your external IdP is expecting a global issuer URL in the SAML request sent by Microsoft Entra ID. | `https://login.microsoftonline.com/<tenant ID>/`Replace `<tenant ID>` with the tenant ID of the Microsoft Entra tenant you're setting up federation with. |
| Issuer | The issuer URI of the partner's IdP, for example `http://www.example.com/exk10l6w90DHM0yi...` | The issuer URI of the partner's IdP, for example `http://www.example.com/exk10l6w90DHM0yi...` |

**Table 4. Required claims for the WS-Fed token issued by the IdP.**

| Attribute | Value |
| --- | --- |
| ImmutableID | `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID` |
| emailaddress | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |

### Step 3: Configure SAML/WS-Fed IdP federation in Microsoft Entra External ID

Next, configure federation with the IdP configured in step 1 in Microsoft Entra External ID. You can use either the Microsoft Entra admin center or the [Microsoft Graph API](/en-us/graph/api/resources/samlorwsfedexternaldomainfederation). It might take 5-10 minutes before the federation policy takes effect. During this time, don't attempt to complete self-service sign-up or redeem an invitation for the federation domain. The following attributes are required:

- Issuer URI of the partner's IdP
- Passive authentication endpoint of partner IdP (only https is supported)
- Certificate

#### To add the IdP to your tenant in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External Identity Provider Administrator](../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your tenant from the **Directories** menu.
3. Browse to **Microsoft Entra ID** &gt; **External Identities** &gt; **All identity providers**.
4. Select the **Custom** tab, and then select **Add new** &gt; **SAML/WS-Fed**.

    [![Screenshot showing button for adding a new SAML or WS-Fed IdP.](media/direct-federation/new-saml-wsfed-idp.png)](media/direct-federation/new-saml-wsfed-idp.png#lightbox)
5. On the **New SAML/WS-Fed IdP** page, enter the following:

    - **Display name** - Enter a name to help you identify the partner's IdP.
    - **Identity provider protocol** - Select **SAML** or **WS-Fed**.
    - **Domainless** - Selecting **Domainless** enforces no domain check of the user's email address. For more details, see [Domainless SAML IdP federation](direct-federation#domainless-saml-idp-federation).
    - **Domain name of federating IdP** - Enter your partner’s IdP target domain name for federation. During this initial configuration, enter just one domain name. You can add more domains later.

    ![Screenshot showing the new SAML or WS-Fed IdP page.](media/direct-federation/new-saml-wsfed-idp-parse.png)
6. Select a method for populating metadata. If you have a file that contains the metadata, you can automatically populate the fields by selecting **Parse metadata file** and browsing for the file. Or, you can select **Input metadata manually** and enter the following information:

    - The **Issuer URI** of the partner's SAML IdP, or the **Entity ID** of the partner's WS-Fed IdP.
    - The **Passive authentication endpoint** of the partner's SAML IdP, or the **Passive requestor endpoint** of the partner's WS-Fed IdP.
    - **Certificate** - The signing certificate ID.
    - **Metadata URL** - The location of the IdP's metadata for automatic renewal of the signing certificate.

    ![Screenshot showing metadata fields.](media/direct-federation/new-saml-wsfed-idp-input.png)

    Note

    Metadata URL is optional. However, we strongly recommend it. If you provide the metadata URL, Microsoft Entra ID can automatically renew the signing certificate when it expires. If the certificate is rotated for any reason before the expiration time or if you don't provide a metadata URL, Microsoft Entra ID is unable to renew it. In this case, you need to update the signing certificate manually.
7. Select **Save**. The identity provider is added to the **SAML/WS-Fed identity providers** list.

    [![Screenshot showing the SAML/WS-Fed identity provider list with the new entry.](media/direct-federation/new-saml-wsfed-idp-list.png)](media/direct-federation/new-saml-wsfed-idp-list.png#lightbox)
8. (Optional) To add more domain names to this federating identity provider:

    1. Select the link in the **Domains** column.

        [![Screenshot showing the link for adding domains to the SAML/WS-Fed identity provider.](media/direct-federation/new-saml-wsfed-idp-add-domain.png)](media/direct-federation/new-saml-wsfed-idp-add-domain.png#lightbox)
    2. Next to **Domain name of federating IdP**, type the domain name, and then select **Add**. Repeat for each domain you want to add. When you're finished, select **Done**.

        ![Screenshot showing the Add button in the domain details pane.](media/direct-federation/add-domain.png)

#### To configure federation using the Microsoft Graph API

You can use the Microsoft Graph API [samlOrWsFedExternalDomainFederation](/en-us/graph/api/resources/samlorwsfedexternaldomainfederation?view=graph-rest-beta&amp;preserve-view=true) resource type to set up federation with an identity provider that supports either the SAML or WS-Fed protocol.

### Step 4: Configure redemption order (B2B collaboration in workforce tenants)

If you're configuring federation in your workforce tenant for B2B collaboration with a verified domain, make sure the federated IdP is used first during invitation redemption. [Configure the **Redemption order** settings](cross-tenant-access-settings-b2b-collaboration) in your cross-tenant access settings for inbound B2B collaboration. Move **SAML/WS-Fed identity providers** to the top of the **Primary identity providers** list to prioritize redemption with the federated IdP.

You can test your federation setup by inviting a new B2B guest user. For details, see [Add Microsoft Entra B2B collaboration users in the Microsoft Entra admin center](add-users-administrator).

Note

You can configure the invitation redemption order using the Microsoft Graph REST API (beta version). See [Example 2: Update default invitation redemption configuration](/en-us/graph/api/crosstenantaccesspolicyconfigurationdefault-update?view=graph-rest-beta&amp;tabs=http#example-2-update-default-invitation-redemption-configuration&amp;preserve-view=true) in the Microsoft Graph reference documentation.

## Domainless SAML IdP federation

Traditional federation in Microsoft Entra ID requires you to verify a custom domain (for example, `contoso.com`) and configure that domain to redirect authentication requests to an external SAML Identity Provider (IdP). In this setup, the domain of the email claim provided by the external IdP after authentication is validated against the domain associated with the configured SAML IdP in Microsoft Entra ID.

If the user's email domain differs from the domain configured on the SAML IdP (for example, yahoo.com or gmail.com), users might encounter the following error during sign-in:

**AADSTS5000819**: SAML Assertion is invalid. Email address claim is missing or does not match domain from an external realm.

This error typically occurs when:

- The external SAML IdP does not send an email claim, or
- The email address domain provided by the IdP does not match the domain configured on the external IdP in Microsoft Entra ID

Even when an email claim is present, authentication might still fail if the email domain doesn't align with the configured IdP domain due to domain-based matching requirements.

Domainless SAML federation with a SAML Identity Provider allows external users to authenticate into your apps or workforce resources using their IdP-managed credentials, regardless of their email domain. Domainless federation removes the need for domain matching between the user's email and pre-configured IdP domains during sign-in or invitation redemption.

### Configure domainless SAML IdP federation

To address the domain matching limitation, you can configure the SAML IdP as domainless. When domainless federation is enabled:

- Microsoft Entra ID routes authentication requests to the configured SAML IdP based on the Issuer URI association.
- The user's email address domain isn't matched against the domain configured for the IdP.

Users can then authenticate successfully using email addresses from any domain (for example, yahoo.com or gmail.com) when signing in with the external SAML IdP.

To enable domainless federation for a new SAML IdP, follow these steps:

- On the **New SAML/WS-Fed IdP** page, select **Domainless**. Selecting **Domainless** enforces no domain check of the user's email address.

    [![Screenshot showing the SAML/WS-Fed identity provider list with the domainless configuration.](media/direct-federation/new-saml-wsfed-identity-provider-domain-less.png)](media/direct-federation/new-saml-wsfed-identity-provider-domain-less.png#lightbox)

Important

When the **Domainless** field is selected, federation is configured as domainless. Microsoft Entra ID uses the **Issuer URI** to match incoming authentication requests instead of domain-based routing. Currently, only **one** wildcard IdP can be configured per tenant.

### User flow for domainless SAML IdP federation

After configuring domainless federation, you can invite guest users from the partner organization by following these steps:

1. In the Microsoft Entra admin center, navigate to **Identity** &gt; **Users** &gt; **All users**.
2. Select **+ New user** and choose **Invite external user**.
3. Enter the guest user's email address. The email domain doesn't need to match a verified domain in your tenant.
4. In the invitation redirect URL, include a **domain\_hint** parameter to ensure the user is routed to the appropriate IdP based on the configured Issuer URI. The **domain\_hint** value must match the **Issuer URI** defined in the SAML IdP configuration.
5. Complete and send the invitation.
6. When the invited user redeems the invitation, Microsoft Entra ID routes the authentication request to the configured SAML IdP using the Issuer URI in the `domain_hint` parameter.
7. The user authenticates with the external SAML IdP. The user's email address domain isn't matched against the domain configured for the IdP, and the user can access the resource tenant.
8. For subsequent sign-ins, the user can directly access the resource tenant application by authenticating with the external SAML IdP because the user object is updated with the external IdP association.

### Known issues

The following known issue is being actively addressed and this section will be updated after the fix is available.

- The IdP configuration gets deleted if an invalid domain name is entered even when the IdP config is not saved.

## How to update the certificate or configuration details

On the **All identity providers** page, you can view the list of SAML/WS-Fed identity providers configured and their certificate expiration dates. From this list, you can renew certificates and modify other configuration details.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External Identity Provider Administrator](../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
2. Browse to **Microsoft Entra ID** &gt; **External Identities** &gt; **All identity providers**.
3. Select the **Custom** tab.
4. Scroll to an identity provider in the list or use the search box.
5. To update the certificate or modify configuration details:

    - In the **Configuration** column for the identity provider, select the **Edit** link.
    - On the configuration page, modify any of the following details:
        - **Display name** - Display name for the partner's organization.
        - **Identity provider protocol** - Select **SAML** or **WS-Fed**.
        - **Passive authentication endpoint** - The partner IdP's passive requestor endpoint.
        - **Certificate** - The ID of the signing certificate. To renew it, enter a new certificate ID.
        - **Metadata URL** - The URL containing the partner's metadata, used for automatic renewal of the signing certificate.
    - Select **Save**.

    ![Screenshot of the IDP configuration details.](media/direct-federation/modify-configuration.png)
6. To edit the domains associated with the partner, select the link in the **Domains** column. In the domain details pane:

    - To add a domain, type the domain name next to **Domain name of federating IdP**, and then select **Add**. Repeat for each domain you want to add.
    - To delete a domain, select the delete icon next to the domain.
    - When you're finished, select **Done**.

    ![Screenshot of the domain configuration page.](media/direct-federation/edit-domains.png)
7. To switch to domainless federation, select the **Domainless** checkbox, and then select **Done**.

    ![Screenshot of the domain configuration page for domainless.](media/direct-federation/edit-domains-domain-less.png)

    Note

    To remove federation with a partner, first delete all domains except one, and then follow the steps in the next section.

## How to remove federation

You can remove your federation configuration. If you do, federation guest users who already redeemed their invitations can no longer sign in. However, you can give them access to your resources again by [resetting their redemption status](reset-redemption-status). To remove a configuration for an IdP in the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External Identity Provider Administrator](../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
2. Browse to **Microsoft Entra ID** &gt; **External Identities** &gt; **All identity providers**.
3. Select the **Custom** tab, and then scroll to the identity provider in the list or use the search box.
4. Select the link in the **Domains** column to view the IdP's domain details.
5. Delete all but one of the domains in the **Domain name** list.
6. Select **Delete Configuration**, and then select **Done**.

    ![Screenshot of deleting a configuration.](media/direct-federation/delete-configuration.png)
7. Select **OK** to confirm deletion.

You can also remove federation using the Microsoft Graph API [samlOrWsFedExternalDomainFederation](/en-us/graph/api/resources/samlorwsfedexternaldomainfederation?view=graph-rest-beta&amp;preserve-view=true) resource type.