---
layout: Conceptual
title: Uninstall Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-uninstall
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document describes how to uninstall Microsoft Entra Connect.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: b7d1708c-708f-706a-35f1-751e9ce9c16b
document_version_independent_id: 696662d5-f3de-9736-fadd-90902f9db714
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-uninstall.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-uninstall
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-uninstall.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 47165d83-d5fc-8b60-c289-3f5739994c43
---

# Uninstall Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

This document describes how to correctly uninstall Microsoft Entra Connect.

## Uninstall Microsoft Entra Connect from the server

The first thing you need to do is remove Microsoft Entra Connect from the server that it's running on. Use the following steps:

1. On the server running Microsoft Entra Connect, navigate to **Control Panel**.
2. Select **Uninstall a program**![Uninstall a program](media/how-to-connect-uninstall/uninstall-1.png)
3. Select **Microsoft Entra Connect**. ![Select Microsoft Entra Connect](media/how-to-connect-uninstall/uninstall-2.png)
4. When prompted, select **Yes** to confirm.
5. This confirmation brings up the Microsoft Entra Connect screen. Select **Remove**. ![Remove](media/how-to-connect-uninstall/uninstall-3.png)
6. Once this action completes, select **Exit**.
7. ![Exit](media/how-to-connect-uninstall/uninstall-4.png)
8. Back in **Control Panel** select **Refresh** and all of the components should be removed.