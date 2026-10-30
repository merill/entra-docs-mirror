---
layout: Conceptual
title: Create a governed workforce tenant - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-create-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: tafra00
ms.author: tazkiaafra
ms.service: entra-id-governance
manager: dougeby
description: Learn how to securely create a governed Microsoft Entra workforce tenant and establish governance from your home tenant.
ms.topic: how-to
ms.date: 2026-08-26T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1018
locale: en-us
document_id: e7c705b4-11d5-0a94-fb6d-5eeac1746387
document_version_independent_id: e7c705b4-11d5-0a94-fb6d-5eeac1746387
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-create-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-create-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-create-tenant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: edcd5133-e960-3e04-0096-e665d7e6302e
---

# Create a governed workforce tenant - Microsoft Entra ID Governance | Microsoft Learn

This article is for IT administrators who need to create an add-on tenant that is governed from an existing Microsoft Entra tenant. Review the prerequisites before you use the secure add-on tenant creation flow.

When you create a tenant using the **Governed Workforce** option in the Microsoft Entra admin center, the secure add-on tenant creation flow automatically:

- Creates the new workforce tenant
- Establishes a [governance relationship](governance-relationships) between your home tenant and the new tenant if your home tenant has a default [governance policy template](governance-policy-templates)
- Provisions a [Microsoft Entra ID Free billing asset](/en-us/azure/cost-management-billing/manage/microsoft-entra-id-free) under your selected Azure subscription and resource group

This article doesn't cover creating an external tenant configuration for consumer-facing apps. For customer identity and access management scenarios, see [Microsoft Entra External ID for customers](../../external-id/customers/overview-customers-ciam).

## Prerequisites

Before you create a governed workforce tenant, review the following requirements:

- Your home tenant has at least one paid, license-based Microsoft product (for example, Microsoft Entra ID P1 or P2, Microsoft 365, or Windows Enterprise E3). Free and trial licenses don't qualify.
- You have either a paid [Enterprise Agreement (EA)](/en-us/azure/cost-management-billing/manage/understand-ea-roles) or [Pay-As-You-Go](https://azure.microsoft.com/pricing/offers/ms-azr-0003p?cid=msft_learn) subscription. Both [Microsoft Online Subscription Agreement (MOSA)](/en-us/azure/cost-management-billing/manage/view-all-accounts#microsoft-online-services-program) and [Microsoft Customer Agreement (MCA)](/en-us/azure/cost-management-billing/manage/view-all-accounts#microsoft-customer-agreement) billing accounts are supported. To identify your billing account type, see [View your billing accounts in the Azure portal](/en-us/azure/cost-management-billing/manage/view-all-accounts).
- Your account has the [Tenant Creator](../../identity/role-based-access-control/permissions-reference#tenant-creator) role. This role is required regardless of the [**Restrict non-admin users from creating tenants**](../../fundamentals/users-default-permissions#restrict-member-users-default-permissions) setting.
- You have the required Azure Resource Manager (ARM) permissions for the selected subscription through the **Tenant Contributor** or **Subscription Owner/Creator** role.
- (Optional) Your home tenant has a configured **default**[governance policy template](governance-policy-templates). The tenant creation service uses only the default template (ID: `default`). If the default template isn't defined, the secure add-on tenant creation flow doesn't establish a governance relationship, even if other templates exist.

## Create the tenant

For step-by-step instructions on creating a governed workforce tenant, see the **Governed Workforce** tab in [Quickstart: Create a new tenant in Microsoft Entra ID](../../fundamentals/create-new-tenant).

## What happens after tenant creation

After the system creates the tenant:

1. If your home tenant has a [default governance policy template](governance-policy-templates), a governance relationship forms between your home tenant and the new tenant. The template provisions resources, including cross-tenant access settings, granular delegated admin privileges (GDAP) assignments, and service principals.
2. A [Microsoft Entra ID Free billing asset](/en-us/azure/cost-management-billing/manage/microsoft-entra-id-free) appears in your Azure subscription under the resource group you selected.
3. The new tenant appears in your [related tenants](related-tenants) inventory.

To learn more about governance relationships and policy templates, see [Governance relationships](governance-relationships) and [Governance policy templates](governance-policy-templates).