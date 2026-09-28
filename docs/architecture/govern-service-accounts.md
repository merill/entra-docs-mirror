---
layout: Conceptual
title: Governing Microsoft Entra service accounts - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/govern-service-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Principles and procedures for managing the lifecycle of service accounts in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-02-09T00:00:00.0000000Z
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
ms.subservice: architecture
locale: en-us
document_id: 795e3876-816e-e7ca-8d2a-4bbdbe786c30
document_version_independent_id: e2d936fa-3ee9-7c11-3667-e0968f1b82d6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/govern-service-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/govern-service-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/govern-service-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: d8a9d211-bfc8-628c-423c-a53ff1eba213
---

# Governing Microsoft Entra service accounts - Microsoft Entra | Microsoft Learn

There are three types of service accounts in Microsoft Entra ID: managed identities, service principals, and user accounts employed as service accounts. When you create service accounts for automated use, they're granted permissions to access resources in Azure and Microsoft Entra ID. Resources can include Microsoft 365 services, software as a service (SaaS) applications, custom applications, databases, HR systems, and so on. Governing Microsoft Entra service account is managing creation, permissions, and lifecycle to ensure security and continuity.

Learn more:

- [Securing managed identities](service-accounts-managed-identities)
- [Securing service principals](service-accounts-principal)

Note

We do not recommend user accounts as service accounts because they are less secure. This includes on-premises service accounts synced to Microsoft Entra ID, because they aren't converted to service principals. Instead, we recommend managed identities, or service principals, and the use of Conditional Access.

Learn more: [What is Conditional Access?](../identity/conditional-access/overview)

## Plan your service account

Before creating a service account, or registering an application, document the service account key information. Use the information to monitor and govern the account. We recommend collecting the following data and tracking it in your centralized Configuration Management Database (CMDB).

| Data | Description | Details |
| --- | --- | --- |
| Owner | User or group accountable for managing and monitoring the service account | Grant the owner permissions to monitor the account and implement a way to mitigate issues. Issue mitigation is done by the owner, or by request to an IT team. |
| Purpose | How the account is used | Map the service account to a service, application, or script. Avoid creating multiuse service accounts. |
| Permissions (Scopes) | Anticipated set of permissions | Document the resources it accesses and permissions for those resources |
| CMDB Link | Link to the accessed resources, and scripts in which the service account is used | Document the resource and script owners to communicate the effects of change |
| Risk assessment | Risk and business effect, if the account is compromised | Use the information to narrow the scope of permissions and determine access to information |
| Period for review | The cadence of service account reviews, by the owner | Review communications and reviews. Document what happens if a review is performed after the scheduled review period. |
| Lifetime | Anticipated maximum account lifetime | Use this measurement to schedule communications to the owner, disable, and then delete the accounts. Set an expiration date for credentials that prevents them from rolling over automatically. |
| Name | Standardized account name | Create a naming convention for service accounts to search, sort, and filter them |

## Principle of least privileges

Grant the service account permissions needed to perform tasks, and no more. If a service account needs high-level permissions, evaluate why and try to reduce permissions.

We recommend the following practices for service account privileges.

### Permissions

- Don't assign built-in roles to service accounts
    - See, [`oAuth2PermissionGrant` resource type](/en-us/graph/api/resources/oauth2permissiongrant)
- The service principal is assigned a privileged role
    - [Create a custom role in Microsoft Entra ID](../identity/role-based-access-control/custom-create)
- Don't include service accounts as members of any groups with elevated permissions
    - See, [Get-MgDirectoryRoleMember](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdirectoryrolemember):

> 
> `Get-MgDirectoryRoleMember`, and filter for objectType "Service Principal", or use`Get-MgServicePrincipal | % { Get-MgServicePrincipalAppRoleAssignment -ObjectId $_ }`

- See, [Introduction to permissions and consent](../identity-platform/permissions-consent-overview) to limit the functionality a service account can access on a resource
- Service principals and managed identities can use Open Authorization (OAuth) 2.0 scopes in a delegated context impersonating a signed-on user, or as service account in the application context. In the application context, no one is signed in.
- Confirm the scopes service accounts request for resources
    - If an account requests Files.ReadWrite.All, evaluate whether it needs File.Read.All
    - [Microsoft Graph permissions reference](/en-us/graph/permissions-reference)
- Ensure you trust the application developer, or API, with the requested access

### Duration

- Limit service account credentials (client secret, certificate) to an anticipated usage period
- Schedule periodic reviews of service account usage and purpose
    - Ensure reviews occur prior to account expiration

After you understand the purpose, scope, and permissions, create your service account, use the instructions in the following articles.

- [How to use managed identities for App Service and Azure Functions](/en-us/azure/app-service/overview-managed-identity?tabs=dotnet)
- [Create a Microsoft Entra application and service principal that can access resources](../identity-platform/howto-create-service-principal-portal)

Use a managed identity when possible. If you can't use a managed identity, use a service principal. If you can't use a service principal, then use a Microsoft Entra user account.

## Build a lifecycle process

A service account lifecycle starts with planning, and ends with permanent deletion. The following sections cover how you monitor, review permissions, determine continued account usage, and ultimately deprovision the account.

### Monitor service accounts

Monitor your service accounts to ensure usage patterns are correct, and that the service account is used.

#### Collect and monitor service account sign-ins

Use one of the following monitoring methods:

- Microsoft Entra sign-in logs in the Azure portal
- Export the Microsoft Entra sign-in logs to
    - [Azure Storage documentation](/en-us/azure/storage/)
    - [Azure Event Hubs documentation](/en-us/azure/event-hubs/), or
    - [Azure Monitor Logs overview](/en-us/azure/azure-monitor/logs/data-platform-logs)

Use the following screenshot to see service principal sign-ins.

![Screenshot of service principal sign-ins.](media/govern-service-accounts/service-accounts-govern-1.png)

#### Sign-in log details

Look for the following details in sign-in logs.

- Service accounts not signed in to the tenant
- Changes in sign-in service account patterns

We recommend you export Microsoft Entra sign-in logs, and then import them into a security information and event management (SIEM) tool, such as Microsoft Sentinel. Use the SIEM tool to build alerts and dashboards.

### Review service account permissions

Regularly review service account permissions and accessed scopes to see whether they can be reduced or eliminated.

- See, [Get-MgServicePrincipalOauth2PermissionGrant](/en-us/powershell/module/microsoft.graph.applications/get-mgserviceprincipaloauth2permissiongrant)
- See, [`AzureADAssessment`](https://github.com/AzureAD/AzureADAssessment) and confirm validity
- Don't set service principal credentials to **Never expire**
- Use certificates or credentials stored in Azure Key Vault, when possible
    - [What is Azure Key Vault?](/en-us/azure/key-vault/general/basic-concepts)

### Recertify service account use

Establish a regular review process to ensure service accounts are regularly reviewed by owners, security team, or IT team.

The process includes:

- Determine service account review cycle, and document it in your CMDB
- Communications to owner, security team, IT team, before a review
- Determine warning communications, and their timing, if the review is missed
- Instructions if owners fail to review or respond
    - Disable, but don't delete, the account until the review is complete
- Instructions to determine dependencies. Notify resource owners of effects

The review includes the owner and an IT partner, and they certify:

- Account is necessary
- Permissions to the account are adequate and necessary, or a change is requested
- Access to the account, and its credentials, are controlled
- Account credentials are accurate: credential type and lifetime
- Account risk score hasn't changed since the previous recertification
- Update the expected account lifetime, and the next recertification date

### Deprovision service accounts

Deprovision service accounts under the following circumstances:

- Account script or application is retired
- Account script or application function is retired. For example, access to a resource.
- Service account is replaced by another service account
- Credentials expired, or the account is non-functional, and there aren't complaints

Deprovisioning includes the following tasks:

After the associated application or script is deprovisioned:

- [Sign-in logs in Microsoft Entra ID](../identity/monitoring-health/concept-sign-ins)and resource access by the service account
    - If the account is active, determine how it's being used before continuing
- For a managed service identity, disable service account sign-in, but don't remove it from the directory
- Revoke service account role assignments and OAuth2 consent grants
- After a defined period, and warning to owners, delete the service account from the directory