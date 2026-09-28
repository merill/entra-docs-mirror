---
layout: Conceptual
title: Conditional Access - Require approved app or app protection policy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-approved-app-or-app-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy require approved app or app protection policy
ms.reviewer: lhuangnorth
ms.date: 2026-03-24T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: 14348ba7-48f0-1862-ebec-0fc3640e587d
document_version_independent_id: 8188cee4-3f28-6014-f3be-1ee9e9b183b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-approved-app-or-app-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-approved-app-or-app-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-approved-app-or-app-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: f4fca17e-01ba-443d-281b-98fee471ab7d
---

# Conditional Access - Require approved app or app protection policy - Microsoft Entra ID | Microsoft Learn

## Overview

People regularly use their mobile devices for both personal and work tasks. While making sure staff can be productive, organizations also want to prevent data loss from applications on devices they may not manage fully.

With Conditional Access, organizations can restrict access to [approved (modern authentication capable) client apps with Intune app protection policies](concept-conditional-access-grant#require-app-protection-policy). For older client apps that may not support app protection policies, administrators can restrict access to [approved client apps](concept-conditional-access-grant#require-approved-client-app).

Warning

App protection policies are supported on iOS and Android where applications meet specific requirements. **App protection policies are supported on Windows in preview for the Microsoft Edge browser only.** Not all applications that are supported as approved applications or support application protection policies. For a list of some common client apps, see [App protection policy requirement](concept-conditional-access-grant#require-app-protection-policy). If your application is not listed there, contact the application developer. To require approved client apps or to enforce app protection policies for iOS and Android devices, these devices must first register in Microsoft Entra ID.

Note

**Require one of the selected controls** under grant controls is like an **OR** clause. This is used within policy to enable users to utilize apps that support either the **Require app protection policy** or **Require approved client app** grant controls. **Require app protection policy** is enforced when the app supports that grant control.

For more information about the benefits of using app protection policies, see the article [App protection policies overview](/en-us/mem/intune/apps/app-protection-policy).

The following policies are put in to [Report-only mode](howto-conditional-access-insights-reporting) to start so administrators can determine the impact they'll have on existing users. When administrators are comfortable that the policies apply as they intend, they can switch to **On** or stage the deployment by adding specific groups and excluding others.

## Require approved client apps or app protection policy with mobile devices.

The following steps help create a Conditional Access policy requiring an approved client app **or** an app protection policy when using an iOS/iPadOS or Android device. This policy prevents the use of Exchange ActiveSync clients using basic authentication on mobile devices. This policy works in tandem with an [app protection policy created in Microsoft Intune](/en-us/mem/intune/apps/app-protection-policies).

Organizations can choose to deploy this policy using the following steps or using the [Conditional Access templates](concept-conditional-access-policy-common).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and exclude at least one account to prevent yourself from being locked out. If you don't exclude any accounts, you can't create the policy.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Device platforms**, set **Configure** to **Yes**.
    1. Under **Include**, **Select device platforms**.
    2. Choose **Android** and **iOS**.
    3. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require approved client app** and **Require app protection policy**
    2. **For multiple controls** select **Require one of the selected controls**
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

Note

When a policy is created in report-only mode for "Require app protection policy" control, your sign-in log may show the result as "Report-only: Failure" in "Conditional Access" tab when all configured policy conditions were satisfied. This is because the control was not satisified in report-only mode. Once you enabled the policy, the control is applied to the app and the sign-in will not be blocked.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Tip

Organizations should also deploy a policy that [blocks access from unsupported or unknown device platforms](policy-all-users-device-unknown-unsupported) along with this policy.

## Block Exchange ActiveSync on all devices

This policy blocks all Exchange ActiveSync clients using basic authentication from connecting to Exchange Online.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and exclude at least one account to prevent yourself from being locked out. If you don't exclude any accounts, you can't create the policy.
    3. Select **Done**.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **Select resources**.
    1. Select **Office 365 Exchange Online**.
    2. Select **Select**.
7. Under **Conditions** &gt; **Client apps**, set **Configure** to **Yes**.
    1. Uncheck all options except **Exchange ActiveSync clients**.
    2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require app protection policy**
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).