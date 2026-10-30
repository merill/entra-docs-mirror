---
layout: Conceptual
title: Restrict device code flow for Microsoft Teams devices with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-teams-devices-device-code-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Use Conditional Access to block device code flow by default and grant persistent, account-based exceptions for Microsoft Teams device resource accounts.
ms.topic: how-to
ms.date: 2026-05-27T00:00:00.0000000Z
ms.reviewer: swethar
ai-usage: ai-assisted
locale: en-us
document_id: 44155d68-f228-b7b8-5a42-acb49c7f2ec3
document_version_independent_id: 44155d68-f228-b7b8-5a42-acb49c7f2ec3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-teams-devices-device-code-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-teams-devices-device-code-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-teams-devices-device-code-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: aed26b11-37c0-bf6b-da50-cdd4165be731
---

# Restrict device code flow for Microsoft Teams devices with Conditional Access - Microsoft Entra ID | Microsoft Learn

Device code flow lets users sign in to devices that don't have a browser or rich input experience. Some Microsoft Teams devices use device code flow during first-time registration, reprovisioning, and some reauthentication scenarios.

Device code flow is also a high-risk authentication flow. An attacker can start the flow, send a user a code, and ask the user to enter that code on a legitimate Microsoft sign-in page. Because the sign-in page is real, this attack can be harder for users to recognize.

Microsoft recommends blocking device code flow wherever possible. If your organization uses Teams devices that require device code flow, scope the exception to specific Teams device resource accounts and exclude the Device Registration Service resource from your Conditional Access policy.

## Who should use this guidance

Use this article if your organization:

- Uses Teams Rooms, Teams Android devices, shared Teams devices, or other Teams device experiences that require device code flow.
- Wants to restrict device code flow with Conditional Access.
- Needs to keep Teams device registration working while reducing tenant-wide device code flow exposure.

This article focuses on Teams device scenarios. If your organization uses device code flow for other tools, such as Azure CLI or developer command-line tools, review the additional guidance in this article before you enforce a blocking policy.

## Before you begin

You need:

- A role that can manage Conditional Access, such as [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) or [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
- A Microsoft Entra ID P1 or higher license for the users in scope. For more information, see [Conditional Access license requirements](overview#license-requirements).
- A list of Teams device resource accounts, such as room or shared-device accounts.
- Access to [Microsoft Entra sign-in logs](../monitoring-health/concept-sign-ins).
- Emergency access accounts that are excluded from Conditional Access policies. For more information, see [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).

Note

In this article, a *Teams device resource account* means the account assigned to the room, common area, or shared Teams device. It doesn't mean the technician or administrator account used to perform setup.

Start with report-only mode. Validate expected Teams device behavior before you turn the policy on.

## Recommended approach

This article uses a default-block approach with two layered exceptions:

- A persistent security group containing the Teams device resource accounts that need device code flow.
- An exclusion for the Device Registration Service resource, so device registration through device code flow isn't blocked by your policy.

Roll the policy out in stages:

1. Inventory device code flow usage in sign-in logs.
2. Create exception groups:

    - A persistent Teams device exception group containing the resource accounts assigned to your Teams devices.
    - A persistent approved non-Teams group, if you have approved non-Teams device code flow scenarios.
3. Create a Conditional Access policy that blocks device code flow, excludes those groups, and excludes the Device Registration Service resource.
4. Pilot the policy with selected accounts and Teams devices in report-only mode.
5. Review report-only results and sign-in logs.
6. Turn the policy on.
7. Add new Teams device resource accounts to the exception group as devices are deployed.
8. Monitor blocked sign-ins and exception group membership.

Teams devices need device code flow both for initial sign-in and for reauthentication scenarios such as password changes or Conditional Access policy changes. The exception for Teams device resource accounts is persistent, not time-boxed. Teams resource accounts that use passwordless authentication are an exception to the reauthentication requirement: they need device code flow only at initial provisioning. Keep these accounts in the persistent exception group so that reprovisioning and recovery scenarios aren't blocked.

An exception is account-scoped. There's no way to scope the exception to just one resource or scenario. During the exception, an excluded account can use device code flow for any app or resource in scope of the policy. Keep exception membership limited to genuine Teams device resource accounts, monitored, and owner-approved.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Create the Conditional Access policy

Create one policy that blocks device code flow by default.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select the users you want in scope for the policy (**All users** recommended).
    2. Under **Exclude**:
        - Select **Users and groups** and choose your organization's emergency access or break-glass accounts and your approved device code flow exception groups. Audit this exclusion list regularly.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**:
    1. Under **Include**, select **All resources (formerly 'All cloud apps')** unless your organization validated a narrower resource scope for the scenario.
    2. Under **Exclude**, select **Select resources** then select **Select specific resources** and add **Device Registration Service**. This exclusion is required so device registration through device code flow isn't blocked by your policy. For more information, see [Enforcement of Authentication Flows policies on Device Registration Service resource](concept-authentication-flows#enforcement-of-authentication-flows-policies-on-device-registration-service-resource).
7. Under **Conditions** &gt; **Authentication Flows**, set **Configure** to **Yes**.
    1. Select **Device code flow**.
    2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Block access**.
    - Select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## Manage Teams device resource account exceptions

Add Teams device resource accounts to the persistent exception group as devices are deployed. Remove an account only when the device is retired or the resource account is no longer used.

1. Identify the Teams device resource account assigned to the device.
2. Add the resource account to the persistent Teams device exception group.
3. Record the owner, the device, and a change or ticket ID for auditing.
4. Register or reprovision the Teams device with device code flow.
5. Confirm the device completes provisioning and signs in as expected.

To retire a Teams device:

1. Remove the resource account from the exception group.
2. Disable or delete the resource account.
3. Document the retirement.

## Validate before enforcement

Before you turn the policy on, use report-only results and sign-in logs to confirm:

- Expected Teams device registration succeeds.
- Registration isn't blocked by the device code flow policy when the resource account exception is in place.
- Device Registration Service is excluded from the policy.
- Teams devices continue to sign in after registration, including reauthentication scenarios such as password changes or Conditional Access policy changes.
- Approved non-Teams device code flow scenarios are represented by explicit exception groups.
- Unknown or unjustified device code flow usage is blocked.
- Emergency access accounts remain excluded.

Use **Authentication protocol = Device code flow** when you inventory active device code flow usage before rollout. Use **Original transfer method = Device code flow** when you need to understand whether a later sign-in or token refresh is still tied to an earlier device code flow session.

| Scenario | Field to use | Why |
| --- | --- | --- |
| Inventory current device code flow usage before rollout | **Authentication protocol = Device code flow** | Finds sign-ins where device code flow was used for that event. |
| Review report-only impact | Both fields | Shows direct device code flow usage and later sessions that would still be evaluated as device-code-derived. |
| Audit ongoing device code flow use by Teams device resource accounts | **Authentication protocol = Device code flow** | Expected to show device code flow for initial sign-in and reauthentication events for accounts in the exception group. |
| Troubleshoot an unexpected block on a Teams device | **Original transfer method = Device code flow** | The current sign-in event might not show device code flow as the authentication protocol, but Conditional Access can still evaluate the session as device-code-derived. |
| Audit approved non-Teams exceptions | Both fields | Shows new device code flow usage and ongoing activity from device-code-derived sessions. |

A session that started with device code flow can remain protocol-tracked on later token refreshes, even when the current sign-in event doesn't show device code flow as the authentication protocol. For more information, see [Protocol tracking](concept-authentication-flows#protocol-tracking).

## Troubleshooting

### A Teams device is unexpectedly blocked

A Teams device shouldn't be blocked by the Conditional Access policy if the resource account is in the exception group and Device Registration Service is excluded from the policy.

If a Teams device is unexpectedly blocked:

1. Confirm the resource account is in the persistent exception group.
2. Confirm Device Registration Service is excluded from **Target resources** in the policy.
3. Review the sign-in logs. If **Original transfer method** shows device code flow, the session might be protocol-tracked from an earlier authentication, even if the current **Authentication protocol** value isn't device code flow.

If the device is still blocked after these checks, open a support ticket to investigate.

### Personal Teams devices need device code flow

Personal Teams device scenarios are harder to scope because the user account might also be able to use device code flow for non-Teams scenarios. Avoid broad user exclusions. If a user-based exception is required, document the risk, monitor usage, and review the exception regularly.

## If you use device code flow outside Teams devices

Some organizations use device code flow for other scenarios, such as Azure CLI, developer tools, admin tools, or legacy command-line experiences. Account for these scenarios as part of your configured policies to avoid impact.

Before you enforce a tenant-wide device code flow block:

1. Review sign-in logs filtered by **Authentication protocol = Device code flow** and sign-ins where **Original transfer method = Device code flow**.
2. Identify the user, app or resource, location, device context, and business owner for each dependency.
3. Move scenarios to safer authentication methods where possible. Prefer browser-based or brokered sign-in for users. For automation, prefer managed identities or workload identity federation.
4. Create exception groups only for approved device code flow dependencies.
5. Treat any remaining non-Teams exception as a documented risk acceptance with an owner and review cadence.

Don't add broad user populations to exception groups. A broad user exception can allow device code flow beyond the intended tool or scenario.

## Maintain the policy after enforcement

After the policy is enforced, continue to monitor device code flow usage and keep exceptions current.

| Do | Don't |
| --- | --- |
| Review exception membership regularly. | Treat persistent device code flow exceptions as permanent defaults without ongoing review. |
| Monitor sign-ins where **Original transfer method** is device code flow. | Rely only on **Authentication protocol** when investigating protocol-tracked sessions. |
| Move non-Teams dependencies away from device code flow when safer authentication methods are available. | Add non-Teams accounts to the Teams device exception group. |
| Alert on unexpected device code flow use by privileged users, emergency access accounts, unfamiliar apps, or unexpected locations. | Assume approved exceptions remain safe without recurring review. |