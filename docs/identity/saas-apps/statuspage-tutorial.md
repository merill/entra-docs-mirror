---
layout: Conceptual
title: Configure StatusPage for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/statuspage-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and StatusPage.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 606c661d-9a7d-6d56-0070-6d0d846dcf3c
document_version_independent_id: b226b61a-ea05-809a-2613-b94e277c0416
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/statuspage-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/statuspage-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/statuspage-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c1221de2-5bea-196a-a198-76c308190cea
---

# Configure StatusPage for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate StatusPage with Microsoft Entra ID. When you integrate StatusPage with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to StatusPage.
- Enable your users to be automatically signed-in to StatusPage with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- StatusPage single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- StatusPage supports **IDP** initiated SSO.

## Add StatusPage from the gallery

To configure the integration of StatusPage into Microsoft Entra ID, you need to add StatusPage from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **StatusPage** in the search box.
4. Select **StatusPage** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for StatusPage

In this section, you configure and test Microsoft Entra single sign-on with StatusPage based on a test user called **Britta Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in StatusPage needs to be established.

To configure and test Microsoft Entra SSO with StatusPage, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure StatusPage SSO**- to configure the Single Sign-On settings on application side.
    1. **Create StatusPage test user** - to have a counterpart of Britta Simon in StatusPage that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AskYourTeam** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up Single Sign-On with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    | Identifier |
    | --- |
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |
    |  |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |
    |  |

    Note

    Contact the StatusPage support team at SupportTeam@statuspage.ioto request metadata necessary to configure single sign-on.

    a. From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.

    b. From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up StatusPage** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure StatusPage SSO

1. In a different web browser window, sign in to your StatusPage company site as an administrator
2. In the main toolbar, select **Manage Account**.

    ![Screenshot shows Manage Account selected from the StatusPage company site.](media/statuspage-tutorial/account.png)
3. Select the **Single Sign-on** tab.
4. On the SSO Setup page, perform the following steps:

    ![Screenshot shows the S S O Setup page where you can enter the values described.](media/statuspage-tutorial/setup.png)

    ![Screenshot shows the Save Configuration button.](media/statuspage-tutorial/configuration.png)

    a. In the **SSO Target URL** textbox, paste the value of **Login URL**.

    b. Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.

    c. Select **SAVE CONFIGURATION**.

### Create StatusPage test user

The objective of this section is to create a user called Britta Simon in StatusPage.

StatusPage supports just-in-time provisioning. You have already enabled it in Configure Microsoft Entra Single Sign-On.

**To create a user called Britta Simon in StatusPage, perform the following steps:**

1. Sign-on to your StatusPage company site as an administrator.
2. In the menu on the top, select **Manage Account**.

    ![Screenshot shows Manage Account selected from the StatusPage company site.](media/statuspage-tutorial/account.png)
3. Select the **Team Members** tab.
4. Select **ADD TEAM MEMBER**.

    ![Screenshot shows the Add Team Member button.](media/statuspage-tutorial/team.png)
5. Type the **Email Address**, **First Name**, and **Surname** of a valid user you want to provision into the related textboxes.
6. As **Role**, choose **Client Administrator**.
7. Select **CREATE ACCOUNT**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the StatusPage for which you set up the SSO
- You can use Microsoft My Apps. When you select the StatusPage tile in the My Apps, you should be automatically signed in to the StatusPage for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).