---
layout: Conceptual
title: Configure OrgChart Now for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/orgchartnow-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and OrgChart Now.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: c3a5ed39-7544-ea51-d634-d9b320bd03ff
document_version_independent_id: ae75ad56-9194-9b68-b4fe-330f68640839
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/orgchartnow-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/orgchartnow-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/orgchartnow-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2e256c95-5ef0-dfae-78d0-49962822ab53
---

# Configure OrgChart Now for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate OrgChart Now with Microsoft Entra ID. When you integrate OrgChart Now with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to OrgChart Now.
- Enable your users to be automatically signed-in to OrgChart Now with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- OrgChart Now single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- OrgChart Now supports **SP** and **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add OrgChart Now from the gallery

To configure the integration of OrgChart Now into Microsoft Entra ID, you need to add OrgChart Now from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **OrgChart Now** in the search box.
4. Select **OrgChart Now** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for OrgChart Now

Configure and test Microsoft Entra SSO with OrgChart Now using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in OrgChart Now.

To configure and test Microsoft Entra SSO with OrgChart Now, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure OrgChart Now SSO**- to configure the single sign-on settings on application side.
    1. **Create OrgChart Now test user** - to have a counterpart of B.Simon in OrgChart Now that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **OrgChart Now** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following step:

    a. In the **Identifier** text box, type the URL: `https://<OrgChartNowServer>.orgchartnow.com/saml/sso_metadata?entityID=<Your_Azure_AD_Entity_ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<OrgChartServer>.orgchartnow.com/saml/sso_acs?entityID=<Your_Azure_AD_Entity_ID>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<OrgChartServer>.orgchartnow.com/saml/sso_acs?entityID=<Your_Azure_AD_Entity_ID>`

    Note

    `<YourEntityID>` is the **Microsoft Entra Identifier** copied from the **Set up OrgChart Now** section, described later in article.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up OrgChart Now** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure OrgChart Now SSO

To configure single sign-on in OrgChart Now, follow the steps enumerated in the [SSO Configuration article](https://help.orgchartnow.com/en/topics/sso-configuration.html#configuring-sso-41334) on OrgChart Now's Help site.

### Create OrgChart Now test user

To enable Microsoft Entra users to log in to OrgChart Now, they must be set up as a user in OrgChart Now, or **Auto-Provisioning** must be enabled in the [SSO Configuration](https://help.orgchartnow.com/en/topics/sso-configuration.html#configuring-sso-41334) panel.

If you don't wish to enable auto-provisioning at this time, you can manually add a user to OrgChart Now for SSO testing purposes. To do so, follow the steps enumerated in the [Creating a New User](https://help.orgchartnow.com/en/account-settings/manage-users.html#UUID-a921b00b-a5a2-3099-8fe5-d0f28f5a50b9_bridgehead-idm4532421481724832584395125038) section of the [Account Settings: Manage Users](https://help.orgchartnow.com/en/account-settings/manage-users.html) article.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to OrgChart Now Sign on URL where you can initiate the login flow.
- Go to OrgChart Now Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the OrgChart Now for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the OrgChart Now tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the OrgChart Now for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).