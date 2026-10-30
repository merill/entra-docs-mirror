---
layout: Conceptual
title: Configure Treasury Intelligence Solutions (TIS) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/treasury-intelligence-solutions-tis-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Treasury Intelligence Solutions (TIS).
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: fbb5781a-fa48-23fe-4f3e-c908a467aa86
document_version_independent_id: 3fa014d7-38df-5afc-45ae-ed1847e3aea7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/treasury-intelligence-solutions-tis-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/treasury-intelligence-solutions-tis-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/treasury-intelligence-solutions-tis-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e57d3086-a46a-3814-c6b9-ba076d686d17
---

# Configure Treasury Intelligence Solutions (TIS) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Treasury Intelligence Solutions (TIS) with Microsoft Entra ID. When you integrate Treasury Intelligence Solutions (TIS) with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Treasury Intelligence Solutions (TIS).
- Enable your users to be automatically signed-in to Treasury Intelligence Solutions (TIS) with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Treasury Intelligence Solutions (TIS) single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Treasury Intelligence Solutions (TIS) supports both **SP and IDP** initiated SSO.

## Add Treasury Intelligence Solutions (TIS) from the gallery

To configure the integration of Treasury Intelligence Solutions (TIS) into Microsoft Entra ID, you need to add Treasury Intelligence Solutions (TIS) from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Treasury Intelligence Solutions (TIS)** in the search box.
4. Select **Treasury Intelligence Solutions (TIS)** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Treasury Intelligence Solutions (TIS)

Configure and test Microsoft Entra SSO with Treasury Intelligence Solutions (TIS) using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Treasury Intelligence Solutions (TIS).

To configure and test Microsoft Entra SSO with Treasury Intelligence Solutions (TIS), perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Treasury Intelligence Solutions (TIS) SSO**- to configure the single sign-on settings on application side.
    1. **Create Treasury Intelligence Solutions (TIS) test user** - to have a counterpart of B.Simon in Treasury Intelligence Solutions (TIS) that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Treasury Intelligence Solutions (TIS)** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type one of the following URLs:

    | Environment | URL |
    | --- | --- |
    | Production | `https://eu.tispayments.com` , `https://us.tispayments.com` |
    | Test | `https://eu-test.tispayments.com` , `https://us-test.tispayments.com` |

    b. In the **Reply URL** text box, type one of the following URLs:

    | Environment | URL |
    | --- | --- |
    | Production | `https://login.eu.tispayments.com/iam-server/SamlSsoLogin` , `https://login.us.tispayments.com/iam-server/SamlSsoLogin` |
    | Test | `https://login.eu-test.tispayments.com/iam-server/SamlSsoLogin` , `https://login.us-test.tispayments.com/iam-server/SamlSsoLogin` |
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type any one of the URLs:

    | Environment | URL |
    | --- | --- |
    | Production | `https://login.eu.tispayments.com` , `https://login.us.tispayments.com` |
    | Test | `https://login.eu-test.tispayments.com` , `https://login.us-test.tispayments.com` |
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (PEM)** and select **PEM certificate download** to download the certificate and save it on your computer.

    ![Certificate shows the Certificate download link.](common/certificate-base64-download.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Treasury Intelligence Solutions (TIS) SSO

To configure single sign-on on **Treasury Intelligence Solutions** side:

1. In TIS, navigate to **Administration** &gt; **Security** &gt; **Single Sign-On Configuration** and select either **IdP-initiated Single Sign-On** or **SP-initiated Single Sign-On**
2. Provide the **Identity Provider (Entity ID)**. This is the value that's provided by Microsoft Entra SSO in the field **Microsoft Entra Identifier**.
3. For the Certificate, select the **PEM certificate** downloaded on your computer.
4. For **SP-initiated Single Sign-On**, provide the **Identity Provider Login URL** which was shown in the field **Login URL**. For the **IdP-initiated Single Sign-On**, both fields **User Login URL** and **User Logout URL** are optional and can be left blank.

### Create Treasury Intelligence Solutions (TIS) test user

In this section, you create a user called B.Simon in Treasury Intelligence Solutions (TIS).

1. For the new user, SSO has to be enabled by selecting the new user and then choose **Edit** &gt; **SSO user** &gt; **Enable SSO Login**.
2. The value for **SSO** id is provided by Microsoft Entra. By default this is the user's attribute **user.userprincipalname** (can be changed by choosing another attribute for **Unique User Identifier** in Microsoft Entra SSO).
3. Select the test user in Microsoft Entra ID and copy the value for **User principal name** and paste it into the field **SSO id** in TIS.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to Treasury Intelligence Solution (TIS) Sign on URL where you can initiate the login flow.
- Go to Treasury Intelligence Solution (TIS) Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to the Treasury Intelligence Solution (TIS) for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Treasury Intelligence Solution (TIS) tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Treasury Intelligence Solution for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).