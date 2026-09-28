---
layout: Conceptual
title: Configure SAP Concur Travel and Expense for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/concur-travel-and-expense-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAP Concur Travel and Expense.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 3e34a9db-6f40-6d8c-1056-713f5fabc2d6
document_version_independent_id: 60af6bcb-3faa-9788-ba3d-c6d4b89cb26b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/concur-travel-and-expense-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/concur-travel-and-expense-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/concur-travel-and-expense-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: de000e0b-cba9-e375-fd5f-2a6ac34162ce
---

# Configure SAP Concur Travel and Expense for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAP Concur Travel and Expense with Microsoft Entra ID. When you integrate SAP Concur Travel and Expense with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAP Concur Travel and Expense.
- Enable your users to be automatically signed-in to SAP Concur Travel and Expense with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAP Concur Travel and Expense subscription.
- A "Company Administrator" role under your Concur user account. You can test if you have the right access by going to [Concur SSO Self-Service Tool](https://www.concursolutions.com/nui/authadmin/ssoadmin). If you don't have the access, please contact Concur support or implementation project manager.

## Scenario description

In this article, you configure and test Microsoft Entra SSO.

- SAP Concur Travel and Expense supports **IDP** and **SP** initiated SSO
- SAP Concur Travel and Expense supports testing SSO in both production and implementation environment

Note

Identifier of this application is a fixed string value for each of the three regions: US, EMEA, and China. So only one instance can be configured for each region in one tenant.

## Adding SAP Concur Travel and Expense from the gallery

To configure the integration of SAP Concur Travel and Expense into Microsoft Entra ID, you need to add SAP Concur Travel and Expense from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAP Concur Travel and Expense** in the search box.
4. Select **SAP Concur Travel and Expense** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for SAP Concur Travel and Expense

Configure and test Microsoft Entra SSO with SAP Concur Travel and Expense using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAP Concur Travel and Expense.

To configure and test Microsoft Entra SSO with SAP Concur Travel and Expense, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SAP Concur Travel and Expense SSO**- to configure the single sign-on settings on application side.
    1. **Create SAP Concur Travel and Expense test user** - to have a counterpart of B.Simon in SAP Concur Travel and Expense that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAP Concur Travel and Expense** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section the application is pre-configured in **IDP** initiated mode and the necessary URLs are already pre-populated with Azure. The user needs to save the configuration by selecting the **Save** button.

    Note

    Identifier (Entity ID) and Reply URL (Assertion Consumer Service URL) are region specific. Please select based on the datacenter of your Concur entity. If you don't know the datacenter of your Concur entity, please contact Concur support.
6. On the **Set up Single Sign-On with SAML** page, select the edit/pen icon for **User Attribute** to edit the settings. The Unique User Identifier needs to match Concur user login\_id. Usually, you should change **user.userprincipalname** to **user.mail**.

    ![Edit User Attribute](common/edit-attribute.png)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the metadata and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAP Concur Travel and Expense SSO

1. In a different web browser window, you need to upload the downloaded **Federation Metadata XML** to [Concur SSO Self-Service Tool](https://www.concursolutions.com/nui/authadmin/ssoadmin) and sign in to your SAP Concur Travel and Expense company site as an administrator.
2. Select **Add**.
3. Enter a custom name for your IdP, for example "Microsoft Entra ID (US)".
4. Select **Upload XML File** and attach **Federation Metadata XML** you downloaded previously.
5. Select **Add Metadata** to save the change.

    ![Concur SSO self-service tool screenshot](media/concur-travel-and-expense-tutorial/add-metadata-concur-self-service-tool.png)

### Create SAP Concur Travel and Expense test user

In this section, you create a user called B.Simon in SAP Concur Travel and Expense. Work with Concur support team to add the users in the SAP Concur Travel and Expense platform. Users must be created and activated before you use single sign-on.

Note

B.Simon's Concur login id needs to match B.Simon's unique identifier at Microsoft Entra ID. For example, if B.Simon's Microsoft Entra unique identifier is `B.Simon@contoso.com`. B.Simon's Concur login id needs to be `B.Simon@contoso.com` as well.

## Configure Concur Mobile SSO

To enable Concur mobile SSO, you need to give Concur support team **User access URL**. Follow steps below to get **User access URL** from Microsoft Entra ID:

1. Go to **Enterprise applications**
2. Select **SAP Concur Travel and Expense**
3. Select **Properties**
4. Copy **User access URL** and give this URL to Concur support

Note

Self-Service option to configure SSO isn't available so work with Concur support team to enable mobile SSO.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to SAP Concur Travel and Expense Sign on URL where you can initiate the login flow.
- Go to SAP Concur Travel and Expense Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the SAP Concur Travel and Expense for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the SAP Concur Travel and Expense tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the SAP Concur Travel and Expense for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).