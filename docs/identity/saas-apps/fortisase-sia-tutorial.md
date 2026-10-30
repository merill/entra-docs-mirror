---
layout: Conceptual
title: Configure FortiSASE for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/fortisase-sia-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and FortiSASE.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e50ba26c-b854-117d-93e0-7e76139a5feb
document_version_independent_id: 69023009-5b32-0fac-2002-caf688d3890b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/fortisase-sia-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/fortisase-sia-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/fortisase-sia-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f9c410d2-ee39-d3d4-59b1-9209ff77a2f4
---

# Configure FortiSASE for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate FortiSASE with Microsoft Entra ID. When you integrate FortiSASE with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to FortiSASE.
- Enable your users to be automatically signed-in to FortiSASE with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- FortiSASE single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- FortiSASE supports **SP** initiated SSO.
- FortiSASE supports **Just In Time** user provisioning.

## Add FortiSASE from the gallery

To configure the integration of FortiSASE into Microsoft Entra ID, you need to add FortiSASE from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **FortiSASE** in the search box.
4. Select **FortiSASE** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for FortiSASE

Configure and test Microsoft Entra SSO with FortiSASE using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in FortiSASE.

To configure and test Microsoft Entra SSO with FortiSASE, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure FortiSASE SSO**- to configure the single sign-on settings on application side.
    1. **Create FortiSASE test user** - to have a counterpart of B.Simon in FortiSASE that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **FortiSASE** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using one of the following patterns:

    | User | URL |
    | --- | --- |
    | For FortiSASE VPN User SSO | `https://<TENANTHOSTNAME>.edge.prod.fortisase.com/remote/saml/metadata` |
    | For FortiSASE SWG User SSO | `https://<TENANTHOSTNAME>.edge.prod.fortisase.com:7831/XX/YY/ZZ/saml/metadata` |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | User | URL |
    | --- | --- |
    | For FortiSASE VPN User SSO | `https://<TENANTHOSTNAME>.edge.prod.fortisase.com/remote/saml/login` |
    | For FortiSASE SWG User SSO | `https://<TENANTHOSTNAME>.edge.prod.fortisase.com:7831/XX/YY/ZZ/saml/login` |

    c. In the **Sign on URL** text box, type a URL using one of the following patterns:

    | User | URL |
    | --- | --- |
    | For FortiSASE VPN User SSO | `https://<TENANTHOSTNAME>.edge.prod.fortisase.com/remote/login` |
    | For FortiSASE SWG User SSO | `https://<TENANTHOSTNAME>.edge.prod.fortisase.com:7831/XX/YY/ZZ/login` |

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. On the FortiSASE portal, go to **Configuration &gt; VPN User SSO** or **Configuration &gt; SWG User SSO** to find the service provider URLs. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. FortiSASE application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, FortiSASE application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | group | user.groups |
    | username | user.userprincipalname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up FortiSASE** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure FortiSASE SSO

1. Log in to your FortiSASE company site as an administrator.
2. Go to **Configuration &gt; VPN User SSO** or **Configuration &gt; SWG User SSO** depending on the FortiSASE mode used.
3. In the **Configure Identity Provider** section, copy the following URLs and paste in the **Basic SAML Configuration** section.

    ![Screenshot that shows the Configuration](media/fortisase-tutorial/general.png)
4. In the **Configure Service Provider** section, perform the following steps:

    ![Screenshot that shows Service Provider configuration](media/fortisase-tutorial/certificate.png)

    a. In the **IdP Entity ID** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.

    b. In the **IdP Single Sign-On URL** textbox, paste the **Login URL** value which you copied previously.

    c. In the **IdP Single Log-Out URL** textbox, paste the **Logout URL** value which you copied previously.

    d. Open the downloaded **Certificate (Base64)** into Notepad and upload the content into the **IdP Certificate** textbox.
5. Review and submit the configuration.

### Create FortiSASE test user

FortiSASE supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to FortiSASE Sign-on URL where you can initiate the login flow.
- Go to FortiSASE Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the FortiSASE tile in the My Apps, this option redirects to FortiSASE Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).