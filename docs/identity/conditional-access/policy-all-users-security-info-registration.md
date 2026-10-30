---
layout: Conceptual
title: Control security information registration with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-security-info-registration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy for security info registration.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: d8685f6c-3ff4-47ba-454d-241ff3abc590
document_version_independent_id: 76de1516-981d-1fd3-efc9-de7908621e5b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-security-info-registration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-security-info-registration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-security-info-registration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 56ddead6-36ab-32a2-230f-96b060884656
---

# Control security information registration with Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

Securing when and how users register for Microsoft Entra multifactor authentication and self-service password reset is possible with user actions in a Conditional Access policy. This feature is available to organizations who enable [combined registration](../authentication/concept-registration-mfa-sspr-combined). This functionality allows organizations to treat the registration process like any application in a Conditional Access policy and use the full power of Conditional Access to secure the experience. Users signing in to the Microsoft Authenticator app or enabling passwordless phone sign-in are subject to this policy.

Important

Starting **July 6, 2026**, Conditional Access policies that target **Register security information** will apply during Windows Hello for Business and macOS Platform SSO credential registration. Today, these registration flows don't evaluate registration-targeting Conditional Access policies. However, MFA is still required by default to register passwordless credentials — regardless of whether a Conditional Access policy is configured. After enforcement, users registering Windows Hello for Business or macOS Platform SSO credentials must also satisfy your policy's Grant controls — such as authentication strength, trusted locations, or a specific MFA method — before completing enrollment. Review your policies scoped to **Register security information** and test with report-only mode before enforcement begins.

Some organizations in the past might have used trusted network location or device compliance as a means to secure the registration experience. With the addition of [Temporary Access Pass](../authentication/howto-authentication-temporary-access-pass) in Microsoft Entra ID, administrators can provide time-limited credentials to their users that allow them to register from any device or location. Temporary Access Pass credentials satisfy Conditional Access requirements for multifactor authentication.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Create a policy to secure registration

The following policy applies to the selected users, who attempt to register using the combined registration experience. The policy requires users who are not on a trusted network to do multifactor authentication. Users from trusted networks are excluded from this policy.

Warning

If you use [external authentication methods](/en-us/entra/identity/authentication/how-to-authentication-external-method-manage), these are currently incompatible with authentication strength and you should use the **[Require multifactor authentication](concept-conditional-access-grant#require-multifactor-authentication)** grant control.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. In Name, Enter a Name for this policy. For example, **Combined Security Info Registration with TAP**.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.

        Warning

        Users must be enabled for the [combined registration](../authentication/howto-registration-mfa-sspr-combined).
    2. Under **Exclude**.

        1. Select **All guest and external users**.

            Note

            Temporary Access Pass does not work for guest users.
        2. Select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **User actions**, check **Register security information**.
7. Under **Conditions** &gt; **Locations**.
    1. Set **Configure** to **Yes**.
        1. Include **Any location**.
        2. Exclude **All trusted locations**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the appropriate built-in or custom authentication strength from the list.
    2. Select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Administrators have to issue Temporary Access Pass credentials to new users so they can satisfy the requirements for multifactor authentication to register. Steps to accomplish this task, are found in the section [Create a Temporary Access Pass in the Microsoft Entra admin center](../authentication/howto-authentication-temporary-access-pass#create-a-temporary-access-pass).

Organizations might choose to require other grant controls with or in place of **Require multifactor authentication** at step 8a. When selecting multiple controls, be sure to select the appropriate radio button toggle to require **all** or **one** of the selected controls when making this change.

### Guest user registration

For [guest users](../../external-id/what-is-b2b) who need to register for multifactor authentication in your directory you might choose to block registration from outside of [trusted network locations](concept-conditional-access-conditions#locations) using the following guide.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. In Name, Enter a Name for this policy. For example, **Combined Security Info Registration on Trusted Networks**.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All guest and external users**.
6. Under **Target resources** &gt; **User actions**, check **Register security information**.
7. Under **Conditions** &gt; **Locations**.
    1. Configure **Yes**.
    2. Include **Any location**.
    3. Exclude **All trusted locations**.
8. Under **Access controls** &gt; **Grant**.
    1. Select **Block access**.
    2. Then choose **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.