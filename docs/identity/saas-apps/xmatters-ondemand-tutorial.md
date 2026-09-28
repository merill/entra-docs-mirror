---
layout: Conceptual
title: Configure xMatters OnDemand for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/xmatters-ondemand-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and xMatters OnDemand.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c875771d-2f98-cfbf-86cf-c89a36282654
document_version_independent_id: 36f16c66-cfcd-9c5a-3c13-62cfe20e012c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/xmatters-ondemand-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/xmatters-ondemand-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/xmatters-ondemand-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e7c70589-ac3a-f207-32c9-4a6e92987fc7
---

# Configure xMatters OnDemand for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate xMatters OnDemand with Microsoft Entra ID. When you integrate xMatters OnDemand with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to xMatters OnDemand.
- Enable your users to be automatically signed-in to xMatters OnDemand with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- xMatters OnDemand single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- xMatters OnDemand supports **IDP** initiated SSO.

## Add xMatters OnDemand from the gallery

To configure the integration of xMatters OnDemand into Microsoft Entra ID, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **xMatters OnDemand** in the search box.
4. Select **xMatters OnDemand** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for xMatters OnDemand

Configure and test Microsoft Entra SSO with xMatters OnDemand using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in xMatters OnDemand.

To configure and test Microsoft Entra SSO with xMatters OnDemand, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure xMatters OnDemand SSO**- to configure the Single Sign-On settings on application side.
    1. **Create xMatters OnDemand test user** - to have a counterpart of Britta Simon in xMatters OnDemand that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **xMatters OnDemand** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    | Identifier |
    | --- |
    | `https://<COMPANY_NAME>.au1.xmatters.com.au/` |
    | `https://<COMPANY_NAME>.cs1.xmatters.com/` |
    | `https://<COMPANY_NAME>.xmatters.com/` |
    | `https://www.xmatters.com` |
    | `https://<COMPANY_NAME>.xmatters.com.au/` |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://<COMPANY_NAME>.au1.xmatters.com.au` |
    | `https://<COMPANY_NAME>.xmatters.com/sp/<INSTANCE_NAME>` |
    | `https://<COMPANY_NAME>.cs1.xmatters.com/sp/<INSTANCE_NAME>` |
    | `https://<COMPANY_NAME>.au1.xmatters.com.au/<INSTANCE_NAME>` |

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [xMatters OnDemand Client support team](https://www.xmatters.com/company/contact-us/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)

    Important

    You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/). The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.
7. On the **Set up xMatters OnDemand** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure xMatters OnDemand SSO

1. In a different web browser window, sign in to your xMatters OnDemand company site as an administrator.
2. Select **Admin**, and then select **Company Details**.

    ![Admin page](media/xmatters-ondemand-tutorial/admin.png)
3. On the **SAML Configuration** page, perform the following steps:

    ![SAML configuration section](media/xmatters-ondemand-tutorial/saml-configuration.png)

    a. Select **Enable SAML**.

    b. In the **Identity Provider ID** textbox, paste **Microsoft Entra Identifier** value which you copied previously.

    c. In the **Single Sign On URL** textbox, paste **Login URL** value which you copied previously.

    d. In the **Logout URL Redirect** textbox, paste **Logout URL**, which you copied previously.

    e. Select **Choose File** to upload the **Certificate (Base64)** which you have downloaded.

    f. On the Company Details page, at the top, select **Save Changes**.

    ![Company details](media/xmatters-ondemand-tutorial/save-button.png)

### Create xMatters OnDemand test user

1. Sign in to your **xMatters OnDemand** tenant.
2. Go to the **Users Icon** &gt; **Users** and then select **Add Users**.

    ![Users](media/xmatters-ondemand-tutorial/add-user.png)
3. In the **Add Users** section, fill the required fields and select **Add User** button.

    ![Add a User](media/xmatters-ondemand-tutorial/add-user-2.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the xMatters OnDemand for which you set up the SSO.
- You can use Microsoft My Apps. When you select the xMatters OnDemand tile in the My Apps, you should be automatically signed in to the xMatters OnDemand for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).