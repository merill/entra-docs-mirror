---
layout: Conceptual
title: Configure Acronis Cyber Protect Cloud for Single Sign-On with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/acronis-cyber-protect-cloud-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Acronis Cyber Protect Cloud.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: b3c1cf70-c159-970d-fbd7-6be2f132b076
document_version_independent_id: b3c1cf70-c159-970d-fbd7-6be2f132b076
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/acronis-cyber-protect-cloud-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/acronis-cyber-protect-cloud-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/acronis-cyber-protect-cloud-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c32dbea3-94b0-dd73-cadb-1ee42cbd2ab6
---

# Configure Acronis Cyber Protect Cloud for Single Sign-On with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Acronis Cyber Protect Cloud with Microsoft Entra ID. When you integrate Acronis Cyber Protect Cloud with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Acronis Cyber Protect Cloud.
- Enable your users to be automatically signed on to Acronis Cyber Protect Cloud with their Microsoft Entra accounts.
- Control SP-initiated and IDP-initiated SAML Single Logout (SLO) processes.
- Manage your accounts in one central location.
- By-pass Acronis 2FA challenge.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An Acronis Cyber Protect Cloud subscription. You can [subscribe for a free 30-day trial](https://www.acronis.com/products/cloud/trial/).
- An Acronis Cyber Protect Cloud **partner tenant**.
- An Acronis Cyber Protect Cloud user account with the company administrator role.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Acronis Cyber Protect Cloud supports both **SP-initiated** and **IDP-initiated** SSO.

## Configure and test the Acronis integration with Microsoft Entra ID

### Activate the Acronis integration with Microsoft Entra ID

You must first activate the Acronis integration with Microsoft Entra ID for your Acronis partner tenant.

1. Open a browser tab.
2. Sign in to Acronis Management Portal as a partner administrator.
3. Select **INTEGRATIONS** from the main menu.
4. Locate the **Microsoft Entra ID** catalog card.
5. Hover over the **Microsoft Entra ID** catalog card and click **Configure**.
6. Enter your Microsoft Entra ID domain.
7. Click **Next**. Do not close this browser tab.

### Add Acronis Cyber Protect Cloud from the gallery

To configure the integration of Acronis Cyber Protect Cloud into Microsoft Entra ID, you need to add Acronis Cyber Protect Cloud from the gallery to your list of managed SaaS apps.

1. Open a new browser tab.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
3. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
4. In the **Add from the gallery** section, type **Acronis Cyber Protect Cloud** in the search box.
5. Select **Acronis Cyber Protect Cloud** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

1. Open the application.
2. Select **Single sign-on** from the menu, and select the **SAML** single sign-on method.
3. Click **Edit** in the **Basic SAML Configuration** section.
4. Switch back to the Acronis Cyber Protect Cloud browser tab and click the copy icon in the **Identifier (Entity ID)** field to copy the value.
5. Switch to the Microsoft Entra admin center browser tab and paste the copied value into the **Identifier (Entity ID)** field.
6. Switch back to the Acronis Cyber Protect Cloud browser tab again and click the copy icon in the **Reply URL (Assertion Consumer Service URL)** field to copy the value.
7. Switch to the Microsoft Entra admin center browser tab and paste the copied value into the **Reply URL (Assertion Consumer Service URL)** field.
8. Click Save.
9. In the Microsoft Entra admin center browser tab, scroll down to the SAML Certificates and click **Download** to download the **Federation Metadata XML** file.
10. Switch to the Acronis Cyber Protect Cloud browser tab. In **App Federation Metadata**, click **Browse files...** to upload the Federation Metadata XML file you downloaded in the previous step.
11. Click **Activate**.

## Configure and test Microsoft Entra SSO for Acronis Cyber Protect Cloud

Configure and test Microsoft Entra SSO with Acronis Cyber Protect Cloud using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Acronis Cyber Protect Cloud.

To configure and test Microsoft Entra SSO with Acronis Cyber Protect Cloud, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Create a Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Create and enable Acronis Cyber Protect Cloud test user** - to have a counterpart of B.Simon in Acronis Cyber Protect Cloud that's linked to the Microsoft Entra ID representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Acronis Cyber Protect Cloud** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a value using the following pattern: `urn:cyber:protect:saml:<YOUR_ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<YOUR_DOMAIN>/api/2/saml/callback`

    c. In the **Logout URL** text box, type a URL using the following pattern: `https://<YOUR_DOMAIN>/api/2/saml/logout`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Logout URL. Contact [Acronis Cyber Protect Cloud support team](mailto:mspsupport@acronis.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. On the **Set up Acronis Cyber Protect Cloud** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create and enable the Acronis Cyber Protect Cloud test user

1. In Acronis Management Portal, create a user called B.Simon to map with the user you created in Microsoft Entra ID. Acronis sends an activation email to the new user.
2. Open the email and activate the user.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select Test this application in Microsoft Entra admin center and you should be automatically signed in to the Acronis Cyber Protect Cloud for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Acronis Cyber Protect Cloud tile in the My Apps, you should be automatically signed in to the Acronis Cyber Protect Cloud for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).