---
layout: Conceptual
title: Configure ServusConnect for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/servusconnect-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ServusConnect.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 74b43889-256e-73b7-6db6-3490a9e4c58a
document_version_independent_id: 55934947-1581-a11f-1ee7-a9cb424e4936
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/servusconnect-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/servusconnect-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/servusconnect-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2b6dc744-72bb-25aa-0dae-e99d9c5c4960
---

# Configure ServusConnect for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ServusConnect with Microsoft Entra ID. ServusConnect uses Microsoft Entra ID to manage user access and enable single sign-on with the ServusConnect maintenance operations platform. An existing ServusConnect subscription is required.

When you integrate ServusConnect with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ServusConnect.
- Enable your users to be automatically signed-in to ServusConnect with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for ServusConnect in your own Azure environment. ServusConnect supports **SP** initiated SSO and **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with ServusConnect, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- ServusConnect single sign-on (SSO) enabled subscription. If you don't have ServusConnect, you can [learn more and request a demo](https://www.netvendor.com/servusconnect/).

## Add application and assign users

Before you begin the process of configuring single sign-on, you must add the ServusConnect application from the Microsoft Entra gallery. You also need a user account to assign to the application. Prior to beginning rollout to your organization, consider creating and assigning a test user first.

### Add ServusConnect from the Microsoft Entra gallery

Add ServusConnect from the Microsoft Entra application gallery to configure single sign-on with ServusConnect. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and/or assign a Microsoft Entra user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a user (if required) and assign one or more users to the ServusConnect enterprise application. Only those users that you assign to the application is able to access ServusConnect via single sign-on. Note that you can assign individual users or entire groups.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ServusConnect** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, enter the value: `urn:amazon:cognito:sp:us-east-1_rlgU6e3y5`

    b. In the **Reply URL** textbox, enter the URL: `https://login.servusconnect.com/saml2/idpresponse`

    c. In the **Sign on URL** textbox, enter the URL: `https://app.servusconnect.com`
6. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)

## Configure ServusConnect SSO

To configure single sign-on with the **ServusConnect** application, you must send the **Federation Metadata XML** file downloaded from Azure portal to the [ServusConnect support team](mailto:support@servusconnect.com). When emailing the ServusConnect support team, please provide the following:

1. The Federation Metadata XML file.
2. A list of all email domains, which connect via SSO from your Microsoft Entra account.

The ServusConnect support team completes the SAML SSO connection and notifies you when it's ready.

## ServusConnect user accounts

ServusConnect user accounts may be provisioned before the user's first SSO attempt, or "just-in-time" as a result of the SSO attempt. However, the two methods differ in terms of what the user is able to access.

### Pre-provisioned users

Users who exist in ServusConnect with an email address that matches the SSO login is automatically given access to ServusConnect after the SSO operation.

### Just-in-time users and the Waiting Room

Users who don't yet exist in ServusConnect has a user account created with an email that matches the SSO login. However, these users are placed into a "Waiting Room" instead of being given direct access to ServusConnect. These users must be provisioned with the correct access levels and property-level access before SSO will allow them past the Waiting Room.

An existing ServusConnect user with appropriate access may complete the ServusConnect "New User" form found on the "Manage" page in ServusConnect for the site/property where they work. Once this is done, the ServusConnect support team processes the request and notifies the user via email. Then, the user may use SSO to sign in and access ServusConnect.

## Testing SSO

You may test your Microsoft Entra single sign-on configuration using one of the following methods:

- Select **Test this application**, this option redirects to ServusConnect Sign-on URL where you can initiate the login flow.
- Go to [ServusConnect Sign-on URL](https://app.servusconnect.com/) directly and initiate the login flow from there. See **Sign-on with SSO**, below.
- You can use Microsoft My Apps. When you select the ServusConnect tile in the My Apps, this option redirects to ServusConnect Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).

## Sign-on with SSO

In order to sign on, perform the following steps:

1. Visit the [ServusConnect Sign-on URL](https://app.servusconnect.com/).
2. Enter your email address and press **Continue**. Note that your email domain must match one you shared with ServusConnect during configuration. (See screenshot below.)

    ![Screenshot shows how to enter your email into the sign-on screen.](media/servusconnect-tutorial/sign-on-email.png)
3. If your domain is properly configured for SSO with Microsoft Entra ID, you see a **Log In with Microsoft** button. (See screenshot below.)

    ![Screenshot shows the Log In with Microsoft button.](media/servusconnect-tutorial/sign-on-microsoft.png)
4. After selecting the **Log In with Microsoft** button, you be directed to the standard Microsoft login screen. After successful login, you be redirected back to ServusConnect.
5. If there is an existing ServusConnect user matching the SSO authentication, you be immediately logged in. Otherwise, you enter the **Waiting Room** as pictured below.

    ![Screenshot shows the ServusConnect Waiting Room.](media/servusconnect-tutorial/waiting-room.png)