---
layout: Conceptual
title: Configure TalentLMS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/talentlms-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TalentLMS.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 384d6ce5-d2cb-558a-629f-159de5c1517b
document_version_independent_id: a5e63730-7a03-ee41-e7cb-50bd07863269
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/talentlms-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/talentlms-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/talentlms-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1a9d6617-6b01-4293-3add-26a19836eb96
---

# Configure TalentLMS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TalentLMS with Microsoft Entra ID. When you integrate TalentLMS with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TalentLMS.
- Enable your users to be automatically signed-in to TalentLMS with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- TalentLMS single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- TalentLMS supports **SP** initiated SSO.

## Add TalentLMS from the gallery

To configure the integration of TalentLMS into Microsoft Entra ID, you need to add TalentLMS from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TalentLMS** in the search box.
4. Select **TalentLMS** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TalentLMS

Configure and test Microsoft Entra SSO with TalentLMS using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TalentLMS.

To configure and test Microsoft Entra SSO with TalentLMS, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TalentLMS SSO**- to configure the single sign-on settings on application side.
    1. **Create TalentLMS test user** - to have a counterpart of B.Simon in TalentLMS that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TalentLMS** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `<tenant-name>.talentlms.com`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
7. In the **SAML Signing Certificate** section, copy the **THUMBPRINT** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
8. On the **Set up TalentLMS** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TalentLMS SSO

1. In a different web browser window, sign in to your TalentLMS company site as an administrator.
2. In the **Account & Settings** section, select the **Users** tab.

    ![Account &amp; Settings](media/talentlms-tutorial/user.png)
3. Select **Single Sign-On (SSO)**,
4. In the Single Sign-On section, perform the following steps:

    ![Single Sign-On](media/talentlms-tutorial/certificate.png)

    a. From the **SSO integration type** list, select **SAML 2.0**.

    b. In the **Identity provider (IDP)** textbox, paste the value of **Microsoft Entra Identifier**.

    c. Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.

    d. In the **Remote sign-in URL** textbox, paste the value of **Login URL**.

    e. In the **Remote sign-out URL** textbox, paste the value of **Logout URL**.

    f. Fill in the following:

    - In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
    - In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    - In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    - In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
5. Select **Save**.

### Create TalentLMS test user

To enable Microsoft Entra users to sign in to TalentLMS, they must be provisioned into TalentLMS. In the case of TalentLMS, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your **TalentLMS** tenant.
2. Select **Users**, and then select **Add User**.
3. On the **Add user** dialog page, perform the following steps:

    ![Add User](media/talentlms-tutorial/account.png)

    a. In the **First name** textbox, enter the first name of user like `Britta`.

    b. In the **Last name** textbox, enter the last name of user like `Simon`.

    c. In the **Email address** textbox, enter the email of user like `brittasimon@contoso.com`.

    d. Select **Add User**.

Note

You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to TalentLMS Sign-on URL where you can initiate the login flow.
- Go to TalentLMS Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the TalentLMS tile in the My Apps, this option redirects to TalentLMS Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).