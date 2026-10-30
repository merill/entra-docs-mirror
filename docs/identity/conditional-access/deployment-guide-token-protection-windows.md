---
layout: Conceptual
title: Token Protection Deployment Guide - Windows - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/deployment-guide-token-protection-windows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Deploy Token Protection with Microsoft Entra Conditional Access for Windows
ms.topic: how-to
ms.date: 2026-09-21T00:00:00.0000000Z
ms.reviewer: sgrandhi
locale: en-us
document_id: 81f3a0d2-05d6-fef7-2214-13b72145d377
document_version_independent_id: 81f3a0d2-05d6-fef7-2214-13b72145d377
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/deployment-guide-token-protection-windows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/deployment-guide-token-protection-windows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/deployment-guide-token-protection-windows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7a23184d-f90b-8b15-0bb9-88e8d9b177d9
---

# Token Protection Deployment Guide - Windows - Microsoft Entra ID | Microsoft Learn

## Overview

This guide covers the steps required to deploy and enforce Token Protection for sign-in session tokens on Windows platform.

For an overview of Token Protection and supported platforms, see [Token Protection in Microsoft Entra Conditional Access](concept-token-protection). Review the overview documentation before using this deployment guide.

## Prerequisites

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## Supported applications and resources

Before enforcing the policy, ensure users are running supported and up-to-date client versions. Older or out-of-support versions might not be compatible and can be blocked.

### Applications

Token Protection can be applied to the following applications:

- Exchange PowerShell module
- Microsoft Copilot
- Microsoft Edge (support for sign-in to Edge profile only)\*
- Microsoft Graph PowerShell with [EnableLoginByWAM](/en-us/powershell/module/microsoft.graph.authentication/set-mggraphoption#example-1-set-web-account-manager-support) option
- Microsoft Loop
- Microsoft Teams
- Microsoft To Do
- OneNote
- OneDrive
- Outlook
- Power BI desktop
- PowerQuery extension for Excel (only available for users on [Current Channel](/en-us/microsoft-365-apps/updates/overview-update-channels#current-channel-overview))
- Visual Studio Code
- Visual Studio when using the 'Windows authentication broker' Sign-in option
- Windows App
- Word, Excel, PowerPoint

\*Token Protection currently supports native applications only. Browser-based applications are not supported.

### Resources

Token Protection on Windows platforms can be used to protect the following resources:

- Exchange Online
- SharePoint Online
- Microsoft Teams
- Azure Virtual Desktop
- Windows 365

### Known limitations

- Office perpetual clients aren't supported.
- The following applications don't support signing in using protected token flows and users are blocked when accessing Exchange and SharePoint:
    - PowerShell modules accessing SharePoint
    - PowerQuery extension for Excel for users not in Current Channel updates
    - Extensions to Visual Studio Code which access Exchange or SharePoint
- The following Windows client devices aren't supported:
    - Surface Hub
    - Windows-based Microsoft Teams Rooms (MTR) systems
- [External users](/en-us/entra/external-id/what-is-b2b) who meet the token protection device registration requirements in their home tenant are supported. However, users who don't meet these requirements see an unclear error message with no indication of the root cause.
- Devices registered with Microsoft Entra ID using the following methods are unsupported:
    - Microsoft Entra joined [Azure Virtual Desktop session hosts](/en-us/azure/virtual-desktop/azure-ad-joined-session-hosts).
    - Windows devices deployed using [bulk enrollment](/en-us/mem/intune-service/enrollment/windows-bulk-enroll).
    - [Cloud PCs deployed by Windows 365](/en-us/windows-365/enterprise/identity-authentication#device-join-types) that are Microsoft Entra joined.
    - Power Automate hosted machine groups that are [Microsoft Entra joined](/en-us/power-automate/desktop-flows/hosted-machine-groups#general-network-requirements).
    - Windows Autopilot devices deployed using [self-deploying mode](/en-us/autopilot/self-deploying).
    - Windows virtual machines deployed in Azure using the virtual machine (VM) extension that are enabled for [Microsoft Entra ID authentication](/en-us/entra/identity/devices/howto-vm-sign-in-azure-ad-windows).

To identify the impacted devices due to unsupported registration types listed previously, inspect the `tokenProtectionStatusDetails` attribute in the sign-in logs. Token requests that are blocked due to an unsupported device registration type, can be identified with a `signInSessionStatusCode` value of 1003.

To prevent disruption during onboarding, modify the token protection Conditional Access policy by adding a device filter condition that excludes devices in the previously described deployment category. For example, to exclude:

- Cloud PCs that are Microsoft Entra joined, you can use `systemLabels -eq "CloudPC" and trustType -eq "AzureAD"`.
- Azure Virtual Desktops that are Microsoft Entra joined, you can use `systemLabels -eq "AzureVirtualDesktop" and trustType -eq "AzureAD"`.
- Power Automate hosted machine groups that are Microsoft Entra joined, you can use `systemLabels -eq "MicrosoftPowerAutomate" and trustType -eq "AzureAD"`.
- Windows Autopilot devices deployed using self-deploying mode, you can use enrollmentProfileName property. As an example, if you created an enrollment profile in Intune for your Autopilot self-deployment mode devices as "Autopilot self-deployment profile," you can use `enrollmentProfileName -eq "Autopilot self-deployment profile"`.
- Windows virtual machines in Azure that are Microsoft Entra joined, you can use `profileType -eq "SecureVM" and trustType -eq "AzureAD"`.

## How to enable Token Protection on Windows

For users, the deployment of a Conditional Access policy to enforce token protection should be invisible when using compatible client platforms on registered devices and compatible applications.

To minimize the likelihood of user disruption due to app or device incompatibility, follow these recommendations:

- Start with a pilot group of users and expand over time.
- Create a Conditional Access policy in [report-only mode](concept-conditional-access-report-only) before enforcing token protection.
- Capture both interactive and non-interactive sign-in logs.
- Analyze these logs long enough to cover normal application use.
- Add known, reliable users to an enforcement policy.

This process helps assess your users' client and app compatibility for token protection enforcement.

## Create a Conditional Access policy

Users who perform specialized roles like those described in [Privileged access security levels](/en-us/security/privileged-access-workstations/privileged-access-security-levels#specialized) are possible targets for this functionality. Pilot with a small subset to begin.

The following steps help you create a Conditional Access policy to require token protection for Exchange Online and SharePoint Online on Windows devices.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select the users or groups who are testing this policy.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include** &gt; **Select resources**
    1. Under **Select**, select the following applications:

        1. Office 365 Exchange Online
        2. Office 365 SharePoint Online
        3. Microsoft Teams Services
        4. If you deployed Windows App in your environment, include:
            1. Azure Virtual Desktop
            2. Windows 365
            3. Windows Cloud Login

        Warning

        Your Conditional Access policy should only be configured for these applications. Selecting the **Office 365** application group might result in unintended failures. This change is an exception to the general rule that the **Office 365** application group should be selected in a Conditional Access policy.
    2. Choose **Select**.
7. Under **Conditions**:
    1. Under **Device platforms**:
        1. Set **Configure** to **Yes**.
        2. **Include** &gt; **Select device platforms** &gt; **Windows**.
        3. Select **Done**.
    2. Under **Client apps**:
        1. Set **Configure** to **Yes**.

            Warning

            Not configuring the **Client Apps** condition, or leaving **Browser** selected might cause applications that use MSAL.js, such as Teams Web to be blocked.
        2. Under Modern authentication clients, only select **Mobile apps and desktop clients**. Leave other items unchecked.
        3. Select **Done**.
8. Under **Access controls** &gt; **Session**, select **Require token protection for sign-in sessions** and select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Tip

Because Conditional Access policies requiring token protection are currently only available for Windows and Apple devices, it's necessary to secure your environment against potential policy bypass when an attacker might appear to come from a different platform.

In addition, you should configure the following policies:

- [Block access from unknown platforms](policy-all-users-device-unknown-unsupported)
- [Require device compliance for all known platforms](policy-all-users-device-compliance)

## Capture logs and analyze

Monitor Conditional Access enforcement of token protection before and after enforcement by using features like [Policy impact](concept-conditional-access-report-only#policy-impact), Sign-in logs, and Log Analytics.

### Sign-in logs

Use Microsoft Entra sign-in log to verify the outcome of a token protection enforcement policy in report only mode or in enabled mode.

[![Screenshot showing an example of a policy not being satisfied.](media/deployment-guide-token-protection-windows/sign-in-log-sample.png)](media/deployment-guide-token-protection-windows/sign-in-log-sample.png#lightbox)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Select a specific request to determine if the policy is applied or not.
4. Go to the **Conditional Access** or **Report-Only** pane depending on its state and select the name of your policy requiring token protection.
5. Under **Session Controls** check to see if the policy requirements were satisfied or not.
6. To find more details about the binding state of the request, select the pane **Basic Info** and see the field **Token Protection - Sign In Session**. Possible values are:
    1. Bound: the request was using bound protocols. Some sign-ins might include multiple requests, and all requests must be bound to satisfy the token protection policy. Even if an individual request appears to be bound, it doesn't ensure compliance with the policy if other requests are unbound. To see all requests for a sign-in, you can filter all requests for a specific user or look by correlation ID.
    2. Unbound: the request wasn't using bound protocols. Possible `statusCodes`when request is unbound are:
        1. 1002: The request is unbound due to the lack of Microsoft Entra ID device state.
        2. 1003: The request is unbound because the Microsoft Entra ID device state doesn't satisfy Conditional Access policy requirements for token protection. This error could be due to an unsupported device registration type, or the device wasn't registered using fresh sign-in credentials.
        3. 1005: The request is unbound for other unspecified reasons.
        4. 1006: The request is unbound because the OS version is unsupported.
        5. 1008: The request is unbound because the client isn't integrated with the platform broker, such as Windows Account Manager (WAM).

[![Screenshot showing a sample sign-in with the Token Protection - Sign In Session attribute highlighted. ](media/deployment-guide-token-protection-windows/sign-in-log-sample-unbound-status-code-1002.png)](media/deployment-guide-token-protection-windows/sign-in-log-sample-unbound-status-code-1002.png#lightbox)

Note

**Sign-in logs output:** The value of the string used in `enforcedSessionControls` and `sessionControlsNotSatisfied` changed from `Binding` to `SignInTokenProtection` in late June 2023. Queries on sign-in log data should be updated to reflect this change. The examples cover both values to include historical data.

### Log Analytics

You can also use [Log Analytics](../monitoring-health/tutorial-configure-log-analytics-workspace) to query the sign-in logs (interactive and non-interactive) for blocked requests due to token protection enforcement failure. These queries are only samples and are subject to change.

**Sample queries**:

The following sample Log Analytics query searches the non-interactive sign-in logs for the last seven days, highlighting **Blocked** versus **Allowed** requests by **Application**.

Requests by application

```kusto
//Per Apps query 
// Select the log you want to query (SigninLogs or AADNonInteractiveUserSignInLogs ) 
//SigninLogs 
AADNonInteractiveUserSignInLogs 
// Adjust the time range below 
| where TimeGenerated > ago(7d) 
| project Id,ConditionalAccessPolicies, Status,UserPrincipalName, AppDisplayName, ResourceDisplayName 
| where ConditionalAccessPolicies != "[]" 
| where ResourceDisplayName == "Office 365 Exchange Online" or ResourceDisplayName =="Office 365 SharePoint Online" or ResourceDisplayName =="Azure Virtual Desktop" or ResourceDisplayName =="Windows 365" or ResourceDisplayName =="Windows Cloud Login"
| where ResourceDisplayName == "Office 365 Exchange Online" or ResourceDisplayName =="Office 365 SharePoint Online" 
//Add userPrincipalName if you want to filter  
// | where UserPrincipalName =="<user_principal_Name>" 
| mv-expand todynamic(ConditionalAccessPolicies) 
| where ConditionalAccessPolicies ["enforcedSessionControls"] contains '["Binding"]' or ConditionalAccessPolicies ["enforcedSessionControls"] contains '["SignInTokenProtection"]' 
| where ConditionalAccessPolicies.result !="reportOnlyNotApplied" and ConditionalAccessPolicies.result !="notApplied" 
| extend SessionNotSatisfyResult = ConditionalAccessPolicies["sessionControlsNotSatisfied"] 
| extend Result = case (SessionNotSatisfyResult contains 'SignInTokenProtection' or SessionNotSatisfyResult contains 'SignInTokenProtection', 'Block','Allow')
| summarize by Id,UserPrincipalName, AppDisplayName, Result 
| summarize Requests = count(), Users = dcount(UserPrincipalName), Block = countif(Result == "Block"), Allow = countif(Result == "Allow"), BlockedUsers = dcountif(UserPrincipalName, Result == "Block") by AppDisplayName 
| extend PctAllowed = round(100.0 * Allow/(Allow+Block), 2) 
| sort by Requests desc 
```

The result of this query should be similar to the following screenshot:

[![Screenshot showing example results of a Log Analytics query looking for token protection policies.](media/concept-token-protection/log-analytics-results.png)](media/concept-token-protection/log-analytics-results.png#lightbox)

The following query example looks at the non-interactive sign-in log for the last seven days, highlighting **Blocked** versus **Allowed** requests by **User**.

Requests by user

```kusto
//Per users query 
// Select the log you want to query (SigninLogs or AADNonInteractiveUserSignInLogs ) 
//SigninLogs 
AADNonInteractiveUserSignInLogs 
// Adjust the time range below 
| where TimeGenerated > ago(7d) 
| project Id,ConditionalAccessPolicies, UserPrincipalName, AppDisplayName, ResourceDisplayName 
| where ConditionalAccessPolicies != "[]" 
| where ResourceDisplayName == "Office 365 Exchange Online" or ResourceDisplayName =="Office 365 SharePoint Online" or ResourceDisplayName =="Azure Virtual Desktop" or ResourceDisplayName =="Windows 365" or ResourceDisplayName =="Windows Cloud Login"
| where ResourceDisplayName == "Office 365 Exchange Online" or ResourceDisplayName =="Office 365 SharePoint Online" 
//Add userPrincipalName if you want to filter  
// | where UserPrincipalName =="<user_principal_Name>" 
| mv-expand todynamic(ConditionalAccessPolicies) 
| where ConditionalAccessPolicies ["enforcedSessionControls"] contains '["Binding"]' or ConditionalAccessPolicies ["enforcedSessionControls"] contains '["SignInTokenProtection"]'
| where ConditionalAccessPolicies.result !="reportOnlyNotApplied" and ConditionalAccessPolicies.result !="notApplied" 
| extend SessionNotSatisfyResult = ConditionalAccessPolicies.sessionControlsNotSatisfied 
| extend Result = case (SessionNotSatisfyResult contains 'SignInTokenProtection' or SessionNotSatisfyResult contains 'SignInTokenProtection', 'Block','Allow')
| summarize by Id, UserPrincipalName, AppDisplayName, ResourceDisplayName,Result  
| summarize Requests = count(),Block = countif(Result == "Block"), Allow = countif(Result == "Allow") by UserPrincipalName, AppDisplayName,ResourceDisplayName 
| extend PctAllowed = round(100.0 * Allow/(Allow+Block), 2) 
| sort by UserPrincipalName asc   
```

The following query example looks at the non-interactive sign-in log for the last seven days, highlighting users that are using devices, where Microsoft Entra ID device state doesn't satisfy Token protection CA policy requirements.

Devices don't meet policy requirements

```kusto
AADNonInteractiveUserSignInLogs 
// Adjust the time range below 
| where TimeGenerated > ago(7d) 
| where TokenProtectionStatusDetails!= "" 
| extend parsedBindingDetails = parse_json(TokenProtectionStatusDetails) 
| extend bindingStatus = tostring(parsedBindingDetails["signInSessionStatus"]) 
| extend bindingStatusCode = tostring(parsedBindingDetails["signInSessionStatusCode"]) 
| where bindingStatusCode == 1003 
| summarize count() by UserPrincipalName 
```

## End user experience

A user that registered or enrolled their supported device doesn't experience any differences in the sign in experience on a token protection supported application when the token protection requirement is enabled.

A user who hasn't registered or enrolled their device and if the token protection policy is enabled will be prompted to register the device.

![Screenshot of the token protection register in line screen.](media/deployment-guide-token-protection-windows/token-protection-register-prompt.png)

For users who have not yet updated to the latest September 2026 Windows update will continue to see the below message:

![Screenshot of the token protection error message when your device isn't registered or enrolled.](media/deployment-guide-token-protection-windows/token-protection-register-or-enroll-device.png)

A user that isn't using a supported application when the token protection policy is enabled will see the following screenshot after authenticating.

![Screenshot of the error message when a token protection policy blocks access.](media/deployment-guide-token-protection-windows/token-protection-required-error-message.png)