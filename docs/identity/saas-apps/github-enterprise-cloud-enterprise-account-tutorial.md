---
layout: Conceptual
title: Configure GitHub Enterprise Cloud - Enterprise Account for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/github-enterprise-cloud-enterprise-account-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and GitHub Enterprise Cloud - Enterprise Account.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 38ddf301-6502-8b20-243e-7af24023e3cd
document_version_independent_id: ae6a3790-e090-de5d-4e13-7b4d3f8c35b9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/github-enterprise-cloud-enterprise-account-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/github-enterprise-cloud-enterprise-account-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/github-enterprise-cloud-enterprise-account-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d5e23f8f-d5f8-cb1d-222b-fcda5d82be11
---

# Configure GitHub Enterprise Cloud - Enterprise Account for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to set up a Microsoft Entra SAML integration with a GitHub Enterprise Cloud - Enterprise Account. When you integrate GitHub Enterprise Cloud - Enterprise Account with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to a GitHub Enterprise Account and any organizations within the Enterprise Account.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A [GitHub Enterprise Account](https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-enterprise-accounts).
- A GitHub user account that's an Enterprise Account owner.

## Scenario description

In this article, you configure a SAML integration for a GitHub Enterprise Account, and test enterprise account owner and enterprise/organization member authentication and access.

Note

The GitHub `Enterprise Cloud - Enterprise Account` application doesn't support enabling [automatic SCIM provisioning](../../architecture/sync-scim). If you need to set up provisioning for your GitHub Enterprise Cloud environment, SAML must be configured at the organization level and the `GitHub Enterprise Cloud - Organization` Microsoft Entra application must be used instead. If you're setting up a SAML and SCIM provisioning integration for an enterprise that's enabled for [Enterprise Managed Users (EMUs)](https://docs.github.com/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users), then you must use the `GitHub Enterprise Managed User` Microsoft Entra application for SAML/Provisioning integrations or the `GitHub Enterprise Managed User (OIDC)` Microsoft Entra application for OIDC/Provisioning integrations.

- GitHub Enterprise Cloud - Enterprise Account supports **SP** and **IDP** initiated SSO.

Note

The GitHub `Enterprise Cloud - Enterprise Account` application currently doesn't support any of the government cloud platforms.

## Adding GitHub Enterprise Cloud - Enterprise Account from the gallery

To configure the integration of GitHub Enterprise Cloud - Enterprise Account into Microsoft Entra ID, you need to add GitHub Enterprise Cloud - Enterprise Account from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **GitHub Enterprise Cloud - Enterprise Account** in the search box.
4. Select **GitHub Enterprise Cloud - Enterprise Account** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for GitHub Enterprise Cloud - Enterprise Account

Configure and test Microsoft Entra SSO with GitHub Enterprise Cloud - Enterprise Account using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in GitHub Enterprise Cloud - Enterprise Account.

To configure and test Microsoft Entra SSO with GitHub Enterprise Cloud - Enterprise Account, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign your Microsoft Entra user and the test user account to the GitHub app** - to enable your user account and test user `B.Simon` to use Microsoft Entra single sign-on.
2. **Enable and Test SAML for the Enterprise Account and its organizations**- to configure the single sign-on settings on application side.
    1. **Test SSO with another enterprise account owner or organization member account** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **GitHub Enterprise Cloud - Enterprise Account** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://github.com/enterprises/<ENTERPRISE-SLUG>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://github.com/enterprises/<ENTERPRISE-SLUG>/saml/consume`
6. Perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** text box, type a URL using the following pattern: `https://github.com/enterprises/<ENTERPRISE-SLUG>/sso`

    Note

    Replace `<ENTERPRISE-SLUG>` with the actual name of your GitHub Enterprise Account.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up GitHub Enterprise Cloud - Enterprise Account** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create a Microsoft Entra test user

In this section, you create a test user in the Azure portal called `B.Simon`.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign your Microsoft Entra user and the test user account to the GitHub app

In this section, you enable `B.Simon` and your user account to use Azure single sign-on by granting access to GitHub Enterprise Cloud - Enterprise Account.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **GitHub Enterprise Cloud - Enterprise Account**.
3. In the app's overview page, find the **Manage** section and select **Users and groups**.
4. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
5. In the **Users and groups** dialog, select **B.Simon** and your user account from the Users list, then select the **Select** button at the bottom of the screen.
6. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
7. In the **Add Assignment** dialog, select the **Assign** button.

## Enable and Test SAML for the Enterprise Account and its organizations

To configure single sign-on on the **GitHub Enterprise Cloud - Enterprise Account** side, follow the steps listed in [this GitHub documentation](https://docs.github.com/en/enterprise-cloud@latest/admin/policies/enforcing-policies-for-your-enterprise/enforcing-policies-for-security-settings-in-your-enterprise#enabling-saml-single-sign-on-for-organizations-in-your-enterprise-account).

1. Sign in to GitHub.com with a user account that's an [enterprise account owner](https://docs.github.com/en/enterprise-cloud@latest/admin/user-management/managing-users-in-your-enterprise/roles-in-an-enterprise#enterprise-owner).
2. Copy the value from the `Login URL` field in the app and paste it in the `Sign on URL` field in the GitHub Enterprise Account SAML settings.
3. Copy the value from the `Microsoft Entra Identifier` field in the app and paste it in the `Issuer` field in the GitHub Enterprise Account SAML settings.
4. Copy the contents of the **Certificate (Base64)** file you downloaded in the steps above from Azure portal and paste them in the appropriate field in the GitHub Enterprise Account SAML settings.
5. Select the `Test SAML configuration` and confirm that you're able to authenticate from the GitHub Enterprise Account to Microsoft Entra ID successfully.
6. Once the test is successful, save the settings.
7. After authenticating via SAML for the first time from the GitHub enterprise account, a *linked external identity* is created in the GitHub enterprise account that associates the signed in GitHub user account with the Microsoft Entra user account.

After you enable SAML SSO for your GitHub Enterprise Account, SAML SSO is enabled by default for all organizations owned by your Enterprise Account. All members are required to authenticate using SAML SSO to gain access to the organizations where they are a member, and enterprise owners are required to authenticate using SAML SSO when accessing an Enterprise Account.

## Test SSO with another enterprise account owner or organization member account

After the SAML integration is set up for the GitHub enterprise account (which also applies to the GitHub organizations in the enterprise account), other enterprise account owners who are assigned to the app in Microsoft Entra ID should be able to navigate to the GitHub enterprise account URL (`https://github.com/enterprises/<enterprise account>`), authenticate via SAML, and access the policies and settings under the GitHub enterprise account.

An organization owner for an organization in an enterprise account should be able to [invite a user to join their GitHub organization](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-organizations-and-teams/inviting-users-to-join-your-organization). Sign in to GitHub.com with an organization owner account and follow the steps in the article to invite `B.Simon` to the organization. A GitHub user account will need to be created for `B.Simon` if one doesn't already exist.

To test GitHub organization access under the Enterprise Account with the `B.Simon` test user account:

1. Invite `B.Simon` to an organization under the Enterprise Account as an organization owner.
2. Sign in to GitHub.com using the user account you would like to link to the `B.Simon` Microsoft Entra user account.
3. Sign in to Microsoft Entra ID using the `B.Simon` user account.
4. Go to the GitHub organization. The user should be prompted to authenticate via SAML. After successful SAML authentication, `B.Simon` should be able to access organization resources.