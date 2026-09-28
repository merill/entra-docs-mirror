---
layout: Conceptual
title: Token Protection Deployment Guide - Apple Platforms - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/deployment-guide-token-protection-apple
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Deploy Token Protection with Microsoft Entra Conditional Access for macOS, iOS, and iPadOS
ms.topic: how-to
ms.date: 2026-08-14T00:00:00.0000000Z
ms.reviewer: sgrandhi
locale: en-us
document_id: b1124793-8e8f-0dc3-639c-e77360803ee9
document_version_independent_id: b1124793-8e8f-0dc3-639c-e77360803ee9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/deployment-guide-token-protection-apple.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/deployment-guide-token-protection-apple
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/deployment-guide-token-protection-apple.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 276e475a-2639-bc75-ebdc-e80ad4d6953d
---

# Token Protection Deployment Guide - Apple Platforms - Microsoft Entra ID | Microsoft Learn

## Overview

This guide covers the steps required to deploy and enforce Token Protection for sign-in session tokens on Apple platforms (iOS, iPadOS, and macOS).

Before using this deployment guide, review [Token Protection in Microsoft Entra Conditional Access](concept-token-protection) for an overview of the feature and supported platforms.

Important

Apple's native Mail and Calendar apps don't support Token Protection. Users will be blocked from accessing resources protected by Token Protection when the policy is enforced. Communicate this behavior to affected users before deployment.

## Prerequisites

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## Supported applications and resources

The following applications and resources are covered by Token Protection on Apple platforms. Review these lists before enforcing the policy.

### Applications

Token Protection can be applied to the following applications.

| Application | iOS/iPadOS | macOS |
| --- | --- | --- |
| Intune Company Portal | ✅ | ✅ |
| Microsoft Authenticator | ✅ |  |
| Microsoft Edge (support for sign-in to Edge profile only) | ✅ | ✅ |
| Microsoft Loop | ✅ |  |
| Microsoft OneNote | ✅ | ✅ |
| Microsoft Scout |  | ✅ |
| Microsoft SharePoint | ✅ |  |
| Microsoft Teams | ✅ | ✅ |
| Microsoft To Do | ✅ | ✅ |
| OneDrive | ✅ | ✅ |
| Outlook | ✅ | ✅ |
| Visual Studio Code |  | ✅ |
| Word, Excel, PowerPoint | ✅ | ✅ |

### Supported Resources

Token Protection on Apple platforms can be used to protect the following resources:

- Exchange Online
- SharePoint Online
- Microsoft Teams

### Known Limitations

- Token Protection currently requires the Microsoft Enterprise single-sign-on (SSO) plug-in, which requires Mobile Device Management (MDM). *Unmanaged iOS and macOS devices aren't supported at this time.*
- *Apple's native Mail and Calendar apps don't support Token Protection.* Users will be blocked from accessing resources protected by Token Protection when the policy is enforced.
- In report-only mode, requests that don't use hardware-backed device registration appear as noncompliant, even if the user is eligible for an upgrade to hardware-backed device registration. Use sign-in logs and status codes to assess true readiness. See the Review readiness with logs and metrics section.
- The **Token Protection – Sign-in Session** column in sign-in logs shows all requests without hardware-backed device identity as "Unbound." These logs include requests from users who are eligible to upgrade their registration.
- [External users](../../external-id/what-is-b2b) who meet the token protection device registration requirements in their home tenant are supported. Users who don't meet these requirements will see an error message with no clear indication of the root cause.

## How to enable Token Protection on Apple platforms

Unlike Windows, Apple platforms don't use a Trusted Platform Module (TPM). Instead, Microsoft Entra ID uses Apple Secure Enclave to store proof-of-possession keys. On macOS devices without Secure Enclave (for example, some older Mac mini models), Microsoft Entra ID falls back to an enhanced version of the Apple Keychain (Data Protection Keychain).

This difference means that some prerequisite configuration is required before users can register devices in a way that supports Token Protection enforcement.

The high-level steps to enable Token Protection on Apple platforms are as follows:

1. Configure hardware-backed device registration
2. Configure the report-only Conditional Access policy
3. Review readiness with logs and metrics
4. Enforce the policy

## Configure hardware-backed device registration

Complete the following steps for *each* platform you're deploying to. These steps must be completed *before* users register their devices.

Note

Users who registered their devices before these steps were completed will be prompted to enter their credentials the first time they access a resource protected by the Token Protection policy. Once they complete authentication successfully, their device registration is automatically upgraded to hardware-backed storage. For more information, see **Upgrade device registration**.

# [iOS and iPadOS](#tab/ios-and-ipados)
1. Install Microsoft Authenticator from the Apple App Store, or deploy it via your MDM solution. Authenticator serves as the authentication broker for Microsoft Entra sign-ins.
2. Enable hardware-backed registration using the [Microsoft Enterprise SSO plug-in for Apple Devices](../../identity-platform/apple-sso-plugin).

# [macOS](#tab/macos)
1. Install the Microsoft Company Portal or deploy it via your MDM solution. Company Portal serves as the authentication broker for Microsoft Entra sign-ins.
2. Enable hardware-backed registration using one of the following options:
    - Option A: Enable the [Microsoft Enterprise SSO plug-in for Apple Devices](../../identity-platform/apple-sso-plugin).
    - Option B: Configure **Platform SSO for macOS**. For setup instructions, see [Configure Platform SSO for macOS devices in Microsoft Intune](/en-us/intune/intune-service/configuration/platform-sso-macos).

---

## Configure the report-only mode policy

Before enforcing the policy, deploy it in report-only mode to assess the effect and identify noncompliant sign-in sessions.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Give your policy a name. Create a meaningful standard for the names of your policies.
4. Under **Assignments**, select **Users, agents, or workload identities**.
    1. Under **Include**, select the users or groups to target.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
5. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include** &gt; **Select resources**
    1. Under **Select**, select the following applications:

        1. Office 365 Exchange Online
        2. Office 365 SharePoint Online

        Warning

        Your Conditional Access policy should only be configured for these applications. Selecting the **Office 365** application group might result in unintended failures. This change is an exception to the general rule that the **Office 365** application group should be selected in a Conditional Access policy.
    2. Choose **Select**.
6. Under **Conditions**:
    1. Under **Device platforms**:
        1. Set **Configure** to **Yes**.
        2. **Include** &gt; **Select device platforms** &gt; **iOS** and **macOS**.
        3. Select **Done**.
    2. Under **Client apps**:
        1. Set **Configure** to **Yes**.

            Warning

            Not configuring the **Client Apps** condition, or leaving **Browser** selected might cause applications that use MSAL.js, such as Teams Web to be blocked.
        2. Under Modern authentication clients, only select **Mobile apps and desktop clients**. Leave other items unchecked.
        3. Select **Done**.
7. Under **Access controls** &gt; **Session**, select **Require token protection for sign-in sessions** and select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

Tip

Because Conditional Access policies requiring token protection are currently only available for Windows and Apple devices, it's necessary to secure your environment against potential policy bypass when an attacker might appear to come from a different platform.

In addition, you should configure the following policies:

- [Block access from unknown platforms](policy-all-users-device-unknown-unsupported)
- [Require device compliance for all known platforms](policy-all-users-device-compliance)

## Review readiness with logs and metrics

After the report-only policy is in place and running, you should review the [Policy impact](concept-conditional-access-report-only#policy-impact), analyze your [sign-in logs](../monitoring-health/concept-sign-ins), and [investigate with Log Analytics](../monitoring-health/howto-analyze-activity-logs-log-analytics) to review enforcement readiness.

### Sign-in logs

To view Token Protection related sign-in events in the admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
    - Add the **Token Protection – Sign-in session status code** column to your view to quickly see related sign-in events.
3. Select the sign-in event you're investigating.
4. Review the **Conditional Access** and **Report-Only** tabs (depending on the policy state) and select your token protection policy.
5. Under **Session Controls** check to see if the policy requirements were satisfied or not.
6. Select the **Basic Info** tab and check the **Token Protection - Sign In Session** field for more information.

The sign-in logs include a `tokenProtectionStatusDetails` property that indicates whether a request uses a device-bound token.

```http
"tokenProtectionStatusDetails": {
  "signInSessionStatus": "bound | unbound",
  "signInSessionStatusCode": <code>
}
```

Note

Users on devices that were registered to Microsoft Entra ID before Token Protection policy was enforced will be prompted to reauthenticate once the policy is enforced. They'll need to complete a one-time device registration upgrade and then sign in again to access resources. These users can be identified by **status codes 1003 and 1004**. Because users in this state can self-remediate, they're eligible for policy enforcement.

To identify which users you can apply the policy to, refer to the following status codes.

| Status Code | Description | Action Required |
| --- | --- | --- |
| 1002 | Unbound - Request is unbound due to the lack of Microsoft Entra ID device state | User must register device |
| 1003 | Unbound - Device not registered with secure credentials (legacy registration) | User must perform one-time registration upgrade |
| 1004 | Unbound - Device registration isn't hardware-backed | User must perform one-time registration upgrade |
| 1005 | Unbound - Unspecified reason | Varies |
| 1006 | Unbound - OS version isn't supported | User must upgrade OS |
| 1007 | Unbound - Not hardware-backed; signed-in user isn't the registered device owner | User must re-register, or registered owner must perform upgrade |
| 1008 | Unbound - Client doesn't use an identity broker | Request is unbound because the client isn't integrated with the platform broker or broker app isn't installed on the device. |

To identify requests that are compliant or upgradeable with user action, filter for:

- `signInSessionStatus` == bound, or
- `signInSessionStatus` == unbound with `signInSessionStatusCode` of 1003 or 1004

Sample Microsoft Graph Query (Non-Interactive Sign-ins): `GET https://graph.microsoft.com/beta/auditLogs/signIns?$filter=(signInEventTypes/any(t: t eq 'nonInteractiveUser') and (tokenProtectionStatusDetails/signInSessionStatusCode eq 1003 or tokenProtectionStatusDetails/signInSessionStatusCode eq 1004 or tokenProtectionStatusDetails/signInSessionStatus eq 'bound'))`

### Log Analytics

You can also use Log Analytics to query interactive and non-interactive sign-in logs for blocked requests due to Token Protection enforcement failure.

The following sample query searches the non-interactive sign-in logs for the last seven days, highlighting **Blocked** versus **Allowed** requests by application. These queries are samples only and are subject to change.

**Sample queries**:

The following sample Log Analytics query searches the non-interactive sign-in logs for the last seven days, highlighting **Blocked** versus **Allowed** requests by **Application**.

Requests by application

```kusto
// Per-app query
// Select the log you want to query (SigninLogs or AADNonInteractiveUserSignInLogs)
// SigninLogs
AADNonInteractiveUserSignInLogs
// Adjust the time range below
| where TimeGenerated > ago(7d)
| project Id, ConditionalAccessPolicies, Status, UserPrincipalName, AppDisplayName, ResourceDisplayName, TokenProtectionStatusDetails
| where ConditionalAccessPolicies != "[]"
| where ResourceDisplayName == "Office 365 Exchange Online"
    or ResourceDisplayName == "Office 365 SharePoint Online"
// Add UserPrincipalName if you want to filter to a specific user
// | where UserPrincipalName == "<user_principal_name>"
| mv-expand todynamic(ConditionalAccessPolicies)
| where ConditionalAccessPolicies["enforcedSessionControls"] contains '["Binding"]'
    or ConditionalAccessPolicies["enforcedSessionControls"] contains '["SignInTokenProtection"]'
| where ConditionalAccessPolicies.result != "reportOnlyNotApplied"
    and ConditionalAccessPolicies.result != "notApplied"
| extend SessionNotSatisfyResult = ConditionalAccessPolicies["sessionControlsNotSatisfied"]
| extend Result = case(
    SessionNotSatisfyResult contains 'SignInTokenProtection'
        or SessionNotSatisfyResult contains 'Binding', 'Block', 'Allow')
| extend parsedBindingDetails = parse_json(TokenProtectionStatusDetails)
| extend bindingStatusCode = tostring(parsedBindingDetails["signInSessionStatusCode"])
| extend IsSelfRemediable = Result == "Block"
    and (bindingStatusCode == "1003" or bindingStatusCode == "1004")
| summarize by Id, UserPrincipalName, AppDisplayName, Result, IsSelfRemediable
| summarize Requests = count(),
    Users = dcount(UserPrincipalName),
    Allow = countif(Result == "Allow"),
    Block = countif(Result == "Block"),
    BlockSelfRemediable = countif(IsSelfRemediable == true),
    BlockedUsers = dcountif(UserPrincipalName, Result == "Block"),
    BlockedUsersSelfRemediable = dcountif(UserPrincipalName, IsSelfRemediable == true)
    by AppDisplayName
| extend PctAllowed = round(100.0 * Allow / (Allow + Block), 2)
| extend PctEnforceable = round(100.0 * (Allow + BlockSelfRemediable) / (Allow + Block), 2)
| project AppDisplayName, Requests, Users, Allow, Block,
    BlockSelfRemediable,
    BlockedUsers, BlockedUsersSelfRemediable,
    PctAllowed, PctEnforceable
| sort by Requests desc
```

The following query example looks at the non-interactive sign-in log for the last seven days, highlighting **Blocked** versus **Allowed** requests by **User**.

Requests by user

The following query searches the non-interactive sign-in logs for the last seven days, highlighting **Blocked** versus **Allowed** requests by user.

```kusto
// Per-user query
// Select the log you want to query (SigninLogs or AADNonInteractiveUserSignInLogs)
// SigninLogs
AADNonInteractiveUserSignInLogs
// Adjust the time range below
| where TimeGenerated > ago(7d)
| project Id, ConditionalAccessPolicies, UserPrincipalName, AppDisplayName, ResourceDisplayName, TokenProtectionStatusDetails
| where ConditionalAccessPolicies != "[]"
| where ResourceDisplayName == "Office 365 Exchange Online"
    or ResourceDisplayName == "Office 365 SharePoint Online"
// Add UserPrincipalName if you want to filter to a specific user
// | where UserPrincipalName == "<user_principal_name>"
| mv-expand todynamic(ConditionalAccessPolicies)
| where ConditionalAccessPolicies["enforcedSessionControls"] contains '["Binding"]'
    or ConditionalAccessPolicies["enforcedSessionControls"] contains '["SignInTokenProtection"]'
| where ConditionalAccessPolicies.result != "reportOnlyNotApplied"
    and ConditionalAccessPolicies.result != "notApplied"
| extend SessionNotSatisfyResult = ConditionalAccessPolicies.sessionControlsNotSatisfied
| extend Result = case(
    SessionNotSatisfyResult contains 'SignInTokenProtection'
        or SessionNotSatisfyResult contains 'Binding', 'Block', 'Allow')
| extend parsedBindingDetails = parse_json(TokenProtectionStatusDetails)
| extend bindingStatusCode = tostring(parsedBindingDetails["signInSessionStatusCode"])
| extend IsSelfRemediable = Result == "Block"
    and (bindingStatusCode == "1003" or bindingStatusCode == "1004")
| summarize by Id, UserPrincipalName, AppDisplayName, ResourceDisplayName, Result, IsSelfRemediable
| summarize Requests = count(),
    Allow = countif(Result == "Allow"),
    Block = countif(Result == "Block"),
    BlockSelfRemediable = countif(IsSelfRemediable == true)
    by UserPrincipalName, AppDisplayName, ResourceDisplayName
| extend PctAllowed = round(100.0 * Allow / (Allow + Block), 2)
| extend PctEnforceable = round(100.0 * (Allow + BlockSelfRemediable) / (Allow + Block), 2)
| project UserPrincipalName, AppDisplayName, ResourceDisplayName,
    Requests, Allow, Block, BlockSelfRemediable,
    PctAllowed, PctEnforceable
| sort by UserPrincipalName asc
```

The following query example looks at the non-interactive sign-in log for the last seven days, highlighting users that are using devices, where Microsoft Entra ID device state doesn't satisfy Token protection CA policy requirements.

Devices don't meet policy requirements

The following query searches the non-interactive sign-in logs for the last seven days to identify users whose devices don't satisfy Token Protection policy requirements and are candidates for a device registration upgrade. This query is useful during the report-only phase. The identified users with status codes 1003 and 1004 will be prompted for a one-time registration upgrade when the policy is enforced, allowing you to proactively communicate the change or provide guidance ahead of enforcement.

```kusto
AADNonInteractiveUserSignInLogs
// Adjust the time range below
| where TimeGenerated > ago(7d)
| where TokenProtectionStatusDetails != ""
| extend parsedBindingDetails = parse_json(TokenProtectionStatusDetails)
| extend bindingStatus = tostring(parsedBindingDetails["signInSessionStatus"])
| extend bindingStatusCode = tostring(parsedBindingDetails["signInSessionStatusCode"])
// Status code 1003: legacy registration — user can self-remediate with a one-time upgrade
// Status code 1004: not hardware-backed — user can self-remediate with a one-time upgrade
| where bindingStatusCode == "1003" or bindingStatusCode == "1004"
| summarize count() by UserPrincipalName
```

## Enforce the Policy

After reviewing sign-in log data and confirming that your targeted users and devices are ready, move the **Enable policy** toggle from **Report-only** to **On**.

Communicate the change to affected users and your help desk team in advance, particularly noting:

- Users who will be prompted to upgrade their device registration.
- Users of Apple's native Mail and Calendar apps, who will be blocked.

## End User Experience

There are some end user experiences to be aware of when deploying Token Protection.

### Upgrade device registration

Users on devices that were registered to Microsoft Entra ID before Token Protection policy was enforced will be prompted to reauthenticate once policy is enforced. They'll need to sign in again to access resources.

![Screenshot of the token protection error message when your device isn't registered or enrolled.](media/deployment-guide-token-protection-apple/token-protection-device-registration-apple.png)

### Unsupported applications

When the Token Protection policy is enabled, users who aren't using a supported application will see the following screen after authenticating:

![Screenshot of the error message when a token protection policy blocks access.](media/deployment-guide-token-protection-apple/token-protection-required-error-message.png)