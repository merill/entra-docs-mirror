---
layout: Conceptual
title: Configure Freshservice for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/freshservice-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Freshservice.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 002415c7-2945-56fa-a280-084e7fa22abd
document_version_independent_id: 7f29a530-236b-197a-5e21-b6732652f684
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/freshservice-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/freshservice-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/freshservice-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 64cae7e3-f058-81eb-e16d-2362e396f99e
---

# Configure Freshservice for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Freshservice with Microsoft Entra ID. When you integrate Freshservice with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Freshservice.
- Enable your users to be automatically signed-in to Freshservice with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Freshservice is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Freshservice single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Freshservice supports **SP** initiated SSO.
- Freshservice supports [Automated user provisioning](freshservice-provisioning-tutorial).

## Add Freshservice from the gallery

To configure the integration of Freshservice into Microsoft Entra ID, you need to add Freshservice from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Freshservice** in the search box.
4. Select **Freshservice** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Freshservice

Configure and test Microsoft Entra SSO with Freshservice using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Freshservice.

To configure and test Microsoft Entra SSO with Freshservice, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Freshservice SSO**- to configure the single sign-on settings on application side.
    1. **Create Freshservice test user** - to have a counterpart of B.Simon in Freshservice that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Freshservice** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<company-name>.freshservice.com`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<company-name>.freshservice.com`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://<company-name>.freshservice.com/login/saml`

    Note

    These values aren't real. Update these values with the actual Sign on URL, Identifier and Reply URL. Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Freshservice** section on the **Azure portal**, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Freshservice SSO

1. In a different web browser window, sign in to your Freshservice company site as an administrator
2. In the menu on the left, select **Admin** and select **Helpdesk Security** in the **General Settings**.
3. In the **Security**, select **Go to Freshservice 360 Security**.
4. In the **Security** section, perform the following steps:

    ![Single Sign On](media/freshservice-tutorial/configure-3.png)

    a. For **Single Sign On**, select **On**.

    b. In the **Login Method**, select **SAML SSO**.

    c. In the **Entity ID provided by the IdP** textbox, paste **Entity ID** value, which you copied previously.

    d. In the **SAML SSO URL** textbox, paste **Login URL** value, which you copied previously.

    e. In the **Signing Options**, select **Only Signed Assertions** from the dropdown.

    f. In the **Logout URL** textbox, paste **Logout URL** value, which you copied previously.

    g. In the **Security Certificate** textbox, paste **Certificate (Base64)** value, which you have obtained earlier.

    h. Select **Save**.

## Create Freshservice test user

To enable Microsoft Entra users to sign in to FreshService, they must be provisioned into FreshService. In the case of FreshService, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your **FreshService** company site as an administrator.
2. In the menu on the left, select **Admin**.
3. In the **User Management** section, select **Requesters**.

    ![Requesters](media/freshservice-tutorial/create-user-1.png)
4. Select **New Requester**.

    ![New Requesters](media/freshservice-tutorial/create-user-2.png)
5. In the **New Requester** section, enter the required fields and select **Save**. ![New Requester](media/freshservice-tutorial/create-user-3.png)

    Note

    The Microsoft Entra account holder gets an email including a link to confirm the account before it becomes active

    Note

    You can use any other FreshService user account creation tools or APIs provided by FreshService to provision Microsoft Entra user accounts.

Note

Freshservice also supports automatic user provisioning, you can find more details [here](freshservice-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Freshservice Sign-on URL where you can initiate the login flow.
- Go to Freshservice Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Freshservice tile in the My Apps, you should be automatically signed in to the Freshservice for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).