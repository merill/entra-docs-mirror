---
layout: Conceptual
title: Configure DB Education Portal for Schools for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/db-education-portal-for-schools-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and DB Education Portal for Schools.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 1beed174-93b5-cb4f-725c-05f8bcd21dd3
document_version_independent_id: 6863c810-074e-7156-836e-659daa47b49c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/db-education-portal-for-schools-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/db-education-portal-for-schools-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/db-education-portal-for-schools-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/545d40c6-c50c-444b-b422-1c707eeab28e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b908d601-32e8-445a-b044-a507b5d1689e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d8eeacec-c748-faf4-c11a-997ef1a43695
---

# Configure DB Education Portal for Schools for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate DB Education Portal for Schools with Microsoft Entra ID. Providing single sign-on access through Microsoft Entra ID, for the DB Education Portal, available for Schools and Multi Academy Trusts across the United Kingdom. When you integrate DB Education Portal for Schools with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to DB Education Portal for Schools.
- Enable your users to be automatically signed-in to DB Education Portal for Schools with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for DB Education Portal for Schools in a test environment. DB Education Portal for Schools supports **SP** initiated single sign-on.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with DB Education Portal for Schools, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- DB Education Portal for Schools single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the DB Education Portal for Schools application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add DB Education Portal for Schools from the Microsoft Entra gallery

Add DB Education Portal for Schools from the Microsoft Entra application gallery to configure single sign-on with DB Education Portal for Schools. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **DB Education Portal for Schools** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the value: `DBEducation`

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://intranet.<CustomerName>.domain.extension/governorintranet/wp-login.php?saml_acs` |
    | `https://portal.<CustomerName>.domain.extension/governorintranet/wp-login.php?saml_acs` |
    | `https://intranet.<CustomerName>.domain.extension/studentportal/wp-login.php?saml_acs` |
    | `https://portal.<CustomerName>.domain.extension/studentportal/wp-login.php?saml_acs` |
    | `https://intranet.<CustomerName>.domain.extension/staffportal/wp-login.php?saml_acs` |
    | `https://portal.<CustomerName>.domain.extension/staffportal/wp-login.php?saml_acs` |
    | `https://intranet.<CustomerName>.domain.extension/parentportal/wp-login.php?saml_acs` |
    | `https://portal.<CustomerName>.domain.extension/parentportal/wp-login.php?saml_acs` |
    | `https://intranet.<CustomerName>.domain.extension/familyportal/wp-login.php?saml_acs` |
    | `https://portal.<CustomerName>.domain.extension/familyportal/wp-login.php?saml_acs` |

    c. In the **Sign on URL** textbox, type a URL using one of the following patterns:

    | **Sign on URL** |
    | --- |
    | `https://portal.<CustomerName>.domain.extension` |
    | `https://intranet.<CustomerName>.domain.extension` |

    Note

    These values aren't real. Update these values with the actual Reply URL and Sign on URL. Contact [DB Education Portal for Schools support team](mailto:contact@dbeducation.org.uk) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. DB Education Portal for Schools application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, DB Education Portal for Schools application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | groups | user.groups |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

## Configure DB Education Portal for Schools SSO

To configure single sign-on on **DB Education Portal for Schools** side, you need to send the **App Federation Metadata Url** to [DB Education Portal for Schools support team](mailto:contact@dbeducation.org.uk). They set this setting to have the SAML SSO connection set properly on both sides.

### Create DB Education Portal for Schools test user

In this section, you create a user called Britta Simon at DB Education Portal for Schools SSO. Work with [DB Education Portal for Schools SSO support team](mailto:contact@dbeducation.org.uk) to add the users in the DB Education Portal for Schools SSO platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to DB Education Portal for Schools Sign-on URL where you can initiate the login flow.
- Go to DB Education Portal for Schools Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the DB Education Portal for Schools tile in the My Apps, this option redirects to DB Education Portal for Schools Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).