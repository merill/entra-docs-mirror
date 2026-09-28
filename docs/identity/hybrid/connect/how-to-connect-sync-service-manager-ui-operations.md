---
layout: Conceptual
title: Microsoft Entra Connect Synchronization Service Manager Operations - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-service-manager-ui-operations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Understand the Operations tab in the Synchronization Service Manager for Microsoft Entra Connect.
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: H1Hack27Feb2017, sfi-image-nochange
locale: en-us
document_id: 8e61bcca-0be9-998c-fca9-feec68f5df52
document_version_independent_id: 3528b3e6-a241-191e-e644-d062a3c3639a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-service-manager-ui-operations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-service-manager-ui-operations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-service-manager-ui-operations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 605f57d7-699c-7d4e-79ce-25fddd70f2b3
---

# Microsoft Entra Connect Synchronization Service Manager Operations - Microsoft Entra ID | Microsoft Learn

![Sync Service Manager](media/how-to-connect-sync-service-manager-ui-operations/operations.png)

The operations tab shows the results from the most recent operations. This tab is key to understand and troubleshoot issues.

## Understand the information visible in the operations tab

The top half shows all runs in chronological order. By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](how-to-connect-sync-feature-scheduler). You want to look for any run that doesn't show a success status. You can change the sorting by selecting the headers.

The **Status** column is the most important information and shows the most severe problem for a run. Here is a quick summary of the most common statuses in order of priority to investigate (where \* indicate several possible error strings).

| Status | Comment |
| --- | --- |
| stopped-\* | The run couldn't complete. For example, if the remote system is down and can't be contacted. |
| stopped-error-limit | There are more than 5,000 errors. The run was automatically stopped due to the large number of errors. |
| completed-\*-errors | The run completed, but there are errors (fewer than 5,000) that should be investigated. |
| completed-\*-warnings | The run completed, but some data isn't in the expected state. If you have errors, then this message is only a symptom. Until you address the errors, you shouldn't investigate warnings. |
| success | No issues. |

When you select a row, the bottom updates to show the details of that run. To the far left of the bottom, you might have a list saying **Step #**. This list only appears if you have multiple domains in your forest where each domain is represented by a step. The domain name can be found under the heading **Partition**. Under **Synchronization Statistics**, you can find more information about the number of changes that were processed. You can select the links to get a list of the changed objects. If you have objects with errors, the errors show up under **Synchronization Errors**.

For more information, see [troubleshoot an object that isn't synchronizing](tshoot-connect-object-not-syncing)