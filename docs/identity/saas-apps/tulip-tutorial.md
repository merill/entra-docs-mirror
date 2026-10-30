---
layout: Conceptual
title: Configure Tulip for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tulip-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Tulip.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
locale: en-us
document_id: 0c052a8e-2a72-ea8c-d32f-0b0805284eaf
document_version_independent_id: 3b906a69-7637-ec16-54c2-fe09ec3d1822
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tulip-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tulip-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tulip-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a4e5dcd8-55bd-f9f6-1266-2f955e4ea29a
---

# Configure Tulip for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Tulip with Microsoft Entra ID. When you integrate Tulip with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Tulip.
- Enable your users to be automatically signed-in to Tulip with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Tulip is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Tulip single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Tulip supports **IDP** initiated SSO.

## Add Tulip from the gallery

To configure the integration of Tulip into Microsoft Entra ID, you need to add Tulip from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Tulip** in the search box.
4. Select **Tulip** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Tulip

To configure and test Microsoft Entra SSO with Tulip, perform the following steps:

1. **Configure Microsoft Entra SSO** - to enable your users to use this feature.
2. **Configure Tulip SSO** - to configure the single sign-on settings on application side.

    1. To configure SSO on a Tulip instance with existing users, reach out to support@tulip.co.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Tulip** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    a.Download Tulip's Metadata File which is accessible under the settings page on your Tulip instance -

    b. Select **Upload metadata file**.

    ![image1](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![image2](common/browse-upload-metadata.png)

    c. Once the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section:

    ![image3](common/idp-intiated.png)

    Note

    If the **Identifier** and **Reply URL** values aren't getting auto populated, then fill in the values manually according to your requirement.
6. Tulip application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. If the `nameID` needs to be an email, change the format to be `Persistent`.

    ![image](common/default-attributes.png)
7. In addition to the above, Tulip application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | displayName | user.displayname |
    | emailAddress | user.mail |
    | badgeID | user.employeeid |
    | groups | user.groups |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

## Configure Tulip SSO

1. Log in to your Tulip instance as an Account Owner.
2. Go to the **Settings** &gt; **SAML** and perform the following steps in the below page.

    ![Screenshot for tulip configuration.](media/tulip-tutorial/configuration.png)

    a. **Enable SAML Logins**.

    b. Select **metadata xml file** to download the **Service Provider metadata file** and use this file to upload in the **Basic SAML Configuration** section in Azure portal.

    c. Upload the Federation Metadata XML file from Azure to Tulip. This will populate the SSO Login, SSO Logout URL and the Certificates.

    d. Verify that the Name, Email and Badge attributes aren't null, that is, enter any unique strings in all three inputs and do a test authentication using the `Authenticate` button on the right.

    e. Upon successful authentication, copy/paste the entire claim URL into the appropriate mapping for the name, email and badgeID attributes.

    - Paste the **Name Attribute** value as `http://schemas.microsoft.com/identity/claims/displayname` or the appropriate claim URL.
    - Paste the **Email Attribute** value as `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` or the appropriate claim URL.
    - Paste the **Badge Attribute** value as `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/badgeID` or the appropriate claim URL.
    - Paste the **Role Attribute** value as `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/groups` or the appropriate claim URL.

    f. Select **Save SAML Configuration**.