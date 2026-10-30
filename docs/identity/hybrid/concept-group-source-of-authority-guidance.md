---
layout: Conceptual
title: Guidance for using Group Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/concept-group-source-of-authority-guidance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Discover how to manage and transition Active Directory groups to Microsoft Entra ID using Group Source of Authority (SOA). Learn best practices for group management, provisioning, restoring, and rolling back changes in hybrid and cloud environments.
ms.subservice: hybrid-cloud-sync
ms.topic: concept-article
ms.date: 2026-08-10T00:00:00.0000000Z
ms.reviewer: dhanyahk
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: 510f2fc7-b001-5b63-bd3b-4f81a115dca4
document_version_independent_id: 510f2fc7-b001-5b63-bd3b-4f81a115dca4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/concept-group-source-of-authority-guidance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/concept-group-source-of-authority-guidance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/concept-group-source-of-authority-guidance.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 66edb667-3c25-5ed1-9f2c-c151367025ab
---

# Guidance for using Group Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Managing groups across hybrid environments is essential for organizations that transition from on-premises Active Directory Domain Services (AD DS) to the cloud. Group Source of Authority (SOA) in Microsoft Entra ID enables you to transfer group management from AD DS to the cloud, providing greater flexibility, modern governance, and streamlined administration. This guidance explains how to use Group SOA to manage, provision, restore, and roll back groups in hybrid and cloud environments. It explains best practices to clean up groups, convert group management, and ensure secure, efficient access control as you modernize your identity infrastructure.

## AD DS group cleanup

One challenge many organizations face is the proliferation of groups, particularly security groups, in their Active Directory domains. An organization might create security groups that are no longer needed after projects complete. These groups can linger unmaintained in the domain.

There's no way to confirm if a group is needed to access a resource, like an app or a file. So we need another way to identify and clean up groups that are no longer needed. One way is to use a scream test methodology to identify groups that are no longer used. For more information, see [How to remove unused groups from Active Directory](how-to-active-directory-group-cleanup).

## Best practices

Follow these best practices to transition group management from on-premises to Microsoft Entra ID.

### Prepare groups for Group SOA conversion and provisioning

If you plan to provision a converted SOA security group (not mail-enabled) back to AD DS, then you need to complete these steps to preserve the original organizational unit (OU) path:

1. Change the group scope for the AD DS groups to Universal.
2. Create a tenant-scoped directory extension property for groups.
3. Map an on-premises value, such as the distinguished name (DN), directly into the extension property.
4. Verify the property value using Microsoft Graph.
5. Convert the Source of Authority (SOA) when ready.
6. Use custom expressions to ensure Cloud Sync provisions groups back to AD DS with the same CN and OU values.

For more information, see [Provision groups to Active Directory Domain Services by using Microsoft Entra Cloud Sync](cloud-sync/how-to-configure-entra-to-active-directory).

### Transition group management

Microsoft Entra ID Governance supports governance of Microsoft Entra ID security groups and Microsoft 365 groups. While Distribution Lists (DLs) and Mail-Enabled Security Groups (MESGs) can exist in the cloud, they're Exchange concepts and you can't manage them in the Microsoft Entra admin center or with Microsoft Graph APIs. So, if you don't need a group to remain mail-enabled, convert it to a standard security group in AD DS, sync the group, and then convert the SOA.

You should replace DLs and MESGs with Microsoft 365 groups for collaboration and access management scenarios. They offer built-in capabilities for governance, collaboration, and self-service. In most cases, DLs and MESGs need to be recreated as Microsoft 365 groups. However, you can directly upgrade simple, non-nested cloud-managed DLs to Microsoft 365 groups. For more information, see [Upgrade Distribution Lists to Microsoft 365 Groups](/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists).

### Transition self-service group management

Microsoft Entra ID provides self-service group management through My Groups for Microsoft 365 and non-mail-enabled security groups. Microsoft Entra ID Governance enables access management through My Access, where you can manage groups with access packages. Access packages allow users to request access to groups as part of a structured governance framework. However, these solutions don't exactly replicate the self-service group management capabilities in Microsoft Identity Manager due to differences in on-premises and cloud solutions.

To transition self-service group management from on-premises AD DS groups, you can modernize applications and use cloud-based security groups and Microsoft 365 groups. For more information, see [Self-service group management guidance for Group Source of Authority (SOA)](how-to-source-of-authority-self-service-group-management).

### Manage on-premises apps tied to Microsoft 365 groups

To manage and govern AD DS-based apps, you can provision Microsoft 365 groups to AD DS with Group Writeback in Microsoft Entra Connect sync. But you can't choose which groups to provision to AD DS.

### On-premises changes to cloud-owned security groups are overwritten

If you provision cloud security groups to AD DS, and someone with permissions makes a change directly to the AD DS group, the change is overwritten the next time you provision the cloud group to AD DS (typically upon the next change to the cloud group). A local AD DS change doesn't reflect in Microsoft Entra ID.

### How Group Provisioning to AD DS works with nested groups

Let's look at an example where you provision a security group named *CloudGroupB* to AD DS. It has a parent on-premises AD DS group named *OnPremGroupA*. You convert SOA for *CloudGroupB*.

Then you start to manage group memberships in Microsoft Entra ID for the converted *CloudGroupB*. You provision it as a nested group within the on-premises group *OnPremGroupA*. If *OnPremGroupA* remains in-scope for sync, when the AD DS to Microsoft Entra ID sync configuration runs for *OnPremGroupA*, the membership reference for *CloudGroupB* doesn't sync. By design, the sync client doesn't recognize the cloud group membership references.

For more information, see [How provisioning to Active Directory works](cloud-sync/how-provisioning-to-active-directory-works#nested-group-membership-behavior).

### How SOA applies to nested groups

SOA applies only to the specified direct individual group object without recursion. If you apply SOA to nested groups within the group, they continue to be managed on-premises. Because this methodology is by design, explicitly apply SOA to each group that you want to convert. If you want to convert nested groups, you might start with the group in the lowest hierarchy, and move up the tree.

### Recreate dynamic group configurations from on-premises AD in the cloud

On-premises AD groups are inherently static. Dynamic membership is implemented through external tools such as Microsoft Identity Manager (MIM) or Forefront Identity Manager (FIM). Dynamic membership rules don't transfer automatically when you convert SOA because there's no native AD attribute that marks a group as dynamic. You need to recreate dynamic membership rules in the cloud after migration. For more information about how to set up dynamic membership group, see [Create or update a dynamic membership group in Microsoft Entra ID](/en-us/entra/identity/users/groups-create-rule).

### Limitation for custom Lightweight Directory Access Protocol (LDAP) connector in Microsoft Entra Connect Sync

Group SOA doesn't support using the custom LDAP connector in Microsoft Entra Connect Sync to sync identities and groups into Microsoft Entra ID. It only supports transfer of SOA of groups that sync from AD to Microsoft Entra ID to be cloud objects. Rollback of SOA operations also only works if the original SOA of the object is AD.

## How to manage cloud security groups

Security groups are fundamental for access control, policy management, and other critical functions. In most collaboration scenarios, Microsoft 365 groups are recommended due to their enhanced collaboration features, self-service options, and API capabilities. Distribution groups (DLs) and mail-enabled security groups (MESGs) remain viable options, particularly for Exchange administrators.

When you transition to the cloud, map on-premises groups to modern group types in Microsoft Entra, Exchange Online, and Microsoft 365. The following table provides information about how to map groups and manage them after SOA conversion.

| On-premises group type | Cloud group type | How they're managed after SOA conversion | Description |
| --- | --- | --- | --- |
| Security group | Microsoft Entra security group (not mail-enabled) | Microsoft Entra admin center  Microsoft Graph APIs | Vital for access control and translate directly as Microsoft Entra security groups, offering management by Microsoft Graph and various admin centers, including the Microsoft Entra admin center. |
| Mail-enabled security group (Exchange on-premises) | Mail-enabled security group (read-only in Microsoft Entra ID and managed in Exchange) | Exchange Online or PowerShell | Can migrate directly, or be recreated as security-enabled Microsoft 365 Groups ([Create group](/en-us/graph/api/group-post-groups)). If email functionality is no longer needed, they might be recreated as Microsoft Entra security groups. Mail-enabled security groups are only editable by using Exchange or PowerShell. Security groups and Microsoft 365 groups are managed with Microsoft Graph and various admin centers, including the Microsoft Entra admin center. |
| Distribution List (Exchange on-premises) | Distribution List (read-only for Microsoft Entra and managed in Exchange) | Exchange Online or via PowerShell | Are for email-only communication. They can be migrated as Exchange Online Distribution Lists, and managed by using Exchange Online or Exchange PowerShell. They can then be recreated as Microsoft 365 groups or you can directly [upgrade them to Microsoft 365 Groups](/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists). They enable shared files, calendars, Teams integration, and self-service management with Outlook, Teams, My Groups, or Microsoft Graph. |
| N/A (In the past with v1) | Microsoft 365 groups (cloud only) | Microsoft Entra admin center Microsoft Graph APIs |  |

Note

Security-enabled Microsoft 365 Groups can be used for both collaboration for apps like Teams, SharePoint, or Outlook, and access control in Microsoft Entra. However, security-enabled Microsoft 365 Groups aren't supported for assigning permissions to Exchange shared mailboxes. For scenarios where you need to secure a shared mailbox, continue to use mail-enabled security groups.