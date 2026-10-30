---
layout: Conceptual
title: Configure Gigya for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/gigya-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Gigya.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 95d574ab-b5a3-d526-ee39-534d5218a9a8
document_version_independent_id: f286a8d1-6192-a333-5bb6-5df3f1569124
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/gigya-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/gigya-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/gigya-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ced0659f-e890-f7f3-1f94-28bac1172b26
---

# Configure Gigya for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Gigya with Microsoft Entra ID. When you integrate Gigya with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Gigya.
- Enable your users to be automatically signed-in to Gigya with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Gigya single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Gigya supports **SP** initiated SSO.

## Add Gigya from the gallery

To configure the integration of Gigya into Microsoft Entra ID, you need to add Gigya from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Gigya** in the search box.
4. Select **Gigya** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Gigya

Configure and test Microsoft Entra SSO with Gigya using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Gigya.

To configure and test Microsoft Entra SSO with Gigya, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Gigya SSO**- to configure the single sign-on settings on application side.
    1. **Create Gigya test user** - to have a counterpart of B.Simon in Gigya that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Gigya** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `http://<companyname>.gigya.com`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Gigya Client support team](https://developers.gigya.com/display/GD/Opening+A+Support+Incident) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Gigya** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Gigya SSO

1. In a different web browser window, log into your Gigya company site as an administrator.
2. Go to **Settings** &gt; **SAML Login**, and then select the **Add** button.

    ![SAML Login](media/gigya-tutorial/login.png)
3. In the **SAML Login** section, perform the following steps:

    ![SAML Configuration](media/gigya-tutorial/configuration.png)

    a. In the **Name** textbox, type a name for your configuration.

    b. In **Issuer** textbox, paste the value of **Microsoft Entra Identifier**..

    c. In **Single Sign-On Service URL** textbox, paste the value of **Login URL**..

    d. In **Name ID Format** textbox, paste the value of **Name Identifier Format**..

    e. Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.

    f. Select **Save Settings**.

## Create Gigya test user

In order to enable Microsoft Entra users to log into Gigya, they must be provisioned into Gigya. In the case of Gigya, provisioning is a manual task.

### To provision a user accounts, perform the following steps:

1. Log in to your **Gigya** company site as an administrator.
2. Go to **Admin** &gt; **Manage Users**, and then select **Invite Users**.

    ![Manage Users](media/gigya-tutorial/users.png)
3. On the Invite Users dialog, perform the following steps:

    ![Invite Users](media/gigya-tutorial/invite-user.png)

    a. In the **Email** textbox, type the email alias of a valid Microsoft Entra account you want to provision.

    b. Select **Invite User**.

    Note

    The Microsoft Entra account holder will receive an email that includes a link to confirm the account before it becomes active.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Gigya Sign-on URL where you can initiate the login flow.
- Go to Gigya Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Gigya tile in the My Apps, this option redirects to Gigya Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).