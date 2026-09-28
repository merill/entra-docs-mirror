---
layout: Conceptual
title: Understand how expression builder works with Application Provisioning in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/expression-builder
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Understand how expression builder works with Application Provisioning in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-08-06T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
locale: en-us
document_id: b3ff9f49-1560-d727-6b82-4e1bde9b59b5
document_version_independent_id: 3241fa8b-8b7f-d1a5-6f73-8077f1632cc2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/expression-builder.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/expression-builder
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/expression-builder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
platformId: 11676758-156b-20fb-4e5b-e9e197d078c0
---

# Understand how expression builder works with Application Provisioning in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

You can use [expressions](functions-for-customizing-application-data) to [map attributes](customize-application-attributes). Previously, you had to create these expressions manually and enter them into the expression box. Expression builder is a tool you can use to help you create expressions.

[![The default expression builder page before selecting a function.](media/expression-builder/expression-builder.png)](media/expression-builder/expression-builder.png#lightbox)

For reference on building expressions, see [Reference for writing expressions for attribute mappings](functions-for-customizing-application-data).

## Finding the expression builder

In application provisioning, you use expressions for attribute mappings. You access Expression Builder on the attribute mapping page by selecting the **Expression builder** from the left navigation menu.

## Using expression builder

To use expression builder, select a function and attribute and then enter a suffix if needed. Then select **Add expression** to add the expression to the code box. To learn more about the functions available and how to use them, see [Reference for writing expressions for attribute mappings](functions-for-customizing-application-data).

Test the expression by providing values and selecting **Test expression**. For example, from the dropdown list, select the **mail** attribute. Fill in the value with the email domain that starts with the @ sign; for example, `@fabrikam.com`. Then select **Test expression** and the output of the expression test appears in the **View expression output** box.

When you're satisfied with the expression, move it to an attribute mapping. Copy and paste it into the expression box for the attribute mapping you're working on.

## Known limitations

- Extension attributes aren't available for selection in the expression builder. However, extension attributes can be used in the attribute mapping expression.
- The maximum supported length for a single attribute mapping expression is **10,000 characters**.