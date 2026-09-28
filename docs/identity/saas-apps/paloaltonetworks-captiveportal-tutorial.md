---
layout: Conceptual
title: Configure Palo Alto Networks Captive Portal for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/paloaltonetworks-captiveportal-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Palo Alto Networks Captive Portal.
ms.topic: how-to
ms.date: 2025-05-09T00:00:00.0000000Z
locale: en-us
document_id: 0acb7bae-f9f1-c1d9-bf2f-eae68593710f
document_version_independent_id: 931111c1-663c-6f75-ed63-0c65ba83cae7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/paloaltonetworks-captiveportal-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/paloaltonetworks-captiveportal-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/paloaltonetworks-captiveportal-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c4f54322-03d3-da7f-9ec9-9232309bec84
---

# Configure Palo Alto Networks Captive Portal for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Palo Alto Networks Captive Portal with Microsoft Entra ID. Integrating Palo Alto Networks Captive Portal with Microsoft Entra ID provides you with the following benefits:

- You can control in Microsoft Entra ID who has access to Palo Alto Networks Captive Portal.
- You can enable your users to be automatically signed-in to Palo Alto Networks Captive Portal (Single Sign-On) with their Microsoft Entra accounts.
- You can manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Palo Alto Networks Captive Portal single sign-on (SSO)-enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Palo Alto Networks Captive Portal supports **IDP** initiated SSO
- Palo Alto Networks Captive Portal supports **Just In Time** user provisioning

## Adding Palo Alto Networks Captive Portal from the gallery

To configure the integration of Palo Alto Networks Captive Portal into Microsoft Entra ID, you need to add Palo Alto Networks Captive Portal from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Palo Alto Networks Captive Portal** in the search box.
4. Select **Palo Alto Networks Captive Portal** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO

In this section, you configure and test Microsoft Entra single sign-on with Palo Alto Networks Captive Portal based on a test user called **B.Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in Palo Alto Networks Captive Portal needs to be established.

To configure and test Microsoft Entra single sign-on with Palo Alto Networks Captive Portal, perform the following steps:

1. **Configure Microsoft Entra SSO**- Enable the user to use this feature.
    - **Create a Microsoft Entra test user** - Test Microsoft Entra single sign-on with the user B.Simon.
    - **Assign the Microsoft Entra test user** - Set up B.Simon to use Microsoft Entra single sign-on.
2. **Configure Palo Alto Networks Captive Portal SSO**- Configure the single sign-on settings in the application.
    - **Create a Palo Alto Networks Captive Portal test user** - to have a counterpart of B.Simon in Palo Alto Networks Captive Portal that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - Verify that the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Palo Alto Networks Captive Portal** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** pane, perform the following steps:

    1. For **Identifier**, enter a URL that has the pattern `https://<customer_firewall_host_name>:6082/SAML20/SP`.
    2. For **Reply URL**, enter a URL that has the pattern `https://<customer_firewall_host_name>:6082/SAML20/SP/ACS`.

        Note

        Update the placeholder values in this step with the actual identifier and reply URLs. To get the actual values, contact [Palo Alto Networks Captive Portal Client support team](https://support.paloaltonetworks.com/support).
6. In the **SAML Signing Certificate** section, next to **Federation Metadata XML**, select **Download**. Save the downloaded file on your computer.

    ![The Federation Metadata XML download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Palo Alto Networks Captive Portal SSO

Next, set up single-sign on in Palo Alto Networks Captive Portal:

1. In a different browser window, sign in to the Palo Alto Networks website as an administrator.
2. Select the **Device** tab.

    ![The Palo Alto Networks website Device tab](media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin1.png)
3. In the menu, select **SAML Identity Provider**, and then select **Import**.

    ![The Import button](media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin2.png)
4. In the **SAML Identity Provider Server Profile Import** dialog box, complete the following steps:

    ![Configure Palo Alto Networks single sign-on](media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin3.png)

    1. For **Profile Name**, enter a name, like `AzureAD-CaptivePortal`.
    2. Next to **Identity Provider Metadata**, select **Browse**. Select the metadata.xml file that you downloaded.
    3. Select **OK**.

### Create a Palo Alto Networks Captive Portal test user

Next, create a user named *Britta Simon* in Palo Alto Networks Captive Portal. Palo Alto Networks Captive Portal supports just-in-time user provisioning, which is enabled by default. You don't need to complete any tasks in this section. If a user doesn't already exist in Palo Alto Networks Captive Portal, a new one is created after authentication.

Note

If you want to create a user manually, contact the [Palo Alto Networks Captive Portal Client support team](https://support.paloaltonetworks.com/support).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Palo Alto Networks Captive Portal for which you set up the SSO
- You can use Microsoft My Apps. When you select the Palo Alto Networks Captive Portal tile in the My Apps, you should be automatically signed in to the Palo Alto Networks Captive Portal for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).