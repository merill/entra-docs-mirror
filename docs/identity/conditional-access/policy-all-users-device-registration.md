---
layout: Conceptual
title: Require MFA for device registration - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-device-registration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Improve visibility and enforce more granular control over the device registration process though Conditional Access.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
ms.custom: sfi-image-nochange
locale: en-us
document_id: 09a405bc-36dc-e120-1111-debc688a8987
document_version_independent_id: 09a405bc-36dc-e120-1111-debc688a8987
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-device-registration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-device-registration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-device-registration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4fc93743-a01f-b65f-2a07-eab4a10ed91f
---

# Require MFA for device registration - Microsoft Entra ID | Microsoft Learn

## Overview

Use the [Conditional Access user action](concept-conditional-access-cloud-apps#user-actions) to enforce policy when users register or join devices to Microsoft Entra ID. This control provides granularity in configuring multifactor authentication for registering or joining devices instead of a tenant-wide policy that currently exists. Administrators can customize this policy to fit the security needs of their organization.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Create a Conditional Access policy

Warning

If you use [external authentication methods](/en-us/entra/identity/authentication/how-to-authentication-external-method-manage), these methods are currently incompatible with authentication strength and you should use the **[Require multifactor authentication](concept-conditional-access-grant#require-multifactor-authentication)** grant control.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **User actions**, select **Register or join devices**.
7. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the built-in **Multifactor authentication** authentication strength from the list.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Warning

When a Conditional Access policy is configured with the **Register or join devices** user action, you must set **Entra ID** &gt; **Devices** &gt; **Overview** &gt; **Device Settings** - `Require Multifactor Authentication to register or join devices with Microsoft Entra` to **No**. Otherwise, Conditional Access policies with this user action aren't properly enforced. More information about this device setting can found in [Configure device settings](../devices/manage-device-identities#configure-device-settings).

[![Screenshot of the Require Multifactor Authentication to register or join devices with Microsoft Entra control to be disabled.](media/policy-all-users-device-registration/device-settings-require-mfa-to-register-or-join.png)](media/policy-all-users-device-registration/device-settings-require-mfa-to-register-or-join.png#lightbox)