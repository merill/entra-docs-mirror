---
layout: Conceptual
title: Set up group writeback within entitlement management - Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-group-writeback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to set up group writeback in entitlement management.
editor: HANKI
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
ms.reviewer: sponnada
locale: en-us
document_id: 3fc5827d-f641-38b6-ad57-64a2592c1f42
document_version_independent_id: 7bb90aa7-8ac6-4146-c15c-09118899af44
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-group-writeback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-group-writeback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-group-writeback.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: b37f4d88-1129-4d3a-24e0-8cb232898c42
---

# Set up group writeback within entitlement management - Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn

This article shows you how to set up group writeback in entitlement management. Group writeback is a feature that allows you to write cloud groups back to your on-premises Active Directory instance by using Microsoft Entra Cloud Sync.

## Set up group writeback in entitlement management

To set up group writeback for Microsoft 365 groups in access packages, you must complete the following prerequisites:

- Set up group writeback in the Microsoft Entra admin center.
- The Organizational Unit (OU) that is used to set up group writeback in Microsoft Entra Cloud Sync Configuration.
- Complete the [group writeback enablement steps](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory) for Microsoft Entra Cloud Sync.

Using group writeback, you can now sync security groups that are part of access packages to on-premises Active Directory. To sync the groups, follow the steps:

1. Create a Microsoft Entra security group.
2. Set the group to be written back to on-premises Active Directory. For instructions, see [Group writeback in the Microsoft Entra admin center](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory).
3. Add the group to an access package as a resource role. See [Create a new access package](entitlement-management-access-package-create#select-resource-roles) for guidance.
4. Launch Active Directory Users and Computers, and wait for the resulting new AD group to be created in the AD domain. When it's present, record the distinguished name, domain, account name and SID of the new AD group.
5. Configure the application to use the new group, either by updating the application or adding the group as a member of an existing group, as described in [Govern on-premises Active Directory based apps (Kerberos) using Microsoft Entra ID Governance](../identity/hybrid/cloud-sync/govern-on-premises-groups).
6. Assign the identities to the access package. See [View, add, and remove assignments for an access package](entitlement-management-access-package-assignments#directly-assign-an-identity) for instructions to directly assign a user.
7. After you've assigned an identity to the access package, confirm that the user is now a member of the on-premises group once Microsoft Entra Cloud Sync cycle completes:

    1. View the member property of the group in the on-premises OU OR
    2. Review the member Of on the user object.

    Note

    Microsoft Entra Cloud Sync's default sync cycle schedule is every 30 minutes. You may need to wait until the next cycle occurs to see results on-premises or choose to run the sync cycle manually to see results sooner.
8. In your AD domain monitoring, allow only the gMSA account that runs the provisioning agent to have authorization to change the membership in the new AD group.