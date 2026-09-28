---
layout: Conceptual
title: Troubleshoot an attribute not synchronizing in Microsoft Entra Connect' - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-connect-attribute-not-syncing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic provides steps for how to troubleshoot issues with attribute synchronization using the troubleshooting task.
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 7cc8731c-38c1-4ff8-ddee-c2bdbe1d8610
document_version_independent_id: ea7c5760-d873-2f9e-a2df-78d0c708bba4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-connect-attribute-not-syncing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-connect-attribute-not-syncing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-connect-attribute-not-syncing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 94a6c3fc-c8a0-9b90-9d81-12850b593676
---

# Troubleshoot an attribute not synchronizing in Microsoft Entra Connect' - Microsoft Entra ID | Microsoft Learn

## **Recommended Steps**

Before investigating attribute syncing issues, let’s understand the **Microsoft Entra Connect** syncing process:

![Microsoft Entra Connect Synchronization Process](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/syncingprocess.png)

### **Terminology**

- **CS:** Connector Space, a table in database.
- **MV:** Metaverse, a table in database.
- **AD:** Active Directory

### **Synchronization Steps**

- Import from AD: Active Directory objects are brought into AD CS.
- Import from Microsoft Entra ID: Microsoft Entra objects are brought into Microsoft Entra CS.
- Synchronization: **Inbound Synchronization Rules** and **Outbound Synchronization Rules** are run in the order of precedence number from lower to higher. To view the Synchronization Rules, you can go to **Synchronization Rules Editor** from the desktop applications. The **Inbound Synchronization Rules** brings in data from CS to MV. The **Outbound Synchronization Rules** moves data from MV to CS.
- Export to AD: After running Synchronization, objects are exported from AD CS to **Active Directory**.
- Export to Microsoft Entra ID: After running Synchronization, objects are exported from Microsoft Entra CS to **Microsoft Entra ID**.

### **Step by Step Investigation**

- We'll start our search from the **Metaverse** and look at the attribute mapping from source to target.
- Launch **Synchronization Service Manager** from the desktop applications, as shown below:

    ![Launch Synchronization Service Manager](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/startmenu.png)
- On the **Synchronization Service Manager**, select the **Metaverse Search**, select **Scope by Object Type**, select the object using an attribute, and click **Search** button.

    ![Metaverse Search](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/mvsearch.png)
- Double click the object found in the **Metaverse** search to view all its attributes. You can click on the **Connectors** tab to look at corresponding object in all the **Connector Spaces**.

    ![Metaverse Object Connectors](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/mvattributes.png)
- Double click on the **Active Directory Connector** to view the **Connector Space** attributes. Click on the **Preview** button, on the following dialog click on the **Generate Preview** button.

    ![Screenshot that shows the Connector Space Object Properties screen with the Preview button highlighted.](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/csattributes.png)
- Now click on the **Import Attribute Flow**, this shows flow of attributes from **Active Directory Connector Space** to the **Metaverse**. **Sync Rule** column shows which **Synchronization Rule** contributed to that attribute. **Data Source** column shows you the attributes from the **Connector Space**. **Metaverse Attribute** column shows you the attributes in the **Metaverse**. You can look for the attribute not syncing here. If you don't find the attribute here, then this isn't mapped and you have to create new custom **Synchronization Rule** to map the attribute.

    ![Connector Space Attributes](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/cstomvattributeflow.png)
- Click on the **Export Attribute Flow** in the left pane to view the attribute flow from **Metaverse** back to **Active Directory Connector Space** using **Outbound Synchronization Rules**.

    ![Screenshot that shows the attribute flow from Metaverse back to Active Directory Connector Space using Outbound Synchronization Rules.](media/tshoot-connect-attribute-not-syncing/tshoot-connect-attribute-not-syncing/mvtocsattributeflow.png)
- Similarly, you can view the **Microsoft Entra Connector Space** object and can generate the **Preview** to view attribute flow from **Metaverse** to the **Connector Space** and vice versa, this way you can investigate why an attribute isn't syncing.

## **Recommended Documents**

- [Microsoft Entra Connect Sync: Technical Concepts](how-to-connect-sync-technical-concepts)
- [Microsoft Entra Connect Sync: Understanding the architecture](concept-azure-ad-connect-sync-architecture)
- [Microsoft Entra Connect Sync: Understanding Declarative Provisioning](concept-azure-ad-connect-sync-declarative-provisioning)
- [Microsoft Entra Connect Sync: Understanding Declarative Provisioning Expressions](concept-azure-ad-connect-sync-declarative-provisioning-expressions)
- [Microsoft Entra Connect Sync: Understanding the default configuration](concept-azure-ad-connect-sync-default-configuration)
- [Microsoft Entra Connect Sync: Understanding Users, Groups, and Contacts](concept-azure-ad-connect-sync-user-and-contacts)
- [Microsoft Entra Connect Sync: Shadow attributes](how-to-connect-syncservice-shadow-attributes)