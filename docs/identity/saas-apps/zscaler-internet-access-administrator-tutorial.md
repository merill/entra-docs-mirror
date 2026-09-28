---
layout: Conceptual
title: Configure Zscaler Internet Access Administrator for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-internet-access-administrator-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zscaler Internet Access Administrator.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: afdacf5d-61ba-7631-fa49-c502efad69f4
document_version_independent_id: 89746314-7742-e2eb-32a6-dc9af224ae50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-internet-access-administrator-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-internet-access-administrator-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-internet-access-administrator-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5d79f58a-3b36-050c-07e6-a35dc1f22b00
---

# Configure Zscaler Internet Access Administrator for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zscaler Internet Access Administrator with Microsoft Entra ID. When you integrate Zscaler Internet Access Administrator with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zscaler Internet Access Administrator.
- Enable your users to be automatically signed-in to Zscaler Internet Access Administrator with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Zscaler Internet Access Administrator is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zscaler Internet Access Administrator single sign-on (SSO) enabled subscription.

Note

This integration is also available to use from Microsoft Entra US Government Cloud environment. You can find this application in the Microsoft Entra US Government Cloud Application Gallery and configure it in the same way as you do from public cloud.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Zscaler Internet Access Administrator supports **IDP** initiated SSO.

## Add Zscaler Internet Access Administrator from the gallery

To configure the integration of Zscaler Internet Access Administrator into Microsoft Entra ID, you need to add Zscaler Internet Access Administrator from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zscaler Internet Access Administrator** in the search box.
4. Select **Zscaler Internet Access Administrator** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zscaler Internet Access Administrator

Configure and test Microsoft Entra SSO with Zscaler Internet Access Administrator using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zscaler Internet Access Administrator.

To configure and test Microsoft Entra SSO with Zscaler Internet Access Administrator, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Zscaler Internet Access Administrator SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Zscaler Internet Access Administrator test user** - to have a counterpart of Britta Simon in Zscaler Internet Access Administrator that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler Internet Access Administrator** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** text box, type one of the following URLs as per your requirement:

    | Identifier |
    | --- |
    | `https://admin.zscaler.net` |
    | `https://admin.zscalerone.net` |
    | `https://admin.zscalertwo.net` |
    | `https://admin.zscalerthree.net` |
    | `https://admin.zscloud.net` |
    | `https://admin.zscalerbeta.net` |

    b. In the **Reply URL** text box, type one of the following URLs as per your requirement:

    | Reply URL |
    | --- |
    | `https://admin.zscaler.net/adminsso.do` |
    | `https://admin.zscalerone.net/adminsso.do` |
    | `https://admin.zscalertwo.net/adminsso.do` |
    | `https://admin.zscalerthree.net/adminsso.do` |
    | `https://admin.zscloud.net/adminsso.do` |
    | `https://admin.zscalerbeta.net/adminsso.do` |
6. Zscaler Internet Access Administrator application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes & Claims** section on application integration page. On the **Set up Single Sign-On with SAML page**, select **Edit** button to open **User Attributes & Claims** dialog.

    ![The Attribute link](media/zscaler-internet-access-administrator-tutorial/attributes.png)
7. In the **User Claims** section on the **User Attributes** dialog, configure SAML token attribute as shown in the image above and perform the following steps:

    | Name | Source Attribute |
    | --- | --- |
    | Role | user.assignedroles |

    a. Select **Add new claim** to open the **Manage user claims** dialog.

    b. From the **Source attribute** list, select the attribute value.

    c. Select **Ok**.

    d. Select **Save**.

    Note

    Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to configure Role in Microsoft Entra ID.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up Zscaler Internet Access Administrator** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Zscaler Internet Access Administrator SSO

1. In a different web browser window, log in to your Zscaler Internet Access Admin UI.
2. Go to **Administration &gt; Administrator Management** and perform the following steps and select Save:

    ![Screenshot shows Administrator Management with options to Enable SAML Authentication, upload S S L Certificate and specify an Issuer.](media/zscaler-internet-access-administrator-tutorial/management.png)

    a. Check **Enable SAML Authentication**.

    b. Select **Upload**, to upload the Azure SAML signing certificate that you have downloaded from Azure portal in the **Public SSL Certificate**.

    c. Optionally, for additional security, add the **Issuer** details to verify the Issuer of the SAML response.
3. On the Admin UI, perform the following steps:

    ![Screenshot shows the Admin U I where you can perform the steps.](media/zscaler-internet-access-administrator-tutorial/activation.png)

    a. Hover over the **Activation** menu near the bottom left.

    b. Select **Activate**.

### Create Zscaler Internet Access Administrator test user

The objective of this section is to create a user called Britta Simon in Zscaler Internet Access Administrator. Zscaler Internet Access doesn't support Just-In-Time provisioning for Administrator SSO. You're required to manually create an Administrator account. For steps on how to create an Administrator account, refer to Zscaler documentation:

https://help.zscaler.com/zia/adding-admins

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Zscaler Internet Access Administrator for which you set up the SSO
- You can use Microsoft My Apps. When you select the Zscaler Internet Access Administrator tile in the My Apps, you should be automatically signed in to the Zscaler Internet Access Administrator for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).