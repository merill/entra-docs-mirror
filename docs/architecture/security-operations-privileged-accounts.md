---
layout: Conceptual
title: Security operations for privileged accounts in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/security-operations-privileged-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn about baselines, and how to monitor and alert on potential security issues with privileged accounts in Microsoft Entra ID.
ms.reviewer: gasinh
ms.topic: how-to
ms.date: 2022-09-06T00:00:00.0000000Z
ms.custom: kr2b-contr-experiment
ms.subservice: architecture
locale: en-us
document_id: 29dfc645-0bee-7f66-8ca5-b27d807503e2
document_version_independent_id: 0e6ad784-c4b9-6c4b-f2f8-d4804dbe711e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/security-operations-privileged-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/security-operations-privileged-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/security-operations-privileged-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d52cfa59-089e-0d8a-a905-d070d9f90c4e
---

# Security operations for privileged accounts in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

The security of business assets depends on the integrity of the privileged accounts that administer your IT systems. Cyber attackers use credential theft attacks and other means to target privileged accounts and gain access to sensitive data.

Traditionally, organizational security has focused on the entry and exit points of a network as the security perimeter. However, software as a service (SaaS) applications and personal devices on the internet have made this approach less effective.

Microsoft Entra ID uses identity and access management (IAM) as the control plane. In your organization's identity layer, users assigned to privileged administrative roles are in control. The accounts used for access must be protected, whether the environment is on-premises, in the cloud, or a hybrid environment.

You're entirely responsible for all layers of security for your on-premises IT environment. When you use Azure services, prevention and response are the joint responsibilities of Microsoft as the cloud service provider and you as the customer.

- For more information on the shared responsibility model, see [Shared responsibility in the cloud](/en-us/azure/security/fundamentals/shared-responsibility).
- For more information on securing access for privileged users, see [Securing privileged access for hybrid and cloud deployments in Microsoft Entra ID](../identity/role-based-access-control/security-planning).
- For a wide range of videos, how-to guides, and content of key concepts for privileged identity, see [Privileged Identity Management documentation](../id-governance/privileged-identity-management/).

## Log files to monitor

The log files you use for investigation and monitoring are:

- [Microsoft Entra audit logs](../identity/monitoring-health/concept-audit-logs)
- [Microsoft 365 Audit logs](/en-us/microsoft-365/compliance/auditing-solutions-overview)
- [Azure Key Vault insights](/en-us/azure/key-vault/key-vault-insights-overview)

From the Azure portal, you can view the Microsoft Entra audit logs and download as comma-separated value (CSV) or JavaScript Object Notation (JSON) files. The Azure portal has several ways to integrate Microsoft Entra logs with other tools that allow for greater automation of monitoring and alerting:

- **[Microsoft Sentinel](/en-us/azure/sentinel/overview)**. Enables intelligent security analytics at the enterprise level by providing security information and event management (SIEM) capabilities.
- **[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure)** - Sigma is an evolving open standard for writing rules and templates that automated management tools can use to parse log files. Where Sigma templates exist for our recommended search criteria, we have added a link to the Sigma repo. The Sigma templates are not written, tested, and managed by Microsoft. Rather, the repo and templates are created and collected by the worldwide IT security community.
- **[Azure Monitor](/en-us/azure/azure-monitor/overview)**. Enables automated monitoring and alerting of various conditions. Can create or use workbooks to combine data from different sources.
- **[Azure Event Hubs](/en-us/azure/event-hubs/event-hubs-about)** integrated with a SIEM. Enables Microsoft Entra logs to be pushed to other SIEMs such as Splunk, ArcSight, QRadar, and Sumo Logic via the Azure Event Hubs integration. For more information, see [Stream Microsoft Entra logs to an Azure event hub](../identity/monitoring-health/howto-stream-logs-to-event-hub).
- **[Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/what-is-cloud-app-security)**. Enables you to discover and manage apps, govern across apps and resources, and check your cloud apps' compliance.
- **Microsoft Graph**. Enables you to export data and use Microsoft Graph to do more analysis. For more information, see [Microsoft Graph PowerShell SDK and Microsoft Entra ID Protection](../id-protection/howto-identity-protection-graph-api).
- **[Microsoft Entra ID Protection](../id-protection/overview-identity-protection)**. Generates three key reports you can use to help with your investigation:

    - **Risky users**. Contains information about which users are at risk, details about detections, history of all risky sign-ins, and risk history.
    - **Risky sign-ins**. Contains information about a sign-in that might indicate suspicious circumstances. For more information on investigating information from this report, see [Investigate risk](../id-protection/howto-identity-protection-investigate-risk).
    - **Risk detections**. Contains information about other risks triggered when a risk is detected and other pertinent information such as sign-in location and any details from Microsoft Defender for Cloud Apps.
- **[Securing workload identities with Microsoft Entra ID Protection](../id-protection/concept-workload-identity-risk)**. Use to detect risk on workload identities across sign-in behavior and offline indicators of compromise.

Although we discourage the practice, privileged accounts can have standing administration rights. If you choose to use standing privileges, and the account is compromised, it can have a strongly negative effect. We recommend you prioritize monitoring privileged accounts and include the accounts in your Privileged Identity Management (PIM) configuration. For more information on PIM, see [Start using Privileged Identity Management](../id-governance/privileged-identity-management/pim-getting-started). Also, we recommend you validate that admin accounts:

- Are required.
- Have the least privilege to execute the require activities.
- Are protected with multifactor authentication at a minimum.
- Are run from privileged access workstation (PAW) or secure admin workstation (SAW) devices.

The rest of this article describes what we recommend you monitor and alert on. The article is organized by the type of threat. Where there are specific prebuilt solutions, we link to them following the table. Otherwise, you can build alerts by using the tools described above.

This article provides details on setting baselines and auditing sign-in and usage of privileged accounts. It also discusses tools and resources you can use to help maintain the integrity of your privileged accounts. The content is organized into the following subjects:

- Emergency "break-glass" accounts
- Privileged account sign-in
- Privileged account changes
- Privileged groups
- Privilege assignment and elevation

## Emergency access accounts

It's important that you prevent being accidentally locked out of your Microsoft Entra tenant.

Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out. These accounts should be created following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).

Send a high-priority alert every time an emergency access account is used.

### Discovery

Because break-glass accounts are only used if there's an emergency, your monitoring should discover no account activity. Send a high-priority alert every time an emergency access account is used or changed. Any of the following events might indicate a bad actor is trying to compromise your environments:

- Sign-in.
- Account password change.
- Account permission or roles changed.
- Credential or auth method added or changed.

For more information on managing emergency access accounts, see [Manage emergency access admin accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access). For detailed information on creating an alert for an emergency account, see [Create an alert rule](../identity/role-based-access-control/security-emergency-access).

## Privileged account sign-in

Monitor all privileged account sign-in activity by using the Microsoft Entra sign-in logs as the data source. In addition to sign-in success and failure information, the logs contain the following details:

- Interrupts
- Device
- Location
- Risk
- Application
- Date and time
- Is the account disabled
- Lockout
- MFA fraud
- Conditional Access failure

### Things to monitor

You can monitor privileged account sign-in events in the Microsoft Entra sign-in logs. Alert on and investigate the following events for privileged accounts.

| What to monitor | Risk level | Where | Filter/subfilter | Notes |
| --- | --- | --- | --- | --- |
| Sign-in failure, bad password threshold | High | Microsoft Entra sign-in log | Status = Failure-and-error code = 50126 | Define a baseline threshold and then monitor and adjust to suit your organizational behaviors and limit false alerts from being generated.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/MultipleDataSources/PrivilegedAccountsSigninFailureSpikes.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Failure because of Conditional Access requirement | High | Microsoft Entra sign-in log | Status = Failure-and-error code = 53003-and-Failure reason = Blocked by Conditional Access | This event can be an indication an attacker is trying to get into the account.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/SigninLogs/UserAccounts-CABlockedSigninSpikes.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Privileged accounts that don't follow naming policy |  | Azure subscription | [List Azure role assignments using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-list-portal) | List role assignments for subscriptions and alert where the sign-in name doesn't match your organization's format. An example is the use of ADM\_ as a prefix. |
| Interrupt | High, medium | Microsoft Entra Sign-ins | Status = Interrupted-and-error code = 50074-and-Failure reason = Strong auth requiredStatus = Interrupted-and-Error code = 500121Failure reason = Authentication failed during strong authentication request | This event can be an indication an attacker has the password for the account but can't pass the multi-factor authentication challenge.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/MultipleDataSources/AADPrivilegedAccountsFailedMFA.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Privileged accounts that don't follow naming policy | High | Microsoft Entra directory | [List Microsoft Entra role assignments](../identity/role-based-access-control/view-assignments) | List role assignments for Microsoft Entra roles and alert where the UPN doesn't match your organization's format. An example is the use of ADM\_ as a prefix. |
| Discover privileged accounts not registered for multi-factor authentication | High | Microsoft Graph API | Query for IsMFARegistered eq false for admin accounts. [List credentialUserRegistrationDetails - Microsoft Graph beta](/en-us/graph/api/reportroot-list-credentialuserregistrationdetails?view=graph-rest-beta&amp;preserve-view=true&amp;tabs=http) | Audit and investigate to determine if the event is intentional or an oversight. |
| Account lockout | High | Microsoft Entra sign-in log | Status = Failure-and-error code = 50053 | Define a baseline threshold, and then monitor and adjust to suit your organizational behaviors and limit false alerts from being generated.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/MultipleDataSources/PrivilegedAccountsLockedOut.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Account disabled or blocked for sign-ins | Low | Microsoft Entra sign-in log | Status = Failure-and-Target = User UPN-and-error code = 50057 | This event could indicate someone is trying to gain access to an account after they've left the organization. Although the account is blocked, it's still important to log and alert on this activity.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/SigninLogs/UserAccounts-BlockedAccounts.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| MFA fraud alert or block | High | Microsoft Entra sign-in log/Azure Log Analytics | Sign-ins&gt;Authentication details Result details = MFA denied, fraud code entered | Privileged user has indicated they haven't instigated the multi-factor authentication prompt, which could indicate an attacker has the password for the account.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/SigninLogs/MFARejectedbyUser.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| MFA fraud alert or block | High | Microsoft Entra audit log log/Azure Log Analytics | Activity type = Fraud reported - User is blocked for MFA or fraud reported - No action taken (based on tenant-level settings for fraud report) | Privileged user has indicated they haven't instigated the multi-factor authentication prompt, which could indicate an attacker has the password for the account.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/SigninLogs/MFARejectedbyUser.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Privileged account sign-ins outside of expected controls |  | Microsoft Entra sign-in log | Status = FailureUserPrincipalName = &lt;Admin account&gt;Location = &lt;unapproved location&gt;IP address = &lt;unapproved IP&gt;Device info = &lt;unapproved Browser, Operating System&gt; | Monitor and alert on any entries that you've defined as unapproved.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/SigninLogs/SuspiciousSignintoPrivilegedAccount.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Outside of normal sign-in times | High | Microsoft Entra sign-in log | Status = Success-and-Location =-and-Time = Outside of working hours | Monitor and alert if sign-ins occur outside of expected times. It's important to find the normal working pattern for each privileged account and to alert if there are unplanned changes outside of normal working times. Sign-ins outside of normal working hours could indicate compromise or possible insider threats.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/MultipleDataSources/AnomolousSignInsBasedonTime.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Microsoft Entra ID Protection risk | High | ID Protection logs | Risk state = At risk-and-Risk level = Low, medium, high-and-Activity = Unfamiliar sign-in/TOR, and so on | This event indicates there's some abnormality detected with the sign-in for the account and should be alerted on. |
| Password change | High | Microsoft Entra audit logs | Activity actor = Admin/self-service-and-Target = User-and-Status = Success or failure | Alert when any administrator account password changes. Write a query for privileged accounts.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/MultipleDataSources/PrivilegedAccountPasswordChanges.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Change in legacy authentication protocol | High | Microsoft Entra sign-in log | Client App = Other client, IMAP, POP3, MAPI, SMTP, and so on-and-Username = UPN-and-Application = Exchange (example) | Many attacks use legacy authentication, so if there's a change in auth protocol for the user, it could be an indication of an attack.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/17ead56ae30b1a8e46bb0f95a458bdeb2d30ba9b/Hunting%20Queries/SigninLogs/LegacyAuthAttempt.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| New device or location | High | Microsoft Entra sign-in log | Device info = Device ID-and-Browser-and-OS-and-Compliant/Managed-and-Target = User-and-Location | Most admin activity should be from [privileged access devices](/en-us/security/compass/privileged-access-devices), from a limited number of locations. For this reason, alert on new devices or locations.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/SigninLogs/SuspiciousSignintoPrivilegedAccount.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Audit alert setting is changed | High | Microsoft Entra audit logs | Service = PIM-and-Category = Role management-and-Activity = Disable PIM alert-and-Status = Success | Changes to a core alert should be alerted if unexpected.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/SecurityAlert/DetectPIMAlertDisablingActivity.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Administrators authenticating to other Microsoft Entra tenants | Medium | Microsoft Entra sign-in log | Status = successResource tenantID != Home Tenant ID | When scoped to Privileged Users, this monitor detects when an administrator has successfully authenticated to another Microsoft Entra tenant with an identity in your organization's tenant. Alert if Resource TenantID isn't equal to Home Tenant ID[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/SigninLogs/AdministratorsAuthenticatingtoAnotherAzureADTenant.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Admin User state changed from Guest to Member | Medium | Microsoft Entra audit logs | Activity: Update userCategory: UserManagementUserType changed from Guest to Member | Monitor and alert on change of user type from Guest to Member. Was this change expected?[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/UserStatechangedfromGuesttoMember.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Guest users invited to tenant by non-approved inviters | Medium | Microsoft Entra audit logs | Activity: Invite external userCategory: UserManagementInitiated by (actor): User Principal Name | Monitor and alert on non-approved actors inviting external users.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/GuestUsersInvitedtoTenantbyNewInviters.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

## Changes by privileged accounts

Monitor all completed and attempted changes by a privileged account. This data enables you to establish what's normal activity for each privileged account and alert on activity that deviates from the expected. The Microsoft Entra audit logs are used to record this type of event. For more information on Microsoft Entra audit logs, see [Audit logs in Microsoft Entra ID](../identity/monitoring-health/concept-audit-logs).

### Microsoft Entra Domain Services

Privileged accounts that have been assigned permissions in Microsoft Entra Domain Services can perform tasks for Microsoft Entra Domain Services that affect the security posture of your Azure-hosted virtual machines that use Microsoft Entra Domain Services. Enable security audits on virtual machines and monitor the logs. For more information on enabling Microsoft Entra Domain Services audits and for a list of sensitive privileges, see the following resources:

- [Enable security audits for Microsoft Entra Domain Services](/en-us/entra/identity/domain-services/security-audit-events)
- [Audit Sensitive Privilege Use](/en-us/windows/security/threat-protection/auditing/audit-sensitive-privilege-use)

| What to monitor | Risk level | Where | Filter/subfilter | Notes |
| --- | --- | --- | --- | --- |
| Attempted and completed changes | High | Microsoft Entra audit logs | Date and time-and-Service-and-Category and name of the activity (what)-and-Status = Success or failure-and-Target-and-Initiator or actor (who) | Any unplanned changes should be alerted on immediately. These logs should be retained to help with any investigation. Any tenant-level changes should be investigated immediately (link out to Infra doc) that would lower the security posture of your tenant. An example is excluding accounts from multifactor authentication or Conditional Access. Alert on any additions or changes to applications. See [Microsoft Entra security operations guide for Applications](security-operations-applications). |
| **Example**Attempted or completed change to high-value apps or services | High | Audit log | Service-and-Category and name of the activity | Date and time, Service, Category and name of the activity, Status = Success or failure, Target, Initiator or actor (who) |
| Privileged changes in Microsoft Entra Domain Services | High | Microsoft Entra Domain Services | Look for event [4673](/en-us/windows/security/threat-protection/auditing/event-4673) | [Enable security audits for Microsoft Entra Domain Services](/en-us/entra/identity/domain-services/security-audit-events)For a list of all privileged events, see [Audit Sensitive Privilege use](/en-us/windows/security/threat-protection/auditing/audit-sensitive-privilege-use). |

## Changes to privileged accounts

Investigate changes to privileged accounts' authentication rules and privileges, especially if the change provides greater privilege or the ability to perform tasks in your Microsoft Entra environment.

| What to monitor | Risk level | Where | Filter/subfilter | Notes |
| --- | --- | --- | --- | --- |
| Privileged account creation | Medium | Microsoft Entra audit logs | Service = Core Directory-and-Category = User management-and-Activity type = Add user-correlate with-Category type = Role management-and-Activity type = Add member to role-and-Modified properties = Role.DisplayName | Monitor creation of any privileged accounts. Look for correlation that's of a short time span between creation and deletion of accounts.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/UserAssignedPrivilegedRole.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Changes to authentication methods | High | Microsoft Entra audit logs | Service = Authentication Method-and-Activity type = User registered security information-and-Category = User management | This change could be an indication of an attacker adding an auth method to the account so they can have continued access.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/MultipleDataSources/AuthenticationMethodsChangedforPrivilegedAccount.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Alert on changes to privileged account permissions | High | Microsoft Entra audit logs | Category = Role management-and-Activity type = Add eligible member (permanent)-or-Activity type = Add eligible member (eligible)-and-Status = Success or failure-and-Modified properties = Role.DisplayName | This alert is especially for accounts being assigned roles that aren't known or are outside of their normal responsibilities.[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Unused privileged accounts | Medium | Microsoft Entra access reviews |  | Perform a monthly review for inactive privileged user accounts.[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Accounts exempt from Conditional Access | High | Azure Monitor Logs-or-Access Reviews | Conditional Access = Insights and reporting | Any account exempt from Conditional Access is most likely bypassing security controls and is more vulnerable to compromise. Break-glass accounts are exempt. See information on how to monitor break-glass accounts later in this article. |
| Addition of a Temporary Access Pass to a privileged account | High | Microsoft Entra audit logs | Activity: Admin registered security infoStatus Reason: Admin registered temporary access pass method for userCategory: UserManagementInitiated by (actor): User Principal NameTarget: User Principal Name | Monitor and alert on a Temporary Access Pass being created for a privileged user.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/tree/master/Detections/AuditLogs/AdditionofaTemporaryAccessPasstoaPrivilegedAccount.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

For more information on how to monitor for exceptions to Conditional Access policies, see [Conditional Access insights and reporting](../identity/conditional-access/howto-conditional-access-insights-reporting).

For more information on discovering unused privileged accounts, see [Create an access review of Microsoft Entra roles in Privileged Identity Management](../id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review).

## Assignment and elevation

Having privileged accounts that are permanently provisioned with elevated abilities can increase the attack surface and risk to your security boundary. Instead, employ just-in-time access by using an elevation procedure. This type of system allows you to assign eligibility for privileged roles. Admins elevate their privileges to those roles only when they perform tasks that need those privileges. Using an elevation process enables you to monitor elevations and non-use of privileged accounts.

### Establish a baseline

To monitor for exceptions, you must first create a baseline. Determine the following information for these elements

- **Admin accounts**

    - Your privileged account strategy
    - Use of on-premises accounts to administer on-premises resources
    - Use of cloud-based accounts to administer cloud-based resources
    - Approach to separating and monitoring administrative permissions for on-premises and cloud-based resources
- **Privileged role protection**

    - Protection strategy for roles that have administrative privileges
    - Organizational policy for using privileged accounts
    - Strategy and principles for maintaining permanent privilege versus providing time-bound and approved access

The following concepts and information help determine policies:

- **Just-in-time admin principles**. Use the Microsoft Entra logs to capture information for performing administrative tasks that are common in your environment. Determine the typical amount of time needed to complete the tasks.
- **Just-enough admin principles**. Determine the least-privileged role, which might be a custom role, that's needed for administrative tasks. For more information, see [Least privileged roles by task in Microsoft Entra ID](../identity/role-based-access-control/delegate-by-task).
- **Establish an elevation policy**. After you have insight into the type of elevated privilege needed and how long is needed for each task, create policies that reflect elevated privileged usage for your environment. As an example, define a policy to limit role elevation to one hour.

After you establish your baseline and set policy, you can configure monitoring to detect and alert usage outside of policy.

### Discovery

Pay particular attention to and investigate changes in assignment and elevation of privilege.

### Things to monitor

You can monitor privileged account changes by using Microsoft Entra audit logs and Azure Monitor logs. Include the following changes in your monitoring process.

| What to monitor | Risk level | Where | Filter/subfilter | Notes |
| --- | --- | --- | --- | --- |
| Added to eligible privileged role | High | Microsoft Entra audit logs | Service = PIM-and-Category = Role management​-and-Activity type = Add member to role completed (eligible)-and-Status = Success or failure​-and-Modified properties = Role.DisplayName | Any account eligible for a role is now being given privileged access. If the assignment is unexpected or into a role that isn't the responsibility of the account holder, investigate.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/UserAssignedPrivilegedRole.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Roles assigned out of PIM | High | Microsoft Entra audit logs | Service = PIM-and-Category = Role management​-and-Activity type = Add member to role (permanent)-and-Status = Success or failure-and-Modified properties = Role.DisplayName | These roles should be closely monitored and alerted. Users shouldn't be assigned roles outside of PIM where possible.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/PrivlegedRoleAssignedOutsidePIM.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Elevations | Medium | Microsoft Entra audit logs | Service = PIM-and-Category = Role management-and-Activity type = Add member to role completed (PIM activation)-and-Status = Success or failure -and-Modified properties = Role.DisplayName | After a privileged account is elevated, it can now make changes that could affect the security of your tenant. All elevations should be logged and, if happening outside of the standard pattern for that user, should be alerted and investigated if not planned. |
| Approvals and deny elevation | Low | Microsoft Entra audit logs | Service = Access Review-and-Category = UserManagement-and-Activity type = Request approved or denied-and-Initiated actor = UPN | Monitor all elevations because it could give a clear indication of the timeline for an attack.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/PIMElevationRequestRejected.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Changes to PIM settings | High | Microsoft Entra audit logs | Service = PIM-and-Category = Role management-and-Activity type = Update role setting in PIM-and-Status reason = MFA on activation disabled (example) | One of these actions could reduce the security of the PIM elevation and make it easier for attackers to acquire a privileged account.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/4ad195f4fe6fdbc66fb8469120381e8277ebed81/Detections/AuditLogs/ChangestoPIMSettings.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Elevation not occurring on SAW/PAW | High | Microsoft Entra sign-in logs | Device ID -and-Browser-and-OS-and-Compliant/ManagedCorrelate with:Service = PIM-and-Category = Role management-and-Activity type = Add member to role completed (PIM activation)-and-Status = Success or failure-and-Modified properties = Role.DisplayName | If this change is configured, any attempt to elevate on a non-PAW/SAW device should be investigated immediately because it could indicate an attacker is trying to use the account.[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Elevation to manage all Azure subscriptions | High | Azure Monitor | Activity Log tab Directory Activity tab  Operations Name = Assigns the caller to user access admin  -and-  Event category = Administrative  -and-Status = Succeeded, start, fail-and-Event initiated by | This change should be investigated immediately if it isn't planned. This setting could allow an attacker access to Azure subscriptions in your environment. |

For more information about managing elevation, see [Elevate access to manage all Azure subscriptions and management groups](/en-us/azure/role-based-access-control/elevate-access-global-admin). For information on monitoring elevations by using information available in the Microsoft Entra logs, see [Azure Activity log](/en-us/azure/azure-monitor/essentials/activity-log), which is part of the Azure Monitor documentation.

For information about configuring alerts for Azure roles, see [Configure security alerts for Azure resource roles in Privileged Identity Management](../id-governance/privileged-identity-management/pim-resource-roles-configure-alerts).