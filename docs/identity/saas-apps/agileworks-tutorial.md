---
layout: Conceptual
title: Configure AgileWorksクラウド版 for single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/agileworks-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and AgileWorksクラウド版 so users can sign in with their Microsoft Entra accounts.
ms.topic: how-to
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1012
locale: en-us
document_id: 1d6d0266-c991-8cc5-fd13-a1ef5c83c2b8
document_version_independent_id: 1d6d0266-c991-8cc5-fd13-a1ef5c83c2b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/agileworks-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/agileworks-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/agileworks-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8c1fb7ea-a1cc-8e5b-965a-03a13a9531bc
---

# Configure AgileWorksクラウド版 for single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate AgileWorksクラウド版 with Microsoft Entra ID. When you integrate AgileWorksクラウド版 with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to AgileWorksクラウド版.
- Enable your users to be automatically signed in to AgileWorksクラウド版 with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- AgileWorksクラウド版 single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- AgileWorksクラウド版 supports **SP** initiated SSO.

## Adding AgileWorksクラウド版 from the gallery

To configure the integration of AgileWorksクラウド版 into Microsoft Entra ID, you need to add AgileWorksクラウド版 from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **AgileWorksクラウド版** in the search box.
4. Select **AgileWorksクラウド版** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for AgileWorksクラウド版

Configure and test Microsoft Entra SSO with AgileWorksクラウド版 using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in AgileWorksクラウド版.

To configure and test Microsoft Entra SSO with AgileWorksクラウド版, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure AgileWorksクラウド版 SSO**- to configure the single sign-on settings on application side.
    1. **Create AgileWorksクラウド版 test user** - to have a counterpart of B.Simon in AgileWorksクラウド版 that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AgileWorksクラウド版** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type the value: `atled.jp`.

    Note

    The default Identifier value is `atled.jp`. If your administrator has changed this value in the system settings, use that updated value instead.

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** | **Site** |
    | --- | --- |
    | `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/PicusSAML` | (User Site) |
    | `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/EMMASAML` | (Admin Site) |
    | `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/MobileSAML` | (Mobile Site) |
    | `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/AppSAML` | (App) |
    | `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/GadgetSAML` | (Gadget) |

    Note

    Replace `<SUBDOMAIN>` in `https://<SUBDOMAIN>.atledcloud.jp` with the subdomain of your AgileWorksクラウド版 instance.

    c. In the **Sign on URL** text box, enter the same URL that you set as the default (first) Reply URL.

    Note

    This setting is optional in production and can be left blank after testing. It's required only for the **Test this application** button in the Microsoft Entra admin center to work correctly. If omitted, the **Test this application** button may fail because the test adds extra data to the link, which can make the URL too long and cause the request to fail.
6. AgileWorksクラウド版 application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, whereas **Unique User Identifier (Name ID)** is mapped with **user.userprincipalname**. AgileWorksクラウド版 application expects **Unique User Identifier (Name ID)** to be mapped with **ExtractMailPrefix(user.mail)**, so you need to edit the attribute mapping by selecting **Edit** icon and change the attribute mapping.

    ![Screenshot of the Attributes &amp; Claims page showing the default Name ID attribute mapping.](media/agileworks-tutorial/attributes.png)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot of the SAML Signing Certificate section with the Certificate (Base64) Download link highlighted.](common/certificatebase64.png)
8. On the **Set up AgileWorksクラウド版** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot of the Set up AgileWorksクラウド版 section with configuration URLs to copy.](common/copy-configuration-urls.png)

## Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

Note

Set the test user's Email (user.mail) when you create the Microsoft Entra test user, and record the value. You'll use it in the **Create AgileWorksクラウド版 test user** section.

## Configure AgileWorksクラウド版 SSO

1. Sign in to the AgileWorksクラウド版 administration site (for example, `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/EMMA`).

    ![Screenshot of AgileWorks administration site.](media/agileworks-tutorial/login.png)
2. Navigate to **Site Administration** &gt; **Site Common Settings** &gt; **Authentication & Security** &gt; **Login Authentication**, select the row named **SAML Authentication**, and then select **Edit**.

    ![Screenshot of Login Authentication settings list.](media/agileworks-tutorial/authentication.png)
3. Set the status to **Available** and select **Save**.

    ![Screenshot of the SAML Authentication status set to Available.](media/agileworks-tutorial/available.png)
4. On the **SAML** tab, configure the following settings and select **Save**.

    | AgileWorksクラウド版 field | Value |
    | --- | --- |
    | **Redirect Authentication URL** | **Login URL** copied from Microsoft Entra |
    | **Public Key Certificate File** | **Certificate (Base64)** downloaded from Microsoft Entra |

    ![Screenshot of SAML tab certificate.](media/agileworks-tutorial/certificate.png)

### Create AgileWorksクラウド版 test user

In this section, you create a user in AgileWorksクラウド版 that corresponds to a user in Microsoft Entra ID.

1. AgileWorksクラウド版 uses the SAML **NameID** to identify the user at login. Microsoft Entra ID is configured to send the **NameID** using the `ExtractMailPrefix(user.mail)` transformation, which extracts the part before `@` from the user's email address.
2. You must set the same value as the **Login ID** in AgileWorksクラウド版.

**Example:** | Microsoft Entra user email | AgileWorksクラウド版 Login ID | | :--- | :--- | | `bsimon@example.com` | `bsimon` |

![Screenshot of the AgileWorksクラウド版 user profile with the Login ID field highlighted.](media/agileworks-tutorial/user.png)

Before you can use single sign-on, ensure the user is created and activated in AgileWorksクラウド版.

Note

If Microsoft Entra ID is configured to send the SAML NameID using a different attribute (for example: user.userprincipalname or mail), make sure the AgileWorks Login ID for the corresponding user matches the value sent in the SAML NameID.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

Note

The **Test this application** button works correctly only if a **Sign on URL** is set in the Basic SAML Configuration.

- Select **Test this application**, which redirects to the AgileWorksクラウド版 Sign on URL where you can initiate the login flow.
- Go to AgileWorksクラウド版 Reply URL (for example, `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/PicusSAML`) directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the AgileWorksクラウド版 tile in My Apps, it redirects to the AgileWorksクラウド版 Reply URL (for example, `https://<SUBDOMAIN>.atledcloud.jp/AgileWorks/Broker/PicusSAML`). For more information about My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).