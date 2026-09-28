---
layout: Conceptual
title: Microsoft Entra Cloud Sync supported topologies and scenarios - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/plan-cloud-sync-topologies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn about various on-premises and Microsoft Entra topologies that use Microsoft Entra Cloud Sync.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 793df638-faa2-8d6b-1b94-f6ac79b84368
document_version_independent_id: 40a3d7d6-8aa5-d2db-9409-c7f5fb11724d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/plan-cloud-sync-topologies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/plan-cloud-sync-topologies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/plan-cloud-sync-topologies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6c94eab0-fd11-7176-46ea-e4045770c5b5
---

# Microsoft Entra Cloud Sync supported topologies and scenarios - Microsoft Entra ID | Microsoft Learn

This article describes various on-premises and Microsoft Entra topologies that use Microsoft Entra Cloud Sync. This article includes only supported configurations and scenarios.

Important

Microsoft doesn't support modifying or operating Microsoft Entra Cloud Sync outside of the configurations or actions that are formally documented. Any of these configurations or actions might result in an inconsistent or unsupported state of Microsoft Entra Cloud Sync. As a result, Microsoft can't provide technical support for such deployments.

## Things to remember about all scenarios and topologies

The following information should be kept in mind, when selecting a solution.

- Users and groups must be uniquely identified across all forests.
- Matching across forests doesn't occur with cloud sync.
- The source anchor for objects is chosen automatically. It uses ms-DS-ConsistencyGuid if present, otherwise ObjectGUID is used.
- You can't change the attribute that is used for source anchor.

## Active Directory to Microsoft Entra ID supported topologies

The following topologies are supported for provisioning from Active Directory to Microsoft Entra ID.

### Single forest, single Microsoft Entra tenant

![Diagram that shows the topology for a single forest and a single tenant.](../../../includes/governance/media/tutorial-single-forest/diagram-2.png)

The simplest topology is a single on-premises forest, with one or multiple domains, and a single Microsoft Entra tenant. For an example of this scenario see [Tutorial: A single forest with a single Microsoft Entra tenant](tutorial-single-forest)

### Multi-forest, single Microsoft Entra tenant

![Diagram that shows a multi-forest topology with a single Microsoft Entra tenant.](media/plan-cloud-provisioning-topologies/multi-forest-2.png)

Multiple AD forests are a common topology, with one or multiple domains, and a single Microsoft Entra tenant.

### Existing forest with Microsoft Entra Connect, new forest with cloud Provisioning

![Diagram that shows the topology for an existing forest and a new forest.](media/tutorial-existing-forest/existing-forest-new-forest-2.png)

This scenario topology is similar to the multi-forest scenario. However, this one involves an existing Microsoft Entra Connect environment and then bringing on a new forest using Microsoft Entra Cloud Sync. For an example of this scenario see [Tutorial: An existing forest with a single Microsoft Entra tenant](tutorial-existing-forest)

### Piloting Microsoft Entra Cloud Sync in an existing hybrid AD forest

![Diagram that shows a single-forest topology with a single Microsoft Entra tenant.](media/tutorial-migrate-aadc-aadccp/diagram-2.png)

The piloting scenario involves the existence of both Microsoft Entra Connect and Microsoft Entra Cloud Sync in the same forest and scoping the users and groups accordingly. NOTE: An object should be in scope in only one of the tools.

For an example of this scenario see [Tutorial: Pilot Microsoft Entra Cloud Sync in an existing synced AD forest](tutorial-pilot-aadc-aadccp)

### Merging objects from disconnected sources

#### (Public Preview)

![Diagram that shows attributes of a single user being merged from two disconnected Active Directory forests.](media/plan-cloud-provisioning-topologies/attributes-multiple-sources.png)

In this scenario, the attributes of a user are contributed to by two disconnected Active Directory forests.

An example would be:

- One forest (1) contains most of the attributes.
- A second forest (2) contains a few attributes.

Since the second forest doesn't have network connectivity to the Microsoft Entra Connect server, the object can't be merged through Microsoft Entra Connect. Cloud sync in the second forest allows the attribute value to be retrieved from the second forest. Microsoft Entra Connect syncs the object in Microsoft Entra ID, and then the value can be merged with it.

This configuration is advanced and there are a few caveats to this topology:

1. You must use `ms-DS-ConsistencyGuid` as the source anchor in the cloud sync configuration.
2. The `ms-DS-ConsistencyGuid` of the user object in the second forest must match that of the corresponding object in Microsoft Entra ID.
3. You must populate the `UserPrincipalName` attribute and the `Alias` attribute in the second forest and it must match the ones that are synced from the first forest.
4. You must remove all attributes from the attribute mapping in the cloud sync configuration that don't have a value or may have a different value in the second forest – you can't have overlapping attribute mappings between the first forest and the second one.
5. If there's no matching object in the first forest, for an object that is synced from the second forest, then cloud sync still creates the object in Microsoft Entra ID. The object only has the attributes that are defined in the mapping configuration of cloud sync for the second forest.
6. If you delete the object from the second forest, it temporarily soft deletes in Microsoft Entra ID. It automatically restores after the next Microsoft Entra Connect Sync cycle.
7. If you delete the object from the first forest, it is soft deleted from Microsoft Entra ID. The object won't be restored unless a change is made to the object in the second forest. After 30 days, the object is hard deleted from Microsoft Entra ID. If a change is made to the object in the second forest, it's created as a new object in Microsoft Entra ID.

## Microsoft Entra ID to Active Directory supported topologies

The following topologies are supported for provisioning from Microsoft Entra ID to Active Directory.

### Single forest group provisioning to Active Directory

[![Conceptual diagram of single forest writeback.](media/plan-cloud-provisioning-topologies/single-forest-group-writeback.png)](media/plan-cloud-provisioning-topologies/single-forest-group-writeback.png#lightbox)

The simplest group provisioning topology is a single on-premises forest, with one or multiple domains, and a single Microsoft Entra tenant. For an example of this scenario, see [Provision users and groups from Microsoft Entra ID to Active Directory](how-to-configure-entra-to-active-directory).

### Multi-forest group provisioning to Active Directory

[![Conceptual diagram of multi-forest writeback.](media/plan-cloud-provisioning-topologies/multi-forest-group-writeback.png)](media/plan-cloud-provisioning-topologies/multi-forest-group-writeback.png#lightbox)

A more advanced group provisioning topology consists of multiple on-premises AD forests sharing a single Microsoft Entra ID tenant.

This configuration is advanced and there are a few things to remember with this topology:

- Group membership provisioned to AD includes only members that have an AD account. Those members can be on-premises synchronized users, cloud-managed users that Cloud Sync provisions to AD because they're in scope of user provisioning, or other cloud created security groups.
- On-premises synchronized users must have the onPremisesObjectIdentifier attribute set on their account.
- The onPremisesObjectIdentifier must match a corresponding objectGUID in the target AD environment.
- An on-premises users objectGUID attribute to a cloud users onPremisesObjectIdentifier attribute can be synchronized using either Microsoft Entra Cloud Sync ([1.1.1370.0](reference-version-history#1113700)) or Microsoft Entra Connect Sync ([2.2.8.0](../connect/reference-connect-version-history#2280))
- Inside your tenant you may share a common group that contains users from both forests.
- However, users that don't exist in the other forest, aren't provisioned as members of the group when it's provisioned on-premises. So if you have a group in Microsoft Entra ID that contains users from contoso.com and fabrikam.com, only users that exist in the contoso.com forest are members of the group when provisioned to contoso.com. The same is true with fabrikam.