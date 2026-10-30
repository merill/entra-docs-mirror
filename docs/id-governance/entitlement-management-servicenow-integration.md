---
layout: Conceptual
title: Microsoft Entra ID Entitlement Management integration with ServiceNow - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-servicenow-integration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how Microsoft Entra ID Entitlement Management integrates with ServiceNow for access package requests and approvals.
ms.subservice: entitlement-management
ms.topic: tutorial
ms.date: 2026-09-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 81cee194-1ad3-342e-512a-dccf1f330b21
document_version_independent_id: 81cee194-1ad3-342e-512a-dccf1f330b21
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-servicenow-integration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-servicenow-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-servicenow-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: b2b46414-0bf6-019f-bb06-4af18946d46e
---

# Microsoft Entra ID Entitlement Management integration with ServiceNow - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Microsoft Entra ID Entitlement Management integrates with ServiceNow, providing an alternative portal where users can request access packages, view request history, and approve or deny requests when they're designated as approvers.

Microsoft Entra ID Entitlement Management remains the system of record. Administrators create and manage catalogs, access packages, assignment policies, requestor eligibility, approvers, and assignments in Microsoft Entra ID Entitlement Management. ServiceNow provides the end-user request and approval experience.

| **Activity** | **Where it's performed** |
| --- | --- |
| Create and manage access packages, policies, and approvers | Microsoft Entra ID Entitlement Management |
| Request an access package | ServiceNow |
| View request status and history | ServiceNow |
| Approve or deny a request | ServiceNow |

## Licensing requirements

A Microsoft Entra ID P2 or Microsoft Entra Suite license is required to use this integration.

Note

Access packages and policies are created and managed in Microsoft Entra ID Entitlement Management, not in ServiceNow.

## Install and configure

Install the application from the [Microsoft Entra ID Governance - ServiceNow Store](https://store.servicenow.com/store/app/9c8ca6a087c80fd4a6c6fc48cebb3560).

For installation and configuration instructions, see the [Microsoft Entra ID Governance Integration with ServiceNow Installation Guide](https://store.servicenow.com/api/sn_store/v1/store/attachment/9837597d97428f503fa8b84bf253af41) under **Links and Documents** on the ServiceNow Store page.

## Available functionality in ServiceNow

In ServiceNow, open **Service Catalog** &gt; **Microsoft Entra ID Governance**. The **Access Package** and **Request History** options are available to requestors, while **Approvals** is available to designated approvers.

[![Screenshot of the Microsoft Entra ID Governance application in ServiceNow showing Access Package, Request History, and Approvals.](media/entitlement-management-servicenow-integration/servicenow-entra-id-governance-application.png)](media/entitlement-management-servicenow-integration/servicenow-entra-id-governance-application.png#lightbox)

*Figure 1. Microsoft Entra ID Governance application in ServiceNow.*

## Request an access package

Select **Access Package**, open the **Available** tab, choose an access package, provide the information required by its assignment policy, and submit the request. Use the **Active** and **Expired** tabs to view current and past access.

[![Screenshot of the Access Packages page in ServiceNow showing available packages that a user can request.](media/entitlement-management-servicenow-integration/servicenow-request-access-package.png)](media/entitlement-management-servicenow-integration/servicenow-request-access-package.png#lightbox)

*Figure 2. Access Packages page in ServiceNow.*

## View access package request history

Select **Request History** to view submitted requests and their current status. Select **View** to open additional request details.

[![Screenshot of the Request History page in ServiceNow showing a submitted access package request and its status.](media/entitlement-management-servicenow-integration/servicenow-request-history.png)](media/entitlement-management-servicenow-integration/servicenow-request-history.png#lightbox)

*Figure 3. Request History page in ServiceNow.*

## Approve or deny an access package request

Select **Approvals**, then select **Review** to open a request assigned to you. Review the details, and select **Approve** or **Deny**.

[![Screenshot of the Approvals page in ServiceNow showing an access package request assigned to an approver.](media/entitlement-management-servicenow-integration/servicenow-approvals.png)](media/entitlement-management-servicenow-integration/servicenow-approvals.png#lightbox)

*Figure 4. Approvals page in ServiceNow.*