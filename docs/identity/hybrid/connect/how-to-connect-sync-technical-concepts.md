---
layout: Conceptual
title: 'Microsoft Entra Connect Sync: Technical concepts - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-technical-concepts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Explains the technical concepts of Microsoft Entra Connect Sync.
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 74c7cc23-9838-bf11-e323-13373d6177fd
document_version_independent_id: 531c07fc-383e-51f7-ae16-d29cfb414cfb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-technical-concepts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-technical-concepts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-technical-concepts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: df05b531-330d-3268-9b38-31b04d62bb4e
---

# Microsoft Entra Connect Sync: Technical concepts - Microsoft Entra ID | Microsoft Learn

This article is a summary of the topic [Understanding architecture](how-to-connect-sync-technical-concepts).

Microsoft Entra Connect Sync builds upon a solid metadirectory synchronization platform. The following sections introduce the concepts for metadirectory synchronization. The Azure Active Directory Sync Services provides a platform for connecting to data sources, synchronizing data between data sources, and the provisioning and deprovisioning of identities.

![Technical Concepts](media/how-to-connect-sync-technical-concepts/scenario.png)

The following sections provide more details about the following aspects of the Synchronization Service:

- Connector
- Attribute flow
- Connector space
- Metaverse
- Provisioning

## Connector

The code modules that are used to communicate with a connected directory are called connectors (formerly known as management agents (MAs)).

These are installed on the computer running Microsoft Entra Connect Sync. The connectors provide the agentless ability to converse by using remote system protocols instead of relying on the deployment of specialized agents. This means decreased risk and deployment times, especially when dealing with critical applications and systems.

In the previous picture, the connector is synonymous with the connector space but encompasses all communication with the external system.

The connector is responsible for all import and export functionality to the system and frees developers from needing to understand how to connect to each system natively when using declarative provisioning to customize data transformations.

Imports and exports only occur when scheduled, allowing for further insulation from changes occurring within the system, since changes don't automatically propagate to the connected data source. In addition, developers may also create their own connectors for connecting to virtually any data source.

## Attribute flow

The metaverse is the consolidated view of all joined identities from neighboring connector spaces. In the previous figure, attribute flow is depicted by lines with arrowheads for both inbound and outbound flow. Attribute flow is the process of copying or transforming data from one system to another and all attribute flows (inbound or outbound).

Attribute flow occurs between the connector space and the metaverse bi-directionally when synchronization (full or delta) operations are scheduled to run.

Attribute flow only occurs when these synchronizations are run. Attribute flows are defined in Synchronization Rules. These can be inbound (ISR in the previous picture) or outbound (OSR in the prior picture).

## Connected system

Connected system is referring to the remote system Microsoft Entra Connect Sync connected to and reading and writing identity data to and from.

## Connector space

Each connected data source is represented as a filtered subset of the objects and attributes in the connector space. This allows the sync service to operate locally without the need to contact the remote system when synchronizing the objects and restricts interaction to imports and exports only.

When the data source and the connector have the ability to provide a list of changes (a delta import), then the operational efficiency increases dramatically as only changes since the last polling cycle are exchanged. The connector space insulates the connected data source from changes propagating automatically by requiring that the connector schedule imports and exports. This added insurance grants you peace of mind while testing, previewing, or confirming the next update.

## Metaverse

The metaverse is the consolidated view of all joined identities from neighboring connector spaces.

As identities are linked together and authority is assigned for various attributes through import flow mappings, the central metaverse object begins to aggregate information from multiple systems. From this object attribute flow, mappings carry information to outbound systems.

Objects are created when an authoritative system projects them into the metaverse. As soon as all connections are removed, the metaverse object is deleted.

Objects in the metaverse can't be edited directly. All data in the object must be contributed through attribute flow. The metaverse maintains persistent connectors with each connector space. These connectors don't require reevaluation for each synchronization run. This means that Microsoft Entra Connect Sync doesn't have to locate the matching remote object each time. This avoids the need for costly agents to prevent changes to attributes that would normally be responsible for correlating the objects.

When discovering new data sources that have preexisting objects which need to be managed, Microsoft Entra Connect Sync uses a process called a join rule to evaluate potential candidates with which to establish a link. Once the link is established, this evaluation doesn't reoccur and normal attribute flow can occur between the remote connected data source and the metaverse.

## Provisioning

When an authoritative source projects a new object into the metaverse a new connector space object can be created in another Connector representing a downstream connected data source.

This inherently establishes a link, and attribute flow can proceed bi-directionally.

Whenever a rule determines that a new connector space object needs to be created, it's called provisioning. However, because this operation only takes place within the connector space, it doesn't carry over into the connected data source until an export is performed.