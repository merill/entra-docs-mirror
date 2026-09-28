---
layout: Conceptual
title: Configure Beeline Enterprise for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/beeline-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Beeline Enterprise.
ms.topic: how-to
ms.date: 2024-08-29T00:00:00.0000000Z
locale: en-us
document_id: 74c57f4a-0452-4089-26e1-4997e2867341
document_version_independent_id: 90978229-6d94-0b41-9740-372227f7572c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/beeline-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/beeline-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/beeline-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 54f9a9ff-160a-eed6-e769-6f77b89851e4
---

# Configure Beeline Enterprise for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Beeline Enterprise with Microsoft Entra ID. When you integrate Beeline Enterprise with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Beeline Enterprise.
- Enable your users to be automatically signed-in to Beeline Enterprise with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Beeline Enterprise single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Beeline Enterprise supports **SP** and **IDP** initiated SSO.

## Add Beeline Enterprise from the gallery

To configure the integration of Beeline Enterprise into Microsoft Entra ID, you need to add Beeline Enterprise from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Browse Microsoft Entra Gallery** section, type **Beeline Enterprise** in the search box.
4. Select **Beeline Enterprise** from the results panel and then select **Create**. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Beeline Enterprise

Configure and test Microsoft Entra SSO with Beeline Enterprise using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Beeline Enterprise.

To configure and test Microsoft Entra SSO with Beeline Enterprise, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Beeline Enterprise SSO**- to configure the single sign-on settings on application side.
    1. **Create Beeline Enterprise test user** - to have a counterpart of B.Simon in Beeline that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Beeline Enterprise** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a value using the following pattern: `urn:auth0:<Auth0TenantName>:<CustomerName>-SSO`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<Auth0TenantName>.<Auth0Environment>.beeline.com/login/callback?connection=<CustomerName>-SSO`
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** text box, type a URL using the following pattern: `https://<Environment>.beeline.com/<CustomerName>/security/auth0/auth0spinitiatedssohandler.ashx`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Beeline Enterprise support team](mailto:support@beeline.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Select **Save**.
8. The Beeline Enterprise application expects the SAML assertions in a specific format. Please work with [Beeline Enterprise support team](mailto:support@beeline.com) first to identify the correct user identifier which is mapped into the application. Also please take the guidance from [Beeline Enterprise support team](mailto:support@beeline.com) about the attribute which they want to use for this mapping. You can manage the value of this attribute from the **User Attributes** tab of the application. The following screenshot shows an example for this. Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which is sent to the Beeline Enterprise application in every successful SAML response.

    ![Screenshot shows the image of default attributes.](common/edit-attribute.png)
9. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Beeline Enterprise** &gt; **Manage** &gt; **Single sign-on**.
10. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
11. In the **Set up Beeline Enterprise** section, copy the **Login URL** and **Logout URL**.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Beeline Enterprise SSO

To configure single sign-on on **Beeline Enterprise** side, you need to send the following items that you gathered from a step earlier in this article to the [Beeline Enterprise support team](mailto:support@beeline.com). They will configure single sign-on on the **Beeline Enterprise** side.

- **Certificate (Base64)**
- **Login URL**
- **Logout URL**

### Create Beeline Enterprise test user

In this section, you create a user, Britta Simon, in Beeline Enterprise. The Beeline Enterprise application needs all users to be provisioned in the application before doing Single Sign On. So work with the [Beeline Enterprise support team](mailto:support@beeline.com) to provision all these users into the application.

## Test SSO

In this section, you have two different ways to test your Microsoft Entra single sign-on configuration.

- Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Beeline Enterprise** &gt; **Manage** &gt; **Single sign-on**. Select **Test this application**, and you should be automatically signed in to the Beeline Enterprise for which you set up the SSO.
- You can use Microsoft My Apps. When you select the **Beeline Enterprise** tile in **My Apps**, you should be automatically signed in to the Beeline Enterprise site for which you set up the SSO. For more information about the My Apps portal, see [Introduction to the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).