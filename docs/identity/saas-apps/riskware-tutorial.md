---
layout: Conceptual
title: Configure Riskware for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/riskware-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Riskware.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3bdf34cb-9176-5d83-86f4-9c7114480f4b
document_version_independent_id: 9d5353eb-62a9-cca4-4d46-7a4bc8e934a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/riskware-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/riskware-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/riskware-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 69263bca-74b1-c7a7-86ba-a7522f656394
---

# Configure Riskware for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Riskware with Microsoft Entra ID. When you integrate Riskware with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Riskware.
- Enable your users to be automatically signed-in to Riskware with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with Riskware, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Riskware single sign-on enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Riskware supports **SP** initiated SSO.

## Add Riskware from the gallery

To configure the integration of Riskware into Microsoft Entra ID, you need to add Riskware from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Riskware** in the search box.
4. Select **Riskware** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Riskware

Configure and test Microsoft Entra SSO with Riskware using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Riskware.

To configure and test Microsoft Entra SSO with Riskware, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Riskware SSO**- to configure the single sign-on settings on application side.
    1. **Create Riskware test user** - to have a counterpart of B.Simon in Riskware that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Riskware** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type one of the following URLs:

    | Environment | URL |
    | --- | --- |
    | UAT | `https://riskcloud.net/uat` |
    | PROD | `https://riskcloud.net/prod` |
    | DEMO | `https://riskcloud.net/demo` |

    b. In the **Sign on URL** text box, type a URL using one of the following patterns:

    | Environment | URL Pattern |
    | --- | --- |
    | UAT | `https://riskcloud.net/uat?ccode=<COMPANYCODE>` |
    | PROD | `https://riskcloud.net/prod?ccode=<COMPANYCODE>` |
    | DEMO | `https://riskcloud.net/demo?ccode=<COMPANYCODE>` |

    Note

    The Sign on URL value isn't real. Update the value with the actual Sign-On URL. Contact [Riskware Client support team](mailto:support@pansoftware.com.au) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. On the **Set up Riskware** section, copy the appropriate URL(s) as per your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Riskware SSO

1. In a different web browser window, sign in to your Riskware company site as an administrator.
2. On the top right, select **Maintenance** to open the maintenance page.

    ![Screenshot shows the Riskware Configurations maintain.](media/riskware-tutorial/maintain.png)
3. In the maintenance page, select **Authentication**.
4. In **Authentication Configuration** page, perform the following steps:

    ![Screenshot shows the Riskware Configuration Authentication Configuration.](media/riskware-tutorial/menu.png)

    a. Select **Type** as **SAML** for authentication.

    b. In the **Code** textbox, type your code like AZURE\_UAT.

    c. In the **Description** textbox, type your description like AZURE Configuration for SSO.

    d. In **Single Sign On Page** textbox, paste the **Login URL** value.

    e. In **Sign out Page** textbox, paste the **Logout URL** value.

    f. In the **Post Form Field** textbox, type the field name present in Post Response that contains SAML like SAMLResponse.

    g. In the **XML Identity Tag Name** textbox, type attribute, which contains the unique identifier in the SAML response like NameID.

    h. Open the downloaded **Metadata Xml** from Azure portal in notepad, copy the certificate from the Metadata file and paste it into the **Certificate** textbox.

    i. In **Consumer URL** textbox, paste the value of **Reply URL**, which you get from the support team.

    j. In **Issuer** textbox, paste the value of **Identifier**, which you get from the support team.

    Note

    Contact [Riskware Client support team](mailto:support@pansoftware.com.au) to get these values

    k. Select **Use POST** checkbox.

    l. Select **Use SAML Request** checkbox.

    m. Select **Save**.

### Create Riskware test user

To enable Microsoft Entra users to sign in to Riskware, they must be provisioned into Riskware. In Riskware, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to Riskware as a Security Administrator.
2. On the top right, select **Maintenance** to open the maintenance page.

    ![Screenshot shows the Riskware Configuration maintain.](media/riskware-tutorial/maintain.png)
3. In the maintenance page, select **People**.

    ![Screenshot shows the Riskware Configuration people.](media/riskware-tutorial/people.png)
4. Select **Details** tab and perform the following steps:

    ![Screenshot shows the Riskware Configuration details.](media/riskware-tutorial/details.png)

    a. Select **Person Type** like Employee.

    b. In **First Name** textbox, enter the first name of user like **Britta**.

    c. In **Surname** textbox, enter the last name of user like **Simon**.
5. On the **Security** tab, perform the following steps:

    ![Screenshot shows the Riskware Configuration security.](media/riskware-tutorial/security.png)

    a. Under **Authentication** section, select the **Authentication** mode, which you have setup like AZURE Configuration for SSO.

    b. Under **Logon Details** section, in the **User ID** textbox, enter the email of user like `brittasimon@contoso.com`.

    c. In the **Password** textbox, enter password of the user.
6. On the **Organization** tab, perform the following steps:

    ![Screenshot shows the Riskware Configuration Organization.](media/riskware-tutorial/status.png)

    a. Select the option as **Level1** organization.

    b. Under **Person's Primary Workplace** section, in the **Location** textbox, type your location.

    c. Under **Employee** section, select **Employee Status** like Casual.

    d. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Riskware Sign-On URL where you can initiate the login flow.
- Go to Riskware Sign-On URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Riskware tile in the My Apps, this option redirects to Riskware Sign-On URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).