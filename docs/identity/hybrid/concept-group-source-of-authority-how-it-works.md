---
layout: Conceptual
title: How to use group Source of Authority (SOA) to manage Active Directory Domain Services (AD DS) groups in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/concept-group-source-of-authority-how-it-works
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to convert group management from Active Directory Domain Services (AD DS) to Microsoft Entra ID using group source of authority (SOA).
ms.subservice: hybrid-cloud-sync
ms.topic: concept-article
ms.date: 2025-08-01T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 67b994ed-1ed9-a2a5-afca-a53a37dda300
document_version_independent_id: 67b994ed-1ed9-a2a5-afca-a53a37dda300
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/concept-group-source-of-authority-how-it-works.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/concept-group-source-of-authority-how-it-works
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/concept-group-source-of-authority-how-it-works.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d945a0bf-5fd2-fe3e-cd9d-2cf60cfa1f28
---

# How to use group Source of Authority (SOA) to manage Active Directory Domain Services (AD DS) groups in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

You can convert the Source of Authority (SOA) of a group from Active Directory Domain Services (AD DS) to Microsoft Entra ID. After you convert the SOA, the group becomes cloud-owned, and you can map it to a corresponding cloud group type in the cloud. For a list of supported groups types, see [How to manage cloud security groups](concept-group-source-of-authority-guidance#how-to-manage-cloud-security-groups).

## Block sync from AD DS to Microsoft Entra ID after SOA change

After you convert the group SOA and it becomes a cloud group, the latest versions of Microsoft Entra Connect Sync and Microsoft Entra Cloud Sync honor the SOA setting. They don't continue to sync the group. When you no longer need the AD DS group, you can delete it rather than remove it as out-of-scope in your scoping filters.

## Seamless integration with security group provisioning to AD DS

To provision a cloud security group that's not mail-enabled back to AD DS and sync it with Microsoft Entra ID, add the group to the scoping configuration when you provision groups to AD DS. Use **Selected Groups** or **All groups** with attribute value scoping. Provision dynamic security groups to AD DS. Cloud security groups are provisioned as Universal groups.

When Microsoft Entra Cloud Sync provisions a security group to AD DS, it recognizes when existing domain groups previously had SOA applied and are provisioned from Microsoft Entra ID to AD DS. The security identifier (SID) value correlates them together. Therefore, provisioning the cloud security group to AD DS does so to the original AD group (if it exists). If it doesn’t find a match in AD DS, it creates a new on-premises security group.

## Delete and restore groups in AD DS

Let's suppose you delete an on-premises group in AD DS. Later, you decide to provision the group with the same SID to the AD DS domain using Microsoft Entra Cloud Sync. In this case, you need to be sure that the **Active Directory Recycle Bin** is enabled. You should restore the group from the **Active Directory Recycle Bin** before you add it to the scope for group provisioning to AD DS.

## Roll back SOA changes

You can reverse SOA changes to a group. In this scenario, the group SOA reverts, and AD DS manages it. During the next synchronization cycle, AD DS takes control of the group. In Microsoft Entra ID, the group becomes read-only.

This method retains any changes made while the group was managed in the cloud. After the object is taken over, any modifications made in the cloud are overridden.