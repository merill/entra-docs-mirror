---
layout: Conceptual
title: Configure RunMyProcess for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/runmyprocess-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and RunMyProcess.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: db775285-1688-8662-4ab6-cb953d0f6be6
document_version_independent_id: 095a95c3-f938-8303-2400-a7e037c3c85c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/runmyprocess-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/runmyprocess-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/runmyprocess-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 82073662-87e3-3a0e-cc50-f1de1805fd39
---

# Configure RunMyProcess for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate RunMyProcess with Microsoft Entra ID. When you integrate RunMyProcess with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to RunMyProcess.
- Enable your users to be automatically signed-in to RunMyProcess with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- RunMyProcess single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- RunMyProcess supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add RunMyProcess from the gallery

To configure the integration of RunMyProcess into Microsoft Entra ID, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **RunMyProcess** in the search box.
4. Select **RunMyProcess** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for RunMyProcess

Configure and test Microsoft Entra SSO with RunMyProcess using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in RunMyProcess.

To configure and test Microsoft Entra SSO with RunMyProcess, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure RunMyProcess SSO**- to configure the single sign-on settings on application side.
    1. **Create RunMyProcess test user** - to have a counterpart of B.Simon in RunMyProcess that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **RunMyProcess** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up RunMyProcess** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure RunMyProcess SSO

1. In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.
2. In left navigation panel, select **Account** and select **Configuration**.

    ![Screenshot shows Configuration selected from Account.](media/runmyprocess-tutorial/account.png)
3. Go to **Authentication method** section and perform below steps:

    ![Screenshot shows the Authentication method tab where you can enter the values described.](media/runmyprocess-tutorial/certificate.png)

    a. As **Method**, select **SSO with Samlv2**.

    b. In the **SSO redirect** textbox, paste the value of **Login URL**.

    c. In the **Logout redirect** textbox, paste the value of **Logout URL**.

    d. In the **Name ID Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.

    e. Open the downloaded certificate file from Azure portal in notepad, copy the content of certificate file and then paste it into the **Certificate** textbox.

    f. Select **Save** icon.

### Create RunMyProcess test user

In order to enable Microsoft Entra users to sign in to RunMyProcess, they must be provisioned into RunMyProcess. In the case of RunMyProcess, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your RunMyProcess company site as an administrator.
2. Select **Account** and select **Users** in left navigation panel, then select **New User**.

    ![New User](media/runmyprocess-tutorial/user.png)
3. In the **User Settings** section, perform the following steps:

    ![Profile](media/runmyprocess-tutorial/new-user.png)

    a. Type the **Name** and **E-mail** of a valid Microsoft Entra account you want to provision into the related textboxes.

    b. Select an **IDE language**, **Language**, and **Profile**.

    c. Select **Send account creation e-mail to me**.

    d. Select **Save**.

    Note

    You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to RunMyProcess Sign-on URL where you can initiate the login flow.
- Go to RunMyProcess Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the RunMyProcess tile in the My Apps, this option redirects to RunMyProcess Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).