---
layout: Conceptual
title: Microsoft Entra security operations for applications - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/security-operations-applications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn how to monitor and alert on applications to identify security threats.
ms.topic: concept-article
ms.date: 2022-09-06T00:00:00.0000000Z
ms.custom: sfi-ropc-nochange
ms.subservice: architecture
locale: en-us
document_id: d297a528-2190-487d-e4bf-681ad940f65e
document_version_independent_id: 4e7caf28-7ccd-d02d-c630-08a0a7139e45
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/security-operations-applications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/security-operations-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/security-operations-applications.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 01a09429-fa88-bda3-ee9b-a982f497303c
---

# Microsoft Entra security operations for applications - Microsoft Entra | Microsoft Learn

Applications have an attack surface for security breaches and must be monitored. While not targeted as often as user accounts, breaches can occur. Because applications often run without human intervention, the attacks may be harder to detect.

This article provides guidance to monitor and alert on application events. It's regularly updated to help ensure you:

- Prevent malicious applications from getting unwarranted access to data
- Prevent applications from being compromised by bad actors
- Gather insights that enable you to build and configure new applications more securely

If you're unfamiliar with how applications work in Microsoft Entra ID, see [Apps and service principals in Microsoft Entra ID](../identity-platform/app-objects-and-service-principals).

Note

If you have not yet reviewed the [Microsoft Entra security operations overview](security-operations-introduction), consider doing so now.

## What to look for

As you monitor your application logs for security incidents, review the following list to help differentiate normal activity from malicious activity. The following events might indicate security concerns. Each is covered in the article.

- Any changes occurring outside normal business processes and schedules
- Application credentials changes
- Application permissions

    - Service principal assigned to a Microsoft Entra ID or an Azure role-based access control (RBAC) role
    - Applications granted highly privileged permissions
    - Azure Key Vault changes
    - End user granting applications consent
    - Stopped end-user consent based on level of risk
- Application configuration changes

    - Universal resource identifier (URI) changed or non-standard
    - Changes to application owners
    - Log-out URLs modified

## Where to look

The log files you use for investigation and monitoring are:

- [Microsoft Entra audit logs](../identity/monitoring-health/concept-audit-logs)
- [Sign-in logs](../identity/monitoring-health/concept-sign-ins)
- [Microsoft 365 Audit logs](/en-us/purview/audit-solutions-overview)
- [Azure Key Vault logs](/en-us/azure/key-vault/general/logging)

From the Azure portal, you can view the Microsoft Entra audit logs and download as comma-separated value (CSV) or JavaScript Object Notation (JSON) files. The Azure portal has several ways to integrate Microsoft Entra logs with other tools, which allow more automation of monitoring and alerting:

- **[Microsoft Sentinel](/en-us/azure/sentinel/overview)** – enables intelligent security analytics at the enterprise level with security information and event management (SIEM) capabilities.
- **[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure)** - Sigma is an evolving open standard for writing rules and templates that automated management tools can use to parse log files. Where there are Sigma templates for our recommended search criteria, we've added a link to the Sigma repo. The Sigma templates aren't written, tested, and managed by Microsoft. Rather, the repo and templates are created and collected by the worldwide IT security community.
- **[Azure Monitor](/en-us/azure/azure-monitor/overview)** – automated monitoring and alerting of various conditions. Can create or use workbooks to combine data from different sources.
- **[Azure Event Hubs](/en-us/azure/event-hubs/event-hubs-about) integrated with a SIEM**- [Microsoft Entra logs can be integrated to other SIEMs](../identity/monitoring-health/howto-stream-logs-to-event-hub) such as Splunk, ArcSight, QRadar, and Sumo Logic via the Azure Event Hubs integration.
- **[Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)** – discover and manage apps, govern across apps and resources, and check your cloud apps’ compliance.
- **[Securing workload identities with Microsoft Entra ID Protection](../id-protection/concept-workload-identity-risk)** - detects risk on workload identities across sign-in behavior and offline indicators of compromise.

Much of what you monitor and alert on are the effects of your Conditional Access policies. You can use the [Conditional Access insights and reporting workbook](../identity/conditional-access/howto-conditional-access-insights-reporting) to examine the effects of one or more Conditional Access policies on your sign-ins, and the results of policies, including device state. Use the workbook to view a summary, and identify the effects over a time period. You can use the workbook to investigate the sign-ins of a specific user.

The remainder of this article is what we recommend you monitor and alert on. It's organized by the type of threat. Where there are pre-built solutions, we link to them or provide samples after the table. Otherwise, you can build alerts using the preceding tools.

## Application credentials

Many applications use credentials to authenticate in Microsoft Entra ID. Any other credentials added outside expected processes could be a malicious actor using those credentials. We recommend using X509 certificates issued by trusted authorities or Managed Identities instead of using client secrets. However, if you need to use client secrets, follow good hygiene practices to keep applications safe. Note, application and service principal updates are logged as two entries in the audit log.

- Monitor applications to identify long credential expiration times.
- Replace long-lived credentials with a short life span. Ensure credentials don't get committed in code repositories, and are stored securely.

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Added credentials to existing applications | High | Microsoft Entra audit logs | Service-Core Directory, Category-ApplicationManagement Activity: Update Application-Certificates and secrets management-and-Activity: Update Service principal/Update Application | Alert when credentials are: added outside of normal business hours or workflows, of types not used in your environment, or added to a non-SAML flow supporting service principal.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/NewAppOrServicePrincipalCredential.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Credentials with a lifetime longer than your policies allow. | Medium | Microsoft Graph | State and end date of Application Key credentials-and-Application password credentials | You can use MS Graph API to find the start and end date of credentials, and evaluate longer-than-allowed lifetimes. See PowerShell script following this table. |

The following pre-built monitoring and alerts are available:

- Microsoft Sentinel – [Alert when new app or service principle credentials added](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/NewAppOrServicePrincipalCredential.yaml)
- Azure Monitor – [Microsoft Entra workbook to help you assess Solorigate risk - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/azure-ad-workbook-to-help-you-assess-solorigate-risk/ba-p/2010718)
- Defender for Cloud Apps – [Defender for Cloud Apps anomaly detection alerts investigation guide](/en-us/defender-cloud-apps/investigate-anomaly-alerts)
- PowerShell - [Sample PowerShell script to find credential lifetime](https://github.com/madansr7/appCredAge).

## Application permissions

Like an administrator account, applications can be assigned privileged roles. Apps can be assigned any Microsoft Entra roles, such as [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator), or Azure RBAC roles such as [Billing Reader](/en-us/azure/role-based-access-control/built-in-roles/management-and-governance#billing-reader). Because they can run without a user, and as a background service, closely monitor when an application is granted privileged roles or permissions.

### Service principal assigned to a role

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| App assigned to Azure RBAC role, or Microsoft Entra role | High to Medium | Microsoft Entra audit logs | Type: service principalActivity: “Add member to role” or “Add eligible member to role”-or-“Add scoped member to role.” | For highly privileged roles risk is high. For lower privileged roles risk is medium. Alert anytime an application is assigned to an Azure role or Microsoft Entra role outside of normal change management or configuration procedures.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ServicePrincipalAssignedPrivilegedRole.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

### Application granted highly privileged permissions

Applications should follow the principle of least privilege. Investigate application permissions to ensure they're needed. You can create an [app consent grant report](https://aka.ms/getazureadpermissions) to help identify applications and highlight privileged permissions.

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| App granted highly privileged permissions, such as permissions with “*.All” (Directory.ReadWrite.All) or wide ranging permissions (Mail.*) | High | Microsoft Entra audit logs | “Add app role assignment to service principal”, - where- Target(s) identifies an API with sensitive data (such as Microsoft Graph) -and-AppRole.Value identifies a highly privileged application permission (app role). | Apps granted broad permissions such as “*.All” (Directory.ReadWrite.All) or wide ranging permissions (Mail.*)[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ServicePrincipalAssignedAppRoleWithSensitiveAccess.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Administrator granting either application permissions (app roles) or highly privileged delegated permissions | High | Microsoft 365 portal | “Add app role assignment to service principal”, -where-Target(s) identifies an API with sensitive data (such as Microsoft Graph)“Add delegated permission grant”, -where-Target(s) identifies an API with sensitive data (such as Microsoft Graph) -and-DelegatedPermissionGrant.Scope includes high-privilege permissions. | Alert when an administrator consents to an application. Especially look for consent outside of normal activity and change procedures.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ServicePrincipalAssignedAppRoleWithSensitiveAccess.yaml)[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/AzureADRoleManagementPermissionGrant.yaml)[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/MailPermissionsAddedToApplication.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Application is granted permissions for Microsoft Graph, Exchange, SharePoint, or Microsoft Entra ID. | High | Microsoft Entra audit logs | “Add delegated permission grant” -or-“Add app role assignment to service principal”, -where-Target(s) identifies an API with sensitive data (such as Microsoft Graph, Exchange Online, and so on) | Alert as in the preceding row.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ServicePrincipalAssignedAppRoleWithSensitiveAccess.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Application permissions (app roles) for other APIs are granted | Medium | Microsoft Entra audit logs | “Add app role assignment to service principal”, -where-Target(s) identifies any other API. | Alert as in the preceding row.[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Highly privileged delegated permissions are granted on behalf of all users | High | Microsoft Entra audit logs | “Add delegated permission grant”, where Target(s) identifies an API with sensitive data (such as Microsoft Graph),  DelegatedPermissionGrant.Scope includes high-privilege permissions, -and-DelegatedPermissionGrant.ConsentType is “AllPrincipals”. | Alert as in the preceding row.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ServicePrincipalAssignedAppRoleWithSensitiveAccess.yaml)[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/AzureADRoleManagementPermissionGrant.yaml)[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/SuspiciousOAuthApp_OfflineAccess.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

For more information on monitoring app permissions, see this tutorial: [Investigate and remediate risky OAuth apps](/en-us/defender-cloud-apps/investigate-risky-oauth).

### Azure Key Vault

Use Azure Key Vault to store your tenant’s secrets. We recommend you pay attention to any changes to Key Vault configuration and activities.

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| How and when your Key Vaults are accessed and by whom | Medium | [Azure Key Vault logs](/en-us/azure/key-vault/general/logging?tabs=Vault) | Resource type: Key Vaults | Look for: any access to Key Vault outside regular processes and hours, any changes to Key Vault ACL.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/AzureDiagnostics/AzureKeyVaultAccessManipulation.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

After you set up Azure Key Vault, [enable logging](/en-us/azure/key-vault/general/howto-logging?tabs=azure-cli). See [how and when your Key Vaults are accessed](/en-us/azure/key-vault/general/logging?tabs=Vault), and [configure alerts](/en-us/azure/key-vault/general/alert) on Key Vault to notify assigned users or distribution lists via email, phone, text, or [Event Grid](/en-us/azure/key-vault/general/event-grid-overview) notification, if health is affected. In addition, setting up [monitoring](/en-us/azure/key-vault/general/alert) with Key Vault insights gives you a snapshot of Key Vault requests, performance, failures, and latency. [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) also has some [example queries](/en-us/azure/azure-monitor/logs/queries) for Azure Key Vault that can be accessed after selecting your Key Vault and then under “Monitoring” selecting “Logs”.

### End-user consent

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| End-user consent to application | Low | Microsoft Entra audit logs | Activity: Consent to application / ConsentContext.IsAdminConsent = false | Look for: high profile or highly privileged accounts, app requests high-risk permissions, apps with suspicious names, for example generic, misspelled, and so on.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/AuditLogs/ConsentToApplicationDiscovery.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

The act of consenting to an application isn't malicious. However, investigate new end-user consent grants looking for suspicious applications. You can [restrict user consent operations](/en-us/azure/security/fundamentals/steps-secure-identity).

For more information on consent operations, see the following resources:

- [Managing consent to applications and evaluating consent requests in Microsoft Entra ID](../identity/enterprise-apps/manage-consent-requests)
- [Detect and Remediate Illicit Consent Grants - Office 365](/en-us/microsoft-365/security/office-365-security/detect-and-remediate-illicit-consent-grants)
- [Incident response playbook - App consent grant investigation](/en-us/security/operations/incident-response-playbook-app-consent)

### End user stopped due to risk-based consent

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| End-user consent stopped due to risk-based consent | Medium | Microsoft Entra audit logs | Core Directory / ApplicationManagement / Consent to application Failure status reason = Microsoft.online.Security.userConsentBlockedForRiskyAppsExceptions | Monitor and analyze any time consent is stopped due to risk. Look for: high profile or highly privileged accounts, app requests high-risk permissions, or apps with suspicious names, for example generic, misspelled, and so on.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/End-userconsentstoppedduetorisk-basedconsent.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

## Application authentication flows

There are several flows in the OAuth 2.0 protocol. The recommended flow for an application depends on the type of application being built. In some cases, there's a choice of flows available to the application. For this case, some authentication flows are recommended over others. Specifically, avoid resource owner password credentials (ROPC) because these require the user to expose their current password credentials to the application. The application then uses the credentials to authenticate the user against the identity provider. Most applications should use the auth code flow, or auth code flow with Proof Key for Code Exchange (PKCE), because this flow is recommended.

The only scenario where ROPC is suggested is for automated application testing. See [Run automated integration tests](../identity-platform/test-automate-integration-testing) for details.

Device code flow is another OAuth 2.0 protocol flow for input-constrained devices and isn't used in all environments. When device code flow appears in the environment, and isn't used in an input constrained device scenario. More investigation is warranted for a misconfigured application or potentially something malicious. Device code flow can also be blocked or allowed in Conditional Access. See [Conditional Access authentication flows](../identity/conditional-access/concept-authentication-flows#device-code-flow) for details.

Monitor application authentication using the following formation:

| What to monitor | Risk level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Applications that are using the ROPC authentication flow | Medium | Microsoft Entra sign-in log | Status=SuccessAuthentication Protocol-ROPC | High level of trust is being placed in this application as the credentials can be cached or stored. Move if possible to a more secure authentication flow. This should only be used in automated testing of applications, if at all. For more information, see [Microsoft identity platform and OAuth 2.0 Resource Owner Password Credentials](../identity-platform/v2-oauth-ropc)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Applications using the Device code flow | Low to medium | Microsoft Entra sign-in log | Status=SuccessAuthentication Protocol-Device Code | Device code flows are used for input constrained devices, which may not be in all environments. If successful device code flows appear, without a need for them, investigate for validity. For more information, see [Microsoft identity platform and the OAuth 2.0 device authorization grant flow](../identity-platform/v2-oauth2-device-code)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

## Application configuration changes

Monitor changes to application configuration. Specifically, configuration changes to the uniform resource identifier (URI), ownership, and log-out URL.

### Dangling URI and Redirect URI changes

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Dangling URI | High | Microsoft Entra logs and Application Registration | Service-Core Directory, Category-ApplicationManagementActivity: Update ApplicationSuccess – Property Name AppAddress | For example, look for dangling URIs that point to a domain name that no longer exists or one that you don’t explicitly own.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/URLAddedtoApplicationfromUnknownDomain.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Redirect URI configuration changes | High | Microsoft Entra logs | Service-Core Directory, Category-ApplicationManagementActivity: Update ApplicationSuccess – Property Name AppAddress | Look for URIs not using HTTPS\*, URIs with wildcards at the end or the domain of the URL, URIs that are NOT unique to the application, URIs that point to a domain you don't control.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ApplicationRedirectURLUpdate.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

Alert when these changes are detected.

### AppID URI added, modified, or removed

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Changes to AppID URI | High | Microsoft Entra logs | Service-Core Directory, Category-ApplicationManagementActivity: UpdateApplicationActivity: Update Service principal | Look for any AppID URI modifications, such as adding, modifying, or removing the URI.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ApplicationIDURIChanged.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

Alert when these changes are detected outside approved change management procedures.

### New owner

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Changes to application ownership | Medium | Microsoft Entra logs | Service-Core Directory, Category-ApplicationManagementActivity: Add owner to application | Look for any instance of a user being added as an application owner outside of normal change management activities.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ChangestoApplicationOwnership.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

### Log-out URL modified or removed

| What to monitor | Risk Level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Changes to log-out URL | Low | Microsoft Entra logs | Service-Core Directory, Category-ApplicationManagementActivity: Update Application-and-Activity: Update service principle | Look for any modifications to a sign-out URL. Blank entries or entries to non-existent locations would stop a user from terminating a session.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ChangestoApplicationLogoutURL.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

## Resources

- GitHub Microsoft Entra toolkit - https://github.com/microsoft/AzureADToolkit
- Azure Key Vault security overview and security guidance - [Azure Key Vault security overview](/en-us/azure/key-vault/general/security-features)
- Solorigate risk information and tools - [Microsoft Entra workbook to help you access Solorigate risk](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/azure-ad-workbook-to-help-you-assess-solorigate-risk/ba-p/2010718)
- OAuth attack detection guidance - [Unusual addition of credentials to an OAuth app](/en-us/defender-cloud-apps/investigate-anomaly-alerts)
- Microsoft Entra monitoring configuration information for SIEMs - [Partner tools with Azure Monitor integration](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs)