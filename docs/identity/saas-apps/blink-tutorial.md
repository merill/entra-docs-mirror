---
layout: Conceptual
title: Configure Blink for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/blink-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Blink.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: fe70acfb-ceea-1da3-c71f-36ff5ffd9b5d
document_version_independent_id: 864b5a23-ac9a-1042-84f6-e78d0326efd9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/blink-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/blink-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/blink-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 322019a4-2049-e6de-041a-ca10f1ddd5c7
---

# Configure Blink for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Blink with Microsoft Entra ID. When you integrate Blink with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Blink.
- Enable your users to be automatically signed-in to Blink with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Blink single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Blink supports **SP** initiated SSO.
- Blink supports **Just In Time** user provisioning.
- Blink supports [Automated user provisioning](blink-provisioning-tutorial).

## Adding Blink from the gallery

To configure the integration of Blink into Microsoft Entra ID, you need to add Blink from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Blink** in the search box.
4. Select **Blink** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Blink

Configure and test Microsoft Entra SSO with Blink using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Blink.

To configure and test Microsoft Entra SSO with Blink, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Blink SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Blink test user** - to have a counterpart of B.Simon in Blink that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Blink** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    1. In the **Sign on URL** text box, type a URL using one of the following patterns:

    | Sign-on URL |
    | --- |
    | `https://app.joinblink.com` |
    | `https://<SUBDOMAIN>.joinblink.com` |

    1. In the **Identifier (Entity ID)** text box, type a URL using the following pattern:

    `https://api.joinblink.com/saml/o-<TENANTID>`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Blink Client support team](https://help.joinblink.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Blink Meetings application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. Select **Edit** icon to open User Attributes dialog.

    ![image](common/edit-attribute.png)
7. In addition to above, Blink Meetings application expects few more attributes to be passed back in SAML response. In the User Claims section on the User Attributes dialog, perform the following steps to add SAML token attribute as shown in the below table:

    | Name | Source Attribute |
    | --- | --- |
    | first\_name | user.givenname |
    | second\_name | user.surname |
    | email | user.mail |
    |  |  |

    1. Select **Add new claim** to open the **Manage user claims** dialog.
    2. In the **Name** textbox, type the attribute name shown for that row.
    3. Leave the **Namespace** blank.
    4. Select Source as **Attribute**.
    5. From the **Source attribute** list, type the attribute value shown for that row.
    6. Select **Save**.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Blink** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Blink SSO

To configure single sign-on on **Blink** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Blink support team](https://help.joinblink.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Blink test user

In this section, a user called Britta Simon is created in Blink. Blink supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Blink, a new one is created after authentication.

Blink also supports automatic user provisioning, you can find more details [here](blink-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Blink Sign-on URL where you can initiate the login flow.
- Go to Blink Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Blink tile in the My Apps, this option redirects to Blink Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).