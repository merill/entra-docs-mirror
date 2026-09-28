---
layout: Conceptual
title: Configure ProdPad for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/prodpad-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ProdPad.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: e1968b34-a5a6-7fac-c3b5-1e05c53f1a09
document_version_independent_id: 0673a74b-c0ed-486e-0808-674579ff7c9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/prodpad-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/prodpad-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/prodpad-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bd31f34e-ed9b-a864-afd2-0ca345b797d5
---

# Configure ProdPad for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ProdPad with Microsoft Entra ID. When you integrate ProdPad with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ProdPad.
- Enable your users to be automatically signed-in to ProdPad with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- ProdPad single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- ProdPad supports **SP and IDP** initiated SSO.
- ProdPad supports **Just In Time** user provisioning.
- ProdPad supports [Automated user provisioning](prodpad-provisioning-tutorial).

## Adding ProdPad from the gallery

To configure the integration of ProdPad into Microsoft Entra ID, you need to add ProdPad from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ProdPad** in the search box.
4. Select **ProdPad** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for ProdPad

Configure and test Microsoft Entra SSO with ProdPad using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ProdPad.

To configure and test Microsoft Entra SSO with ProdPad, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ProdPad SSO**- to configure the single sign-on settings on application side.
    1. **Create ProdPad test user** - to have a counterpart of B.Simon in ProdPad that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ProdPad** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://app.prodpad.com/login`
7. Select **Save**.
8. ProdPad application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
9. In addition to above, ProdPad application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | User.FirstName | user.givenname |
    | User.LastName | user.surname |
    | User.ProdpadRole | user.assignedroles |

    Note

    ProdPad expects roles for users assigned to the application. Please set up these roles in Microsoft Entra ID so that users can be assigned the appropriate roles. To understand how to configure roles in Microsoft Entra ID, see [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui).
10. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
11. On the **Set up ProdPad** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ProdPad SSO

1. Go to Account Settings and select the Security tab.
2. Now select the SSO/SAML sub-tab.
3. Select the "Add authentication type" button and select Microsoft Entra from the dropdown.
4. Select the Next button on the Microsoft Entra modal.
5. Copy into the field labelled "IdP Entity ID/URL" in ProdPad, the URL from the field "Microsoft Entra Identifier" in Microsoft Entra.
6. Copy into the field "IdP SAML Single Sign-On URL" in ProdPad, the URL in the field "Login URL" in Microsoft Entra.
7. Copy into the field "Logout URL" in ProdPad, the URL in the field "Logout URL" in Microsoft Entra.
8. Paste the text of X.509 certificate (public key generated above) into the X.509 certificate field.

Now you must decide whether you want your users to login by IdP initiated login only or by IdP and SP initiated login.

1. If you select IdP only, you users must login from the Microsoft Entra dashboard, rather than the ProdPad login page.

    1. Select save. Your users can now use the ProdPad app link on their Microsoft Entra dashboard.
2. If you opt for IdP & SP initiated login

    1. you must set up the Domains that your users can login from, more about this [here](https://help.prodpad.com/article/704-domain-verification)
    2. Once set up and verified, select the domain from the Domains list.
    3. Hit save.

**Note: for a domain to appear as an option here it must be verified under the Domains tab.**

### Create ProdPad test user

In this section, a user called Britta Simon is created in ProdPad. ProdPad supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in ProdPad, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to ProdPad Sign on URL where you can initiate the login flow.
- Go to ProdPad Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the ProdPad for which you set up the SSO

You can also use Microsoft Access Panel to test the application in any mode. When you select the ProdPad tile in the Access Panel, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the ProdPad for which you set up the SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).