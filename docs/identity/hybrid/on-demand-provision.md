---
layout: Conceptual
title: On-demand provisioning using cloud sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/on-demand-provision
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to use on-demand provisioning with Microsoft Entra Cloud Sync.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 8f1a4bf8-be49-11b9-eaae-c8192424d845
document_version_independent_id: 45749c9d-91fd-0395-53c9-8833a27d50b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/on-demand-provision.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/on-demand-provision
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/on-demand-provision.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c874f313-13e4-108f-043e-ea0d2b50f1b9
---

# On-demand provisioning using cloud sync - Microsoft Entra ID | Microsoft Learn

You can use cloud sync to test configuration changes by applying these changes to a single user. This on-demand provisioning helps you validate and verify that the changes made to the configuration were applied properly and are being correctly synchronized to Microsoft Entra ID. This feature is only available in cloud sync and not Microsoft Entra Connect.

## Steps to use on-demand provisioning

To use on-demand provisioning, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Enter the distinguished name of a user and select the **Provision** button.
4. Once the process completes, a success screen appears with four green check marks. Any errors appear on the left side of the screen.