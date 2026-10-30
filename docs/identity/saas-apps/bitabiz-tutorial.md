---
layout: Conceptual
title: Configure BitaBIZ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bitabiz-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and BitaBIZ.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7c0460bf-1b00-a1ed-947c-774e4f1a2f1a
document_version_independent_id: b8cf7c65-628e-b9cc-fd8d-4e8d17668479
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bitabiz-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bitabiz-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bitabiz-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ba69d59c-e8e6-ece4-23ff-48511f80a57d
---

# Configure BitaBIZ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate BitaBIZ with Microsoft Entra ID. When you integrate BitaBIZ with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to BitaBIZ.
- Enable your users to be automatically signed-in to BitaBIZ with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- BitaBIZ single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- BitaBIZ supports **SP and IDP** initiated SSO.
- BitaBIZ supports [Automated user provisioning](bitabiz-provisioning-tutorial).

## Add BitaBIZ from the gallery

To configure the integration of BitaBIZ into Microsoft Entra ID, you need to add BitaBIZ from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **BitaBIZ** in the search box.
4. Select **BitaBIZ** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for BitaBIZ

Configure and test Microsoft Entra SSO with BitaBIZ using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in BitaBIZ.

To configure and test Microsoft Entra SSO with BitaBIZ, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure BitaBIZ SSO**- to configure the Single Sign-On settings on application side.
    1. **Create BitaBIZ test user** - to have a counterpart of Britta Simon in BitaBIZ that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **BitaBIZ** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP initiated** mode perform the following steps:

    In the **Identifier** text box, type a URL using the following pattern: `https://www.bitabiz.com/<INSTANCE_ID>`

    Note

    The value in the above URL is for demonstration only. Update the value with the actual identifier, which is explained later in the article.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://www.bitabiz.com/dashboard`
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up BitaBIZ** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure BitaBIZ SSO

1. In a different web browser window, sign-on to your BitaBIZ tenant as an administrator.
2. Select **SETUP ADMIN**.

    ![Screenshot shows part of a browser window with Setup Admin selected.](media/bitabiz-tutorial/setup-admin.png)
3. Select **Microsoft integrations** under **Add value** section.
4. Scroll down to the section **Microsoft Entra ID (Enable single sign on)** and enter the appropriate values in the provided fields:

    a. Copy the value from the **Entity ID (”Identifier” in Microsoft Entra ID)** textbox and paste it into the **Identifier** textbox on the **Basic SAML Configuration** section in Azure portal.

    b. In the **Microsoft Entra Single Sign-On Service URL** textbox, paste **Login URL**.

    c. In the **Microsoft Entra SAML Entity ID** textbox, paste **Microsoft Entra Identifier**.

    d. Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Microsoft Entra ID Signing Certificate (Base64 encoded)** textbox.

    e. Add your business e-mail domain name that is, mycompany.com in **Domain name** textbox to assign SSO to the users in your company with this email domain (NOT MANDATORY).

    f. Mark **SSO enabled** the BitaBIZ account.

    g. Select **Save Microsoft Entra configuration** to save and activate the SSO configuration.

### Create BitaBIZ test user

To enable Microsoft Entra users to log in to BitaBIZ, they must be provisioned into BitaBIZ. In the case of BitaBIZ, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to your BitaBIZ company site as an administrator.
2. Select **SETUP ADMIN**.

    ![Screenshot shows part of your browser window with Setup Admin selected.](media/bitabiz-tutorial/setup-admin.png)
3. Select **Add users** under **Organization** section.

    ![Screenshot shows the Organization section with Add users selected.](media/bitabiz-tutorial/add-user.png)
4. Select **Add new employee**.

    ![Screenshot shows Add users with Add new employee selected.](media/bitabiz-tutorial/new-employee.png)
5. On the **Add new employee** dialog page, perform the following steps:

    ![Screenshot shows the page where you enter the information described in this step.](media/bitabiz-tutorial/save-employee.png)

    a. In the **First Name** textbox, type the first name of user like Britta.

    b. In the **Last Name** textbox, type the last name of user like Simon.

    c. In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.

    d. Select a date in **Date of employment**.

    e. There are other non-mandatory user attributes which can be set up for the user. Please refer the [Employee Setup Doc](https://help.bitabiz.dk/manage-or-set-up-your-account/on-boarding-employees/new-employee) for more details.

    f. Select **Save employee**.

    Note

    The Microsoft Entra account holder receives an email and follows a link to confirm their account before it becomes active.

Note

BitaBIZ also supports automatic user provisioning, you can find more details [here](bitabiz-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to BitaBIZ Sign on URL where you can initiate the login flow.
- Go to BitaBIZ Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the BitaBIZ for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the BitaBIZ tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the BitaBIZ for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).