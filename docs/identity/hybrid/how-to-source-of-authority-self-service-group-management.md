---
layout: Conceptual
title: Set up self-service group management after Group SOA conversion - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/how-to-source-of-authority-self-service-group-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Configure self-service group management in Microsoft Entra for security groups, mail-enabled security groups, and distribution groups after SOA conversion.
ms.subservice: hybrid
ms.topic: how-to
ms.date: 2025-08-01T00:00:00.0000000Z
ms.reviewer: mbhargav
locale: en-us
document_id: a44a791c-9b22-17a3-095e-eecf6bb37207
document_version_independent_id: a44a791c-9b22-17a3-095e-eecf6bb37207
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/how-to-source-of-authority-self-service-group-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/how-to-source-of-authority-self-service-group-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/how-to-source-of-authority-self-service-group-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a2b2e249-7ece-ac6f-7167-31481160eea4
---

# Set up self-service group management after Group SOA conversion - Microsoft Entra ID | Microsoft Learn

When you convert groups to Microsoft Entra using Source of Authority (SOA), enabling self-service group management empowers your users to manage their own group memberships while reducing administrative overhead. This article explains how to configure self-service group management for different group types after SOA conversion, including the capabilities, limitations, and best practices for each group type.

- Security groups
- Mail-enabled security groups
- Distribution groups

## Security groups

### Self-service management experience

After you convert the SOA for security groups to Microsoft Entra, they become fully manageable as Microsoft Entra security groups through self-service experiences:

- [My Groups](https://myaccount.microsoft.com/groups) - Group owners can manage membership, view group details, and perform other self-service tasks. Tenant admins must explicitly enable security groups for self-service management in My Groups in the Microsoft Entra ID tenant settings. For more information, see [Set up self-service group management in Microsoft Entra ID](/en-us/entra/identity/users/groups-self-service-management).
- Microsoft Entra admin center - Admins can manage group settings and ownership.
- Microsoft Graph - Admins can use Microsoft Graph API to automate tasks and manage groups in bulk.

### Supported scenarios

- Assigning roles and permissions
- Applying Conditional Access policies
- Controlling access to apps and resources
- Managing group membership, ownership, and properties
- Scoping of Access Package assignment policies
- Triggering lifecycle workflow execution

### Governance integration

Security groups in Microsoft Entra can be integrated with governance features:

- Access packages (using Entitlement Management): Bundle and delegate access to resources, automate approval workflows, and manage access lifecycle.
- Lifecycle workflows: Automate user and group lifecycle events, such as provisioning, deprovisioning, and access review.

### How to enable self-service and correct group ownership and join policies

1. Populate group owners: Ensure group ownership is established in your on-premises group management tool before you convert SOA.
2. Convert SOA: Transition the group source of authority to Microsoft Entra.
3. Set self-service group management policies (if applicable): If your organization uses **Self-Service Group Management**, manually apply policies in **My Groups** after the group is transferred.

## Mail-enabled security groups

### Self-service management experience

After you convert SOA for mail-enabled security groups, they become cloud-managed mail-enabled security groups.

There are some limitations for cloud-managed mail-enabled security groups:

- These groups are read-only in Microsoft Entra.
- They can't be managed through My Groups or self-service interfaces.
- Management is only available to admins by using Exchange Online Admin Center or Exchange PowerShell.

As a workaround if self-service management is required, consider converting mail-enabled security groups to standard security groups in your on-premises environment, and then convert SOA. This workaround removes the mail-enabled capability of the group.

### Governance integration

Mail-enabled security groups are currently not compatible with Microsoft Entra governance features such as access packages, or lifecycle workflows.

## Distribution groups

### Self-service management experience

After you convert SOA of on-premises distribution lists, they can be transitioned to cloud-managed distribution groups. Where possible, convert distribution groups to Microsoft 365 Groups for full self-service and governance integration. For more information, see [Upgrade Distribution Lists to Microsoft 365 Groups](/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists).

### Limitations

- Cloud distribution groups can't be managed by using **My Groups**.
- Self-service management is only possible through Exchange’s end user self-service portal.
- Nested distribution groups aren't supported for direct conversion to Microsoft 365 Groups.

### Governance integration

Distribution groups can't be used with Microsoft Entra Governance features, such as access packages, or lifecycle workflows. However, if distribution groups are converted to Microsoft 365 groups, governance scenarios are unblocked.

## Summary table

| Group type | Self-service in My Groups | Management experience | Governance support | Recommended action |
| --- | --- | --- | --- | --- |
| Security group | Yes | Microsoft Entra admin center, Graph, My Groups | Yes | Populate owners, convert SOA, use self-service group management |
| Mail-enabled security group | No (read-only) | Exchange Online, PowerShellNo self-service experience for end users | No | Convert to security group if needed |
| Distribution group | No | Exchange Admin Center, Exchange Self-Service Portal | No | Convert to Microsoft 365 group if possible |

## Key takeaways for admins

- **Enable security groups for self-service**: Enable security groups for self-service in Microsoft Entra Admin Center before user rollout.
- **Establish group ownership**: Ownership must be set on-premises before you convert SOA to ensure proper self-service experience.
- **Support governance scenarios**: Only Microsoft Entra security groups and Microsoft 365 groups support governance features. Distribution groups and mail-enabled security groups don't.
- **Plan for limitations**: Review current group types and consider [upgrading them to Microsoft 365 Groups](/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists) for the best end-user and governance experience.

For more information about group management, see [Learn about group types, membership types, and access management](/en-us/entra/fundamentals/concept-learn-about-groups).