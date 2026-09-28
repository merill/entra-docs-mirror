---
layout: Conceptual
title: How to customize a synchronization rule in Microsoft Entra Connect' - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-create-custom-sync-rule
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to use the synchronization rule editor to edit or create a new synchronization rule.
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: cdac63f7-e72c-ab3f-ce31-b1c3043f3d28
document_version_independent_id: 80496454-fe0d-ead3-a051-70f86b4e078c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-create-custom-sync-rule.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-create-custom-sync-rule
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-create-custom-sync-rule.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5f5ca900-88f1-960d-29fd-935e55e372a7
---

# How to customize a synchronization rule in Microsoft Entra Connect' - Microsoft Entra ID | Microsoft Learn

## **Recommended Steps**

You can use the synchronization rule editor to edit or create a new synchronization rule. You need to be an advanced user to make changes to synchronization rules. Any wrong changes may result in deletion of objects from your target directory. Please review the Recommended Documents section. To modify a synchronization rule, go through following steps:

- Launch the synchronization editor from the application menu in desktop as shown below:

    ![Synchronization Rule Editor Menu](media/how-to-connect-create-custom-sync-rule/how-to-connect-create-custom-sync-rule/syncruleeditormenu.png)
- In order to customize a default synchronization rule, clone the existing rule by clicking the “Edit” button on the Synchronization Rules Editor, which will create a copy of the standard default rule and disable it. Save the cloned rule with a precedence less than 100. Precedence determines what rule wins(lower numeric value) a conflict resolution if there's an attribute flow conflict.

    ![Synchronization Rule Editor](media/how-to-connect-create-custom-sync-rule/how-to-connect-create-custom-sync-rule/clonerule.png)
- When modifying a specific attribute, ideally you should only keep the modifying attribute in the cloned rule. Then enable the default rule so that modified attribute comes from cloned rule and other attributes are picked from default standard rule.
- In the case where the calculated value of the modified attribute is NULL, in your cloned rule, and isn't NULL in the default standard rule then, the not NULL value will win and will replace the NULL value. If you don’t want a NULL value to be replaced with a not NULL value, then assign AuthoritativeNull in your cloned rule.
- To modify an **Outbound** rule, change filter from the synchronization rule editor.

## **Recommended Documents**

- [Microsoft Entra Connect Sync: Technical Concepts](how-to-connect-sync-technical-concepts)
- [Microsoft Entra Connect Sync: Understanding the architecture](concept-azure-ad-connect-sync-architecture)
- [Microsoft Entra Connect Sync: Understanding Declarative Provisioning](concept-azure-ad-connect-sync-declarative-provisioning)
- [Microsoft Entra Connect Sync: Understanding Declarative Provisioning Expressions](concept-azure-ad-connect-sync-declarative-provisioning-expressions)
- [Microsoft Entra Connect Sync: Understanding the default configuration](concept-azure-ad-connect-sync-default-configuration)
- [Microsoft Entra Connect Sync: Understanding Users, Groups, and Contacts](concept-azure-ad-connect-sync-user-and-contacts)
- [Microsoft Entra Connect Sync: Shadow attributes](how-to-connect-syncservice-shadow-attributes)