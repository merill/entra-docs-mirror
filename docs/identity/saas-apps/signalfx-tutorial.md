---
layout: Conceptual
title: Configure SignalFx for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/signalfx-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SignalFx.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 8afbcd9e-e943-7cb8-0f51-d3b956979da4
document_version_independent_id: ddf91550-2028-c9db-d153-7cb3f2c4eeb4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/signalfx-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/signalfx-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/signalfx-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: f37ab976-cbad-5b6f-3624-b5201608c3d1
---

# Configure SignalFx for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SignalFx with Microsoft Entra ID. When you integrate SignalFx with Microsoft Entra ID, you can:

- Control from Microsoft Entra ID who has access to SignalFx.
- Enable your users to be automatically signed-in to SignalFx with their Microsoft Entra accounts.
- Manage your accounts in one location (the Azure portal).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SignalFx single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SignalFx supports **IDP** initiated SSO.
- SignalFx supports **Just In Time** user provisioning.

## Step 1: Add the SignalFx application in Azure

Use these instructions to add the SignalFx application to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SignalFx** in the search box.
4. Select **SignalFx** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.
5. Leave the Microsoft Entra admin center open, and then open a new browser tab.

## Step 2: Begin SignalFx SSO configuration

Use these instructions to begin the configuration process for the SignalFx SSO.

1. In the newly opened tab, access and log into the SignalFx UI.
2. In the top menu, select **Integrations**.
3. In the search field, enter and select **Microsoft Entra ID**.
4. Select **Create New Integration**.
5. In **Name**, enter an easily recognizable name that your users will understand.
6. Mark **Show on login page**.
    - This feature will display a customized button in the login page that your users can select on.
    - The information you entered in **Name** appears on the button. As a result, enter a **Name** that your users will recognize.
    - This option will only function if you use a custom subdomain for the SignalFx application, such as **yourcompanyname.signalfx.com**. To obtain a custom subdomain, contact SignalFx support.
7. Copy the **Integration ID**. you need this information in a later step.
8. Leave the SignalFx UI open.

## Step 3: Configure Microsoft Entra SSO

Use these instructions to enable Microsoft Entra SSO.

1. Return to the Microsoft Entra admin center, and on the **SignalFx** application integration page, locate the **Manage** section, and then select **Single sign-on**.
2. On the **Select a single sign-on method** page, select **SAML**.
3. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
4. On the **Set up single sign-on with SAML** page, perform the following steps:

    a. In **Identifier**, enter the following URL `https://api.<realm>.signalfx.com/v1/saml/metadata` and replace `<realm>` with your SignalFx realm, and `<integration ID>` with the Integration ID you copied earlier from the SignalFx UI. (except realm US0, the url should be `https://api.signalfx.com/v1/saml/metadata`).

    b. In **Reply URL**, enter the following URL `https://api.<realm>.signalfx.com/v1/saml/acs/<integration ID>` and replace `<realm>` with your SignalFx realm, and `<integration ID>` with the **Integration ID** you copied earlier from the SignalFx UI. (except US0, the url should be `https://api.signalfx.com/v1/saml/acs/<integration ID>`)
5. SignalFx application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.
6. Review and verify that the following claims map to the source attributes that are populated in the Active Directory.

    | Name | Source Attribute |
    | --- | --- |
    | User.FirstName | user.givenname |
    | User.email | user.mail |
    | PersonImmutableID | user.userprincipalname |
    | User.LastName | user.surname |

    Note

    This process requires that your Active Directory is configured with at least one verified custom domain, and has access to the email accounts in this domain. If you're unsure or need assistance with this configuration, please contact SignalFx support.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)**, and then select **Download**. Download the certificate, and save it on your computer. Then, copy the **App Federation Metadata Url** value; you need this information in a later step in the SignalFx UI.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up SignalFx** section, copy the **Microsoft Entra Identifier** value. you need this information in a later step in the SignalFx UI.

## Step 4: Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

## Step 5: Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to SignalFx.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SignalFx**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Step 6: Complete the SignalFx SSO configuration

1. Open the previous tab, and return to the SignalFx UI to view the current Microsoft Entra integration page.
2. Next to **Certificate (Base64)**, select **Upload File**, and then locate the **Base64 encoded certificate** file that you previously downloaded previously.
3. Next to **Microsoft Entra Identifier**, paste the **Microsoft Entra Identifier** value that you copied earlier.
4. Next to **Federation Metadata URL**, paste the **App Federation Metadata Url** value that you copied earlier.
5. Select **Save**.

## Step 7: Test SSO

Review the following information regarding how to test SSO, and expectations for logging into SignalFx for the first time.

### Test logins

- To test the login, you should use a private / incognito window, or you can log out. If not, cookies for the user who configured the application will interfere and prevent a successful login with the test user.
- When a new test user logs in for the first time, Azure will force a password change. When this occurs, the SSO login process isn't completed; the test user is directed to the Azure portal. To troubleshoot, the test user should change their password, and navigate to the SignalFx login page or to the MyApps and try again.

    - When you select the SignalFx tile in the MyApps, you should be automatically logged into the SignalFx.
        - For more information about the MyApps, see [Introduction to the MyApps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
- SignalFx application can be accessed from the MyApps or via a custom login page assigned to the organization. The test user should test the integration starting from either of these locations.

    - The test user can use the credentials created earlier in this process for **b.simon@contoso.com**.

### First-time logins

- When a user logs into SignalFx from the SAML SSO for the first time, the user will receive a SignalFx email with a link. The user must select the link for authentication purposes. This email validation will only take place for first-time users.
- SignalFx supports **Just In Time** user creation, which means that if a user doesn't exist in SignalFx, then the user's account is created upon first login attempt.