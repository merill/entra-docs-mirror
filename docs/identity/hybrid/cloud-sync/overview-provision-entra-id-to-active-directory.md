---
layout: Conceptual
title: Provision Microsoft Entra ID objects to AD - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/overview-provision-entra-id-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: teeearls
description: Learn how Microsoft Entra Cloud Sync provisions users, groups, and memberships from Microsoft Entra ID to Active Directory and review supported scenarios.
ms.reviewer: marshmacy
ms.subservice: hybrid-cloud-sync
ms.topic: concept-article
ms.date: 2026-08-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: 1c8bf20d-a9b4-a4ab-3a6f-86fa156b788b
document_version_independent_id: 1c8bf20d-a9b4-a4ab-3a6f-86fa156b788b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/overview-provision-entra-id-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/overview-provision-entra-id-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/overview-provision-entra-id-to-active-directory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 065d1231-9c02-d4d3-26cd-d1d8888e809f
---

# Provision Microsoft Entra ID objects to AD - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Cloud Sync can provision **users, groups, and group memberships** from Microsoft Entra ID to on-premises Active Directory Domain Services (AD DS). This lets you manage the identity lifecycle from the cloud, using [Microsoft Entra ID Governance](/en-us/entra/id-governance/identity-governance-overview), while maintaining uninterrupted access to applications that still depend on Active Directory (AD). It builds on [Microsoft Entra Cloud Sync](what-is-cloud-sync) and complements the [user](/en-us/entra/identity/hybrid/user-source-of-authority-overview) and [group](/en-us/entra/identity/hybrid/concept-source-of-authority-overview) Source of Authority (SOA) capabilities.

Many organizations are adopting a cloud-first identity model but still rely on AD for application access. Provisioning from Microsoft Entra ID to AD bridges this gap by allowing administrators to:

- Manage identities directly in Microsoft Entra ID as the **source of authority**.
- Provision **cloud-native users, SOA-converted users, and guest business-to-business (B2B) users** into AD.
- Provision **security groups** and their memberships into AD.
- Maintain identity continuity by preserving key attributes such as the **security identifier (SID)**.
- Keep identity attributes and group memberships aligned between Microsoft Entra ID and AD.
- Ensure continued access to on-premises applications without disruption.

Note

Provisioning **users** to Active Directory is currently in **preview**. Provisioning **groups** to Active Directory is generally available. For preview terms, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## How it works

Microsoft Entra ID is the source of authority. The Microsoft Entra provisioning service detects changes and sends them, through the Cloud Sync provisioning agent, into the target AD domain.

[![Diagram showing the provisioning flow from Microsoft Entra ID through the provisioning service and Cloud Sync agent into Active Directory.](media/overview-provision-entra-id-to-active-directory/entra-id-to-active-directory-provisioning-flow.png)](media/overview-provision-entra-id-to-active-directory/entra-id-to-active-directory-provisioning-flow.png#lightbox)

1. An administrator configures a provisioning configuration in the Microsoft Entra admin center.
2. The Microsoft Entra provisioning service detects object changes (creates, updates, deletes).
3. Changes are sent to the on-premises Cloud Sync provisioning agent.
4. The agent provisions user and group objects into the target Active Directory domain.

Note

**Password writeback** (synchronizing password changes from Microsoft Entra ID to AD) isn't available.

For a detailed explanation of how the sync engine matches, provisions, and deletes objects, see [How provisioning to Active Directory works](how-provisioning-to-active-directory-works). To choose between provisioning groups only, users only, or both, see [Deployment options](concept-deployment-options-provision-to-active-directory).

## What you can provision

| Capability | Description |
| --- | --- |
| Combined users + groups configuration | A single configuration provisions both users and groups into the same AD domain. |
| Standalone user-only configuration | A dedicated configuration provisions only users. |
| Standalone group-only configuration | A dedicated configuration provisions only groups. |
| Cloud-native user provisioning | Users created in Microsoft Entra ID are provisioned into AD. |
| SOA-converted user provisioning | Users whose source of authority is converted to the cloud can still be provisioned to AD with continuity. |
| Guest (B2B) user provisioning | External users can be provisioned into AD. |
| Security group provisioning | Security groups from Microsoft Entra ID are provisioned into AD. |
| Group membership (cloud + synced users) | Groups support both cloud-only and synced user members. |
| Attribute updates (Entra ID → AD) | Attribute changes in Microsoft Entra ID flow to AD. |
| Directory extension attributes | Directory extensions tied to user and group accounts flow through to AD. See [Use directory extensions](tutorial-directory-extension-group-provisioning). |
| Provisioning logs and auditing | Logs are available for validation and troubleshooting. |

## Key behaviors

- **Cloud is the source of truth.** Changes made directly in AD might be overwritten by Microsoft Entra ID during the next sync cycle. To protect provisioned objects from on-premises changes, see [Configure AD user and group enforcement](how-to-active-directory-object-enforcement).
- **SOA-converted objects remain cloud-managed.** These users and groups can still be provisioned back into AD after conversion.
- **Match then create.** Existing objects are matched and updated; new objects are created only when no match is found.
- **Target OU behavior.** A default organizational unit (OU) is used unless overridden. A user whose SOA is converted to the cloud is returned to their original OU automatically. Groups aren't — to keep a converted group in its original OU, use a directory extension. See [Preserve the OU path](how-to-configure-entra-to-active-directory#preserve-the-ou-path).
- **Groups.** Only security groups are supported. On-premises user membership must be explicitly enabled.

## When to use provisioning to Active Directory

Provisioning to AD is the mechanism that supports several Source of Authority (SOA) scenarios. Rather than repeat those scenarios here, use the table to jump to the scenario that matches your goal:

| Goal | Scenario | Learn more |
| --- | --- | --- |
| Move group management to the cloud but keep AD access | Govern access with Microsoft Entra ID Governance; AD DS minimization | [Convert Group SOA to the cloud](../concept-source-of-authority-overview) |
| Move user management to the cloud but keep AD access | Minimize AD users and govern the user lifecycle | [Transfer user SOA to the cloud](../user-source-of-authority-overview) |
| Keep Kerberos app access after transferring user SOA | Provision users to AD; use passwordless (Windows Hello for Business / Cloud Kerberos Trust) | [Transfer user SOA to the cloud](../user-source-of-authority-overview) |
| Lock down provisioned groups so only the cloud can change them | AD group enforcement | [Configure AD user and group enforcement](how-to-active-directory-object-enforcement#mark-groups-for-enforcement) |
| Lock down provisioned users so only the cloud can change them | AD user enforcement | [Configure AD user and group enforcement](how-to-active-directory-object-enforcement#mark-users-for-enforcement) |

## What isn't supported

The following scenarios aren't supported:

- Provisioning the **same user to multiple AD domains**. A single target domain per user is enforced to ensure authentication consistency.
- Provisioning identities to **multiple forests that share the same domain name**.
- **Cross-forest** provisioning of user relationships (for example, manager or membership across forests).
- Provisioning **custom security attributes (CSA)** to AD.
- Provisioning **Exchange attributes** to AD. Because user SOA is in the cloud, Exchange-related information isn't needed in AD. For managing Exchange recipients without an on-premises Exchange Server, see [Decommission the last Exchange Server after transferring SOA to cloud](/en-us/exchange/hybrid-deployment/decommission-last-exchange-server) and [Manage recipients in Exchange hybrid environments using management tools](/en-us/exchange/manage-hybrid-exchange-recipients-with-management-tools).
- **Mail-enabled groups and distribution groups.** Only security groups are supported.
- **Password writeback**, which applications that collect a user's password need, isn't supported. This includes applications that authenticate users by performing an LDAP bind with the user's password. Cloud-managed users have no AD DS password to present, so use passwordless authentication for applications that support Kerberos instead. For more information, see [How cloud-managed users sign in to the application](tutorial-users-groups-provisioning-walkthrough#how-cloud-managed-users-sign-in-to-the-application).
- Complex **multi-domain hybrid identity architectures**. Provisioning to AD is designed for single-domain identity continuity.

## License requirements

Provisioning to Active Directory follows a configuration-based licensing model.

| Configuration | License required |
| --- | --- |
| **Existing configurations** (created before general availability) | No license change is required. These configurations continue to run under their existing Microsoft Entra ID P1 licensing. |
| First **2** new configurations per tenant | Microsoft Entra ID P1. |
| **More than 2** new configurations per tenant (3–20) | Microsoft Entra ID Governance. |

Note

A maximum of **20** configurations (domains) can be configured per tenant.