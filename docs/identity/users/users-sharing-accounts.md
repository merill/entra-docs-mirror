---
layout: Conceptual
title: Sharing accounts and credentials - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-sharing-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to configure shared accounts in Microsoft Entra ID using password-based single sign-on so multiple users can securely access apps without sharing passwords directly.
ms.topic: how-to
ms.date: 2026-03-18T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: d58eacc8-9b10-77c5-e3e6-5b12693c1510
document_version_independent_id: 6ff4f006-cfd9-8890-57c8-9a99f6b819ff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-sharing-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-sharing-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-sharing-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bd00a6a3-80fc-aa02-9e4b-e4667b1d89f6
---

# Sharing accounts and credentials - Microsoft Entra ID | Microsoft Learn

## Overview

In Microsoft Entra ID, part of Microsoft Entra, sometimes organizations need to use a single username and password for multiple people, which often happens in the following cases:

- When accessing applications that require a unique sign in and password for each user, whether on-premises apps or consumer cloud services (for example, corporate social media accounts).
- When creating multi-user environments. You might have a single, local account that has elevated privileges and is used to do core setup, administration, and recovery activities. For example, an Application Administrator account for Microsoft 365 or the root account in Salesforce.

Traditionally, these accounts are shared by distributing the credentials (username and password) to the right individuals, or storing them in a shared location where multiple trusted agents can access them.

The traditional sharing model has several drawbacks:

- Enabling access to new applications requires you to distribute credentials to everyone that needs access.
- Each shared application might require its own unique set of shared credentials, requiring users to remember multiple sets of credentials. When users have to remember many credentials, the risk increases that they resort to risky practices (for example, writing down passwords).
- You can't tell who has access to an application.
- You can't tell who *accessed* an application.
- When you want to remove access to an application, you have to update the credentials and redistribute them to everyone that needs access to that application.

## Prerequisites

To configure shared accounts, you need the following resources and roles:

- An Enterprise Mobility Suite (EMS) or Microsoft Entra ID P1 or P2 license plan for each user who accesses shared accounts. For more information, see [Microsoft Entra plans and pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).
- A user account with at least the [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) role to configure SSO and assign users. The [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) role also works.
- At least the [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator) role to create security groups. If your tenant allows users to create security groups, this role isn't required.
- An application that supports password-based single sign-on (SSO).

## Microsoft Entra account sharing

Microsoft Entra ID provides a new approach to using shared accounts that eliminates these drawbacks.

The Microsoft Entra administrator configures which applications a user can access by using the Access Panel and choosing the type of single sign-on best suited for that application. One of those types, *password-based single sign-on*, lets Microsoft Entra ID act as a kind of "broker" during the sign-in process for that app.

Users sign in once with their organizational account. This account is the same one they regularly use to access their desktop or email. They can discover and access only those applications that they're assigned to. With shared accounts, this list of applications can include any number of shared credentials. The end-user doesn't need to remember or write down the various accounts they might be using.

Shared accounts increase oversight, improve usability, and enhance your security. Users with permissions to use the credentials don't see the shared password, but rather get permissions to use the password as part of an orchestrated authentication flow. Further, some password SSO applications give you the option of using Microsoft Entra ID to periodically rollover (update) passwords. The system uses large, complex passwords, which increase account security. The administrator can easily grant or revoke access to an application, knows who has access to the account, and who accessed it in the past.

Microsoft Entra ID supports shared accounts for any Enterprise Mobility Suite (EMS) or Microsoft Entra ID P1 or P2 license plan, across all types of password single sign-on applications. You can share accounts for any of thousands of preintegrated applications in the application gallery and can add your own password-authenticating application with [custom SSO apps](../enterprise-apps/what-is-single-sign-on).

Microsoft Entra features that enable account sharing include:

- [Password single sign-on](../enterprise-apps/plan-sso-deployment#single-sign-on-options)
- Password single sign-on agent
- [Group assignment](groups-self-service-management)
- Custom Password apps
- [Usage and insights reports](../monitoring-health/concept-usage-insights-report)
- End-user access portals
- [App proxy](/en-us/entra/identity/app-proxy)
- [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps)

## Configure a shared account

To set up a shared account using password-based SSO, complete the following steps.

### Step 1: Add the application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select **New application**.
4. Search the gallery for the application you want to add, or select **Create your own application** if the app isn't listed. For more information, see [Add an enterprise application](../enterprise-apps/add-application-portal).

### Step 2: Configure password-based SSO

1. Select the application you added, then select **Single sign-on** in the left menu.
2. Select **Password-based** as the single sign-on mode.
3. Enter the URL for the sign-in page of the application.
4. Select **Save**.

Microsoft Entra ID parses the HTML of the sign-in page for username and password input fields. If the automatic parsing fails, you can manually configure the sign-in fields. For detailed instructions, see [Add password-based single sign-on to an application](../enterprise-apps/configure-password-single-sign-on-non-gallery-applications).

### Step 3: Create a security group

Create a security group for each set of users who share the same application credentials. Creating groups requires at least the [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator) role, unless your tenant allows users to create security groups.

1. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
2. Select **New group**.
3. Set **Group type** to **Security**.
4. Provide a name that identifies the shared account and application (for example, "Marketing - Social Media Account").
5. Add the users who need access to the shared account as members.
6. Select **Create**.

For more information, see [Use a group to manage access to SaaS applications](groups-saasapps).

### Step 4: Assign the group and set shared credentials

1. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications** and select the application.
2. Select **Users and groups**, then select **Add user/group**.
3. Select the security group you created and complete the assignment.
4. Select **Users and groups** again, select the checkbox for the group's row, and then select **Update Credentials**.
5. Enter the shared username and password for the application. Microsoft Entra ID securely stores the credentials and provides them to group members during sign-in.

Tip

After the application is deployed, individuals don't need the password of the shared account. Consider setting a long, complex password. Microsoft Entra ID stores the password and the users don't see it.

### Step 5: Configure password rotation (optional)

If the application supports it, configure automatic rollover of the password. Automatic password rotation provides another layer of security because not even the administrator who set up the shared account needs to know the password after the initial configuration.

## Access a shared account

After an administrator configures a shared account, end users access the application in the following way:

1. Navigate to the [My Apps portal](https://myapps.microsoft.com) and sign in with your organizational account.
2. Find and select the shared application tile. If you have the My Apps Secure Sign-in Extension installed, the application launches and Microsoft Entra ID automatically submits the shared credentials.

Note

The My Apps browser extension is required for password-based SSO applications. Users are prompted to install the extension when they first launch a password-based SSO app. The extension is available for [Microsoft Edge](https://microsoftedge.microsoft.com/addons/detail/my-apps-secure-signin-ex/gaaceiggkkiffbfdpmfapegoiohkiipl) and [Google Chrome](https://chrome.google.com/webstore/detail/my-apps-secure-sign-in-ex/ggjhpefgjjfobnfoldnjipclpcfbgbhl). For mobile devices, use Microsoft Edge mobile and enable password-based SSO in **Settings** &gt; **Privacy and Security** &gt; **Microsoft Entra Password SSO**.

End users don't see or interact with the shared credentials directly. Microsoft Entra ID handles the credential submission as part of an orchestrated authentication flow.

## Security considerations

When using shared accounts, keep the following security practices in mind:

- **Credential visibility**: Users with permissions to use the shared credentials don't see the actual password. Microsoft Entra ID brokers the authentication on their behalf.
- **Multifactor authentication (MFA)**: You can require MFA for users who access shared accounts to provide another layer of protection. For more information, see [How Microsoft Entra multifactor authentication works](../authentication/concept-mfa-howitworks).
- **Access management**: Use [Microsoft Entra self-service group management](groups-self-service-management) to delegate the ability to manage who has access to the application. Group owners can add or remove members without administrator involvement.
- **Password complexity**: Set a long, complex password for the shared account since end users don't need to know or type the password.
- **Audit and monitoring**: Microsoft Entra ID logs sign-in activity, so administrators can see who accessed the application and when.