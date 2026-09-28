---
layout: Conceptual
title: Configure myMobilityHQ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mymobilityhq-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and myMobilityHQ.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 41ed9d9d-5f19-4bea-ab55-0ca983ae3eab
document_version_independent_id: 2361c5c1-588f-bfe3-8b63-8f76fac54f8e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mymobilityhq-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mymobilityhq-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mymobilityhq-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4e11c056-61b5-48b4-b752-176071edb31d
---

# Configure myMobilityHQ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate myMobilityHQ with Microsoft Entra ID. myMobilityHQ is the secure portal that allows your company mobility managers to see a real-time dashboard of the status of their expatriate tax program. When you integrate myMobilityHQ with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to myMobilityHQ.
- Enable your users to be automatically signed-in to myMobilityHQ with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You configure and test Microsoft Entra single sign-on for myMobilityHQ in a test environment. myMobilityHQ supports only **SP** initiated single sign-on.

## Prerequisites

To integrate Microsoft Entra ID with myMobilityHQ, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- myMobilityHQ single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the myMobilityHQ application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add myMobilityHQ from the Microsoft Entra gallery

Add myMobilityHQ from the Microsoft Entra application gallery to configure single sign-on with myMobilityHQ. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **myMobilityHQ** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using one of the following patterns:

    | **Identifier** |
    | --- |
    | `urn:auth0:prod:s<COMPANYNAME>` |
    | `urn:auth0:stage:s<COMPANYNAME>` |

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://stage.vialto.auth0app.com/login/callback?connection=s<COMPANYNAME>` |
    | `https://prod.vialto.auth0app.com/login/callback?connection=s<COMPANYNAME>` |
    | `https://auth-stage.vialto.com/login/callback?connection=s<COMPANYNAME>` |
    | `https://auth.vialto.com/login/callback?connection=s<COMPANYNAME>` |

    c. In the **Sign on URL** textbox, type one of the following URLs:

    | **Sign on URL** |
    | --- |
    | `https://mymobilityhq-stage.vialto.com` |
    | `https://mymobilityhq.vialto.com` |

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [myMobilityHQ support team](mailto:gbl_vialto_iam_engineering_support@vialto.com) to get these values. You can also refer to the patterns shown in the Basic SAML Configuration section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

## Configure myMobilityHQ SSO

To configure single sign-on on **myMobilityHQ** side, you need to send the **App Federation Metadata Url** to [myMobilityHQ support team](mailto:gbl_vialto_iam_engineering_support@vialto.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create myMobilityHQ test user

In this section, you create a user called Britta Simon in myMobilityHQ. Work with [myMobilityHQ support team](mailto:gbl_vialto_iam_engineering_support@vialto.com) to add the users in the myMobilityHQ platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to myMobilityHQ Sign-on URL where you can initiate the login flow.
- Go to myMobilityHQ Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the myMobilityHQ tile in the My Apps, this option redirects to myMobilityHQ Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).