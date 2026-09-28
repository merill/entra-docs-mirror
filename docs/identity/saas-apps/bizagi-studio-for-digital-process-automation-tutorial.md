---
layout: Conceptual
title: Configure Bizagi for Digital Process Automation for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bizagi-studio-for-digital-process-automation-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Bizagi for Digital Process Automation.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: edb3daae-437f-4f2a-539d-76638652e0e0
document_version_independent_id: 3758c464-fc23-bb18-f4d2-3afe33887c1d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bizagi-studio-for-digital-process-automation-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bizagi-studio-for-digital-process-automation-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bizagi-studio-for-digital-process-automation-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ec5c199d-fb7a-65ae-e9aa-79317b8ee19d
---

# Configure Bizagi for Digital Process Automation for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Bizagi for Digital Process Automation Services or Server with Microsoft Entra ID. When you integrate Bizagi for Digital Process Automation with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to a Bizagi project for Digital Process Automation Services or Server.
- Enable your users to be automatically signed-in to a project of Bizagi for Digital Process AutomationServices or Server with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Bizagi project using Automation Services or Server.
- Have your own certificates for SAML assertion signatures. This certificates must be generate in p12 or pfx format.
- Have a metadata file in XML format generated from the Bizagi project.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a Bizagi project using Automation services or server.

- Bizagi for Digital Process Automation supports **SP** initiated SSO.
- Bizagi for Digital Process Automation supports [Automated user provisioning](bizagi-studio-for-digital-process-automation-provisioning-tutorial).

## Add Bizagi for Digital Process Automation from the gallery

To configure the integration of Bizagi for Digital Process Automation into Microsoft Entra ID, you need to add Bizagi for Digital Process Automation from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Bizagi for Digital Process Automation** in the search box.
4. Select **Bizagi for Digital Process Automation** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Bizagi for Digital Process Automation

Configure and test Microsoft Entra SSO with Bizagi for Digital Process Automation using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in the Bizagi project.

To configure and test Microsoft Entra SSO with Bizagi for Digital Process Automation, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Bizagi for Digital Process Automation SSO**- to configure the single sign-on settings on application side.
    1. **Create Bizagi for Digital Process Automation test user** - to have a counterpart of B.Simon in Bizagi for Digital Process Automation that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Bizagi for Digital Process Automation** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.bizagi.com/<PROJECT_NAME>`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.bizagi.com/<PROJECT_NAME>`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [Bizagi for Digital Process Automation support team](mailto:jarvein.rivera@bizagi.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

    This metadata URL must be registered in the authentication options of your Bizagi project.
7. On the **Set up single sign-on with SAML**page, select the pencil icon for **User Attributes & Claims** to edit the Unique User Identifier.

    Set the Unique User Identifier as the user.mail.

### Create a Microsoft Entra ID test

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to Bizagi for Digital Process Automation.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Bizagi for Digital Process Automation**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Bizagi for Digital Process Automation SSO

To configure single sign-on on **Bizagi for Digital Process Automation** side, you need to send the **App Federation Metadata Url** to [Bizagi for Digital Process Automation support team](mailto:jarvein.rivera@bizagi.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Bizagi for Digital Process Automation test user

In this section, you create a user called Britta Simon in Bizagi for Digital Process Automation. Work with [Bizagi for Digital Process Automation support team](mailto:jarvein.rivera@bizagi.com) to add the users in the Bizagi for Digital Process Automation platform. Users must be created and activated before you use single sign-on.

Bizagi for Digital Process Automation also supports automatic user provisioning, you can find more details [here](bizagi-studio-for-digital-process-automation-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Bizagi for Digital Process Automation Sign-on URL where you can initiate the login flow.
- Go to Bizagi for Digital Process Automation Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Bizagi for Digital Process Automation tile in the My Apps, this option redirects to Bizagi for Digital Process Automation Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).