---
layout: Conceptual
title: Configure Salesforce Sandbox for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/salesforce-sandbox-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Salesforce Sandbox.
ms.topic: how-to
ms.date: 2026-06-24T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c206e955-bb5b-0707-5cf5-7b29cdf0ff6e
document_version_independent_id: f00eff35-9f21-ea45-45a6-eba4be4fda04
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/salesforce-sandbox-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/salesforce-sandbox-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/salesforce-sandbox-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d7f71632-57e0-28c3-68c5-2663024f0fd9
---

# Configure Salesforce Sandbox for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Salesforce Sandbox with Microsoft Entra ID. When you integrate Salesforce Sandbox with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Salesforce Sandbox.
- Enable your users to be automatically signed-in to Salesforce Sandbox with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Note

**Updated: July 24, 2026** - Starting June 29, 2026, Microsoft Entra ID will automatically include Authentication Method References (`amr`) and Authentication Context References (`acr`) claims in tokens issued for SAML 2.0 and OpenID Connect (OIDC) applications using the Microsoft identity platform v2.0 token. **If you have configured External MFA Provider with Entra ID and if that provider is sending AMR signals then Entra ID will forward that AMR signal to Salesforce or other 3P applications as needed.** These claims provide additional information about how the user authenticated and the authentication context satisfied during sign-in. No configuration changes are required in Microsoft Entra ID for Salesforce Sandbox single sign-on. To help satisfy Salesforce [phishing-resistant MFA requirements](https://help.salesforce.com/s/articleView?id=005321563&amp;type=1) for Salesforce admins, and [device activation changes for Single Sign-On (SSO) Logins](https://help.salesforce.com/s/articleView?id=005237070&amp;type=1) customers should apply Microsoft Entra Conditional Access policies that require phishing-resistant authentication methods for Salesforce administrator sign-ins.

For customers using AD FS as the federation provider with Entra ID, please follow the [MFA expected inbound assertions guidance for SAML 2.0 federated IdPs](../authentication/how-to-mfa-expected-inbound-assertions#using-saml-20-federated-idp) so that Entra ID will have this claim in the SAML token.

If you are using any other federation provider then we are still working on standardizing the AMR and ACR signals first and will provide the update soon.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Salesforce Sandbox single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Salesforce Sandbox supports **SP and IDP** initiated SSO
- Salesforce Sandbox supports **Just In Time** user provisioning
- Salesforce Sandbox supports [**Automated** user provisioning](salesforce-sandbox-provisioning-tutorial)

## Adding Salesforce Sandbox from the gallery

To configure the integration of Salesforce Sandbox into Microsoft Entra ID, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Salesforce Sandbox** in the search box.
4. Select **Salesforce Sandbox** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Salesforce Sandbox

Configure and test Microsoft Entra SSO with Salesforce Sandbox using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Salesforce Sandbox.

To configure and test Microsoft Entra SSO with Salesforce Sandbox, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Salesforce Sandbox SSO**- to configure the single sign-on settings on application side.
    1. **Create Salesforce Sandbox test user** - to have a counterpart of B.Simon in Salesforce Sandbox that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Salesforce Sandbox** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file** and wish to configure in **IDP** initiated mode perform the following steps:

    a. Select **Upload metadata file**.

    ![Upload metadata file](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![choose metadata file](common/browse-upload-metadata.png)

    Note

    You get the service provider metadata file from the Salesforce Sandbox admin portal which is explained later in the article.

    c. After the metadata file is successfully uploaded, the **Reply URL** value gets auto populated in **Reply URL** textbox.

    ![image](common/both-replyurl.png)

    Note

    If the **Reply URL** value don't get auto populated, then fill in the value manually according to your requirement.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Salesforce Sandbox** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Salesforce Sandbox SSO

1. Open a new tab in your browser and sign in to your Salesforce Sandbox administrator account.
2. Select the **Setup** under **settings icon** on the top right corner of the page.

    ![Screenshot that shows the &quot;Settings&quot; icon in the top-right selected, and &quot;Setup&quot; selected from the drop-down.](media/salesforce-sandbox-tutorial/configure1.png)
3. Scroll down to the **SETTINGS** in the left navigation pane, select **Identity** to expand the related section. Then select **Single Sign-On Settings**.

    ![Screenshot that shows the &quot;Settings&quot; menu in the left pane, with &quot;Single Sign-On Settings&quot; selected from the &quot;Identity&quot; menu.](media/salesforce-sandbox-tutorial/sf-admin-sso.png)
4. On the **Single Sign-On Settings** page, select the **Edit** button.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;Edit&quot; button selected.](media/salesforce-sandbox-tutorial/configure3.png)
5. Select **SAML Enabled**, and then select **Save**.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;S A M L Enabled&quot; checkbox selected and the &quot;Save&quot; button selected.](media/salesforce-sandbox-tutorial/sf-enable-saml.png)
6. To configure your SAML single sign-on settings, select **New from Metadata File**.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;New from Metadata File&quot; button selected.](media/salesforce-sandbox-tutorial/sf-admin-sso-new.png)
7. Select **Choose File** to upload the metadata XML file which you have downloaded and select **Create**.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;Choose File&quot; and &quot;Create&quot; buttons selected.](media/salesforce-sandbox-tutorial/xmlchoose.png)
8. On the **SAML Single Sign-On Settings** page, fields populate automatically and select save.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with fields populated and the &quot;Save&quot; button selected.](media/salesforce-sandbox-tutorial/salesforcexml.png)
9. On the **Single Sign-On Settings** page, select the **Download Metadata** button to download the service provider metadata file. Use this file in the **Basic SAML Configuration** section in the Azure portal for configuring the necessary URLs as explained above.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;Download Metadata&quot; button selected.](media/salesforce-sandbox-tutorial/configure4.png)
10. If you wish to configure the application in **SP** initiated mode, following are the prerequisites for that:

    a. You should have a verified domain.

    b. You need to configure and enable your domain on Salesforce Sandbox, steps for this are explained later in this article.

    c. In the Azure portal, on the **Basic SAML Configuration** section, select **Set additional URLs** and perform the following step:

    ![Salesforce Sandbox Domain and URLs single sign-on information](common/both-signonurl.png)

    In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instancename>--Sandbox.<entityid>.my.salesforce.com`

    Note

    This value should be copied from the Salesforce Sandbox portal once you have enabled the domain.
11. On the **SAML Signing Certificate** section, select **Federation Metadata XML** and then save the xml file on your computer.

    ![The Certificate download link](common/metadataxml.png)
12. Open a new tab in your browser and sign in to your Salesforce Sandbox administrator account.
13. Select the **Setup** under **settings icon** on the top right corner of the page.

    ![Screenshot that shows the &quot;Settings&quot; icon in the top-right selected, and &quot;Setup&quot; selected from the drop-down menu.](media/salesforce-sandbox-tutorial/configure1.png)
14. Scroll down to the **SETTINGS** in the left navigation pane, select **Identity** to expand the related section. Then select **Single Sign-On Settings**.

    ![Screenshot that shows the &quot;Settings&quot; menu in the left navigation pane, with &quot;Single Sign-On Settings&quot; selected from the &quot;Identity&quot; menu.](media/salesforce-sandbox-tutorial/sf-admin-sso.png)
15. On the **Single Sign-On Settings** page, select the **Edit** button.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with &quot;Edit&quot; button selected.](media/salesforce-sandbox-tutorial/configure3.png)
16. Select **SAML Enabled**, and then select **Save**.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;S A M L Enabled&quot; box checked and the &quot;Save&quot; button selected.](media/salesforce-sandbox-tutorial/sf-enable-saml.png)
17. To configure your SAML single sign-on settings, select **New from Metadata File**.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page and &quot;New from Metadata File&quot; button selected.](media/salesforce-sandbox-tutorial/sf-admin-sso-new.png)
18. Select **Choose File** to upload the metadata XML file and select **Create**.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with the &quot;Choose File&quot; button and &quot;Create&quot; button selected.](media/salesforce-sandbox-tutorial/xmlchoose.png)
19. On the **SAML Single Sign-On Settings** page, fields populate automatically, type the name of the configuration (for example: *SPSSOWAAD\_Test*), in the **Name** textbox and select save.

    ![Screenshot that shows the &quot;Single Sign-On Settings&quot; page with fields populated, an example name in the &quot;Name&quot; textbox, and the &quot;Save&quot; button selected.](media/salesforce-sandbox-tutorial/sf-saml-config.png)
20. To enable your domain on Salesforce Sandbox, perform the following steps:

    Note

    Before enabling the domain you need to create the same on Salesforce Sandbox. For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&amp;language=en_US). Once the domain is created, please make sure that it's configured correctly.
21. On the left navigation pane in Salesforce Sandbox, select **Company Settings** to expand the related section, and then select **My Domain**.

    ![Screenshot that shows the &quot;Company Settings&quot; and &quot;My Domain&quot; selected from the left navigation pane.](media/salesforce-sandbox-tutorial/sf-my-domain.png)
22. In the **Authentication Configuration** section, select **Edit**.

    ![Screenshot that shows the &quot;Authentication Configuration&quot; section, with the &quot;Edit&quot; button selected.](media/salesforce-sandbox-tutorial/sf-edit-auth-config.png)
23. In the **Authentication Configuration** section, as **Authentication Service**, select the name of the SAML single sign-on setting which you have set during SSO configuration in Salesforce Sandbox and select **Save**.

    ![Configure Single Sign-On](media/salesforce-sandbox-tutorial/configure2.png)

### Create Salesforce Sandbox test user

In this section, a user called Britta Simon is created in Salesforce Sandbox. Salesforce Sandbox supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox. Salesforce Sandbox also supports automatic user provisioning, you can find more details [here](salesforce-sandbox-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Salesforce Sandbox Sign on URL where you can initiate the login flow.
- Go to Salesforce Sandbox Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Salesforce Sandbox for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Salesforce Sandbox tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Salesforce Sandbox for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).