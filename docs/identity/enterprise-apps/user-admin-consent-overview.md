---
layout: Conceptual
title: Overview of user and admin consent - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/user-admin-consent-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn about the fundamental concepts of user and admin consent in Microsoft Entra ID.
ms.topic: overview
ms.date: 2025-03-18T00:00:00.0000000Z
ms.reviewer: phsignor
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps
locale: en-us
document_id: f2c3c5b1-355f-3a30-a1b1-9826ae9727dd
document_version_independent_id: 9e19b96d-dc6e-7ffd-1eac-20494273d7a5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/user-admin-consent-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/user-admin-consent-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/user-admin-consent-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 827de13d-8287-c1bf-a53a-5be4a13a185a
---

# Overview of user and admin consent - Microsoft Entra ID | Microsoft Learn

Consent is a process where users can grant permission for an application to access a protected resource. To indicate the level of access required, an application requests the API permissions it requires. For example, an application can request the permission to see a signed-in user's profile and read the contents of the user's mailbox.

Consent can be initiated in various ways. For example, users can be prompted for consent when they attempt to sign in to an application for the first time. Depending on the permissions they require, some applications might require an administrator to be the one who grants consent.

In this article, you learn the foundational concepts and scenarios around user and admin consent in Microsoft Entra ID.

## User consent

A user can authorize an application to access some data at the protected resource, while acting as that user. The permissions that allow this type of access are called "delegated permissions."

User consent is initiated when a user signs in to an application. After the user provides sign-in credentials, they're checked to determine whether consent is already granted. If no previous record of user or admin consent for the required permissions exists, the user is directed to the consent prompt window to grant the application the requested permissions.

User consent by nonadministrators is possible only in organizations where user consent is allowed for the application and for the set of permissions the application requires. If user consent is disabled, or users aren't allowed to consent for the requested permissions, they aren't prompted for consent. If users are allowed to consent and they accept the requested permissions, the consent is recorded. The users usually don't have to consent again on future sign-ins to the same application.

### User consent settings

Users are in control of their data. A Privileged Administrator can configure whether nonadministrator users are allowed to grant user consent to an application. This setting can take into account aspects of the application and the application's publisher, and the permissions being requested. For step by step instructions on how to configure user consent, see [Configure user consent settings](configure-user-consent).

As an administrator, you can choose whether user consent is allowed. If you choose to allow user consent, you can also choose what conditions must be met before a user can consent to an application.

By choosing which application consent policies apply for all users, you can set limits on when users are allowed to grant consent to applications. The consent policies also inform when users are required to request administrator review and approval. The Microsoft Entra admin center provides the following built-in options:

- *You can disable user consent*. Users can't grant permissions to applications. Users continue to sign in to applications they already consented to or to applications that administrators grant consent to on their behalf. However, they're not allowed to consent to new permissions to applications on their own. Only users who are granted a directory role that includes the permission to grant consent can consent to new applications.
- *Users can consent to applications from verified publishers or your organization, but only for permissions you select*. All users can consent only to applications published by a [verified publisher](../../identity-platform/publisher-verification-overview) and applications that are registered in your tenant. Users can consent only to the permissions classified as *low impact*. You must [classify permissions](configure-permission-classifications) to select which permissions users are allowed to consent to.
- *Users can consent to all applications*. This option allows all users to consent to any permissions that don't require admin consent, for any application.

For most organizations, one of the built-in options is appropriate. Some advanced customers might want more control over the conditions that govern when users are allowed to consent. These customers can [create custom app consent policy](manage-app-consent-policies#create-a-custom-app-consent-policy-using-powershell) and configure those policies to apply to user consent.

## Admin consent

During admin consent, a Privileged Administrator might grant an application access on behalf of other users (usually, on behalf of the entire organization). Also during admin consent, applications or services provide direct access to an API, which is used by the application if there's no signed-in user. The specific role needed to grant admin consent differs based on the permissions requested, which are outlined in the [grant admin consent](grant-admin-consent#prerequisites) article.

When your organization purchases a license or subscription for a new application, you might proactively want to set up the application so that all users in the organization can use it. To avoid the need for user consent, an administrator can grant consent for the application on behalf of all users in the organization.

After an administrator grants admin consent on behalf of the organization, users aren't prompted for consent for that application. In certain cases, a user might be prompted for consent even after an administrator grants consent. An example might be if an application requests another permission that the administrator hasn't granted.

Granting admin consent on behalf of an organization is a sensitive operation, potentially allowing the application's publisher access to significant portions of the organization's data, or the permission to do highly privileged operations. Examples of such operations might be role management, full access to all mailboxes or all sites, and full user impersonation.

Before you grant tenant-wide admin consent, ensure that you trust the application and the application publisher, for the level of access you're granting. If you aren't confident that you understand who controls the application and why the application is requesting the permissions, don't grant consent.

For guidance on evaluating admin consent requests, see [Evaluating a request for tenant-wide admin consent](manage-consent-requests#evaluate-a-request-for-tenant-wide-admin-consent).

For step-by-step instructions for granting tenant-wide admin consent from the Microsoft Entra admin center, see [Grant tenant-wide admin consent to an application](grant-admin-consent).

### Grant consent on behalf of a specific user

Instead of granting consent for an entire organization, an admin can also use the [Microsoft Graph API](/en-us/graph/use-the-api) to grant consent to delegated permissions on behalf of a single user. For a detailed example that uses Microsoft Graph PowerShell, see [Grant consent on behalf of a single user by using PowerShell](grant-consent-single-user).

### Limit user access to an application

User access to applications can still be limited, even when tenant-wide admin consent is already granted. Configure the application’s properties to require user assignment to limit user access to the application. For more information, see [Methods for assigning users and groups](assign-user-or-group-access-portal).

For a broader overview, including how to handle other complex scenarios, see [Use Microsoft Entra ID for application access management](what-is-access-management).

## Admin consent workflow

The admin consent workflow gives users a way to request admin consent for applications when they aren't allowed to consent themselves. When the admin consent workflow is enabled, users are presented with an "Approval required" window for requesting admin approval for access to the application.

After users submit the admin consent request, the admins who are designated as reviewers receive a notification. The users are notified after a reviewer acts on their request. For step-by-step instructions for configuring the admin consent workflow by using the Microsoft Entra admin center, see [configure the admin consent workflow](configure-admin-consent-workflow).

### How users request admin consent

After the admin consent workflow is enabled, users can request admin approval for an application that they're unauthorized to consent to. Here are the steps in the process:

- A user attempts to sign in to the application.
- An **Approval required** message appears. The user types a justification for needing access to the application and then selects "Request approval."
- A **Request sent** message confirms that the request was submitted to the admin. If the user sends several requests, only the first request is submitted to the admin.
- The user receives an email notification when the request is approved, denied, or blocked.