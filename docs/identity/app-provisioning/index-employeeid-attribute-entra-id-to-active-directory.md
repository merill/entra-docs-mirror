---
layout: Conceptual
title: Index the employeeId attribute in Active Directory to improve provisioning performance - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/index-employeeid-attribute-entra-id-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to get index the employeeId attribute to automate user account creation and updates from Inbound Provisioning to Active Directory
ms.topic: how-to
ms.date: 2025-07-24T00:00:00.0000000Z
ms.reviewer: cmmdesai
locale: en-us
document_id: bf17757c-f4ef-f3fe-c4cf-f1a4be46e0a8
document_version_independent_id: bf17757c-f4ef-f3fe-c4cf-f1a4be46e0a8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/index-employeeid-attribute-entra-id-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/index-employeeid-attribute-entra-id-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/index-employeeid-attribute-entra-id-to-active-directory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fabbacd8-8cb2-5407-bd0c-d844bc82f43d
---

# Index the employeeId attribute in Active Directory to improve provisioning performance - Microsoft Entra ID | Microsoft Learn

Microsoft Entra inbound provisioning allows organizations to automate user account creation and updates in on-premises Active Directory (AD) environments from sources such as Workday, SuccessFactors, or API-driven integrations. To ensure smooth and efficient synchronization, it's important to understand the role of attribute indexing—particularly the `employeeId` attribute, which is used as the default matching property during provisioning. This article provides guidance for optimizing synchronization performance with the `employeeId` attribute.

## Why indexing employeeId is needed

By default, the `employeeId` attribute isn't indexed in Active Directory. However, we recommend indexing this attribute as it's used as the primary property to match identities between Microsoft Entra and AD during both full and incremental provisioning runs. Without indexing, directory lookups may be slower as your user base grows, potentially impacting synchronization performance and increasing provisioning times. Indexing ensures that these operations are completed efficiently and reliably.

## Scope: Applies to multiple provisioning scenarios

This guidance applies to all Microsoft Entra inbound provisioning scenarios that synchronize identities to on-premises AD, including:

- Workday-to-Active Directory provisioning
- SuccessFactors-to-Active Directory provisioning
- API-driven inbound provisioning-to-Active Directory

## Multiple matching properties

If your provisioning setup uses more than one matching property (for example, `employeeId` and `mail`), be sure to check that each property is indexed in Active Directory. Indexing all matching properties used in synchronization helps maintain optimal performance and reduces the risk of delays or timeouts during provisioning runs.

## Impact on Active Directory domain storage

Enabling indexing for other attributes such as `employeeId` increases storage requirements within your AD domain. While the storage impact is typically modest, it's important to consider this when planning large-scale deployments or when working with domains that have limited available resources.

## How to use the AD schema snap-in to index an attribute (for example, employeeId)

**Prerequisites:**

- Ensure you're a member of the **Schema Admins** group in Active Directory.
- The AD Schema snap-in isn't registered by default; you must register it first.

### Register the schema snap-in

1. Open a Command Prompt as a *Windows Server Administrator*.
2. Run: `regsvr32 schmmgmt.dll` You should see a confirmation dialog that the registration succeeded.

### Open the schema snap-in

1. Press **Win + R**, type **mmc**, then press **Enter** to open the Microsoft Management Console.
2. In the console, go to **File &gt; Add/Remove Snap-in**.
3. Select **Active Directory Schema** from the list, then click **Add**.
4. Click **OK**.

### Locate the attribute to index

1. In the left pane, expand Active Directory Schema and select **Attributes**.
2. Scroll through the list to find the attribute you want to index (for example, `employeeId`).

### Edit attribute properties

1. Right-click the attribute (for example, `employeeId`), then select **Properties**.
2. In the properties dialog, check the box labeled **Index this attribute** (or similar wording, depending on your Windows Server version).![Screenshot of the employee ID attribute properties.](media/index-employee-id-attribute-entra-id-to-active-directory/screenshot-employee-id-attributes-properties.png)

### Apply and replicate changes

Click **OK** to save your changes. Schema changes are replicated to all domain controllers. It may take some time for the change to propagate.