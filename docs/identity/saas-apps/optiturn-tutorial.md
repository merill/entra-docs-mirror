---
layout: Conceptual
title: Configure OptiTurn for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/optiturn-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and OptiTurn.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: e2802ad2-e179-9233-75cc-944c3bd6c414
document_version_independent_id: f5e35e64-086d-353e-3c1e-0a78563588b3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/optiturn-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/optiturn-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/optiturn-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ec91859d-96db-e1ff-1894-086712e2f0c4
---

# Configure OptiTurn for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate OptiTurn with Microsoft Entra ID. OptiTurn is a returns management platform that helps retailers route returned items, improve warehouse operations, and manage inventory backlogs. When you integrate OptiTurn with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to OptiTurn.
- Enable your users to be automatically signed-in to OptiTurn with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for OptiTurn in a test environment. OptiTurn supports **SP** initiated single sign-on and **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with OptiTurn, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- OptiTurn single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the OptiTurn application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add OptiTurn from the Microsoft Entra gallery

Add OptiTurn from the Microsoft Entra application gallery to configure single sign-on with OptiTurn. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **OptiTurn** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL using one of the following:

    | **Identifier** |
    | --- |
    | `https://optiturn.com/sp` - production |
    | `https://sandbox.optiturn.com/sp` - testing |

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://optiturn.com/auth/saml/<Customer_Name>_azure_saml/callback` - production |
    | `https://sandbox.optiturn.com/auth/saml/<Customer_Name>_azure_saml/callback` - testing |

    c. In the **Sign on URL** textbox, type one of the following:

    | **Sign on URL** |
    | --- |
    | `https://optiturn.com/session/new` - production |
    | `https://sandbox.optiturn.com/session/new` - testing |

    Note

    `<Customer_Name>` should be replaced with a lowercased and underscored version of your company’s name. For example, Fake Corp. would become fake\_corp. The [OptiTurn support team](mailto:support@optoro.com) can help choose this value.
6. OptiTurn application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, OptiTurn application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | first\_name | user.givenname |
    | last\_name | user.surname |

    Note

    The warehouse\_identifier assertion attribute is recommended for ease of use, but it isn't required. warehouse\_identifier is an identifier for the warehouse where a given employee is physically located. We will match the identifier against a warehouse that's configured in OptiTurn. The user’s activity and data will then be “scoped” to that warehouse.
8. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
9. On the **Set up OptiTurn** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure OptiTurn SSO

To configure single sign-on on **OptiTurn** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [OptiTurn support team](mailto:support@optoro.com). They set this setting to have the SAML SSO connection set properly on both sides

### Create OptiTurn test user

In this section, a user called B.Simon is created in OptiTurn. OptiTurn supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in OptiTurn, a new one is commonly created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to OptiTurn Sign-on URL where you can initiate the login flow.
- Go to OptiTurn Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the OptiTurn tile in the My Apps, this option redirects to OptiTurn Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).