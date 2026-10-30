---
layout: Conceptual
title: Roles across Microsoft services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/m365-workload-docs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Find content, API references, and audit and monitoring references related to role-based access control (RBAC) for Microsoft 365 and other services
ms.topic: reference
ms.date: 2024-08-31T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, sfi-ga-nochange
locale: en-us
document_id: 7a69ea97-18b4-0984-0972-54d2d7e865a4
document_version_independent_id: 6858b35c-e4b9-60d0-eb4c-6c68b453de55
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/m365-workload-docs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/m365-workload-docs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/m365-workload-docs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 7d3f0fc0-21a4-1f9f-b905-ea312b7c17d6
---

# Roles across Microsoft services - Microsoft Entra ID | Microsoft Learn

Services in Microsoft 365 can be managed with administrative roles in Microsoft Entra ID. Some services also provide additional roles that are specific to that service. This article lists content, API references, and audit and monitoring references related to role-based access control (RBAC) for Microsoft 365 and other services.

## Microsoft Entra

Microsoft Entra ID and related services in Microsoft Entra.

### Microsoft Entra ID

| Area | Content |
| --- | --- |
| Overview | [Microsoft Entra built-in roles](permissions-reference) |
| Management API reference | **Microsoft Entra roles**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• When role is assigned to a group, manage group memberships with the [Microsoft Graph v1.0 groups API](/en-us/graph/api/resources/groups-overview) |
| Audit and monitoring reference | **Microsoft Entra roles**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category• When a role is assigned to a group, to audit changes to group memberships, see audits with category `GroupManagement` and activities `Add member to group` and `Remove member from group` |

### Entitlement management

| Area | Content |
| --- | --- |
| Overview | [Entitlement management roles](/en-us/entra/id-governance/entitlement-management-delegate#entitlement-management-roles) |
| Management API reference | **Entitlement Management-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with: `microsoft.directory/entitlementManagement`**Entitlement Management-specific roles**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `entitlementManagement` provider |
| Audit and monitoring reference | **Entitlement Management-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category**Entitlement Management-specific roles**In Microsoft Entra audit log, with category `EntitlementManagement` and Activity is one of:• `Remove Entitlement Management role assignment`• `Add Entitlement Management role assignment` |

## Microsoft 365

Services in the Microsoft 365 suite.

### Exchange

| Area | Content |
| --- | --- |
| Overview | [Permissions in Exchange Online](/en-us/exchange/permissions-exo/permissions-exo) |
| Management API reference | **Exchange-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• Roles with permissions starting with: `microsoft.office365.exchange`**Exchange-specific roles**[Microsoft Graph Beta roleManagement API](/en-us/graph/api/resources/rolemanagement?view=graph-rest-beta&amp;preserve-view=true)• Use `exchange` provider |
| Audit and monitoring reference | **Exchange-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category**Exchange-specific roles**Use the [Microsoft Graph Beta Security API](/en-us/graph/api/resources/security-api-overview?view=graph-rest-beta&amp;preserve-view=true#audit-logs-query-preview) ([audit log query](/en-us/graph/api/resources/security-auditlogquery)) and list audit events where recordType == `ExchangeAdmin` and Operation is one of:`Add-RoleGroupMember`, `Remove-RoleGroupMember`, `Update-RoleGroupMember`, `New-RoleGroup`, `Remove-RoleGroup`, `New-ManagementRole`, `Remove-ManagementRoleEntry`, `New-ManagementRoleAssignment` |

### SharePoint

Includes SharePoint, OneDrive, Delve, Lists, Project Online, and Loop.

| Area | Content |
| --- | --- |
| Overview | [About the SharePoint Administrator role in Microsoft 365](/en-us/sharepoint/sharepoint-admin-role)[Delve for admins](/en-us/sharepoint/delve-for-office-365-admins)[Control settings for Microsoft Lists](/en-us/sharepoint/control-lists)[Change permission management in Project Online](/en-us/projectonline/change-permission-management-in-project-online) |
| Management API reference | **SharePoint-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• Roles with permissions starting with: `microsoft.office365.sharepoint` |
| Audit and monitoring reference | **SharePoint-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Intune

| Area | Content |
| --- | --- |
| Overview | [Role-based access control (RBAC) with Microsoft Intune](/en-us/mem/intune/fundamentals/role-based-access-control) |
| Management API reference | **Intune-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• Roles with permissions starting with: `microsoft.intune`**Intune-specific roles**[Microsoft Graph Beta roleManagement API](/en-us/graph/api/resources/rolemanagement?view=graph-rest-beta&amp;preserve-view=true)• Use `deviceManagement` provider• Alternatively, use Intune-specific [Microsoft Graph Beta RBAC management API](/en-us/graph/api/resources/intune-rbac-conceptual?view=graph-rest-beta&amp;preserve-view=true) |
| Audit and monitoring reference | **Intune-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• `RoleManagement` category**Intune-specific roles**[Intune auditing overview](/en-us/mem/intune/fundamentals/monitor-audit-logs)API access to Intune-specific audit logs:• [Microsoft Graph Beta getAuditActivityTypes API](/en-us/graph/api/intune-auditing-auditevent-getauditactivitytypes?view=graph-rest-beta&amp;preserve-view=true)• First list activity types where category=`Role`, then use [Microsoft Graph Beta auditEvents API](/en-us/graph/api/intune-auditing-auditevent-list?view=graph-rest-beta&amp;preserve-view=true) to list all auditEvents for each activity type |

### Teams

Includes Teams, Bookings, Copilot Studio for Teams, and Shifts.

| Area | Content |
| --- | --- |
| Overview | [Use Microsoft Teams administrator roles to manage Teams](/en-us/microsoftteams/using-admin-roles) |
| Management API reference | **Teams-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• Roles with permissions starting with: `microsoft.teams` |
| Audit and monitoring reference | **Teams-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Purview suite

Includes Purview suite, Azure Information Protection, and Information Barriers.

| Area | Content |
| --- | --- |
| Overview | [Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview](/en-us/defender-office-365/scc-permissions) |
| Management API reference | **Purview-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with:`microsoft.office365.complianceManager``microsoft.office365.protectionCenter``microsoft.office365.securityComplianceCenter`**Purview-specific roles**Use PowerShell: [Security & Compliance PowerShell](/en-us/powershell/exchange/scc-powershell). Specific cmdlets are:[Get-RoleGroup](/en-us/powershell/module/exchange/get-rolegroup)[Get-RoleGroupMember](/en-us/powershell/module/exchange/get-rolegroupmember)[New-RoleGroup](/en-us/powershell/module/exchange/new-rolegroup)[Add-RoleGroupMember](/en-us/powershell/module/exchange/add-rolegroupmember)[Update-RoleGroupMember](/en-us/powershell/module/exchange/update-rolegroupmember)[Remove-RoleGroupMember](/en-us/powershell/module/exchange/remove-rolegroupmember)[Remove-RoleGroup](/en-us/powershell/module/exchange/remove-rolegroup) |
| Audit and monitoring reference | **Purview-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category**Purview-specific roles**Use the [Microsoft Graph Beta Security API](/en-us/graph/api/resources/security-api-overview?view=graph-rest-beta&amp;preserve-view=true#audit-logs-query-preview) ([audit log query Beta](/en-us/graph/api/resources/security-auditlogquery?view=graph-rest-beta&amp;preserve-view=true)) and list audit events where recordType == `SecurityComplianceRBAC` and Operation is one of `Add-RoleGroupMember`, `Remove-RoleGroupMember`, `Update-RoleGroupMember`, `New-RoleGroup`, `Remove-RoleGroup` |

### Power Platform

Includes Power Platform, Dynamics 365, Flow, and Dataverse for Teams.

| Area | Content |
| --- | --- |
| Overview | [Use service admin roles to manage your tenant](/en-us/power-platform/admin/use-service-admin-role-manage-tenant)[Security roles and privileges](/en-us/power-platform/admin/security-roles-privileges) |
| Management API reference | **Power Platform-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with:`microsoft.powerApps``microsoft.dynamics365``microsoft.flow`**Dataverse-specific roles**[Perform operations using the Web API](/en-us/power-apps/developer/data-platform/webapi/perform-operations-web-api)• Query the [User (SystemUser) table/entity reference](/en-us/power-apps/developer/data-platform/reference/entities/systemuser)• Role assignments are part of the [systemuserroles_association](/en-us/power-apps/developer/data-platform/reference/entities/systemuser#BKMK_systemuserroles_association) tables |
| Audit and monitoring reference | **Power Platform-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category**Dataverse-specific roles**[Dataverse auditing overview](/en-us/power-platform/admin/manage-dataverse-auditing)API to access dataverse-specific audit logs[Dataverse Web API](/en-us/power-apps/developer/data-platform/webapi/perform-operations-web-api)• [Audit table reference](/en-us/power-apps/developer/data-platform/reference/entities/audit)• Audits with [action codes](/en-us/power-apps/developer/data-platform/reference/entities/audit#action-choicesoptions):53 – Assign Role To Team54 – Remove Role From Team55 – Assign Role To User56 – Remove Role From User57 – Add Privileges to Role58 – Remove Privileges From Role59 – Replace Privileges In Role |

### Defender suite

Includes Defender suite, Secure Score, Cloud App Security, and Threat Intelligence.

| Area | Content |
| --- | --- |
| Overview | [Microsoft Defender XDR Unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) |
| Management API reference | **Defender-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• The following roles have permissions ([reference](/en-us/microsoft-365/security/defender/m365d-permissions)): Security Administrator, Security Operator, Security Reader, Global Administrator, and Global Reader**Defender-specific roles**Workloads must be activated to use Defender unified RBAC. See [Activate Microsoft Defender XDR Unified role-based access control (RBAC)](/en-us/microsoft-365/security/defender/activate-defender-rbac). Activating defender Unified RBAC will turn off individual Defender solution roles.• Can only be managed via security.microsoft.com portal. |
| Audit and monitoring reference | **Defender-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Viva Engage

| Area | Content |
| --- | --- |
| Overview | [Manage administrator roles in Viva Engage](/en-us/viva/engage/eac-key-admin-roles-permissions) |
| Management API reference | **Viva Engage-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.office365.yammer`.**Viva Engage-specific roles**• Verified admin and Network admin roles can be managed via the Yammer admin center.• Corporate communicator role can be assigned via the Viva Engage admin center.• [Yammer Data Export API](/en-us/rest/api/yammer/network-data-export) can be used to export admins.csv to read the list of admins |
| Audit and monitoring reference | **Viva Engage-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category**Viva Engage-specific roles**• Use [Yammer Data Export API](/en-us/rest/api/yammer/network-data-export) to incrementally export admins.csv for a list of admins |

### Viva Connections

| Area | Content |
| --- | --- |
| Overview | [Admin roles and tasks in Microsoft Viva](/en-us/viva/microsoft-viva-admin-roles#viva-connections) |
| Management API reference | **Viva Connections-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• The following roles have permissions: SharePoint Administrator, Teams Administrator, and Global Administrator |
| Audit and monitoring reference | **Viva Connections-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Viva Learning

| Area | Content |
| --- | --- |
| Overview | [Set up Microsoft Viva Learning in the Teams admin center](/en-us/viva/learning/set-up-viva-learning#admin-roles-and-permissions) |
| Management API reference | **Viva Learning-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.office365.knowledge` |
| Audit and monitoring reference | **Viva Learning-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Viva Insights

| Area | Content |
| --- | --- |
| Overview | [Roles in Viva Insights](/en-us/viva/insights/advanced/setup-maint/user-roles) |
| Management API reference | **Viva Insights-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.office365.insights` |
| Audit and monitoring reference | **Viva Insights-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Search

| Area | Content |
| --- | --- |
| Overview | [Set up Microsoft Search](/en-us/microsoftsearch/setup-microsoft-search) |
| Management API reference | **Search-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.office365.search` |
| Audit and monitoring reference | **Search-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Universal Print

| Area | Content |
| --- | --- |
| Overview | [Universal Print Administrator Roles](/en-us/universal-print/fundamentals/universal-print-administrator-roles) |
| Management API reference | **Universal Print-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.azure.print` |
| Audit and monitoring reference | **Universal Print-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

### Microsoft 365 Apps suite management

Includes Microsoft 365 Apps suite management and Forms.

| Area | Content |
| --- | --- |
| Overview | [Overview of the Microsoft 365 Apps admin center](/en-us/microsoft-365-apps/admin-center/overview)[Administrator settings for Microsoft Forms](/en-us/microsoft-forms/administrator-settings-microsoft-forms) |
| Management API reference | **Microsoft 365 Apps-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• The following roles have permissions: Office Apps Administrator, Security Administrator, Global Administrator |
| Audit and monitoring reference | **Microsoft 365 Apps-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with `RoleManagement` category |

## Azure

Azure role-based access control (Azure RBAC) for the Azure control plane and subscription information.

### Azure

Includes Azure and Sentinel.

| Area | Content |
| --- | --- |
| Overview | [What is Azure role-based access control (Azure RBAC)?](/en-us/azure/role-based-access-control/overview)[Roles and permissions in Microsoft Sentinel](/en-us/azure/sentinel/roles) |
| Management API reference | **Azure service-specific roles in Azure**[Azure Resource Manager Authorization API](/en-us/rest/api/authorization)• Role assignment: [List](/en-us/azure/role-based-access-control/role-assignments-list-rest), [Create/Update](/en-us/azure/role-based-access-control/role-assignments-rest), [Delete](/en-us/azure/role-based-access-control/role-assignments-remove#rest-api)• Role definition: [List](/en-us/rest/api/authorization/role-definitions/list), [Create/Update](/en-us/rest/api/authorization/role-definitions/create-or-update), [Delete](/en-us/rest/api/authorization/role-definitions/delete)• There is a legacy method to grant access to Azure resources called [classic administrators](/en-us/azure/role-based-access-control/classic-administrators). Classic administrators are equivalent to the Owner role in Azure RBAC. Classic administrators will be retired in August 2024.• Note that an Microsoft Entra Global Administrator can gain unilateral access to Azure via [elevate access](/en-us/azure/role-based-access-control/elevate-access-global-admin). |
| Audit and monitoring reference | **Azure service-specific roles in Azure**[Monitor Azure RBAC changes in the Azure Activity Log](/en-us/azure/role-based-access-control/change-history-report)• [Azure Activity Log API](/en-us/rest/api/monitor/activity-logs/list)• Audits with Event Category `Administrative` and Operation `Create role assignment`, `Delete role assignment`, `Create or update custom role definition`, `Delete custom role definition`.[View Elevate Access logs in the tenant level Azure Activity Log](/en-us/azure/role-based-access-control/elevate-access-global-admin#view-elevate-access-log-entries-in-the-directory-activity-logs)• [Azure Activity Log API – Tenant Activity Logs](/en-us/rest/api/monitor/tenant-activity-logs/list)• Audits with Event Category `Administrative` and containing string `elevateAccess`.• Access to tenant level activity logs requires using [elevate access](/en-us/azure/role-based-access-control/elevate-access-global-admin) at least once to gain tenant level access. |

## Commerce

Services related to purchasing and billing.

### Cost Management and Billing – Enterprise Agreements

| Area | Content |
| --- | --- |
| Overview | [Managing Azure Enterprise Agreement roles](/en-us/azure/cost-management-billing/manage/understand-ea-roles) |
| Management API reference | **Enterprise Agreements-specific roles in Microsoft Entra ID**Enterprise Agreements does not support Microsoft Entra roles.**Enterprise Agreements-specific roles**[Billing Role Assignments API](/en-us/rest/api/billing/role-assignments)• Enterprise Administrator (Role ID: 9f1983cb-2574-400c-87e9-34cf8e2280db)• Enterprise Administrator (read only) (Role ID: 24f8edb6-1668-4659-b5e2-40bb5f3a7d7e)• EA Purchaser (Role ID: da6647fb-7651-49ee-be91-c43c4877f0c4)[Enrollment Department Role Assignments API](/en-us/rest/api/billing/enrollment-department-role-assignments)• Department Admin (Role ID: fb2cf67f-be5b-42e7-8025-4683c668f840)• Department Reader (Role ID: db609904-a47f-4794-9be8-9bd86fbffd8a)[Enrollment Account Role Assignments API](/en-us/rest/api/billing/enrollment-account-role-assignments)• Account Owner (Role ID: c15c22c0-9faf-424c-9b7e-bd91c06a240b) |
| Audit and monitoring reference | **Enterprise Agreements-specific roles**[Azure Activity Log API – Tenant Activity Logs](/en-us/rest/api/monitor/tenant-activity-logs/list)• Access to tenant level activity logs requires using [elevate access](/en-us/azure/role-based-access-control/elevate-access-global-admin) at least once to gain tenant level access.• Audits where resourceProvider == `Microsoft.Billing` and operationName contains `billingRoleAssignments` or `EnrollmentAccount` |

### Cost Management and Billing – Microsoft Customer Agreements

| Area | Content |
| --- | --- |
| Overview | [Understand Microsoft Customer Agreement administrative roles in Azure](/en-us/azure/cost-management-billing/manage/understand-mca-roles)[Understand your Microsoft business billing account](/en-us/microsoft-365/commerce/manage-billing-accounts#what-are-billing-account-roles) |
| Management API reference | **Microsoft Customer Agreements-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• The following roles have permissions: Billing Administrator, Global Administrator.**Microsoft Customer Agreements-specific roles**• By default, the Microsoft Entra Global Administrator and Billing Administrator roles are automatically assigned the Billing Account Owner role in Microsoft Customer Agreements-specific RBAC.• [Billing Role Assignment API](/en-us/rest/api/billing/billing-role-assignments) |
| Audit and monitoring reference | **Microsoft Customer Agreements-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with category `RoleManagement`**Microsoft Customer Agreements-specific roles**[Azure Activity Log API – Tenant Activity Logs](/en-us/rest/api/monitor/tenant-activity-logs/list)• Access to tenant level activity logs requires using [elevate access](/en-us/azure/role-based-access-control/elevate-access-global-admin) at least once to gain tenant level access.• Audits where resourceProvider == `Microsoft.Billing` and operationName one of the following (all prefixed with `Microsoft.Billing`):`/permissionRequests/write``/billingAccounts/createBillingRoleAssignment/action``/billingAccounts/billingProfiles/createBillingRoleAssignment/action``/billingAccounts/billingProfiles/invoiceSections/createBillingRoleAssignment/action``/billingAccounts/customers/createBillingRoleAssignment/action``/billingAccounts/billingRoleAssignments/write``/billingAccounts/billingRoleAssignments/delete``/billingAccounts/billingProfiles/billingRoleAssignments/delete``/billingAccounts/billingProfiles/customers/createBillingRoleAssignment/action``/billingAccounts/billingProfiles/invoiceSections/billingRoleAssignments/delete``/billingAccounts/departments/billingRoleAssignments/write``/billingAccounts/departments/billingRoleAssignments/delete``/billingAccounts/enrollmentAccounts/transferBillingSubscriptions/action``/billingAccounts/enrollmentAccounts/billingRoleAssignments/write``/billingAccounts/enrollmentAccounts/billingRoleAssignments/delete``/billingAccounts/billingProfiles/invoiceSections/billingSubscriptions/transfer/action``/billingAccounts/billingProfiles/invoiceSections/initiateTransfer/action``/billingAccounts/billingProfiles/invoiceSections/transfers/delete``/billingAccounts/billingProfiles/invoiceSections/transfers/cancel/action``/billingAccounts/billingProfiles/invoiceSections/transfers/write``/transfers/acceptTransfer/action``/transfers/accept/action``/transfers/decline/action``/transfers/declineTransfer/action``/billingAccounts/customers/initiateTransfer/action``/billingAccounts/customers/transfers/delete``/billingAccounts/customers/transfers/cancel/action``/billingAccounts/customers/transfers/write``/billingAccounts/billingProfiles/invoiceSections/products/transfer/action``/billingAccounts/billingSubscriptions/elevateRole/action` |

### Business Subscriptions and Billing – Volume Licensing

| Area | Content |
| --- | --- |
| Overview | [Manage volume licensing user roles Frequently Asked Questions](/en-us/microsoft-365/commerce/licenses/user-roles-faq) |
| Management API reference | **Volume Licensing-specific roles in Microsoft Entra ID**Volume Licensing does not support Microsoft Entra roles.**Volume Licensing-specific roles**[VL users and roles](/en-us/microsoft-365/commerce/licenses/user-roles-faq#how-do-i-manage-vl-users-and-roles) are managed in the M365 Admin Center. |

### Partner Center

| Area | Content |
| --- | --- |
| Overview | [Roles, permissions, and workspace access for users](/en-us/partner-center/permissions-overview) |
| Management API reference | **Partner Center-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• The following roles have permissions: Global Administrator, User Administrator.**Partner Center-specific roles**[Partner Center-specific roles](/en-us/partner-center/permissions-overview#microsoft-entra-tenant-roles-and-non-azure-ad-roles) can only be managed via Partner Center. |
| Audit and monitoring reference | **Partner Center-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with category `RoleManagement` |

## Other services

### Azure DevOps

| Area | Content |
| --- | --- |
| Overview | [About permissions and security groups](/en-us/azure/devops/organizations/security/about-permissions) |
| Management API reference | **Azure DevOps-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.azure.devOps`.**Azure DevOps-specific roles**Create/read/update/delete permissions granted via [Roleassignments API](/en-us/rest/api/azure/devops/securityroles/roleassignments)• View permissions of roles with [Roledefinitions API](/en-us/rest/api/azure/devops/securityroles/roledefinitions)• [Permissions reference topic](/en-us/azure/devops/organizations/security/permissions)• When an Azure DevOps group (note: different from Microsoft Entra group) is assigned to a role, create/read/update/delete group memberships with the [Memberships API](/en-us/rest/api/azure/devops/graph/memberships) |
| Audit and monitoring reference | **Azure DevOps-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with category `RoleManagement`**Azure DevOps-specific roles**• [Accessing the AzureDevOps Audit Log](/en-us/azure/devops/organizations/audit/azure-devops-auditing)• [Audit API reference](/en-us/rest/api/azure/devops/audit/)• [AuditId reference](/en-us/azure/devops/organizations/audit/auditing-events)• Audits with ActionId `Security.ModifyPermission`, `Security.RemovePermission`.• For changes to groups assigned to roles, audits with ActionId `Group.UpdateGroupMembership`, `Group.UpdateGroupMembership.Add`, `Group.UpdateGroupMembership.Remove` |

### Fabric

Includes Fabric and Power BI.

| Area | Content |
| --- | --- |
| Overview | [Understand Microsoft Fabric admin roles](/en-us/fabric/admin/roles) |
| Management API reference | **Fabric-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 roleManagement API](/en-us/graph/api/resources/rolemanagement)• Use `directory` provider• See roles with permissions starting with `microsoft.powerApps.powerBI`. |
| Audit and monitoring reference | **Fabric-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with category `RoleManagement` |

### Unified Support Portal for managing customer support cases

Includes Unified Support Portal and Services Hub.

| Area | Content |
| --- | --- |
| Overview | [Services Hub roles and permissions](/en-us/services-hub/unified/getting-started/roles-permissions) |
| Management API reference | Manage these roles in the Services Hub portal, https://serviceshub.microsoft.com. |

## Microsoft Graph application permissions

In addition to the previously mentioned RBAC systems, elevated permissions can be granted to Microsoft Entra application registrations and service principals using application permissions. For example, a non-interactive, non-human application identity can be granted the ability to read all mail in a tenant (the `Mail.Read` application permission). The following table lists how to manage and monitor application permissions.

| Area | Content |
| --- | --- |
| Overview | [Overview of Microsoft Graph permissions](/en-us/graph/permissions-overview?tabs=http#application-permissions) |
| Management API reference | **Microsoft Graph-specific roles in Microsoft Entra ID**[Microsoft Graph v1.0 servicePrincipal API](/en-us/graph/api/resources/serviceprincipal)• Enumerate the [appRoleAssignments](/en-us/graph/api/resources/approleassignment) for each [servicePrincipal](/en-us/graph/api/resources/serviceprincipal) in the tenant.• For each appRoleAssignment, get information about the permissions granted by the assignment by reading the appRole property on the servicePrincipal object referenced by the resourceId and appRoleId in the appRoleAssignment.• Of specific interest are app permissions to the Microsoft Graph (servicePrincipal with appID == "00000003-0000-0000-c000-000000000000") which grant access to Exchange, SharePoint, Teams, and so on. Here is a reference for [Microsoft Graph permissions](/en-us/graph/permissions-reference).• Also see [Microsoft Entra security operations for applications](/en-us/entra/architecture/security-operations-applications). |
| Audit and monitoring reference | **Microsoft Graph-specific roles in Microsoft Entra ID**[Microsoft Entra activity log overview](/en-us/entra/identity/monitoring-health/howto-access-activity-logs)API access to Microsoft Entra audit logs:• [Microsoft Graph v1.0 directoryAudit API](/en-us/graph/api/resources/directoryaudit)• Audits with category `ApplicationManagement` and Activity name `Add app role assignment to service principal` |