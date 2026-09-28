---
layout: Landing
title: Microsoft Entra managed identities for Azure resources documentation - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/
summary: Learn how to use managed identities in Microsoft Entra ID.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn how to use managed identities for Azure resources in Microsoft Entra ID.
ms.topic: landing-page
ms.date: 2025-01-15T00:00:00.0000000Z
locale: en-us
document_id: 58281697-10d2-8497-7fbd-2ff0dbbcbde9
document_version_independent_id: 1359ac31-a75a-42e4-44fb-e08cdd39fe93
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: landing
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/index.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bc8e71a6-11fe-e086-ec80-56a5f553bc6d
---

# Managed identities for Azure resources documentation

Learn how to use managed identities in Microsoft Entra ID.

## About managed identities

### Overview

- [What is managed identities for Azure resources?](overview)

## Configure managed identities on Azure virtual machines

### How-To Guide

- [Portal](qs-configure-portal-windows-vmss)
- [CLI](qs-configure-cli-windows-vmss)
- [PowerShell](qs-configure-powershell-windows-vmss)
- [Azure Resource Manager Template](qs-configure-template-windows-vmss)
- [REST](qs-configure-rest-vmss)

## Use managed identities on VMs

### How-To Guide

- [Acquire an access token](qs-configure-rest-vmss)
- [Sign in to PowerShell and CLI](how-to-use-vm-sign-in)
- [Use with Azure SDK](how-to-use-vm-sdk)

## Configuring applications

### How-To Guide

- [Configure an application to trust a managed identity (preview)](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity?toc=/entra/identity/managed-identities-azure-resources/toc.json)

## Assign a managed identity access to another Azure resource

### How-To Guide

- [Portal](how-to-configure-managed-identities-scale-sets?pivots=identity-mi-methods-azp)
- [CLI](how-to-assign-access-azure-resource?pivots=identity-mi-access-cli)
- [PowerShell](how-to-assign-access-azure-resource?pivots=identity-mi-access-powershell)