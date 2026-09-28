---
layout: Conceptual
title: Configure TINFOIL SECURITY for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tinfoil-security-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TINFOIL SECURITY.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4f7b1e71-24be-1e8a-3a97-6334d1d11750
document_version_independent_id: a4224974-613a-3695-31f3-64b6603b8ed5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tinfoil-security-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tinfoil-security-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tinfoil-security-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3c25c3a8-4012-ea3e-e7ef-d54ef391a7bb
---

# Configure TINFOIL SECURITY for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TINFOIL SECURITY with Microsoft Entra ID. When you integrate TINFOIL SECURITY with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TINFOIL SECURITY.
- Enable your users to be automatically signed-in to TINFOIL SECURITY with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- TINFOIL SECURITY single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- TINFOIL SECURITY supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add TINFOIL SECURITY from the gallery

To configure the integration of TINFOIL SECURITY into Microsoft Entra ID, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TINFOIL SECURITY** in the search box.
4. Select **TINFOIL SECURITY** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TINFOIL SECURITY

Configure and test Microsoft Entra SSO with TINFOIL SECURITY using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TINFOIL SECURITY.

To configure and test Microsoft Entra SSO with TINFOIL SECURITY, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TINFOIL SECURITY SSO**- to configure the single sign-on settings on application side.
    1. **Create TINFOIL SECURITY test user** - to have a counterpart of B.Simon in TINFOIL SECURITY that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TINFOIL SECURITY** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the application is pre-configured and the necessary URLs are already pre-populated with Azure. The user needs to save the configuration by selecting the **Save** button.
6. Visitly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, Visitly application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | accountid | UXXXXXXXXXXXXX |

    Note

    You get the accountid value explained later in the article.
8. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
9. In the **SAML Signing Certificate** section, copy the **Thumbprint Value** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
10. On the **Set up TINFOIL SECURITY** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TINFOIL SECURITY SSO

1. In a different web browser window, sign into your TINFOIL SECURITY company site as an administrator.
2. In the toolbar on the top, select **My Account**.

    ![Dashboard](media/tinfoil-security-tutorial/account.png)
3. Select **Security**.

    ![Security](media/tinfoil-security-tutorial/details.png)
4. On the **Single Sign-On** configuration page, perform the following steps:

    ![Single Sign-On](media/tinfoil-security-tutorial/certificate.png)

    a. Select **Enable SAML**.

    b. Select **Manual Configuration**.

    c. In **SAML Post URL** textbox, paste the value of **Login URL**.

    d. In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.

    e. Copy **Your Account ID** value and paste the value in **Source Attribute** textbox under **User Attributes & Claims** section in Azure portal.

    f. Select **Save**.

### Create TINFOIL SECURITY test user

In order to enable Microsoft Entra users to sign in to TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY. In the case of TINFOIL SECURITY, provisioning is a manual task.

**To get a user provisioned, perform the following steps:**

1. If the user is a part of an Enterprise account, you need to contact the TINFOIL SECURITY support team to get the user account created.
2. If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites. This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.

Note

You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the TINFOIL SECURITY for which you set up the SSO.
- You can use Microsoft My Apps. When you select the TINFOIL SECURITY tile in the My Apps, you should be automatically signed in to the TINFOIL SECURITY for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).