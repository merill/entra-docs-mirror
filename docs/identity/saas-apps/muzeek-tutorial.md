---
layout: Conceptual
title: Configure Muzeek for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/muzeek-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra and Muzeek.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-06-19T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 40928c03-e3da-cbcd-4843-85238bfe6034
document_version_independent_id: 40928c03-e3da-cbcd-4843-85238bfe6034
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/muzeek-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/muzeek-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/muzeek-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f5876341-b5f3-af6a-ff24-30e5d571aaac
---

# Configure Muzeek for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Muzeek with Microsoft Entra ID. When you integrate Muzeek with Microsoft Entra ID, you can:

Use Microsoft Entra ID to control who can access Muzeek. Enable your users to be automatically signed in to Muzeek with their Microsoft Entra accounts. Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Muzeek single sign-on (SSO) enabled subscription.

## Add Muzeek from the gallery

To configure the integration of Muzeek into Microsoft Entra ID, you need to add Muzeek from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Muzeek** in the search box.
4. Select **Muzeek** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Muzeek** &gt; **Single sign-on**.
3. Perform the following steps in the below section:

    a. Select **Go to application**.

    [![Screenshot showing the identity configuration.](common/go-to-application.png)](common/go-to-application.png#lightbox)

    b. Copy **Application (client) ID** and **Directory (tenant) ID**, use it later in the Muzeek side configuration.

    ![Screenshot of application client values.](media/muzeek-tutorial/application-id.png)
4. Navigate to **Authentication** tab on the left menu and perform the following steps:

    a. Enable the **Access tokens** and **ID tokens**

    [![Screenshot showing the Access tokens.](media/muzeek-tutorial/access-token.png)](media/muzeek-tutorial/access-token.png#lightbox)

    b. select **Save**.

    Note

    The **Redirect URIs** value is auto populate, you don't need to perform any manual configuration here.
5. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        [![Screenshot showing the client secrets value.](common/client-secret.png)](common/client-secret.png#lightbox)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the Muzeek side configuration.

        [![Screenshot showing how to add a client secret.](common/client.png)](common/client.png#lightbox)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Muzeek SSO

Below are the configuration steps to complete the OIDC federation setup:

1. Sign into the Muzeek site as an administrator.
2. Select **Settings** icon at the bottom of the page and perform of the below steps.

    [![Screenshot showing Muzeek configuration.](media/muzeek-tutorial/configuration.png)](media/muzeek-tutorial/configuration.png#lightbox)

    a. Go to the **Integrations** tab.

    b. In the **ENTRA Domain** field, enter the domain URL value using the following pattern: `https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize`

    Note

    The domain URL value isn't real, replace the **Tenant\_ID** value with actual **Directory (tenant) ID**, which you have copied from Entra side.

    c. In the **ENTRA Client ID** field, paste the **Application ID** value, which you have copied from Entra page.

    d. In the **ENTRA Client Secret** field, paste the value, which you have copied from **Certificates & secrets** section at Entra side.

    e. Select **Save Changes**.

    f. Once saved, Muzeek populates the **Home Page URL** which can be used later in Connect SSO via MyApps section. [![Screenshot showing the details of Home Page.](media/muzeek-tutorial/image.png)](media/muzeek-tutorial/image.png#lightbox)

## Connect SSO via MyApps

To connect your MyApps account to Muzeek in the Microsoft Entra admin center, please follow the below steps:

1. Navigate to **App Registrations** &gt; \*\*Muzeek **Branding & Properties**. [![Screenshot showing the app registrations of Muzeek.](media/muzeek-tutorial/home.png)](media/muzeek-tutorial/home.png#lightbox)
2. Paste the Home Page URL you copied from Muzeek portal into the **Home Page URL** field in Microsoft Entra admin center.
3. Select **Save** and wait for 10 - 15 minutes for the change to propagate in the system.

Once done, you should now be able to successfully navigate to your Muzeek account while logged into MyApps, and any users you have added to your tenant should be able to do so as well.