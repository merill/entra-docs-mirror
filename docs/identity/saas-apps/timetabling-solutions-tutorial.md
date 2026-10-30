---
layout: Conceptual
title: Configure Timetabling Solutions for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/timetabling-solutions-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Timetabling Solutions.
ms.topic: how-to
ms.date: 2025-09-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 22f496e5-8f71-ec09-5115-edb88ae7aa16
document_version_independent_id: b43ca345-23be-be26-6ffc-c8000ac7ee52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/timetabling-solutions-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/timetabling-solutions-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/timetabling-solutions-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 58ba0441-5f2d-6cb8-ea84-2da0f435234c
---

# Configure Timetabling Solutions for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Timetabling Solutions with Microsoft Entra ID. When you integrate Timetabling Solutions with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Timetabling Solutions.
- Enable your users to be automatically signed-in to Timetabling Solutions with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Timetabling Solutions single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Timetabling Solutions supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Timetabling Solutions from the gallery

To configure the integration of Timetabling Solutions into Microsoft Entra ID, you need to add Timetabling Solutions from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Timetabling Solutions** in the search box.
4. Select **Timetabling Solutions** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure and test Microsoft Entra SSO for Timetabling Solutions

Configure and test Microsoft Entra SSO with Timetabling Solutions using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Timetabling Solutions.

To configure and test Microsoft Entra SSO with Timetabling Solutions, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Timetabling Solutions SSO**- to configure the single sign-on settings on application side.
    1. **Create Timetabling Solutions test user** - to have a counterpart of B.Simon in Timetabling Solutions that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Timetabling Solutions** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type the URL: `https://auth.timetabling.education`

    b. In the **Reply URL (Assertion Consumer Service URL)** text box, type the URL: `https://auth.timetabling.education`

    c. In the **Sign-on URL** text box, type the URL: `https://auth.timetabling.education`
6. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Screenshot shows to edit SAML Signing Certificate.](common/edit-certificate.png)
7. In the **SAML Signing Certificate** section, copy the **Thumbprint Value** and save it on your computer.

    ![Screenshot shows to copy thumbprint value.](common/copy-thumbprint.png)
8. On the **Set up Timetabling Solutions** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Timetabling Solutions SSO

In this section, you populate the relevant SSO values in the Timetabling Solutions Management Portal.

1. In the [Management Portal](https://admin.timetabling.education/), select **5 Settings**, and then select the **SAML SSO** tab.
2. Perform the following steps in the **SAML SSO** section:

    ![Screenshot for SSO settings.](media/timetabling-solutions-tutorial/timetabling-configuration.png)

    a. Enable SAML Integration.

    b. In the **SAML Login Path** textbox, paste the **Login URL** value, which you copied previously.

    c. In the **SAML Logout Path** textbox, paste the **Logout URL** value, which you copied previously.

    d. In the **SAML Certificate Fingerprint** textbox, paste the **Thumbprint Value**, which you copied previously.

    e. Enter the **Custom Domain** name.

    f. **Save** the settings.

## Create Timetabling Solutions test user

In this section, you create a user called Britta Simon in the Timetabling Solutions Management Portal.

1. In the [Management Portal](https://admin.timetabling.education/), select **1 Manage Users**, and select **Add**.
2. Enter the mandatory fields **First Name**, **Family Name** and **Email Address**. Add other appropriate values in the non-mandatory fields.
3. Ensure **Online** is active in Status.
4. Select **Save and Next**.

Note

To add the users in the Timetabling Solutions platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Timetabling Solutions Sign-On URL where you can initiate the login flow.
- Go to Timetabling Solutions Sign-On URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Timetabling Solutions tile in the My Apps, this option redirects to Timetabling Solutions Sign-On URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).