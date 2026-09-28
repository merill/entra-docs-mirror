---
layout: Conceptual
title: Configure Field iD for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/field-id-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Field iD.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 91968791-35d9-3fca-eae8-8a54b7ff3534
document_version_independent_id: f66b5d0c-b0cc-1b4d-2363-03cd3f3c5434
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/field-id-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/field-id-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/field-id-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 334692e0-6d0a-dd16-f0a7-be3317bf8ea9
---

# Configure Field iD for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Field iD with Microsoft Entra ID. When you integrate Field iD with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Field iD.
- Enable your users to be automatically signed in to Field iD with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Field iD single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Field iD supports IDP initiated SSO.

## Add Field iD from the gallery

To configure the integration of Field iD into Microsoft Entra ID, you need to add Field iD from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Field iD** in the search box.
4. Select **Field iD** from results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Field iD

Configure and test Microsoft Entra SSO with Field iD by using a test user called **B.Simon**. For SSO to work, you need to establish a linked relationship between a Microsoft Entra user and the related user in Field iD.

To configure and test Microsoft Entra SSO with Field iD, complete the following steps:

1. Configure Microsoft Entra SSOto enable your users to use this feature.
    1. Create a Microsoft Entra test user to test Microsoft Entra single sign-on with B.Simon.
    2. Assign the Microsoft Entra test user to enable B.Simon to use Microsoft Entra single sign-on.
2. Configure Field iD SSOto configure the single sign-on settings on the application side.
    1. Create a Field iD test user to have a counterpart of B.Simon in Field iD, linked to the Microsoft Entra representation of the user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Field iD** application integration page, find the **Manage** section. Then select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot of Set up Single Sign-On with SAML page, with the pencil icon highlighted](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL that uses the following pattern: `https://<tenantname>.fieldid.com/fieldid`

    b. In the **Reply URL** text box, type a URL that uses the following pattern: `https://<tenantname>.fieldid.com/fieldid/saml/SSO/alias/<Tenant Name>`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact the [Field iD support team](mailto:support@ecompliance.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select the copy icon to copy **App Federation Metadata Url**. Save it on your computer.

    ![Screenshot of SAML Signing Certificate, with copy icon highlighted](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Field iD SSO

To configure single sign-on on Field iD side, send the **App Federation Metadata Url** to the [Field iD support team](mailto:support@ecompliance.com). They ensure that the SAML SSO connection is set properly on both sides.

### Create a Field iD test user

In this section, you create a user called Britta Simon in Field iD. Work with the [Field iD support team](mailto:support@ecompliance.com) to add the users in the Field iD platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Field iD for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Field iD tile in the My Apps, you should be automatically signed in to the Field iD for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).