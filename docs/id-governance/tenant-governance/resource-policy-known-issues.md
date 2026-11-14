---
layout: Conceptual
title: Microsoft Entra resource policy known issues (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-known-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Understand resource policy assignment propagation and collect diagnostics for unexpected policy behavior.
ms.topic: reference
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 06545a5f-9d9d-d603-d6c4-4fa3b2a03fa3
document_version_independent_id: 06545a5f-9d9d-d603-d6c4-4fa3b2a03fa3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-known-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-known-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-known-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ac0825c9-b3f3-8bff-eaa0-7e251424348a
---

# Microsoft Entra resource policy known issues (preview) - Microsoft Entra ID Governance | Microsoft Learn

Use this article with [Test and troubleshoot a resource policy](resource-policy-test-troubleshoot) when policy management or request-time behavior differs from your expectations.

## Assignment changes aren't immediately reflected in requests

Assignment changes can take up to 10 minutes to affect incoming requests. Use `evaluateAssignedPolicies` to test saved settings without that delay, then wait for [assignment propagation](resource-policy-evaluation#assignment-propagation) before testing real requests again.

## Report an unexpected result

Collect the operation, approximate time, request correlation information, assignment reference, policy version, enforcement mode, and available evaluation error details. Remove secrets and unnecessary personal data before sharing diagnostic information.