---
layout: Conceptual
title: Configure SolarWinds Service Desk (previously Samanage) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/samanage-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SolarWinds Service Desk (previously Samanage).
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: a9542543-ff14-b441-1e24-136c0108a9a3
document_version_independent_id: 756ea4f6-3274-fa69-93c7-808f36f8fef8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/samanage-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/samanage-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/samanage-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e7ee28a4-5320-9181-36f6-f947e19fc850
---

# Configure SolarWinds Service Desk (previously Samanage) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SolarWinds with Microsoft Entra ID. When you integrate SolarWinds with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SolarWinds.
- Enable your users to be automatically signed-in to SolarWinds with their Microsoft Entra accounts.
- Manage your accounts in one central location.

SolarWinds Service Desk is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- SolarWinds single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SolarWinds supports **SP** initiated SSO.
- SolarWinds supports [Automated user provisioning](samanage-provisioning-tutorial).

## Add SolarWinds from the gallery

To configure the integration of SolarWinds into Microsoft Entra ID, you need to add SolarWinds from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SolarWinds** in the search box.
4. Select **SolarWinds** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SolarWinds

Configure and test Microsoft Entra SSO with SolarWinds using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SolarWinds.

To configure and test Microsoft Entra SSO with SolarWinds, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SolarWinds SSO**- to configure the single sign-on settings on application side.
    1. **Create SolarWinds test user** - to have a counterpart of B.Simon in SolarWinds that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SolarWinds** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<Company Name>.samanage.com`

    Note

    These values aren't real. Update these values with the actual Sign-on URL and Identifier, which is explained later in the article. For more details contact [Samanage Client support team](https://www.samanage.com/support). You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up SolarWinds** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SolarWinds SSO

1. In a different web browser window, log into your SolarWinds company site as an administrator.
2. Select **Dashboard** and select **Setup** in left navigation pane.

    ![Dashboard](media/samanage-tutorial/tutorial-samanage-1.png)
3. Select **Single Sign-On**.

    ![Single Sign-On](media/samanage-tutorial/tutorial-samanage-2.png)
4. Navigate to **Login using SAML** section, perform the following steps:

    ![Login using SAML](media/samanage-tutorial/tutorial-samanage-3.png)

    a. Select **Enable Single Sign-On with SAML**.

    b. In the **Identity Provider URL** textbox, enter the value like `https://YourAccountName.samanage.com`.

    c. Confirm the **Login URL** matches the **Sign On URL** of **Basic SAML Configuration** section in Azure portal.

    d. In the **Logout URL** textbox, enter the value of **Logout URL**..

    e. In the **SAML Issuer** textbox, type the app id URI set in your identity provider.

    f. Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.

    g. Select **Create users if they don't exist in SolarWinds**.

    h. Select **Update**.

### Create SolarWinds test user

To enable Microsoft Entra users to log in to SolarWinds, they must be provisioned into SolarWinds. In the case of SolarWinds, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log into your SolarWinds company site as an administrator.
2. Select **Dashboard** and select **Setup** in left navigation pan.

    ![Setup](media/samanage-tutorial/tutorial-samanage-1.png)
3. Select the **Users** tab

    ![Users](media/samanage-tutorial/tutorial-samanage-6.png)
4. Select **New User**.

    ![New User](media/samanage-tutorial/tutorial-samanage-7.png)
5. Type the **Name** and the **Email Address** of a Microsoft Entra account you want to provision and select **Create user**.

    ![Create User](media/samanage-tutorial/tutorial-samanage-8.png)

    Note

    The Microsoft Entra account holder will receive an email and follow a link to confirm their account before it becomes active. You can use any other SolarWinds user account creation tools or APIs provided by SolarWinds to provision Microsoft Entra user accounts.

Note

SolarWinds also supports automatic user provisioning, you can find more details [here](samanage-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to SolarWinds Sign-on URL where you can initiate the login flow.
- Go to SolarWinds Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the SolarWinds tile in the My Apps, this option redirects to SolarWinds Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).