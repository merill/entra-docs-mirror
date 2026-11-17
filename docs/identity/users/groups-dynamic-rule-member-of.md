---
layout: Conceptual
title: Deprecated memberOf preview for dynamic membership groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-dynamic-rule-member-of
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn about the deprecated memberOf preview for dynamic membership groups in Microsoft Entra ID and find guidance for moving to MemberOf Next.
ms.topic: concept-article
ms.date: 2026-11-16T00:00:00.0000000Z
ms.reviewer: mbhargav
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: a30c67d5-6cc0-16f3-db2a-8244d7344aa3
document_version_independent_id: ab230d40-68c6-3a1f-c4c3-12d4a76e42df
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-dynamic-rule-member-of.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-dynamic-rule-member-of
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-dynamic-rule-member-of.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0c7cfd28-27d2-eb3f-9eca-8e6024fad234
---

# Deprecated memberOf preview for dynamic membership groups - Microsoft Entra ID | Microsoft Learn

Important

The earlier `memberOf` preview was deprecated in favor of **MemberOf Next**. The earlier preview ended on **November 3, 2026**. Dynamic membership groups, dynamic administrative units, and entitlement management auto-assignment policies that still used the earlier preview stopped updating and remained in their last known state.

For current capabilities, requirements, and setup instructions, see [Use MemberOf Next and Transitive Reports To in dynamic membership groups (preview)](groups-dynamic-rule-advanced). To move existing groups to MemberOf Next, see [Move existing MemberOf groups to MemberOf Next](groups-dynamic-rule-advanced#move-existing-memberof-groups-to-memberof-next).

The earlier `memberOf` preview in Microsoft Entra ID enabled admins to create dynamic membership groups and administrative units that populated by adding members of other groups. Apps that couldn't read group-based membership previously could read the flattened membership of these `memberOf` groups. These groups could also be used for licensing assignments.

The following diagram illustrates how the earlier preview populated Dynamic-Group-A with direct members of Security-Group-X and Security-Group-Y. Members of nested groups inside Security-Group-X and Security-Group-Y weren't included in Dynamic-Group-A.

![Diagram that shows how the memberOf attribute worked in the deprecated preview.](media/groups-dynamic-rule-member-of/member-of-diagram.png)

The earlier preview was available through the Azure portal, Microsoft Graph, and PowerShell. Source groups could be security groups, Microsoft 365 groups, or groups synced from on-premises Active Directory.

## Preview limitations

The following limitations applied to the deprecated preview. For the limitations of its replacement, see [MemberOf Next and Transitive Reports To preview limitations](groups-dynamic-rule-advanced#preview-limitations).

- The earlier preview was intended only for test environments because it could affect dynamic group processing across the tenant.
- Each Microsoft Entra tenant was limited to 500 dynamic groups that used the `memberOf` attribute. These groups counted toward the total dynamic group quota of 15,000.
- Each dynamic group could reference up to 50 source groups.
- Only direct members of source groups were included. Members of nested groups weren't included.
- A `memberOf` dynamic group couldn't define the membership of another `memberOf` dynamic group.
- The `memberOf` attribute couldn't be combined with other rules or operators.
- The dynamic group rule builder and rule validation weren't supported for `memberOf`.
- Large numbers of groups or frequent membership updates could slow dynamic membership processing for the tenant.
- Membership didn't automatically update when a source group was deleted. Affected users or devices remained members until the rule was modified.
- The earlier preview was available only in the public cloud.

## Move to MemberOf Next

MemberOf Next replaces the earlier preview with separate processing on a twice-daily schedule. It requires Microsoft Entra ID Governance and Standard priority. The name shown in the product and the rule syntax are unchanged.

For migration requirements and instructions, see [Move existing MemberOf groups to MemberOf Next](groups-dynamic-rule-advanced#move-existing-memberof-groups-to-memberof-next). For current setup instructions and guidance for dynamic administrative units, see [Use MemberOf Next and Transitive Reports To in dynamic membership groups (preview)](groups-dynamic-rule-advanced).