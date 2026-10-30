---
layout: Conceptual
title: Monitor on-premises Microsoft Entra Password Protection - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-monitor
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to monitor and review logs for Microsoft Entra Password Protection for an on-premises Active Directory Domain Services environment
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: jsimmons
ms.custom: 
locale: en-us
document_id: 23a4bc15-af79-3d85-105b-745c3e92511e
document_version_independent_id: 5e9a9849-9b97-b494-960b-a9601d1d9cfb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-password-ban-bad-on-premises-monitor.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-password-ban-bad-on-premises-monitor
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-password-ban-bad-on-premises-monitor.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: e0f83fbe-f2be-87f4-7413-d6bd9433e1b6
---

# Monitor on-premises Microsoft Entra Password Protection - Microsoft Entra ID | Microsoft Learn

After the deployment of Microsoft Entra Password Protection, monitoring and reporting are essential tasks. This article goes into detail to help you understand various monitoring techniques, including where each service logs information and how to report on the use of Microsoft Entra Password Protection.

Monitoring and reporting are done either by event log messages or by running PowerShell cmdlets. The DC agent and proxy services both log event log messages. All PowerShell cmdlets described below are only available on the proxy server (see the AzureADPasswordProtection PowerShell module). The DC agent software does not install a PowerShell module.

## DC agent event logging

On each domain controller, the DC agent service software writes the results of each individual password validation operation (and other status) to a local event log:

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Admin`

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Operational`

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Trace`

The DC agent Admin log is the primary source of information for how the software is behaving.

Note that the Trace log is off by default.

Events logged by the various DC agent components fall within the following ranges:

| Component | Event ID range |
| --- | --- |
| DC Agent password filter dll | 10000-19999 |
| DC agent service hosting process | 20000-29999 |
| DC agent service policy validation logic | 30000-39999 |

## DC agent Admin event log

### Password validation outcome events

On each domain controller, the DC agent service software writes the results of each individual password validation to the DC agent admin event log.

For a successful password validation operation, there is generally one event logged from the DC agent password filter dll. For a failing password validation operation, there are generally two events logged, one from the DC agent service, and one from the DC Agent password filter dll.

Discrete events to capture these situations are logged, based around the following factors:

- Whether a given password is being set or changed.
- Whether validation of a given password passed or failed.
- Whether validation failed due to the Microsoft global policy, the organizational policy, or a combination.
- Whether audit only mode is currently on or off for the current password policy.

The key password-validation-related events are as follows:

| Event | Password change | Password set |
| --- | --- | --- |
| Pass | 10014 | 10015 |
| Fail (due to customer password policy) | 10016, 30002 | 10017, 30003 |
| Fail (due to Microsoft password policy) | 10016, 30004 | 10017, 30005 |
| Fail (due to combined Microsoft and customer password policies) | 10016, 30026 | 10017, 30027 |
| Fail (due to user name) | 10016, 30021 | 10017, 30022 |
| Audit-only Pass (would have failed customer password policy) | 10024, 30008 | 10025, 30007 |
| Audit-only Pass (would have failed Microsoft password policy) | 10024, 30010 | 10025, 30009 |
| Audit-only Pass (would have failed combined Microsoft and customer password policies) | 10024, 30028 | 10025, 30029 |
| Audit-only Pass (would have failed due to user name) | 10016, 30024 | 10017, 30023 |

The cases in the table above that refer to "combined policies" are referring to situations where a user's password was found to contain at least one token from both the Microsoft banned password list and the customer banned password list.

The cases in the table above that refer to "user name" are referring to situations where a user's password was found to contain either the user's account name and/or one of the user's friendly names. Either scenario will cause the user's password to be rejected when the policy is set to Enforce, or passed if the policy is in Audit mode.

When a pair of events is logged together, both events are explicitly associated by having the same CorrelationId.

### Password validation summary reporting via PowerShell

The `Get-AzureADPasswordProtectionSummaryReport` cmdlet may be used to produce a summary view of password validation activity. An example output of this cmdlet is as follows:

```powershell
Get-AzureADPasswordProtectionSummaryReport -DomainController bplrootdc2
DomainController                : bplrootdc2
PasswordChangesValidated        : 6677
PasswordSetsValidated           : 9
PasswordChangesRejected         : 10868
PasswordSetsRejected            : 34
PasswordChangeAuditOnlyFailures : 213
PasswordSetAuditOnlyFailures    : 3
PasswordChangeErrors            : 0
PasswordSetErrors               : 1
```

The scope of the cmdlet's reporting may be influenced using one of the –Forest, -Domain, or –DomainController parameters. Not specifying a parameter implies –Forest.

Note

If you only install the DC agent on one DC, the Get-AzureADPasswordProtectionSummaryReport will read events only from that DC. To get events from multiple DCs, you'll need the DC agent installed on each DC.

The `Get-AzureADPasswordProtectionSummaryReport` cmdlet works by querying the DC agent admin event log, and then counting the total number of events that correspond to each displayed outcome category. The following table contains the mappings between each outcome and its corresponding event ID:

| Get-AzureADPasswordProtectionSummaryReport property | Corresponding event ID |
| --- | --- |
| PasswordChangesValidated | 10014 |
| PasswordSetsValidated | 10015 |
| PasswordChangesRejected | 10016 |
| PasswordSetsRejected | 10017 |
| PasswordChangeAuditOnlyFailures | 10024 |
| PasswordSetAuditOnlyFailures | 10025 |
| PasswordChangeErrors | 10012 |
| PasswordSetErrors | 10013 |

Note that the `Get-AzureADPasswordProtectionSummaryReport` cmdlet is shipped in PowerShell script form and if needed may be referenced directly at the following location:

`%ProgramFiles%\WindowsPowerShell\Modules\AzureADPasswordProtection\Get-AzureADPasswordProtectionSummaryReport.ps1`

Note

This cmdlet works by opening a PowerShell session to each domain controller. In order to succeed, PowerShell remote session support must be enabled on each domain controller, and the client must have sufficient privileges. For more information on PowerShell remote session requirements, run 'Get-Help about\_Remote\_Troubleshooting' in a PowerShell window.

Note

This cmdlet works by remotely querying each DC agent service's Admin event log. If the event logs contain large numbers of events, the cmdlet may take a long time to complete. In addition, bulk network queries of large data sets may impact domain controller performance. Therefore, this cmdlet should be used carefully in production environments.

### Sample event log messages

#### Event ID 10014 (Successful password change)

```text
The changed password for the specified user was validated as compliant with the current Azure password policy.

UserName: SomeUser
FullName: Some User
```

#### Event ID 10017 (Failed password change):

```text
The reset password for the specified user was rejected because it did not comply with the current Azure password policy. Please see the correlated event log message for more details.

UserName: SomeUser
FullName: Some User
```

#### Event ID 30003 (Failed password change):

```text
The reset password for the specified user was rejected because it matched at least one of the tokens present in the per-tenant banned password list of the current Azure password policy.

UserName: SomeUser
FullName: Some User
```

#### Event ID 10024 (Password accepted due to policy in audit only mode)

```text
The changed password for the specified user would normally have been rejected because it did not comply with the current Azure password policy. The current Azure password policy is con-figured for audit-only mode so the password was accepted. Please see the correlated event log message for more details. 
 
UserName: SomeUser
FullName: Some User
```

#### Event ID 30008 (Password accepted due to policy in audit only mode)

```text
The changed password for the specified user would normally have been rejected because it matches at least one of the tokens present in the per-tenant banned password list of the current Azure password policy. The current Azure password policy is configured for audit-only mode so the password was accepted. 

UserName: SomeUser
FullName: Some User

```

#### Event ID 30001 (Password accepted due to no policy available)

```text
The password for the specified user was accepted because an Azure password policy is not available yet

UserName: SomeUser
FullName: Some User

This condition may be caused by one or more of the following reasons:%n

1. The forest has not yet been registered with Azure.

   Resolution steps: an administrator must register the forest using the Register-AzureADPasswordProtectionForest cmdlet.

2. An Azure AD password protection Proxy is not yet available on at least one machine in the current forest.

   Resolution steps: an administrator must install and register a proxy using the Register-AzureADPasswordProtectionProxy cmdlet.

3. This DC does not have network connectivity to any Azure AD password protection Proxy instances.

   Resolution steps: ensure network connectivity exists to at least one Azure AD password protection Proxy instance.

4. This DC does not have connectivity to other domain controllers in the domain.

   Resolution steps: ensure network connectivity exists to the domain.
```

#### Event ID 30006 (New policy being enforced)

```text
The service is now enforcing the following Azure password policy.

 Enabled: 1
 AuditOnly: 1
 Global policy date: ‎2018‎-‎05‎-‎15T00:00:00.000000000Z
 Tenant policy date: ‎2018‎-‎06‎-‎10T20:15:24.432457600Z
 Enforce tenant policy: 1
```

#### Event ID 30019 (Microsoft Entra Password Protection is disabled)

```text
The most recently obtained Azure password policy was configured to be disabled. All passwords submitted for validation from this point on will automatically be considered compliant with no processing performed.

No further events will be logged until the policy is changed.%n
```

## DC Agent Operational log

The DC agent service will also log operational-related events to the following log:

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Operational`

## DC Agent Trace log

The DC agent service can also log verbose debug-level trace events to the following log:

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Trace`

Trace logging is disabled by default.

Warning

When enabled, the Trace log receives a high volume of events and may impact domain controller performance. Therefore, this enhanced log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.

## DC Agent text logging

The DC agent service can be configured to write to a text log by setting the following registry value:

```text
HKLM\System\CurrentControlSet\Services\AzureADPasswordProtectionDCAgent\Parameters!EnableTextLogging = 1 (REG_DWORD value)
```

Text logging is disabled by default. A restart of the DC agent service is required for changes to this value to take effect. When enabled the DC agent service will write to a log file located under:

`%ProgramFiles%\Azure AD Password Protection DC Agent\Logs`

Tip

The text log receives the same debug-level entries that can be logged to the Trace log, but is generally in an easier format to review and analyze.

Warning

When enabled, this log receives a high volume of events and may impact domain controller performance. Therefore, this enhanced log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.

## DC agent performance monitoring

The DC agent service software installs a performance counter object named **Microsoft Entra Password Protection**. The following perf counters are currently available:

| Perf counter name | Description |
| --- | --- |
| Passwords processed | This counter displays the total number of passwords processed (accepted or rejected) since last restart. |
| Passwords accepted | This counter displays the total number of passwords that were accepted since last restart. |
| Passwords rejected | This counter displays the total number of passwords that were rejected since last restart. |
| Password filter requests in progress | This counter displays the number of password filter requests currently in progress. |
| Peak password filter requests | This counter displays the peak number of concurrent password filter requests since the last restart. |
| Password filter request errors | This counter displays the total number of password filter requests that failed due to an error since last restart. Errors can occur when the Microsoft Entra Password Protection DC agent service is not running. |
| Password filter requests/sec | This counter displays the rate at which passwords are being processed. |
| Password filter request processing time | This counter displays the average time required to process a password filter request. |
| Peak password filter request processing time | This counter displays the peak password filter request processing time since the last restart. |
| Passwords accepted due to audit mode | This counter displays the total number of passwords that would normally have been rejected, but were accepted because the password policy was configured to be in audit-mode (since last restart). |

## DC Agent discovery

The `Get-AzureADPasswordProtectionDCAgent` cmdlet may be used to display basic information about the various DC agents running in a domain or forest. This information is retrieved from the serviceConnectionPoint object(s) registered by the running DC agent service(s).

An example output of this cmdlet is as follows:

```powershell
Get-AzureADPasswordProtectionDCAgent
ServerFQDN            : bplChildDC2.bplchild.bplRootDomain.com
Domain                : bplchild.bplRootDomain.com
Forest                : bplRootDomain.com
PasswordPolicyDateUTC : 2/16/2018 8:35:01 AM
HeartbeatUTC          : 2/16/2018 8:35:02 AM
```

The various properties are updated by each DC agent service on an approximate hourly basis. The data is still subject to Active Directory replication latency.

The scope of the cmdlet's query may be influenced using either the –Forest or –Domain parameters.

If the HeartbeatUTC value gets stale, this may be a symptom that the Microsoft Entra Password Protection DC Agent on that domain controller is not running, or has been uninstalled, or the machine was demoted and is no longer a domain controller.

If the PasswordPolicyDateUTC value gets stale, this may be a symptom that the Microsoft Entra Password Protection DC Agent on that machine is not working properly.

## DC agent newer version available

The DC agent service will log a 30034 warning event to the Operational log upon detecting that a newer version of the DC agent software is available, for example:

```text
An update for Azure AD Password Protection DC Agent is available.

If autoupgrade is enabled, this message may be ignored.

If autoupgrade is disabled, refer to the following link for the latest version available:

https://aka.ms/AzureADPasswordProtectionAgentSoftwareVersions

Current version: 1.2.116.0
```

The event above does not specify the version of the newer software. You should go to the link in the event message for that information.

Note

Despite the references to "autoupgrade" in the above event message, the DC agent software does not currently support this feature.

## Proxy service event logging

The Proxy service emits a minimal set of events to the following event logs:

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Admin`

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Operational`

`\Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Trace`

Note that the Trace log is off by default.

Warning

When enabled, the Trace log receives a high volume of events and this may impact performance of the proxy host. Therefore, this log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.

Events are logged by the various Proxy components using the following ranges:

| Component | Event ID range |
| --- | --- |
| Proxy service hosting process | 10000-19999 |
| Proxy service core business logic | 20000-29999 |
| PowerShell cmdlets | 30000-39999 |

## Proxy service text logging

The Proxy service can be configured to write to a text log by setting the following registry value:

HKLM\System\CurrentControlSet\Services\AzureADPasswordProtectionProxy\Parameters!EnableTextLogging = 1 (REG\_DWORD value)

Text logging is disabled by default. A restart of the Proxy service is required for changes to this value to take effect. When enabled the Proxy service will write to a log file located under:

`%ProgramFiles%\Azure AD Password Protection Proxy\Logs`

Tip

The text log receives the same debug-level entries that can be logged to the Trace log, but is generally in an easier format to review and analyze.

Warning

When enabled, this log receives a high volume of events and may impact the machine's performance. Therefore, this enhanced log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.

## PowerShell cmdlet logging

PowerShell cmdlets that result in a state change (for example, Register-AzureADPasswordProtectionProxy) will normally log an outcome event to the Operational log.

In addition, most of the Microsoft Entra Password Protection PowerShell cmdlets will write to a text log located under:

`%ProgramFiles%\Azure AD Password Protection Proxy\Logs`

If a cmdlet error occurs and the cause and\or solution is not readily apparent, these text logs may also be consulted.

## Proxy discovery

The `Get-AzureADPasswordProtectionProxy` cmdlet may be used to display basic information about the various Microsoft Entra Password Protection Proxy services running in a domain or forest. This information is retrieved from the serviceConnectionPoint object(s) registered by the running Proxy service(s).

An example output of this cmdlet is as follows:

```powershell
Get-AzureADPasswordProtectionProxy
ServerFQDN            : bplProxy.bplchild2.bplRootDomain.com
Domain                : bplchild2.bplRootDomain.com
Forest                : bplRootDomain.com
HeartbeatUTC          : 12/25/2018 6:35:02 AM
```

The various properties are updated by each Proxy service on an approximate hourly basis. The data is still subject to Active Directory replication latency.

The scope of the cmdlet's query may be influenced using either the –Forest or –Domain parameters.

If the HeartbeatUTC value gets stale, this may be a symptom that the Microsoft Entra Password Protection Proxy on that machine is not running or has been uninstalled.

## Proxy agent newer version available

The Proxy service will log a 20002 warning event to the Operational log upon detecting that a newer version of the proxy software is available, for example:

```text
An update for Azure AD Password Protection Proxy is available.

If autoupgrade is enabled, this message may be ignored.

If autoupgrade is disabled, refer to the following link for the latest version available:

https://aka.ms/AzureADPasswordProtectionAgentSoftwareVersions

Current version: 1.2.116.0
.
```

The event above does not specify the version of the newer software. You should go to the link in the event message for that information.

This event will be emitted even if the Proxy agent is configured with autoupgrade enabled.