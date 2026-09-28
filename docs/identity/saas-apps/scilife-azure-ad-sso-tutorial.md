---
layout: Conceptual
title: Configure Scilife Microsoft Entra SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/scilife-azure-ad-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Scilife Microsoft Entra SSO.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: aef6fda4-8189-d66d-91d9-f328147b8923
document_version_independent_id: 9541b114-5155-445c-0725-c390850fdbff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/scilife-azure-ad-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/scilife-azure-ad-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/scilife-azure-ad-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c0a868c8-4b78-f908-ff91-6f9b81796ab9
---

# Configure Scilife Microsoft Entra SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Scilife Microsoft Entra SSO with Microsoft Entra ID. With the help of this application SSO integration is made simple and hassle free as most of the configuration will take place on its own with minimalist efforts. When you integrate Scilife Microsoft Entra SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Scilife Microsoft Entra SSO.
- Enable your users to be automatically signed-in to Scilife Microsoft Entra SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Scilife Microsoft Entra SSO in a test environment. Scilife Microsoft Entra SSO supports **SP** initiated single sign-on and **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with Scilife Microsoft Entra SSO, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Scilife Microsoft Entra SSO single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Scilife Microsoft Entra SSO application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Scilife Microsoft Entra SSO from the Microsoft Entra gallery

Add Scilife Microsoft Entra SSO from the Microsoft Entra application gallery to configure single sign-on with Scilife Microsoft Entra SSO. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Scilife Microsoft Entra SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a URL using one of the following patterns:

    | **Identifier** |
    | --- |
    | `https://ldap-Environment.scilife.io/simplesaml/module.php/saml/sp/metadata.php/<CustomerUrlPrefix>-<Environment>-sp` |
    | `https://ldap.scilife.io/simplesaml/module.php/saml/sp/metadata.php/<CustomerUrlPrefix>-sp` |

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://<CustomerUrlPrefix>.scilife.io/<languageCode>/login` |
    | `https://ldap.scilife.io/simplesaml/module.php/saml/sp/metadata.php/<CustomerUrlPrefix>-sp` |
    | `https://ldap.scilife.io/simplesaml/module.php/saml/sp/saml2-acs.php/<CustomerUrlPrefix>-sp` |
    | `https://<CustomerUrlPrefix>-<Environment>.scilife.io/<languageCode>/login` |
    | `https://ldap-<Environment>.scilife.io/simplesaml/module.php/saml/sp/metadata.php/<CustomerUrlPrefix>-<Environment>-sp` |
    | `https://ldap-<Environment>.scilife.io/simplesaml/module.php/saml/sp/saml2-acs.php/<CustomerUrlPrefix>-<Environment>-sp` |

    c. In the **Sign on URL** textbox, type a URL using one of the following patterns:

    | **Sign on URL** |
    | --- |
    | `https://<CustomerUrlPrefix>.scilife.io/<languageCode>/login` |
    | `https://<CustomerUrlPrefix>-<Environment>.scilife.io/<languageCode>/login` |

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Scilife Microsoft Entra SSO support team](mailto:support@scilife.io) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Scilife Microsoft Entra SSO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, Scilife Microsoft Entra SSO application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | firstname | user.givenname |
    | lastname | user.surname |
    | ldap\_user\_id | user.userprincipalname |
    | mobile | user.mobilephone |
8. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
9. On the **Set up Scilife Microsoft Entra SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure Scilife Microsoft Entra SSO

1. Log in to your Scilife Microsoft Entra SSO company site as an administrator.
2. Go to **Manage** &gt; **Active Directory Settings** and perform the following steps:

    ![Screenshot shows the Scilife Azure administration portal.](media/scilife-azure-ad-sso-tutorial/manage.png)

    1. Enable **Configure Active Directory**.
    2. Select **AD Azure** type from the drop-down.
    3. Download the **Federation Metadata XML file** and **Upload MetadataXML** file by selecting **Choose file**.
    4. Select **Parse Metadata**.
3. Enter **Tenant ID**, **Application ID** and **Client ID** in the following fields.

    ![Screenshot shows the Scilife Azure tenant ID.](media/scilife-azure-ad-sso-tutorial/tenant.png)
4. Copy **AD TRUST URL**, paste this value into the **Identifier (Entity ID)** text box in the **Basic SAML Configuration** section.
5. Copy **AD CONSUMER SERVICE URL**, paste this value into the **Reply URL (Assertion Consumer Service URL)** text box in the **Basic SAML Configuration** section.

    ![Screenshot shows the Scilife Azure portal URLs.](media/scilife-azure-ad-sso-tutorial/portal.png)
6. Select **Save Configuration**.

### Create Scilife Microsoft Entra SSO test user

In this section, a user called B.Simon is created in Scilife Microsoft Entra SSO. Scilife Microsoft Entra SSO supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Scilife Microsoft Entra SSO, a new one is commonly created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Scilife Microsoft Entra SSO Sign-on URL where you can initiate the login flow.
- Go to Scilife Microsoft Entra SSO Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Scilife Microsoft Entra SSO tile in the My Apps, this option redirects to Scilife Microsoft Entra SSO Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).