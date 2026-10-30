---
layout: Conceptual
title: Configure Cloudflare with Microsoft Entra ID for secure hybrid access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/cloudflare-integration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: In this tutorial, learn how to integrate Cloudflare with Microsoft Entra ID for secure hybrid access
ms.topic: how-to
ms.date: 2025-05-21T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 1448d841-4852-07bd-0abf-0a1160fe3ee6
document_version_independent_id: 57b849d0-7ae6-b2ba-7588-8d139e4a9acc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/cloudflare-integration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/cloudflare-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/cloudflare-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c0378865-8e2e-cf8c-0d69-b85f930f9e73
---

# Configure Cloudflare with Microsoft Entra ID for secure hybrid access - Microsoft Entra ID | Microsoft Learn

In this tutorial, learn to integrate Microsoft Entra ID with Cloudflare Zero Trust. Build rules based on user identity and group membership. Users authenticate with Microsoft Entra credentials and connect to Zero Trust protected applications.

## Prerequisites

- A Microsoft Entra subscription
    - If you don't have one, get an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- A Microsoft Entra tenant linked to the Microsoft Entra subscription
    - See, [Quickstart: Create a new tenant in Microsoft Entra ID](../../fundamentals/create-new-tenant)
- A Cloudflare Zero Trust account
    - If you don't have one, go to [Get started with Cloudflare's Zero Trust platform](https://dash.cloudflare.com/sign-up/teams)
- One of the following roles: Cloud Application Administrator, or Application Administrator.

## Integrate organization identity providers with Cloudflare Access

Cloudflare Zero Trust Access helps enforce default-deny, Zero Trust rules that limit access to corporate applications, private IP spaces, and hostnames. This feature connects users faster and safer than a virtual private network (VPN). Organizations can use multiple identity providers (IdPs), reducing friction when working with partners or contractors.

To add an IdP as a sign-in method, sign in to Cloudflare on the [Cloudflare sign in page](https://dash.teams.cloudflare.com/) and Microsoft Entra ID.

The following architecture diagram shows the integration.

![Diagram of the Cloudflare and Microsoft Entra integration architecture.](media/cloudflare-integration/cloudflare-architecture-diagram.png)

## Integrate a Cloudflare Zero Trust account with Microsoft Entra ID

Integrate Cloudflare Zero Trust account with an instance of Microsoft Entra ID.

1. Sign in to the Cloudflare Zero Trust dashboard on the [Cloudflare sign in page](https://dash.teams.cloudflare.com/).
2. Navigate to **Settings**.
3. Select **Authentication**.
4. For **Login methods**, select **Add new**.

    ![Screenshot of the Login methods option on Authentication.](media/cloudflare-integration/login-methods.png)
5. Under **Select an identity provider**, select **Microsoft Entra ID**.
6. The **Add Azure ID** dialog appears.
7. Enter Microsoft Entra instance credentials and make needed selections.
8. Select **Save**.

## Register Cloudflare with Microsoft Entra ID

Use the instructions in the following three sections to register Cloudflare with Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Navigate to **Entra ID** &gt; **App registrations**.
3. Select **New registration**.
4. Enter an application **Name**.
5. Enter a team name with **callback** at the end of the path. For example, `https://<your-team-name>.cloudflareaccess.com/cdn-cgi/access/callback`
6. Select **Register**.

See the [team domain](https://developers.cloudflare.com/cloudflare-one/glossary#team-domain) definition in the Cloudflare Glossary.

![Screenshot of options and selections for Register an application.](media/cloudflare-integration/register-application.png)

### Certificates & secrets

1. On the **Cloudflare Access** screen, under **Essentials**, copy and save the Application (Client) ID and the Directory (Tenant) ID.

    [![Screenshot of the Cloudflare Access screen.](media/cloudflare-integration/cloudflare-access.png)](media/cloudflare-integration/cloudflare-access.png#lightbox)
2. In the left menu, under **Manage**, select **Certificates & secrets**.

    ![Screenshot of the certificates and secrets screen.](media/cloudflare-integration/add-client-secret.png)
3. Under **Client secrets**, select **+ New client secret**.
4. In **Description**, enter the Client Secret.
5. Under **Expires**, select an expiration.
6. Select **Add**.
7. Under **Client secrets**, from the **Value** field, copy the value. Consider the value an application password. The example value appears, Azure values appear in the Cloudflare Access configuration.

### Permissions

1. In the left menu, select **API permissions**.
2. Select **+ Add a permission**.
3. Under **Select an API**, select **Microsoft Graph**.

    ![Screenshot of the Microsoft Graph option under Request API permissions.](media/cloudflare-integration/microsoft-graph.png)
4. Select **Delegated permissions** for the following permissions:

    - Email
    - openid
    - profile
    - offline\_access
    - user.read
    - directory.read.all
    - group.read.all
5. Under **Manage**, select **+ Add permissions**.

    [![Screenshot options and selections for Request API permissions.](media/cloudflare-integration/request-api-permissions.png)](media/cloudflare-integration/request-api-permissions.png#lightbox)
6. Select **Grant Admin Consent for ...**.

    [![Screenshot of configured permissions under API permissions.](media/cloudflare-integration/grant-admin-consent.png)](media/cloudflare-integration/grant-admin-consent.png#lightbox)
7. On the Cloudflare Zero Trust dashboard, navigate to **Settings &gt; Authentication**.
8. Under **Login methods**, select **Add new**.
9. Select **Microsoft Entra ID**.
10. Enter values for **Application ID**, **Application Secret**, and **Directory ID**.
11. Select **Save**.

Note

For Microsoft Entra groups, in **Edit your Microsoft Entra identity provider**, for **Support Groups** select **On**.

## Test the integration

1. On the Cloudflare Zero Trust dashboard, navigate to **Settings** &gt; **Authentication**.
2. Under **Login methods**, for Microsoft Entra ID select **Test**.
3. Enter Microsoft Entra credentials.
4. The **Your connection works** message appears.

    ![Screenshot of the Your connection works message.](media/cloudflare-integration/connection-success-screen.png)