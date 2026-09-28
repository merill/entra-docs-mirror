---
layout: Conceptual
title: Add Azure AD B2C for customer sign-in - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-b2c-federation-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to configure an Azure AD B2C tenant as an external identity provider in Microsoft Entra External ID, enabling users to sign in using their existing accounts.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.reviewer: brozbab
ms.custom: it-pro
locale: en-us
document_id: 51078253-48cf-a095-794c-a33db9031334
document_version_independent_id: 51078253-48cf-a095-794c-a33db9031334
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-b2c-federation-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-b2c-federation-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-b2c-federation-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 3dc120c4-65ee-3ca5-1c7a-d8cca4e017bb
---

# Add Azure AD B2C for customer sign-in - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Important

Effective May 1, 2025, Azure AD B2C will no longer be available to purchase for new customers. To learn more, please see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

Tip

This article covers federating with an existing Azure AD B2C tenant. If you're looking to migrate your users and applications from Azure AD B2C to External ID instead, see [Plan your migration from Azure AD B2C to External ID](plan-your-migration-from-b2c-to-external-id).

To configure your Azure AD B2C tenant as an identity provider, you need to create an Azure AD B2C custom policy, and then an application.

## Prerequisites

- Your Azure AD B2C tenant configured with the custom policy starter pack. See [Tutorial - Create user flows and custom policies - Azure Active Directory B2C | Microsoft Learn](/en-us/azure/active-directory-b2c/tutorial-create-user-flows?pivots=b2c-custom-policy)
    - When the email is a required claim in the ID Token, to receive the email claim, you might need to use a custom policy in your Azure AD B2C tenant.
    - You can use the [custom policy deployment tool](https://aka.ms/iefsetup)

## Configure your custom policy

If it's enabled in the user flow, the external tenant may require the email claim to be returned in the token from your Azure AD B2C custom policy.

After provisioning the custom policy starter pack, download the `B2C_1A_signup_signin` file from the **Identity Experience Framework** blade within your Azure AD B2C tenant.

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Azure AD B2C**.
2. On the overview page, under **Policies**, select **Identity Experience Framework**.
3. Search and select the `B2C_1A_signup_signin` file.
4. Download `B2C_1A_signup_signin`.

Open the `B2C_1A_signup_signin.xml` file in a text editor. Under the `<OutputClaims>` node, add the following output claim:

```xml
<OutputClaim ClaimTypeReferenceId="signInName" PartnerClaimType="email"/>
```

Save the file as `B2C_1A_signup_signin.xml` and upload it through the **Identity Experience Framework** blade within your Azure AD B2C tenant. Select to **Overwrite existing policy**. This step will ensure that the email address is issued as a claim to Microsoft Entra ID after authentication at Azure AD B2C.

## Register Microsoft Entra ID as an application

You must register Microsoft Entra ID as an application in your Azure AD B2C tenant. This step allows Azure AD B2C to issue tokens to your Microsoft Entra ID for federation.

To create an application:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Azure AD B2C**.
2. Select **App registrations**, and then select **New registration**.
3. Under **Name**, enter "Federation with Microsoft Entra ID".
4. Under **Supported account types**, select **Accounts in any identity provider or organizational directory (for authenticating users with user flows)**.
5. Under **Redirect URI**, select **Web**, and then enter the following URL in all lowercase letters, where `tenant-subdomain` is replaced with the name of your Entra tenant (for example, Contoso):

    `https://<tenant-subdomain>.ciamlogin.com/<tenant-ID>/federation/oauth2`

    `https://<tenant-subdomain>.ciamlogin.com/<tenant-subdomain>.onmicrosoft.com/federation/oauth2`

    For example:

    `https://contoso.ciamlogin.com/00aa00aa-bb11-cc22-dd33-44ee44ee44ee/federation/oauth2`

    `https://contoso.ciamlogin.com/contoso.onmicrosoft.com/federation/oauth2`

    If you use a custom domain, enter:

    `https://<your-domain-name>/<your-tenant-name>.onmicrosoft.com/oauth2/authresp`

    Replace `your-domain-name` with your custom domain, and `your-tenant-name` with the name of your tenant.
6. Under **Permissions**, select the **Grant admin consent to openid and offline\_access permissions** check box.
7. Select **Register**.
8. In the Azure AD B2C - App registrations page, select the application you created and record the **Application (client) ID** shown on the application overview page. You need this ID when you configure the identity provider in the next section.
9. In the left menu, under **Manage**, select **Certificates & secrets**.
10. Select **New client secret**.
11. Enter a description for the client secret in the **Description** box. For example: "FederationWithEntraID".
12. Under **Expires**, select a duration for which the [secret is valid](/en-us/azure/active-directory-b2c/policy-keys-overview), and then select **Add**.
13. Record the secret's **Value**. You need this value when you configure the identity provider in the next section.

## Configure your Azure AD B2C tenant as an identity provider in your external tenant

Construct your OpenID Connect `well-known` endpoint: replace `<your-B2C-tenant-name>` with the name of your Azure AD B2C tenant.

If you're using a custom domain name, replace `<custom-domain-name>` with your custom domain. Replace the `<policy>` with the policy name you configured in your B2C tenant. If you're using the starter pack, it's the `B2C_1A_signup_signin` file.

`https://<your-B2C-tenant-name>.b2clogin.com/<your-B2C-tenant-name>.onmicrosoft.com/<policy>/v2.0/.well-known/openid-configuration`

OR

`https://<custom-domain-name>/<your-B2C-tenant-name>.onmicrosoft.com/<policy>/v2.0/.well-known/openid-configuration`

1. Configure the issuer URI as: `https://<your-b2c-tenant-name>.b2clogin.com/<your-b2c-tenant-id>/v2.0/`, or if you're using a custom domain, use your custom domain, domain instead of `your-b2c-tenant-name.b2clogin.com`.
2. For **Client ID**, enter the application ID that you previously recorded.
3. Select **Client authentication** as `client_secret`.
4. For **Client secret**, enter the client secret that you previously recorded.
5. For the **Scope**, enter `openid profile email offline_access`
6. Select `code` as the response type.
7. Configure the following for claim mappings:

- **Sub**: sub
- **Name**: name
- **Given name**: given\_name
- **Family name**: family\_name
- **Email** (required): email

Create the identity provider and attach it to your user flow associated with your application for sign in and sign up.