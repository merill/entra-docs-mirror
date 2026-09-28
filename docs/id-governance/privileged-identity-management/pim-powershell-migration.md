---
layout: Conceptual
title: PIM PowerShell for Azure resources migration guidance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-powershell-migration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: The following documentation provides guidance for Privileged Identity Management (PIM) PowerShell migration.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, devx-track-azurepowershell
locale: en-us
document_id: 5a09341f-6a01-0dad-9b6f-4541c0c63e42
document_version_independent_id: eea7f456-57e1-f818-547b-1b275fc26e29
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-powershell-migration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-powershell-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-powershell-migration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a7e769be-8fb4-1f7d-e5d5-93f3102afcac
---

# PIM PowerShell for Azure resources migration guidance - Microsoft Entra ID Governance | Microsoft Learn

## Overview

The following table provides guidance on using the new PowerShell cmdlets in the newer Azure PowerShell module.

## New cmdlets in the Azure PowerShell module

| Old AzureADPreview cmd | New Az cmd equivalent | Description |
| --- | --- | --- |
| Get-AzureADMSPrivilegedResource | [Get-AzResource](/en-us/powershell/module/az.resources/get-azresource) | Get resources |
| Get-AzureADMSPrivilegedRoleDefinition | [Get-AzRoleDefinition](/en-us/powershell/module/az.resources/get-azroledefinition) | Get role definitions |
| Get-AzureADMSPrivilegedRoleSetting | [Get-AzRoleManagementPolicy](/en-us/powershell/module/az.resources/get-azrolemanagementpolicy) | Get the specified role management policy for a resource scope |
| Set-AzureADMSPrivilegedRoleSetting | [Update-AzRoleManagementPolicy](/en-us/powershell/module/az.resources/update-azrolemanagementpolicy) | Update a rule defined for a role management policy |
| Open-AzureADMSPrivilegedRoleAssignmentRequest | [New-AzRoleAssignmentScheduleRequest](/en-us/powershell/module/az.resources/new-azroleassignmentschedulerequest) | Used for Assignment RequestsCreate role assignment schedule request |
| Open-AzureADMSPrivilegedRoleAssignmentRequest | [New-AzRoleEligibilityScheduleRequest](/en-us/powershell/module/az.resources/new-azroleeligibilityschedulerequest) | Used for Eligibility RequestsCreate role eligibility schedule request |