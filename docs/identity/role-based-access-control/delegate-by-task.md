---
layout: Conceptual
title: Least privileged roles by task - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/delegate-by-task
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Least privileged roles to delegate for tasks in Microsoft Entra ID
ms.topic: reference
ms.date: 2026-06-17T00:00:00.0000000Z
ms.custom: it-pro, sfi-ga-nochange
locale: en-us
document_id: 0f9558c0-abb6-24f8-81c8-9000b80539e8
document_version_independent_id: a4739135-863b-27bb-1f2e-cf297f21b4cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/delegate-by-task.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/delegate-by-task
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/delegate-by-task.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 088a52dc-56af-b1c2-71b4-8ccc8987ae49
---

# Least privileged roles by task - Microsoft Entra ID | Microsoft Learn

This article describes the least privileged role you should use for several tasks in Microsoft Entra ID. You will find tasks organized by feature area and the least privileged role required to perform each task, along with additional non-Global Administrator roles that can perform the task.

You can further restrict permissions by assigning roles at smaller scopes or by creating your own custom roles. For more information, see [Assign Microsoft Entra roles](manage-roles-portal) or [Create a custom role in Microsoft Entra ID](custom-create).

## Application proxy least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra application proxy](../app-proxy/overview-what-is-app-proxy).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Configure application proxy app | [Application Administrator](permissions-reference#application-administrator) |  |
| Configure connector group properties | [Application Administrator](permissions-reference#application-administrator) |  |
| Create application registration when ability is disabled for all users | [Application Developer](permissions-reference#application-developer) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator) |
| Create connector group | [Application Administrator](permissions-reference#application-administrator) |  |
| Delete connector group | [Application Administrator](permissions-reference#application-administrator) |  |
| Disable application proxy | [Application Administrator](permissions-reference#application-administrator) |  |
| Download connector service | [Application Administrator](permissions-reference#application-administrator) |  |
| Read all configuration | [Application Administrator](permissions-reference#application-administrator) |  |

## External Identities/Azure AD B2C least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra External ID](../../external-id/external-identities-overview) and [Azure Active Directory B2C](/en-us/azure/active-directory-b2c/overview).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Create Azure AD B2C directories | [All non-guest users](../../fundamentals/users-default-permissions) |  |
| Create enterprise applications | [Cloud Application Administrator](permissions-reference#cloud-application-administrator) | [Application Administrator](permissions-reference#application-administrator) |
| Create, read, update, and delete B2C policies | [B2C IEF Policy Administrator](permissions-reference#b2c-ief-policy-administrator) |  |
| Create, read, update, and delete identity providers | [External Identity Provider Administrator](permissions-reference#external-identity-provider-administrator) |  |
| Create, read, update, and delete password reset user flows | [External ID User Flow Administrator](permissions-reference#external-id-user-flow-administrator) |  |
| Create, read, update, and delete profile editing user flows | [External ID User Flow Administrator](permissions-reference#external-id-user-flow-administrator) |  |
| Create, read, update, and delete sign-in user flows | [External ID User Flow Administrator](permissions-reference#external-id-user-flow-administrator) |  |
| Create, read, update, and delete sign-up user flow | [External ID User Flow Administrator](permissions-reference#external-id-user-flow-administrator) |  |
| Create, read, update, and delete user attributes | [External ID User Flow Attribute Administrator](permissions-reference#external-id-user-flow-attribute-administrator) |  |
| Create, read, update, and delete users | [User Administrator](permissions-reference#user-administrator) |  |
| [Configure B2B external collaboration settings - Guest user access](../../external-id/external-collaboration-settings-configure) | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| [Configure B2B external collaboration settings - Guest invite settings](../../external-id/external-collaboration-settings-configure) | [Guest Inviter](permissions-reference#guest-inviter) | [External ID User Flow Administrator](permissions-reference#external-id-user-flow-administrator) |
| [Configure B2B external collaboration settings - External user leave settings](../../external-id/external-collaboration-settings-configure) | [External Identity Provider Administrator](permissions-reference#external-identity-provider-administrator) |  |
| [Configure B2B external collaboration settings - Collaboration restrictions](../../external-id/external-collaboration-settings-configure) | [Global Administrator](permissions-reference#global-administrator) |  |
| Read all configuration | [Global Reader](permissions-reference#global-reader) |  |
| [Read B2C audit logs](/en-us/azure/active-directory-b2c/faq) | [Global Reader](permissions-reference#global-reader) |  |

Note

Azure AD B2C Global Administrators do not have the same permissions as Microsoft Entra Global Administrators. If you have Azure AD B2C Global Administrator privileges, make sure that you are in an Azure AD B2C directory and not a Microsoft Entra directory.

## Company branding least privileged roles

Here are the least privileged roles you should use when performing tasks for [company branding](../../fundamentals/how-to-customize-branding) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Configure company branding | [Organizational Branding Administrator](permissions-reference#organizational-branding-administrator) |  |
| Read all configuration | [Directory Readers](permissions-reference#directory-readers) | [Default user role](../../fundamentals/users-default-permissions) |

## Connect least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra Connect](../hybrid/connect/whatis-azure-ad-connect).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Passthrough authentication | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |  |
| Read all configuration | [Global Reader](permissions-reference#global-reader) | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |
| Seamless single sign-on | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |  |

## Connect Sync least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra Connect Sync](../hybrid/connect/how-to-connect-sync-whatis).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Manage on-premises directory synchronization | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |  |

## Cloud Provisioning least privileged roles

Here are the least privileged roles you should use when performing tasks for [identity provisioning](../hybrid/what-is-provisioning) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Passthrough authentication | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |  |
| Read all configuration | [Global Reader](permissions-reference#global-reader) | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |
| Seamless single sign-on | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |  |

## Connect Health least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra Connect Health](../hybrid/connect/whatis-azure-ad-connect).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| [Add or delete services](../hybrid/connect/how-to-connect-health-operations) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |  |
| Apply fixes to sync error | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Configure notifications | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| [Configure settings](../hybrid/connect/how-to-connect-health-operations) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |  |
| Configure sync notifications | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Read ADFS security reports | [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Read all configuration | [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Read sync errors | [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Read sync services | [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| View metrics and alerts | [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| View metrics and alerts | [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| View sync service metrics and alerts | [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |

## Custom domain names least privileged roles

Here are the least privileged roles you should use when performing tasks for [custom domain names](../../fundamentals/add-custom-domain) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Manage domains | [Domain Name Administrator](permissions-reference#domain-name-administrator) |  |
| Read all configuration | [Directory Readers](permissions-reference#directory-readers) | [Default user role](../../fundamentals/users-default-permissions) |

## Domain Services least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra Domain Services](../domain-services/overview).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Create Microsoft Entra Domain Services instance | [Application Administrator](permissions-reference#application-administrator)[Groups Administrator](permissions-reference#groups-administrator)[Domain Services Contributor](/en-us/azure/role-based-access-control/built-in-roles#domain-services-contributor) |  |
| Perform all Microsoft Entra Domain Services tasks | [AAD DC Administrators group](../domain-services/tutorial-create-management-vm#administrative-tasks-you-can-perform-on-a-managed-domain) |  |
| Read all configuration | Reader on Azure subscription containing AD DS service |  |

## Devices least privileged roles

Here are the least privileged roles you should use when performing tasks for [device identity](../devices/overview) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Delete device | [Cloud Device Administrator](permissions-reference#cloud-device-administrator) | [Intune Administrator](permissions-reference#intune-administrator) |
| Disable device | [Cloud Device Administrator](permissions-reference#cloud-device-administrator) | [Intune Administrator](permissions-reference#intune-administrator) |
| Enable device | [Cloud Device Administrator](permissions-reference#cloud-device-administrator) | [Intune Administrator](permissions-reference#intune-administrator) |
| Read basic configuration | [Default user role](../../fundamentals/users-default-permissions) |  |
| Read BitLocker keys | [Cloud Device Administrator](permissions-reference#cloud-device-administrator) | [Helpdesk Administrator](permissions-reference#helpdesk-administrator)[Intune Administrator](permissions-reference#intune-administrator)[Security Administrator](permissions-reference#security-administrator)[Security Reader](permissions-reference#security-reader) |
| Provision and manage IoT devices | [IoT Device Administrator](permissions-reference#iot-device-administrator) | [Cloud Device Administrator](permissions-reference#cloud-device-administrator) |
| Manage IoT device templates | [IoT Device Administrator](permissions-reference#iot-device-administrator) | [Cloud Device Administrator](permissions-reference#cloud-device-administrator) |

## Enterprise applications least privileged roles

Here are the least privileged roles you should use when performing tasks for [application management](../enterprise-apps/what-is-application-management) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Consent to any delegated permissions | [Cloud Application Administrator](permissions-reference#cloud-application-administrator) | [Application Administrator](permissions-reference#application-administrator) |
| Consent to application permissions not including Microsoft Graph | [Cloud Application Administrator](permissions-reference#cloud-application-administrator) | [Application Administrator](permissions-reference#application-administrator) |
| Consent to application permissions to Microsoft Graph | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| Consent to applications accessing own data | [Default user role](../../fundamentals/users-default-permissions) |  |
| Create enterprise application | [Cloud Application Administrator](permissions-reference#cloud-application-administrator) | [Application Administrator](permissions-reference#application-administrator) |
| Manage Application Proxy | [Application Administrator](permissions-reference#application-administrator) |  |
| Read access review of a group or of an app | [Security Reader](permissions-reference#security-reader) | [Security Administrator](permissions-reference#security-administrator)[User Administrator](permissions-reference#user-administrator) |
| Read all configuration | [Default user role](../../fundamentals/users-default-permissions) |  |
| Update enterprise application assignments | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator)[User Administrator](permissions-reference#user-administrator) |
| Update enterprise application owners | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator) |
| Update enterprise application properties | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator) |
| Update enterprise application provisioning | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator) |
| Update enterprise application self-service | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator) |
| Update single sign-on properties | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership) | [Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Application Administrator](permissions-reference#application-administrator) |
| Create and modify custom authentication extensions | [Authentication Extensibility Administrator](permissions-reference#authentication-extensibility-administrator) | [Application Administrator](permissions-reference#application-administrator) |

Note

In practice, consenting to Microsoft Graph application permissions typically requires the Global Administrator role. Privileged Role Administrator may not be sufficient depending on tenant consent policies, permission scopes, or Graph protection requirements.

## Entitlement management least privileged roles

Here are the least privileged roles you should use when performing tasks for [entitlement management](../../id-governance/entitlement-management-overview) in Microsoft Entra ID Governance.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Tasks in Entitlement Management | [Identity Governance Administrator](permissions-reference#identity-governance-administrator). For roles lesser privilege than this within the Entitlement Management system, see: [Delegation and roles in entitlement management](../../id-governance/entitlement-management-delegate). |  |

## Groups least privileged roles

Here are the least privileged roles you should use when performing tasks for [groups](../../fundamentals/how-to-manage-groups) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Assign license | [User Administrator](permissions-reference#user-administrator) |  |
| Create group | [Groups Administrator](permissions-reference#groups-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Create, update, or delete access review of a group or of an app | [User Administrator](permissions-reference#user-administrator) |  |
| Manage group expiration | [User Administrator](permissions-reference#user-administrator) |  |
| Manage group settings | [Groups Administrator](permissions-reference#groups-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Read all configuration (except hidden membership) | [Directory Readers](permissions-reference#directory-readers) | [Default user role](../../fundamentals/users-default-permissions) |
| Read hidden membership | Group member | [Group owner](../../fundamentals/users-default-permissions#object-ownership)[Password Administrator](permissions-reference#password-administrator)[Exchange Administrator](permissions-reference#exchange-administrator)[SharePoint Administrator](permissions-reference#sharepoint-administrator)[Teams Administrator](permissions-reference#teams-administrator)[User Administrator](permissions-reference#user-administrator) |
| Read membership of groups with hidden membership | [Helpdesk Administrator](permissions-reference#helpdesk-administrator) | [User Administrator](permissions-reference#user-administrator)[Teams Administrator](permissions-reference#teams-administrator) |
| Revoke license | [License Administrator](permissions-reference#license-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Update dynamic membership groups | [Group owner](../../fundamentals/users-default-permissions#object-ownership) | [User Administrator](permissions-reference#user-administrator) |
| Update group owners | [Group owner](../../fundamentals/users-default-permissions#object-ownership) | [User Administrator](permissions-reference#user-administrator) |
| Update group properties | [Group owner](../../fundamentals/users-default-permissions#object-ownership) | [User Administrator](permissions-reference#user-administrator) |
| Delete group | [Groups Administrator](permissions-reference#groups-administrator) | [User Administrator](permissions-reference#user-administrator) |

## Licenses least privileged roles

Here are the least privileged roles you should use when performing tasks for [Microsoft Entra licensing](../../fundamentals/licensing).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Assign license | [License Administrator](permissions-reference#license-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Read all configuration | [Directory Readers](permissions-reference#directory-readers) | [Default user role](../../fundamentals/users-default-permissions) |
| Revoke license | [License Administrator](permissions-reference#license-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Try or buy subscription | [Billing Administrator](permissions-reference#billing-administrator) |  |

## Lifecycle Workflows least privileged roles

Here are the least privileged roles you should use when performing tasks for [lifecycle workflows](../../id-governance/what-are-lifecycle-workflows) in Microsoft Entra ID Governance.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Create a workflow | [Lifecycle workflows Administrator](permissions-reference#lifecycle-workflows-administrator) |  |
| Add a custom extension to a workflow | [Lifecycle workflows Administrator](permissions-reference#lifecycle-workflows-administrator). You must also have either the [Logic App contributor](/en-us/azure/role-based-access-control/built-in-roles/integration#logic-app-contributor) or [Owner](/en-us/azure/role-based-access-control/built-in-roles/integration#logic-app-operator) Azure Resource Manager role. |  |

## Microsoft Entra Health least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra Health monitoring](../monitoring-health/concept-microsoft-entra-health).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| View scenario monitoring signals and alert configurations | [Reports Reader](permissions-reference#reports-reader) | [Security Reader](permissions-reference#security-reader)[Security Operator](permissions-reference#security-operator)[Security Administrator](permissions-reference#security-administrator)[Helpdesk Administrator](permissions-reference#helpdesk-administrator)[Global Reader](permissions-reference#global-reader) |
| Update alerts and alert email configurations | [Helpdesk Administrator](permissions-reference#helpdesk-administrator) |  |

## Microsoft Entra ID Protection least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra ID Protection](../../id-protection/overview-identity-protection).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Configure alert notifications | [Security Administrator](permissions-reference#security-administrator) |  |
| Configure and enable or disable MFA policy | [Security Administrator](permissions-reference#security-administrator) |  |
| Configure and enable or disable sign-in risk policy | [Security Administrator](permissions-reference#security-administrator) |  |
| Configure and enable or disable user risk policy | [Security Administrator](permissions-reference#security-administrator) |  |
| Configure weekly digests | [Security Administrator](permissions-reference#security-administrator) |  |
| Dismiss all risk detections | [Security Operator](permissions-reference#security-operator) |  |
| Fix or dismiss vulnerability | [Security Administrator](permissions-reference#security-administrator) |  |
| Read all configuration | [Security Reader](permissions-reference#security-reader) |  |
| Read all risk detections | [Security Reader](permissions-reference#security-reader) |  |
| Read vulnerabilities | [Security Reader](permissions-reference#security-reader) |  |

## Monitoring and health - Audit and sign-in logs least privileged roles

Here are the least privileged roles you should use when performing tasks for audit and sign-in logs in [Microsoft Entra monitoring](../monitoring-health/overview-monitoring-health).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Read audit and sign-in logs | [Reports Reader](permissions-reference#reports-reader) | [Application Administrator](permissions-reference#application-administrator)[Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Cloud Device Administrator](permissions-reference#cloud-device-administrator)[Global Secure Access Administrator](permissions-reference#global-secure-access-administrator)[Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator)[Security Administrator](permissions-reference#security-administrator)[Security Operator](permissions-reference#security-operator)[Security Reader](permissions-reference#security-reader) |

## Monitoring and health - Provisioning logs least privileged roles

Here are the least privileged roles you should use when performing tasks for [Microsoft Entra provisioning logs](../monitoring-health/concept-provisioning-logs).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Read provisioning logs | [Reports Reader](permissions-reference#reports-reader) | [Enterprise application owner](../../fundamentals/users-default-permissions#object-ownership)[Application Administrator](permissions-reference#application-administrator)[Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Cloud Device Administrator](permissions-reference#cloud-device-administrator)[Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator)[Security Administrator](permissions-reference#security-administrator)[Security Operator](permissions-reference#security-operator)[Security Reader](permissions-reference#security-reader) |

## Monitoring and health - Recommendations least privileged roles

Here are the least privileged roles you should use when performing tasks for [Microsoft Entra identity recommendations](../monitoring-health/overview-recommendations).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Read recommendations | [Reports Reader](permissions-reference#reports-reader) | [Security Reader](permissions-reference#security-reader)[Global Reader](permissions-reference#global-reader)[Helpdesk Administrator](permissions-reference#helpdesk-administrator)[Service Support Administrator](permissions-reference#service-support-administrator)[User Administrator](permissions-reference#user-administrator) |
| Update recommendations | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) | [Application Administrator](permissions-reference#application-administrator)[Authentication Administrator](permissions-reference#authentication-administrator)[Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Conditional Access Administrator](permissions-reference#conditional-access-administrator)[Exchange Administrator](permissions-reference#exchange-administrator)[Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator)[Identity Governance Administrator](permissions-reference#identity-governance-administrator)[Privileged Role Administrator](permissions-reference#privileged-role-administrator)[Security Administrator](permissions-reference#security-administrator)[Security Operator](permissions-reference#security-operator)[SharePoint Administrator](permissions-reference#sharepoint-administrator) |
| Read Identity Secure Score improvement action | [Service Support Administrator](permissions-reference#service-support-administrator) | [Security Administrator](permissions-reference#security-administrator)[Exchange Administrator](permissions-reference#exchange-administrator) |
| Update Identity Secure Score improvement action | [SharePoint Administrator](permissions-reference#sharepoint-administrator) | [Helpdesk Administrator](permissions-reference#helpdesk-administrator)[User Administrator](permissions-reference#user-administrator)[Security Reader](permissions-reference#security-reader)[Security Operator](permissions-reference#security-operator)[Global Reader](permissions-reference#global-reader) |

## Monitoring and health - Sign-in diagnostic tool

Here are the least privileged roles you should use when running the [sign-in diagnostic tool](../monitoring-health/howto-use-sign-in-diagnostics).

| Task | Least privileged roles | Additional roles |
| --- | --- | --- |
| Use sign-in diagnostic from **Diagnose and solve problems** | [Billing Administrator](permissions-reference#billing-administrator) | [Application Administrator](permissions-reference#application-administrator)[Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Cloud Device Administrator](permissions-reference#cloud-device-administrator)[Conditional Access Administrator](permissions-reference#conditional-access-administrator)[Customer LockBox Access Approver](permissions-reference#customer-lockbox-access-approver)[Groups Administrator](permissions-reference#groups-administrator)[License Administrator](permissions-reference#license-administrator)[Global Reader](permissions-reference#global-reader)[Helpdesk Administrator](permissions-reference#helpdesk-administrator)[Privileged Role Administrator](permissions-reference#privileged-role-administrator)[Security Administrator](permissions-reference#security-administrator)[User Administrator](permissions-reference#user-administrator) |
| Use sign-in diagnostic from the **Sign-in logs** | BOTH [Reports Reader](permissions-reference#reports-reader) AND [Billing Administrator](permissions-reference#billing-administrator) | [Global Secure Access Administrator](permissions-reference#global-secure-access-administrator)[Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator)[Security Administrator](permissions-reference#security-administrator)[Security Operator](permissions-reference#security-operator)[Security Reader](permissions-reference#security-reader) |

## Multifactor authentication least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra authentication](../authentication/overview-authentication).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Delete all existing app passwords generated by the selected users | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) | [Authentication Administrator](permissions-reference#authentication-administrator) |
| [Disable per-user MFA](../authentication/howto-mfa-userstates) | [Authentication Administrator](permissions-reference#authentication-administrator) | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |
| [Enable per-user MFA](../authentication/howto-mfa-userstates) | [Authentication Administrator](permissions-reference#authentication-administrator) | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |
| Manage MFA service settings | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Require selected users to provide contact methods again | [Authentication Administrator](permissions-reference#authentication-administrator) |  |
| Restore multifactor authentication on all remembered devices | [Authentication Administrator](permissions-reference#authentication-administrator) |  |

## MFA Server least privileged roles

Here are the least privileged roles you should use when performing tasks in [MFA Server](../authentication/how-to-migrate-mfa-server-to-azure-mfa).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Block/unblock users | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure account lockout | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure caching rules | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure fraud alert | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure notifications | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure one-time bypass | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure phone call settings | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure providers | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure server settings | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Read activity report | [Global Reader](permissions-reference#global-reader) |  |
| Read all configuration | [Global Reader](permissions-reference#global-reader) |  |
| Read server status | [Global Reader](permissions-reference#global-reader) |  |

## Organizational relationships least privileged roles

Here are the least privileged roles you should use when performing tasks for [external collaboration settings](../../external-id/external-collaboration-settings-configure) in Microsoft Entra External ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Manage identity providers | [External Identity Provider Administrator](permissions-reference#external-identity-provider-administrator) |  |
| Read all configuration | [Global Reader](permissions-reference#global-reader) |  |

## Password reset least privileged roles

Here are the least privileged roles you should use when performing tasks for [password reset](../authentication/concept-sspr-howitworks) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Configure authentication methods | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure customization | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure notification | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure on-premises integration | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Configure password reset properties | [User Administrator](permissions-reference#user-administrator) | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |
| Configure registration | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| Read all configuration | [Security Administrator](permissions-reference#security-administrator) | [User Administrator](permissions-reference#user-administrator) |

## Privileged Identity Management least privileged roles

Here are the least privileged roles you should use when performing tasks for [Microsoft Entra Privileged Identity Management](../../id-governance/privileged-identity-management/pim-configure) in Microsoft Entra ID Governance.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Assign users to roles | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| Configure role settings | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| View audit activity | [Security Reader](permissions-reference#security-reader) |  |
| View role memberships | [Security Reader](permissions-reference#security-reader) |  |

## Roles and administrators least privileged roles

Here are the least privileged roles you should use when performing tasks for [roles and administrators](manage-roles-portal) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Manage role assignments | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| Read access review of a Microsoft Entra role | [Security Reader](permissions-reference#security-reader) | [Security Administrator](permissions-reference#security-administrator)[Privileged Role Administrator](permissions-reference#privileged-role-administrator) |
| Read all configuration | [Default user role](../../fundamentals/users-default-permissions) |  |

## Security - Authentication methods least privileged roles

Here are the least privileged roles you should use when performing tasks for [authentication methods](../authentication/overview-authentication) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Enable or disable authentication methods | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |
| View, provision on behalf of, and manage individual user authentication methods | [Authentication Administrator](permissions-reference#authentication-administrator) | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |
| Configure password protection | [Security Administrator](permissions-reference#security-administrator) |  |
| Configure smart lockout | [Security Administrator](permissions-reference#security-administrator) |  |
| Read all configuration | [Global Reader](permissions-reference#global-reader) |  |

## Security - Conditional Access least privileged roles

Here are the least privileged roles you should use when performing tasks for [Conditional Access](../conditional-access/overview) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Configure MFA trusted IP addresses | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) |  |
| Create custom controls | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Create named locations | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Create policies | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Create terms of use | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Create VPN connectivity certificate | [Cloud Application Administrator](permissions-reference#cloud-application-administrator) | [Application Administrator](permissions-reference#application-administrator) |
| Delete classic policy | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Restore a soft-deleted policy | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Delete terms of use | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Delete VPN connectivity certificate | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Disable classic policy | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Manage custom controls | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Manage named locations | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Manage terms of use | [Conditional Access Administrator](permissions-reference#conditional-access-administrator) | [Security Administrator](permissions-reference#security-administrator) |
| Read all configuration | [Security Reader](permissions-reference#security-reader) |  |
| Read named locations | [Security Reader](permissions-reference#security-reader) |  |
| Read terms of use | [Security Reader](permissions-reference#security-reader) | [Global Reader](permissions-reference#global-reader) |
| Read which terms of use were accepted by the signed-in user | [Default user role](../../fundamentals/users-default-permissions) |  |

## Security - Identity Security Score least privileged roles

Here are the least privileged roles you should use when performing tasks for [Identity Secure Score](../monitoring-health/concept-identity-secure-score) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Read all configuration | [Security Reader](permissions-reference#security-reader) | [Security Administrator](permissions-reference#security-administrator) |
| Read security score | [Security Reader](permissions-reference#security-reader) | [Security Administrator](permissions-reference#security-administrator) |
| Update event status | [Security Administrator](permissions-reference#security-administrator) |  |

## Security - Risky sign-ins least privileged roles

Here are the least privileged roles you should use when performing tasks for [risky sign-ins](../../id-protection/overview-identity-protection) in Microsoft Entra ID Protection.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Read all configuration | [Security Reader](permissions-reference#security-reader) |  |
| Read risky sign-ins | [Security Reader](permissions-reference#security-reader) |  |

## Security - Users flagged for risk least privileged roles

Here are the least privileged roles you should use when performing tasks for [users flagged for risk](../../id-protection/howto-identity-protection-configure-notifications) in Microsoft Entra ID Protection.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Dismiss all events | [Security Administrator](permissions-reference#security-administrator) |  |
| Perform identity containment actions for SOC incident response | [Entra SOC Identity Responder](permissions-reference#entra-soc-identity-responder) |  |
| Read all configuration | [Security Reader](permissions-reference#security-reader) |  |
| Read users flagged for risk | [Security Reader](permissions-reference#security-reader) |  |

## Temporary Access Pass least privileged roles

Here are the least privileged roles you should use when performing tasks for [Temporary Access Pass](../authentication/howto-authentication-temporary-access-pass) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Create, delete, or view a Temporary Access Pass for admins or members (except themselves) | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |  |
| Create, delete, or view a Temporary Access Pass for members (except themselves) | [Authentication Administrator](permissions-reference#authentication-administrator) |  |
| View a Temporary Access Pass details for a user (without reading the code itself) | [Global Reader](permissions-reference#global-reader) |  |
| Configure or update the Temporary Access Pass authentication method policy | [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) |  |

## Tenants least privileged roles

Here are the least privileged roles you should use when performing tasks in [Microsoft Entra tenants](../../fundamentals/create-new-tenant).

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Create Microsoft Entra ID or Azure AD B2C Tenant | [Tenant Creator](permissions-reference#tenant-creator) |  |
| Update Microsoft Entra tenant properties | [Billing Administrator](permissions-reference#billing-administrator) |  |
| [Manage privacy statement and contact](../../fundamentals/properties-area) | [Billing Administrator](permissions-reference#billing-administrator) |  |

## Users least privileged roles

Here are the least privileged roles you should use when performing tasks for [users](../../fundamentals/how-to-create-delete-users) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Add user to directory role | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| Add user to group | [User Administrator](permissions-reference#user-administrator) |  |
| Assign license | [License Administrator](permissions-reference#license-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Create guest user | [Guest Inviter](permissions-reference#guest-inviter) | [User Administrator](permissions-reference#user-administrator) |
| Reset guest user invite | [Helpdesk Administrator](permissions-reference#helpdesk-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Create user | [User Administrator](permissions-reference#user-administrator) |  |
| Delete users | [User Administrator](permissions-reference#user-administrator) |  |
| Invalidate refresh tokens of limited admins | [User Administrator](permissions-reference#user-administrator) |  |
| Invalidate refresh tokens of non-admins | [Helpdesk Administrator](permissions-reference#helpdesk-administrator) | [User Administrator](permissions-reference#user-administrator)[Security Administrator](permissions-reference#security-administrator) |
| Invalidate refresh tokens of privileged admins | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |  |
| Read basic configuration | [Default user role](../../fundamentals/users-default-permissions) |  |
| Reset password for limited admins | [User Administrator](permissions-reference#user-administrator) |  |
| Reset password of non-admins | [Password Administrator](permissions-reference#password-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Reset password of privileged admins | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |  |
| Revoke license | [License Administrator](permissions-reference#license-administrator) | [User Administrator](permissions-reference#user-administrator) |
| Update all properties except User Principal Name | [User Administrator](permissions-reference#user-administrator) |  |
| Update On-premises sync enabled property | [Hybrid Identity Administrator](permissions-reference#hybrid-identity-administrator) |  |
| Update profile photos and people settings | [People Administrator](permissions-reference#people-administrator) |  |
| Update User Principal Name for limited admins | [User Administrator](permissions-reference#user-administrator) |  |
| Update User Principal Name property on privileged admins | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |  |
| Update user settings - Default user role permissions | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| [Update user settings - Guest user access](../users/users-restrict-guest-permissions) | [Privileged Role Administrator](permissions-reference#privileged-role-administrator) |  |
| Update user settings - Administration center | [Global Administrator](permissions-reference#global-administrator) |  |
| [Update user settings - LinkedIn account connections](../users/linkedin-integration) | [Global Administrator](permissions-reference#global-administrator) |  |
| [Update user settings - Show keep user signed in](../../fundamentals/how-to-manage-stay-signed-in-prompt) | [Global Administrator](permissions-reference#global-administrator) |  |
| Update Authentication methods | [Authentication Administrator](permissions-reference#authentication-administrator) | [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) |

## Support least privileged roles

Here are the least privileged roles you should use when performing tasks for [support](../../fundamentals/how-to-get-support) in Microsoft Entra ID.

| Task | Least privileged role | Additional roles |
| --- | --- | --- |
| Submit support ticket | [Service Support Administrator](permissions-reference#service-support-administrator) | [Application Administrator](permissions-reference#application-administrator)[Azure Information Protection Administrator](permissions-reference#azure-information-protection-administrator)[Billing Administrator](permissions-reference#billing-administrator)[Cloud Application Administrator](permissions-reference#cloud-application-administrator)[Compliance Administrator](permissions-reference#compliance-administrator)[Dynamics 365 Administrator](permissions-reference#dynamics-365-administrator)[Desktop Analytics Administrator](permissions-reference#desktop-analytics-administrator)[Exchange Administrator](permissions-reference#exchange-administrator)[Helpdesk Administrator](permissions-reference#helpdesk-administrator)[Intune Administrator](permissions-reference#intune-administrator)[Password Administrator](permissions-reference#password-administrator)[Fabric Administrator](permissions-reference#fabric-administrator)[Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator)[SharePoint Administrator](permissions-reference#sharepoint-administrator)[Skype for Business Administrator](permissions-reference#skype-for-business-administrator)[Teams Administrator](permissions-reference#teams-administrator)[Teams Communications Administrator](permissions-reference#teams-communications-administrator)[User Administrator](permissions-reference#user-administrator) |