---
layout: Conceptual
title: Configure Salesforce for Single sign-on in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/salesforce-tutorial
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
description: Learn how to configure the single sign-on between Microsoft Entra ID and Salesforce.
ms.topic: how-to
ms.date: 2026-06-24T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: adf2d1dc-ab4d-5e4a-d18d-a9f4fba5aedb
document_version_independent_id: 2a58c27f-19e8-1a9a-f14a-45db73b91cc2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/salesforce-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/salesforce-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/salesforce-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e32f4412-b0be-c5a9-423b-684a8a46dc11
---

# Configure Salesforce for Single sign-on in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Salesforce with Microsoft Entra ID. When you integrate Salesforce with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Salesforce.
- Enable your users to be automatically signed-in to Salesforce with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Note

**Updated: July 24, 2026** - Starting June 29, 2026, Microsoft Entra ID will automatically include Authentication Method References (`amr`) and Authentication Context References (`acr`) claims in tokens issued for SAML 2.0 and OpenID Connect (OIDC) applications using the Microsoft identity platform v2.0 token. **If you have configured External MFA Provider with Entra ID and if that provider is sending AMR signals then Entra ID will forward that AMR signal to Salesforce or other 3P applications as needed.** These claims provide additional information about how the user authenticated and the authentication context satisfied during sign-in. No configuration changes are required in Microsoft Entra ID for Salesforce single sign-on. To help satisfy Salesforce [phishing-resistant MFA requirements](https://help.salesforce.com/s/articleView?id=005321563&amp;type=1) for Salesforce admins, and [device activation changes for Single Sign-On (SSO) Logins](https://help.salesforce.com/s/articleView?id=005237070&amp;type=1) customers should apply Microsoft Entra Conditional Access policies that require phishing-resistant authentication methods for Salesforce administrator sign-ins.

For customers using AD FS as the federation provider with Entra ID, please follow the [MFA expected inbound assertions guidance for SAML 2.0 federated IdPs](../authentication/how-to-mfa-expected-inbound-assertions#using-saml-20-federated-idp) so that Entra ID will have this claim in the SAML token.

If you are using any other federation provider then we are still working on standardizing the AMR and ACR signals first and will provide the update soon.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Salesforce single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Salesforce supports **SP** initiated SSO.
- Salesforce supports [**Automated** user provisioning and deprovisioning](salesforce-provisioning-tutorial) (recommended).
- Salesforce supports **Just In Time** user provisioning.
- Salesforce Mobile application can now be configured with Microsoft Entra ID for enabling SSO. In this article, you configure and test Microsoft Entra SSO in a test environment.

## Add Salesforce from the gallery

To configure the integration of Salesforce into Microsoft Entra ID, you need to add Salesforce from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Salesforce** in the search box.
4. Select **Salesforce** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Salesforce

Configure and test Microsoft Entra SSO with Salesforce using a test user called **B.Simon**. For SSO to work, you need to establish a link between the Microsoft Entra test user B.Simon and the corresponding user account in Salesforce.

To configure and test Microsoft Entra SSO with Salesforce, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Salesforce SSO**- to configure the single sign-on settings on application side.
    - **Create Salesforce test user** - to have a counterpart of B.Simon in Salesforce that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Salesforce** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** textbox, type the value using the following pattern:

    Enterprise account: `https://<subdomain>.my.salesforce.com`

    Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`

    b. In the **Reply URL** textbox, type the value using the following pattern:

    Enterprise account: `https://<subdomain>.my.salesforce.com`

    Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`

    c. In the **Sign-on URL** textbox, type the value using the following pattern:

    Enterprise account: `https://<subdomain>.my.salesforce.com`

    Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, and Sign-on URL. Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Salesforce** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Salesforce SSO

1. In a different web browser window, sign in to your up Salesforce company site as an administrator
2. Select the **Setup** under **settings icon** on the top right corner of the page.

    ![Configure Single Sign-On settings icon](media/salesforce-tutorial/configure1.png)
3. Scroll down to the **SETTINGS** in the navigation pane, select **Identity** to expand the related section. Then select **Single Sign-On Settings**.

    ![Configure Single Sign-On Settings](media/salesforce-tutorial/sf-admin-sso.png)
4. On the **Single Sign-On Settings** page, select the **Edit** button.

    ![Configure Single Sign-On Edit](media/salesforce-tutorial/sf-admin-sso-edit.png)

    Note

    If you're unable to enable single sign-on settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).
5. Select **SAML Enabled**, and then select **Save**.

    ![Configure Single Sign-On SAML Enabled](media/salesforce-tutorial/sf-enable-saml.png)
6. To configure your SAML single sign-on settings, select **New from Metadata File**.

    ![Configure Single Sign-On New from Metadata File](media/salesforce-tutorial/sf-admin-sso-new.png)
7. Select **Choose File** to upload the metadata XML file which you have downloaded and select **Create**.

    ![Configure Single Sign-On Choose File](media/salesforce-tutorial/xmlchoose.png)
8. On the **SAML Single Sign-On Settings** page, fields populate automatically, if you want to use SAML JIT, select the **User Provisioning Enabled** and select **SAML Identity Type** as **Assertion contains the Federation ID from the User object** otherwise, unselect the **User Provisioning Enabled** and select **SAML Identity Type** as **Assertion contains the User's Salesforce username**. Select **Save**.

    ![Configure Single Sign-On User Provisioning Enabled](media/salesforce-tutorial/salesforcexml.png)

    Note

    If you configured SAML JIT, you must add the required SAML token attributes in the **Configure Microsoft Entra SSO** section. The Salesforce application expects specific SAML assertions, which requires you to have specific attributes in your SAML token attributes configuration. The following screenshot shows the list of required attributes by Salesforce.

    ![Screenshot that shows the JIT required attributes pane.](media/salesforce-tutorial/just-in-time-attributes-required.png)

    If you still have issues with getting users provisioned with SAML JIT, see [Just-in-time provisioning requirements and SAML assertion fields](https://help.salesforce.com/s/articleView?id=sf.sso_jit_requirements.htm&amp;type=5). Generally, when JIT fails, you might see an error like `We can't log you in because of an issue with single sign-on. Contact your Salesforce admin for help.`
9. On the left navigation pane in Salesforce, select **Company Settings** to expand the related section, and then select **My Domain**.

    ![Configure Single Sign-On My Domain](media/salesforce-tutorial/sf-my-domain.png)
10. Scroll down to the **Authentication Configuration** section, and select the **Edit** button.

    ![Configure Single Sign-On Authentication Configuration](media/salesforce-tutorial/sf-edit-auth-config.png)
11. In the **Authentication Configuration** section, Check the **Login Page** and **AzureSSO** as **Authentication Service** of your SAML SSO configuration, and then select **Save**.

    Note

    If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment. If you don’t want it to happen, then you should **leave all other authentication services unchecked**.

### Create Salesforce test user

In this section, a user called B.Simon is created in Salesforce. Salesforce supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce. Salesforce also supports automatic user provisioning. For more details, see [Configure Salesforce automatic user provisioning](salesforce-provisioning-tutorial).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Salesforce Sign-on URL where you can initiate the login flow.
- Go to Salesforce Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Salesforce tile in the My Apps portal, you should be automatically signed in to the Salesforce for which you set up the SSO. For more information about the My Apps portal, see [Introduction to the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Test SSO for Salesforce (Mobile)

Perform the following steps to test SSO in the Salesforce mobile app:

1. Open Salesforce mobile application. On the sign-in page, select **Use Custom Domain**.

    ![Salesforce mobile app Use Custom Domain](media/salesforce-tutorial/mobile-app1.png)
2. In the **Custom Domain** textbox, enter your registered custom domain name and select **Continue**.

    ![Salesforce mobile app Custom Domain](media/salesforce-tutorial/mobile-app2.png)
3. Enter your Microsoft Entra credentials to sign in to the Salesforce application and select **Next**.

    ![Salesforce mobile app Microsoft Entra credentials](media/salesforce-tutorial/mobile-app3.png)
4. On the **Allow Access** page as shown below, select **Allow** to give access to the Salesforce application.

    ![Salesforce mobile app Allow Access](media/salesforce-tutorial/mobile-app4.png)
5. Finally after successful sign-in, the application homepage is displayed.

    ![Salesforce mobile app homepage](media/salesforce-tutorial/mobile-app5.png)![Salesforce mobile app](media/salesforce-tutorial/mobile-app6.png)

## Discover existing users in Salesforce

Prior to integration with Microsoft Entra, your Salesforce account may already have one or more users. Using the account discovery functionality, you can generate a report of all the users in Salesforce, identify which users have matching accounts in Entra, and which users are local to Salesforce with one click. Learn more in [How to use account discovery for application provisioning](../app-provisioning/how-to-account-discovery). This enables you to simplify onboarding to Entra, while also periodically monitoring for unauthorized access.

## Prevent application access through local accounts

Once you've validated that SSO works and rolled it out in your organization, disable application access using [local credentials](https://help.salesforce.com/s/articleView?id=sf.sso_enforce_sso_login.htm&amp;type=5). This ensures that your Conditional Access policies, MFA, etc. is in place to protect sign-ins to Salesforce.