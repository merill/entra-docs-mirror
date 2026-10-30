---
layout: Conceptual
title: Configure GovWin IQ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/govwin-iq-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and GovWin IQ.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: c33c7be2-3918-15b3-a52d-9de07ce64a8b
document_version_independent_id: c8f3cd93-fb6b-78f7-554a-97233456f634
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/govwin-iq-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/govwin-iq-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/govwin-iq-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 01ba0c5f-b424-2578-4ec1-1e9089eda744
---

# Configure GovWin IQ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate GovWin IQ with Microsoft Entra ID. GovWin IQ by Deltek is the industry-leading platform providing the most comprehensive market intelligence for U.S. federal, state and local, and Canadian governments. When you integrate GovWin IQ with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to GovWin IQ.
- Enable your users to be automatically signed-in to GovWin IQ with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An active GovWin IQ Subscription. Single sign-on can be enabled at no cost. Make sure your Customer Success Manager has enabled a user at your organization as a SAML SSO Admin to perform the following steps.
- All users must have same email address in Azure as provisioned in GovWin IQ.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- GovWin IQ supports only **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding GovWin IQ from the gallery

To configure the integration of GovWin IQ into Microsoft Entra ID, you need to add GovWin IQ from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **GovWin IQ** in the search box.
4. Select **GovWin IQ** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for GovWin IQ

Configure and test Microsoft Entra SSO with GovWin IQ using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in GovWin IQ.

To configure and test Microsoft Entra SSO with GovWin IQ, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure GovWin IQ SSO**- to configure the single sign-on settings on application side.
    1. **Assign GovWin IQ test user to SSO** - to have a counterpart of B.Simon in GovWin IQ that's linked to the Microsoft Entra ID representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **GovWin IQ** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL: `https://iq.govwin.com/cas`

    b. In the **Reply URL** textbox, enter the value from the GovWin IQ Reply URL field.

    Reply URL is of the following pattern: `https://iq.govwin.com/cas/login?client_name=ORG_<ID>`

    c. In the **Sign on URL** textbox, enter the value from the GovWIn IQ Sign On URL field.

    Sign on URL is of the following pattern: `https://iq.govwin.com/cas/clientredirect?client_name=ORG_<ID>`

    Note

    Update these values with the actual Reply URL and Sign on URL found in the GovWin SAML Single Sign-On Configuration page, accessible by your designated SAML SSO Admin. Reach out to your [Customer Success Manager](mailto:CustomerSuccess@iq.govwin.com) for assistance. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Assign the Microsoft Entra ID test user

In this section, you enable a test user to use Microsoft Entra single sign-on by granting access to GovWin IQ.

Note

The user selected for testing must have an existing active GovWin IQ account.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **GovWin IQ**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select a test user from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure GovWin IQ SSO

1. Log in to GovWin IQ company site as the SAML SSO Admin user.
2. Navigate to [**SAML Single Sign-On Configuration** page](https://iq.govwin.com/neo/authenticationConfiguration/viewSamlSSOConfig) and perform the following steps:

    ![Screenshot shows settings of the configuration.](media/govwin-iq-tutorial/settings.png)

    1. Select **Azure** from the Identity Provider (IdP) dropdown.
    2. Copy **Identifier (EntityID)** value, paste this value into the **Identifier** textbox in the **Basic SAML Configuration** section in Microsoft Entra admin center.
    3. Copy **Reply URL** value, paste this value into the **Reply URL** textbox in the **Basic SAML Configuration** section in Microsoft Entra admin center.
    4. Copy **Sign On URL** value, paste this value into the **Sign on URL** textbox in the **Basic SAML Configuration** section in Microsoft Entra admin center.
3. In the **Metadata URL** textbox, paste the **App Federation Metadata Url**, which you have copied from the Microsoft Entra admin center.

    ![Screenshot shows metadata of the configuration.](media/govwin-iq-tutorial/values.png)
4. Select **Submit IDP Metadata**.

### Assign GovWin IQ test user to SSO

1. In the [**SAML Single Sign-On Configuration** page](https://iq.govwin.com/neo/authenticationConfiguration/viewSamlSSOConfig), navigate to **Excluded Users** tab and select **Select Users to Exclude from SSO**.

    ![Screenshot shows how to exclude users from the page.](media/govwin-iq-tutorial/data.png)

    Note

    Here you can select users to include or exclude from SSO. If you have a webservices subscription, the webservices user should always be excluded from SSO.
2. Next, select **Exclude All Users from SSO** for testing purposes. This is to prevent any impact to existing access for users while testing SSO.
3. Next, select the test user and select Add Selected Users to SSO.
4. Once testing is successful, add the rest of the users you want to enable for SSO.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

Note

It may take up to 10 minutes for the configuration to sync.

- Select **Test this application** in Microsoft Entra admin center. this option redirects to GovWin IQ Sign-on URL where you can initiate the login flow.
- Go to GovWin IQ Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the GovWin IQ tile in the My Apps, this option redirects to GovWin IQ Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).