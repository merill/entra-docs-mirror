---
layout: Conceptual
title: Troubleshoot writeback issues with HR provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/hr-writeback-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This article provides potential issues and resolutions so you can troubleshoot writeback issues with HR provisioning.
ms.topic: troubleshooting
ms.workload: identity
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: chmutali
locale: en-us
document_id: 68b5136c-54ac-e14d-f974-fb1b6ff26f55
document_version_independent_id: fbac30c5-42f9-d111-759a-81fbc6be6963
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/hr-writeback-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/hr-writeback-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/hr-writeback-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 87edd375-0556-4ab2-df8c-6b8f763470a2
---

# Troubleshoot writeback issues with HR provisioning - Microsoft Entra ID | Microsoft Learn

## Null and empty values not processed as expected

**Applies to:**

- Workday Writeback
- SAP SuccessFactors Writeback

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You successfully configured the Writeback app. You're getting null or empty value from Microsoft Entra ID. You expect the provisioning service to clear the corresponding email or phone number value in the HR app. But the operation fails. |
| **Cause** | The provisioning service doesn't have a default logic for null value processing. When the provisioning service gets an empty string from the source app, it tries to flow the value "as-is" to the target app. If Workday or SuccessFactors can't process empty values, then an error is returned. |
| **Resolution** | Update the attribute mapping to use expression mappings as recommended. |

**Recommended resolutions**

Let's say the attribute `telephoneNumber` mapped to SAP SuccessFactors attribute `businessPhoneNumber` may be null or empty in Microsoft Entra ID.

- Option 1: Define an expression to check for empty or null values using functions like [IIF,](functions-for-customizing-application-data#iif)[IsNullOrEmpty,](functions-for-customizing-application-data#isnullorempty)[Coalesce,](functions-for-customizing-application-data#coalesce) or [IsPresent](functions-for-customizing-application-data#ispresent) and pass a nonblank literal value (example: 000-000-0000 in this case).

    `IIF(IsNullOrEmpty([telephoneNumber]),"000-000-0000",[telephoneNumber])`
- Option 2: Use the function [IgnoreFlowIfNullOrEmpty](functions-for-customizing-application-data#ignoreflowifnullorempty) to drop empty or null attributes in the payload sent to SuccessFactors.

    `IgnoreFlowIfNullOrEmpty([telephoneNumber])`