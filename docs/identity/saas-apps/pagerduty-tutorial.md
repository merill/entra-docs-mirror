---
layout: Conceptual
title: Configure PagerDuty for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/pagerduty-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and PagerDuty.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8d904d9d-5d25-9648-17fa-6f5516ff1f0f
document_version_independent_id: bb8369b7-6681-4bf8-23ae-9eee48eb31ce
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/pagerduty-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/pagerduty-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/pagerduty-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 14770aa2-edb3-7202-83f3-48a933eaa76f
---

# Configure PagerDuty for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate PagerDuty with Microsoft Entra ID. When you integrate PagerDuty with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to PagerDuty.
- Enable your users to be automatically signed-in to PagerDuty with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- PagerDuty single sign-on (SSO) enabled subscription.

Note

If you're using MFA or Passwordless authentication with Microsoft Entra ID then switch off the AuthnContext value in the SAML Request. Otherwise Microsoft Entra ID will throw the error on mismatch of the AuthnContext and doesn't send the token back to the application.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- PagerDuty supports **SP** initiated SSO

## Add PagerDuty from the gallery

To configure the integration of PagerDuty into Microsoft Entra ID, you need to add PagerDuty from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **PagerDuty** in the search box.
4. Select **PagerDuty** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra single sign-on for PagerDuty

Configure and test Microsoft Entra SSO with PagerDuty using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in PagerDuty.

To configure and test Microsoft Entra SSO with PagerDuty, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure PagerDuty SSO**- to configure the single sign-on settings on application side.
    1. **Create PagerDuty test user** - to have a counterpart of B.Simon in PagerDuty that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **PagerDuty** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL, Identifier and Reply URL. Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up PagerDuty** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure PagerDuty SSO

1. In a different web browser window, sign into your Pagerduty company site as an administrator.
2. In the menu on the top, select **Account Settings**.

    ![Account Settings](media/pagerduty-tutorial/ic778535.png)
3. Select **Single Sign-on**.

    ![Single sign-on](media/pagerduty-tutorial/ic778536.png)
4. On the **Enable Single Sign-on (SSO)** page, perform the following steps:

    ![Enable single sign-on](media/pagerduty-tutorial/ic778537.png)

    a. Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox

    b. In the **Login URL** textbox, paste **Login URL**..

    c. In the **Logout URL** textbox, paste **Logout URL**..

    d. Select **Allow username/password login**.

    e. Select **Require EXACT authentication context comparison** checkbox.

    f. Select **Save Changes**.

### Create PagerDuty test user

To enable Microsoft Entra users to sign into PagerDuty, they must be provisioned into PagerDuty. In the case of PagerDuty, provisioning is a manual task.

Note

You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Microsoft Entra user accounts.

**To provision a user account, perform the following steps:**

1. Sign into your **Pagerduty** tenant.
2. In the menu on the top, select **Users**.
3. Select **Add Users**.

    ![Add Users](media/pagerduty-tutorial/ic778539.png)
4. On the **Invite your team** dialog, perform the following steps:

    ![Invite your team](media/pagerduty-tutorial/ic778540.png)

    a. Type the **First and Last Name** of user like **B.Simon**.

    b. Enter **Email** address of user like **b.simon@contoso.com**.

    c. Select **Add**, and then select **Send Invites**.

    Note

    All added users will receive an invite to create a PagerDuty account.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to PagerDuty Sign-on URL where you can initiate the login flow.
- Go to PagerDuty Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the PagerDuty tile in the My Apps, this option redirects to PagerDuty Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).