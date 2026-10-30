---
layout: Conceptual
title: Configure Coupa for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/coupa-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Coupa.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f65ec9b8-c945-f89f-8e8a-765187fe9799
document_version_independent_id: 599229e9-2eff-0eb2-469a-6217b8c5759e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/coupa-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/coupa-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/coupa-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7802f7ef-f877-aabe-22df-95a8a9687f76
---

# Configure Coupa for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Coupa with Microsoft Entra ID. When you integrate Coupa with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Coupa.
- Enable your users to be automatically signed-in to Coupa with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Coupa single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Coupa supports **SP** initiated SSO

## Add Coupa from the gallery

To configure the integration of Coupa into Microsoft Entra ID, you need to add Coupa from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Coupa** in the search box.
4. Select **Coupa** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Coupa

Configure and test Microsoft Entra SSO with Coupa using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Coupa.

To configure and test Microsoft Entra SSO with Coupa, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Coupa SSO**- to configure the single sign-on settings on application side.
    1. **Create Coupa test user** - to have a counterpart of B.Simon inCoupa that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Coupa** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<companyname>.coupahost.com`

    Note

    The Sign-on URL value isn't real. Update this value with the actual Sign-On URL. Contact [Coupa Client support team](https://success.coupa.com/Support/Contact_Us?) to get this value.

    b. In the **Identifier** box, type the URL:

    | Environment | URL |
    | --- | --- |
    | Sandbox | `sso-stg1.coupahost.com` |
    | Production | `sso-prd1.coupahost.com` |
    |  |  |

    c. In the **Reply URL** text box, type the URL:

    | Environment | URL |
    | --- | --- |
    | Sandbox | `https://sso-stg1.coupahost.com/sp/ACS.saml2` |
    | Production | `https://sso-prd1.coupahost.com/sp/ACS.saml2` |
    |  |  |
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Coupa** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Coupa SSO

1. Sign on to your Coupa company site as an administrator.
2. Go to **Setup** &gt; **Security Control**.

    ![Security Controls](media/coupa-tutorial/setup.png)
3. In the **Log in using Coupa credentials** section, perform the following steps:

    ![Coupa SP metadata](media/coupa-tutorial/login.png)

    a. Select **Log in using SAML**.

    b. Select **Browse** to upload the metadata downloaded.

    c. Select **Save**.

### Create Coupa test user

In order to enable Microsoft Entra users to log into Coupa, they must be provisioned into Coupa.

- In the case of Coupa, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Log in to your **Coupa** company site as administrator.
2. In the menu on the top, select **Setup**, and then select **Users**.

    ![Users](media/coupa-tutorial/user.png)
3. Select **Create**.

    ![Create Users](media/coupa-tutorial/create.png)
4. In the **User Create** section, perform the following steps:

    ![User Details](media/coupa-tutorial/details.png)

    a. Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Microsoft Entra account you want to provision into the related textboxes.

    b. Select **Create**.

    Note

    The Microsoft Entra account holder gets an email with a link to confirm the account before it becomes active.

Note

You can use any other Coupa user account creation tools or APIs provided by Coupa to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Coupa Sign-on URL where you can initiate the login flow.
- Go to Coupa Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Coupa tile in the My Apps, you should be automatically signed in to the Coupa for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).