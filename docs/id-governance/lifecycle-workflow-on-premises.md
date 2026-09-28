---
layout: Conceptual
title: Managing Users synchronized from Active Directory Domain Services to Microsoft Entra ID with Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-on-premises
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Conceptual article discussing managing Users synchronized from Active Directory Domain Services (AD DS) to Microsoft Entra with Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.workload: identity
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-concept
locale: en-us
document_id: a1885b5e-f6e2-5835-398a-032fc0da41b6
document_version_independent_id: a1885b5e-f6e2-5835-398a-032fc0da41b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-on-premises.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-on-premises
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-on-premises.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 7b7579b8-cf75-93ca-c3c3-598b902e44d1
---

# Managing Users synchronized from Active Directory Domain Services to Microsoft Entra ID with Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows supports governing the identity lifecycle for user accounts that are synchronized from Active Directory Domain Services (AD DS) to Microsoft Entra ID. For Lifecycle Workflows, it's essential that a user account exists in Microsoft Entra ID, but how the account was created, or how lifecycle relevant changes are being made to the account, plays a minor role when it comes to processing workflows and associated tasks for the user account. This support includes accounts, and changes, made via options such as [HR driven provisioning](../identity/app-provisioning/what-is-hr-driven-provisioning), Microsoft Graph APIs, the Microsoft Entra Admin Portal, and changes synchronized by Microsoft Entra Connect and Microsoft Cloud Sync.

The following table lists common automation scenarios for synchronized users from AD DS using Microsoft Entra ID Governance:

| Scenario to automate | Microsoft Entra ID Governance solution |
| --- | --- |
| Creating the user account in Active Directory Domain Services | [HR driven provisioning](../identity/app-provisioning/what-is-hr-driven-provisioning) |
| Providing initial credentials or password for user accounts | The [Generate Temporary Access Pass and send via email to user's manager](lifecycle-workflow-tasks#generate-temporary-access-pass-and-send-via-email-to-users-manager) task can be used to set up password-less credentials. For setting up a regular Active Directory password, you can use [Microsoft Entra self-service password reset](../identity/authentication/concept-sspr-howitworks). |
| Assigning licenses | The [Assign licenses to user](lifecycle-workflow-tasks#assign-licenses-to-user) Lifecycle Workflow task can be used to assign licenses. You're also able to assign licenses to users via [a group](../fundamentals/licensing). |
| Give users access to Active Directory group-based applications | [Govern on-premises Active Directory (Kerberos) application access](../identity/hybrid/cloud-sync/govern-on-premises-groups) |
| Update user attributes in Active Directory as they move organizations | [Plan scoping filters and attribute mapping](../identity/app-provisioning/plan-cloud-hr-provision#plan-scoping-filters-and-attribute-mapping) |
| Move users to different OUs as they move organizations | [Configure Active Directory OU container assignment](../identity/app-provisioning/plan-cloud-hr-provision#configure-active-directory-ou-container-assignment) |
| Disable users on last day | The [Disable user account](lifecycle-workflow-tasks#disable-user-account) Lifecycle Workflow task can be used to disable a user account on their last day. |
| Deleting users a set number of days after termination | The [Delete User](lifecycle-workflow-tasks#delete-user) Lifecycle Workflow task can be used within a workflow template to delete users a set number of days after their termination. |

In this article, you learn what needs to be considered if you want to use Lifecycle Workflows for user accounts that are synchronized from AD DS to Microsoft Entra ID.

## Workflow execution conditions with users synchronized from Active Directory Domain Services (AD DS) to Microsoft Entra ID

Lifecycle Workflows are processed for user accounts when they meet the workflow's execution conditions. Executing conditions are composed of a trigger and scope. The trigger describes the event that occurs for a user account. The scope allows you to further define for whom the workflow runs when the event occurs.

### Workflow triggers

The following table shows what should be considered for each workflow trigger when used with users synchronized from AD DS:

| Workflow Trigger | Requirements |
| --- | --- |
| Attribute changes | No further configuration needed as long as attributes are synced. For information on synced attributes, see: [Attribute mapping in Microsoft Entra Cloud Sync](../identity/hybrid/cloud-sync/how-to-attribute-mapping) and [Microsoft Entra Connect Sync: Directory extensions](../identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions). When a change is made in Active Directory, the synchronization via Microsoft Entra Cloud Sync or Microsoft Entra Connect Sync needs to occur before changes can be picked up from Lifecycle Workflows. |
| Group membership based | As any type of group is supported, no further configuration is required. If the group originates from Active Directory, it must be synchronized to Microsoft Entra. The Microsoft Entra Cloud Sync, or Microsoft Entra Connect Sync, synchronization needs to occur before changes can be picked up from Lifecycle Workflows. |
| On-demand | No further configuration needed. |
| Time based | **employeeHireDate**, **employeeLeaveDateTime**: These attributes must be synced before being used. For more information on this process, see: [How to synchronize attributes for Lifecycle workflows](how-to-lifecycle-workflow-sync-attributes).**createdDateTime**: No further configuration needed. This date is the day the user account is synced to Microsoft Entra ID, not when they were created within Active Directory. |

### Workflow scoping

For user attributes used within the workflow scoping capabilities, no further configuration is needed if the selected attributes are already synchronized. For information on synchronized attributes, see: [Attribute mapping in Microsoft Entra Cloud Sync](../identity/hybrid/cloud-sync/how-to-attribute-mapping) and [Microsoft Entra Connect Sync: Directory extensions](../identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions). When a change is made in Active Directory, the synchronization via Microsoft Entra Cloud Sync or Microsoft Entra Connect Sync needs to occur before changes can be picked up from Lifecycle Workflows.

## Workflow tasks for users synchronized from Active Directory Domain Services to Microsoft Entra ID

All Lifecycle workflow tasks work for both cloud, and synchronized from Active Directory, users out of the box except for limitations listed on specific tasks further in this article. For more information on all Lifecycle Workflow tasks, see: [Lifecycle Workflow built-in tasks](lifecycle-workflow-tasks).

### Tasks to govern group memberships

**Scenario:** When you synchronize users from AD DS to Microsoft Entra ID, you're able to add, or remove, users from cloud-based security groups via Lifecycle Workflow's group tasks. This allows you to govern group membership of the synchronized users in the cloud, and to also add this group back to Active Directory using [Microsoft Entra Cloud Sync group writeback](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory).

For groups that are synchronized from AD DS to Microsoft Entra ID, you wouldn't be able to use Lifecycle Workflow group tasks as mentioned in the scenario. However, Microsoft Entra ID Governance can be used to [govern on-premises Active Directory (Kerberos) application access](../identity/hybrid/cloud-sync/govern-on-premises-groups) with groups from the cloud, which are supported within Lifecycle Workflows.

## User account tasks

Additional configuration is required for the Lifecycle Workflow tasks that enable, disable, and delete user accounts to work with users synchronized from AD DS. The following prerequisites must be completed before you can configure the tasks to perform actions in Active Directory.

- You must have the [Microsoft Entra provisioning agent](../identity/hybrid/cloud-sync/what-is-provisioning-agent) installed in your environment. For prerequisites on installing the Microsoft Entra provisioning agent, see: [Cloud provisioning agent requirements](../identity/hybrid/cloud-sync/how-to-prerequisites#cloud-provisioning-agent-requirements). For a step by step guide on installing the Microsoft Entra Provisioning agent, see: [Install the Microsoft Entra Provisioning Agent](../identity/hybrid/cloud-sync/how-to-install). During installation, choose “**HR-driven provisioning / Microsoft Entra Connect Sync**” as “**extension configuration**”. You aren't required to add any other configuration for the provisioning agent, such as the cloud sync configuration, and you can install the provisioning agent even if you're also currently using Microsoft Entra Connect Sync for your user synchronization.

Note

The Provisioning agent installed must be at least version 1.1.1586.0, which was released May 13th, 2024.

- Ensure the Group Managed Service Account (gMSA) used by the provisioning agent has the [appropriate permissions](../identity/hybrid/cloud-sync/how-to-prerequisites#custom-gmsa-account) to perform operations on user accounts.
- To delete user accounts, you must enable the Active Directory recycle bin. For a step-by-step guide on enabling the recycle bin, see: [Active Directory Recycle Bin step-by-step](/en-us/windows-server/identity/ad-ds/get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-#active-directory-recycle-bin-step-by-step).

For a step by step guide on setting the flag so that user account tasks run for users synchronized from Active Directory Domain Services, see: [Manage synchronized from Active Directory Domain Services (AD DS) with workflows](manage-workflow-on-premises).