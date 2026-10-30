---
layout: Conceptual
title: Add Google as an identity provider - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-google-federation-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add Google as an identity provider for your external tenant.
ms.topic: how-to
ms.date: 2026-03-27T00:00:00.0000000Z
ms.custom: it-pro, has-azure-ad-ps-ref, sfi-ga-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 92ff7dd1-dbcc-02f1-fa68-198186b6e846
document_version_independent_id: 8c35551d-62a7-f2ad-0a1e-ff2eb2343063
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-google-federation-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-google-federation-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-google-federation-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 6dc0b509-e5bd-9525-3944-e3bc43c7e1b0
---

# Add Google as an identity provider - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

By setting up federation with Google, you allow customers to sign in to your applications with their own Google accounts. (Learn more about [authentication methods and identity providers for customers](concept-authentication-methods-customers).)

## Prerequisites

- An [external tenant](how-to-create-external-tenant-portal).
- A [sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).

## Create a Google application

To enable sign-in for customers with a Google account, you need to create an application in [Google Cloud console](https://console.cloud.google.com/). For more information, see [Manage OAuth clients](https://support.google.com/cloud/answer/15549257). If you don't already have a Google account, you can sign up at [`https://accounts.google.com/signup`](https://accounts.google.com/signup).

1. Sign in to the [Google Cloud console](https://console.cloud.google.com/) with your Google account credentials.
2. Accept the terms of service if you're prompted to do so.
3. In the upper-left corner of the page, select the project list, and then select **New Project**.
4. Enter a **Project Name**, select **Create**.
5. Make sure you're using the new project by selecting the project drop-down in the top-left of the screen. Select your project by name, then select **Open**.
6. Under the **Quick access**, or in the left menu, select **APIs & services** and then **OAuth consent screen**.
7. For the **User Type**, select **External** and then select **Create**.
8. On the **OAuth consent screen**, under **App information**

    1. Enter a **Name** for your application.
    2. Select a **User support email** address.
9. Under the **Authorized domains** section, select **Add domain**, and then add `ciamlogin.com` and `microsoftonline.com`.
10. In the **Developer contact information** section, enter comma separated emails for Google to notify you about any changes to your project.
11. Select **Save and Continue**.
12. From the left menu, select **Credentials**
13. Select **Create credentials**, and then **OAuth client ID**.
14. Under **Application type**, select **Web application**.

    1. Enter a suitable **Name** for your application, such as "Microsoft Entra External ID."
    2. In **Valid OAuth redirect URIs**, enter the following URIs. Replace `<tenant-ID>` with your customer Directory (tenant) ID and `<tenant-subdomain>` with your customer Directory (tenant) subdomain. If you don't have your tenant name, [learn how to read your tenant details](how-to-create-external-tenant-portal#get-the-external-tenant-details).

    - `https://login.microsoftonline.com`
    - `https://login.microsoftonline.com/te/<tenant-ID>/oauth2/authresp`
    - `https://login.microsoftonline.com/te/<tenant-subdomain>.onmicrosoft.com/oauth2/authresp`
    - `https://<tenant-ID>.ciamlogin.com/<tenant-ID>/federation/oidc/accounts.google.com`
    - `https://<tenant-ID>.ciamlogin.com/<tenant-subdomain>.onmicrosoft.com/federation/oidc/accounts.google.com`
    - `https://<tenant-subdomain>.ciamlogin.com/<tenant-ID>/federation/oauth2`
    - `https://<tenant-subdomain>.ciamlogin.com/<tenant-subdomain>.onmicrosoft.com/federation/oauth2`
15. Select **Create**.
16. Record the values of **Client ID** and **Client secret**. You need both values to configure Google as an identity provider in your tenant.

Note

In some cases, your app might require verification by Google (for example, if you update the application logo). For more information, check out the [Google's verification status guide](https://support.google.com/cloud/answer/10311615#verification-status).

## Configure Google federation in Microsoft Entra External ID

After you create the Google application, in this step you set the Google client ID and client secret in Microsoft Entra ID. You can use the Microsoft Entra admin center or PowerShell to do so. To configure Google federation in the Microsoft Entra admin center, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **All identity providers**.
3. On the **Built-in** tab, next to **Google**, select **Configure**.
4. Enter a **Name**. For example, *Google*.
5. For the **Client ID**, enter the Client ID of the Google application that you created earlier.
6. For the **Client secret**, enter the Client Secret that you recorded.
7. Select **Save**.

To configure Google federation by using PowerShell, follow these steps:

1. Install the latest version of the [Microsoft Graph PowerShell for Graph module](/en-us/powershell/microsoftgraph/installation).
2. Run the following command: `Connect-MgGraph`
3. At the sign-in prompt, sign in as at least an [External Identity Provider Administrator](../../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
4. Run the following command:

    ```powershell
    Import-Module Microsoft.Graph.Identity.SignIns
    $params = @{
    "@odata.type" = "microsoft.graph.socialIdentityProvider"
    displayName = "Login with Google"
    identityProviderType = "Google"
    clientId = "00001111-aaaa-2222-bbbb-3333cccc4444"
    clientSecret = "000000000000"
    }
    New-MgIdentityProvider -BodyParameter $params
    ```

Use the client ID and client secret from the app you created in Create a Google application step.

## Enable users to sign in and sign up with the identity provider

After you configure Google as an identity provider, add it to a user flow to allow sign-in and sign-up with the identity provider. See [Add an identity provider to a user flow](how-to-add-identity-provider-to-user-flow-customers).