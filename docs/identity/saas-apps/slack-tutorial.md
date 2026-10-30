---
layout: Conceptual
title: Configure Slack for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/slack-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Slack.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 919ac673-c2e9-6768-1071-7607c5c6a5c9
document_version_independent_id: 7620fb9f-2085-ab9b-60dd-7e5a73355c0d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/slack-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/slack-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/slack-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 93ca592d-f9b7-f4fb-bd58-b517ad58e45e
---

# Configure Slack for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Slack with Microsoft Entra ID. When you integrate Slack with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Slack.
- Enable your users to be automatically signed-in to Slack with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Slack is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- Slack single sign-on (SSO) enabled subscription.

Note

If you need to integrate with more than one Slack instance in one tenant, the identifier for each application can be a variable.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Slack supports **SP (service provider)** initiated SSO.
- Slack supports **Just In Time** user provisioning.
- Slack supports [**Automated** user provisioning](slack-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding Slack from the gallery

To configure the integration of Slack into Microsoft Entra ID, you need to add Slack from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Slack** in the search box.
4. Select **Slack** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Slack

Configure and test Microsoft Entra SSO with Slack using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Slack.

To configure and test Microsoft Entra SSO with Slack, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Slack SSO**- to configure the single sign-on settings on application side.
    1. **Create Slack test user** - to have a counterpart of B.Simon in Slack that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Slack** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier (Entity ID)** text box, type the URL: `https://slack.com`

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://<DOMAIN NAME>.slack.com/sso/saml` |
    | `https://<DOMAIN NAME>.enterprise.slack.com/sso/saml` |

    c. In the **Sign on URL** text box, type a URL using one of the following patterns:

    | Sign on URL |
    | --- |
    | `https://<DOMAIN>.slack.com` |
    | `https://<DOMAIN>.enterprise.slack.com` |

    Note

    These values aren't real. You need to update these values with the actual Sign-on URL and Reply URL. Contact [Slack support team](https://slack.com/help/contact) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.

    Note

    The value for **Identifier (Entity ID)** can be a variable if you have more than one Slack instance that you need to integrate with the tenant. Use the pattern `https://<DOMAIN NAME>.slack.com`. In this scenario, you also must pair with another setting in Slack by using the same value.
6. Slack application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, Slack application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    ![Screenshot of the Required Claims.](media/slack-tutorial/claims.png)
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
9. On the **Set up Slack** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Slack SSO

1. In a different web browser window, sign in to your up Slack company site as an administrator
2. select your workspace name in the top left, then go to **Settings & administration** &gt; **Workspace settings**.

    ![Screenshot of Configure single sign-on for Microsoft Entra ID.](media/slack-tutorial/tutorial-slack-team-settings.png)
3. In the **Settings & permissions** section, select the **Authentication** tab, and then select **Configure** button at SAML authentication method.

    ![Screenshot of Configure single sign-on On Team Settings.](media/slack-tutorial/tutorial-slack-authentication.png)
4. On the **Configure SAML authentication for Azure** dialog, perform the below steps:

    a. In the top right, toggle **Test** mode on.

    b. In the **SAML SSO URL** textbox, paste the value of **Login URL**.

    c. In the **Identity provider issuer** textbox, paste the value of **Microsoft Entra Identifier**.

    d. Open your downloaded certificate file in Notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.
5. Expand the **Advanced options** and perform the below steps:

    ![Screenshot of Configure Advanced options single sign-on On App Side.](media/slack-tutorial/advanced-settings.png)

    a. If you need an end-to-end encryption key, tick the box **Sign AuthnRequest** to show the certificate.

    b. Enter `https://slack.com` in the **Service provider issuer** textbox.

    c. Choose how the SAML response from your IDP is signed from the two options.

    Note

    In order to set up the service provider (SP) configuration, you must select **Expand** next to **Advanced Options** in the SAML configuration page. In the **Service Provider Issuer** box, enter the workspace URL. The default is slack.com.

    Note

    Set the **AuthnContextClassRef** to **Don't send this value** to resolve the error message, "Error - AADSTS75011 Authentication method by which the user authenticated with the service doesn't match requested authentication method AuthnContextClassRef".
6. Under **Settings**, decide if members can edit their profile information (like their email or display name) after SSO is enabled. You can also choose whether SSO is required, partially required or optional.

    ![Screenshot of Configure Save configuration single sign-on On App Side.](media/slack-tutorial/save-configuration-button.png)
7. Select **Save Configuration**.

    Note

    If you have more than one Slack instance that you need to integrate with Microsoft Entra ID, set `https://<DOMAIN NAME>.slack.com` to **Service provider issuer** so that it can pair with the Azure application **Identifier** setting.

### Create Slack test user

The objective of this section is to create a user called B.Simon in Slack. Slack supports just-in-time provisioning, which is by default enabled. There's no action item for you in this section. A new user is created during an attempt to access Slack if it doesn't exist yet. Slack also supports automatic user provisioning, you can find more details [here](slack-provisioning-tutorial) on how to configure automatic user provisioning.

Note

If you need to create a user manually, you need to contact [Slack support team](https://slack.com/help/contact).

Note

Microsoft Entra Connect is the synchronization tool which can sync on premises Active Directory Identities to Microsoft Entra ID and then these synced users can also use the applications as like other cloud users.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Slack Sign-on URL where you can initiate the login flow.
- Go to Slack Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Slack tile in the My Apps, this option redirects to Slack Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).