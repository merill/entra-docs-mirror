---
layout: Conceptual
title: Configure SilkRoad Life Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/silkroad-life-suite-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SilkRoad Life Suite.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1c70d5af-f19b-e80a-c32c-7491b1b83790
document_version_independent_id: 7405ad81-2911-a163-ba73-1b032600bfbf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/silkroad-life-suite-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/silkroad-life-suite-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/silkroad-life-suite-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f33e524e-926b-b2c0-5098-e0088dcabf5c
---

# Configure SilkRoad Life Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SilkRoad Life Suite with Microsoft Entra ID. When you integrate SilkRoad Life Suite with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SilkRoad Life Suite.
- Enable your users to be automatically signed-in to SilkRoad Life Suite with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SilkRoad Life Suite single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SilkRoad Life Suite supports **SP** initiated SSO.

## Add SilkRoad Life Suite from the gallery

To configure the integration of SilkRoad Life Suite into Microsoft Entra ID, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SilkRoad Life Suite** in the search box.
4. Select **SilkRoad Life Suite** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SilkRoad Life Suite

Configure and test Microsoft Entra SSO with SilkRoad Life Suite using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SilkRoad Life Suite.

To configure and test Microsoft Entra SSO with SilkRoad Life Suite, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SilkRoad Life Suite SSO**- to configure the single sign-on settings on application side.
    1. **Create SilkRoad Life Suite test user** - to have a counterpart of B.Simon in SilkRoad Life Suite that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SilkRoad Life Suite** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    Note

    You get the **Service Provider metadata file** explained later in this article.

    a. Select **Upload metadata file**.

    ![Screenshot shows Basic SAML Configuration with the Upload metadata file link.](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Screenshot shows a dialog box where you can select and upload a file.](common/browse-upload-metadata.png)

    c. Once the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    Note

    If the **Identifier** and **Reply URL** values aren't getting auto populated, then fill in the values manually according to your requirement.

    d. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.silkroad-eng.com/Authentication/`
6. On the **Basic SAML Configuration** section, if you don't have **Service Provider metadata file**, perform the following steps:

    a. In the **Identifier** box, type a URL using one of the following patterns:

    | Identifier URL |
    | --- |
    | `https://<SUBDOMAIN>.silkroad-eng.com/Authentication/SP` |
    | `https://<SUBDOMAIN>.silkroad.com/Authentication/SP` |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://<SUBDOMAIN>.silkroad-eng.com/Authentication/` |
    | `https://<SUBDOMAIN>.silkroad.com/Authentication/` |

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.silkroad-eng.com/Authentication/`

    Note

    These values aren't real. Update these values with the actual Identifier,Reply URL and Sign-On URL. Contact [SilkRoad Life Suite Client support team](https://www.silkroad.com/locations/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up SilkRoad Life Suite** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SilkRoad Life Suite SSO

1. Sign in to your SilkRoad company site as administrator.

    Note

    To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Entra ID, please contact SilkRoad Support or your SilkRoad Services representative.
2. Go to **Service Provider**, and then select **Federation Details**.

    ![Screenshot shows Federation Details selected from Service Provider.](media/silkroad-life-suite-tutorial/details.png)
3. Select **Download Federation Metadata**, and then save the metadata file on your computer. Use Downloaded Federation Metadata as a **Service Provider metadata file** in the **Basic SAML Configuration** section.

    ![Screenshot shows the Download Federation Metadata link.](media/silkroad-life-suite-tutorial/metadata.png)
4. In your **SilkRoad** application, select **Authentication Sources**.

    ![Screenshot shows Authentication Sources selected.](media/silkroad-life-suite-tutorial/sources.png)
5. Select **Add Authentication Source**.

    ![Screenshot shows the Add Authentication Source link.](media/silkroad-life-suite-tutorial/add-source.png)
6. In the **Add Authentication Source** section, perform the following steps:

    ![Screenshot shows Add Authentication Source with the Create Identity Provider using File Data button selected.](media/silkroad-life-suite-tutorial/metadata-file.png)

    a. Under **Option 2 - Metadata File**, select **Browse** to upload the downloaded metadata file from Azure portal.

    b. Select **Create Identity Provider using File Data**.
7. In the **Authentication Sources** section, select **Edit**.

    ![Screenshot shows Authentication Sources with the Edit option selected.](media/silkroad-life-suite-tutorial/edit-source.png)
8. On the **Edit Authentication Source** dialog, perform the following steps:

    ![Screenshot shows the Edit Authentication Source dialog box where you can enter the values described.](media/silkroad-life-suite-tutorial/authentication.png)

    a. As **Enabled**, select **Yes**.

    b. In the **EntityId** textbox, paste the value of **Microsoft Entra Identifier**..

    c. In the **IdP Description** textbox, type a description for your configuration (for example: **Microsoft Entra SSO**).

    d. In the **Metadata File** textbox, Upload the **metadata** file which you have downloaded previously.

    e. In the **IdP Name** textbox, type a name that's specific to your configuration (for example: *Azure SP*).

    f. In the **Logout Service URL** textbox, paste the value of **Logout URL**..

    g. In the **Sign-on service URL** textbox, paste the value of **Login URL**..

    h. Select **Save**.
9. Disable all other authentication sources.

    ![Screenshot shows Authentication Sources where you can disable other sources.](media/silkroad-life-suite-tutorial/manage-source.png)

### Create SilkRoad Life Suite test user

In this section, you create a user called Britta Simon in SilkRoad Life Suite. Work with [SilkRoad Life Suite Client support team](https://www.silkroad.com/locations/) to add the users in the SilkRoad Life Suite platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to SilkRoad Life Suite Sign-on URL where you can initiate the login flow.
- Go to SilkRoad Life Suite Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the SilkRoad Life Suite tile in the My Apps, this option redirects to SilkRoad Life Suite Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).