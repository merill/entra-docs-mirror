---
layout: Conceptual
title: Troubleshoot resource access denied in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to troubleshoot system errors with roles in Microsoft Entra Privileged Identity Management (PIM).
ms.topic: troubleshooting
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
locale: en-us
document_id: c986eb5c-680e-d358-e29e-4216bc198235
document_version_independent_id: 6dc430c9-4364-be06-90e0-addaa9817dd8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 485c5a29-813c-0728-837c-bd3de9771f41
---

# Troubleshoot resource access denied in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

If you're experiencing issues with Privileged Identity Management (PIM) in Microsoft Entra ID, the information included in this article can help you resolve these issues.

## Access to Azure resources denied

### Problem

As an active owner or user access administrator for an Azure resource, you're able to see your resource inside Privileged Identity Management but can't perform any actions such as making an eligible assignment or viewing a list of role assignments from the resource overview page. Any of these actions results in an authorization error.

### Cause

This issue can occur when the User Access Administrator role for the PIM service principal was accidentally removed from the subscription. For the Privileged Identity Management service to access Azure resources, the MS-PIM service principal should always have the [User Access Administrator role](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) assigned.

### Resolution

Assign the User Access Administrator role to the Privileged Identity Management service principal name (MS–PIM) at the subscription level. This assignment allows the Privileged Identity Management service to access the Azure resources. Assign the role at a management group level or at the subscription level, depending on your requirements. For more information about service principals, see [Assign an application to a role](../../identity-platform/howto-create-service-principal-portal#assign-a-role-to-the-application).