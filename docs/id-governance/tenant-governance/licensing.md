---
layout: Conceptual
title: Licensing for Microsoft Entra Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/licensing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: tafra00
ms.author: tazkiaafra
ms.service: entra-id-governance
manager: dougeby
description: Learn which Microsoft Entra Tenant Governance features are available with each license tier, including P1, P2, and ID Governance
ms.topic: concept-article
ms.date: 2026-09-14T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1018
ai-usage: ai-assisted
locale: en-us
document_id: 657ce2f0-1c72-5402-6395-2d63827ad0ef
document_version_independent_id: 657ce2f0-1c72-5402-6395-2d63827ad0ef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/licensing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/licensing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/licensing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 85f1fc46-81bd-bbfc-0b13-a92a022acada
---

# Licensing for Microsoft Entra Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra Tenant Governance licensing applies to administrators who use Tenant Governance capabilities. This article is for IT decision makers, IT administrators, and partners. Use it to evaluate licensing for discovering, creating, managing, or governing tenants across an organization or customer environments.

Licensing isn't required for every user in a tenant. For governance relationships, administrators who perform delegated administration activities need licenses in the governing tenant.

## Features by license

The following tables show which Tenant Governance features are available with each license.

Note

Microsoft Entra P1 is also included in Microsoft 365 E3 and Microsoft 365 Business Premium. Microsoft Entra P2 is also included in Microsoft 365 E5. Microsoft Entra ID Governance is also included in Microsoft Entra Suite and Microsoft 365 E7.

### Configuration management

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| Single tenant configuration monitoring and drift reporting |  | ✅ Up to 30 monitors and 800 configuration resources per tenant per day | ✅ Up to 30 monitors and 800 configuration resources per tenant per day | ✅ Base capacity plus 10 additional configuration resources per day for each license |
| Single tenant configuration snapshots |  | ✅ Up to 20,000 resources per tenant per month and 12 active snapshot jobs | ✅ Up to 20,000 resources per tenant per month and 12 active snapshot jobs | ✅ Base capacity plus 35 additional configuration resources per month for each license |

### Related tenants

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| Discover related tenants through B2B collaboration, multitenant apps, and shared billing accounts |  |  |  | ✅ |

### Governance relationships

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| Governance relationship with cross-tenant granular delegated admin privileges (GDAP) |  | ✅ | ✅ | ✅ |
| Governance relationship with custom multitenant app injection |  |  |  | ✅ |

### Secure tenant creation

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| New tenant creation with governance relationship | ✅ | ✅ | ✅ | ✅ |

## Licensing scenarios by feature

The following scenarios show how to calculate licensing needs for common Tenant Governance uses.

### Configuration management

Tenant Governance Basic provides configuration monitoring and snapshot capacity. Tenant Governance Premium licenses add capacity for organizations that need to cover more configuration resources.

#### Monitor daily configuration drift with an E3 license

**Situation:** Contoso has Microsoft 365 E3, which includes Microsoft Entra P1. Its identity team wants to use Tenant Configuration Management without buying more licenses. Its monitoring scope fits within the Basic limit of 800 configuration resources per tenant per day.

**Licensing calculation:** Contoso can monitor up to 800 configuration resources each day with the Basic capacity included with its existing E3 licensing. It doesn't need more licenses for this scope.

**How Contoso uses the capacity:** The team prioritizes authentication methods, Conditional Access policies, role settings, and other high-impact tenant configurations. When a monitored setting changes, the team reviews the drift report to understand what changed and whether the change was expected. It restores the approved configuration after an unauthorized change or updates the baseline after an intentional change.

**Outcome:** Contoso gets daily drift visibility and stronger control for its most important tenant resources without additional licensing cost.

#### Expand monitoring beyond the Basic daily limit

**Situation:** Fabrikam's environment grows from within the Basic capacity to 1,000 configuration resources that need daily monitoring. The Basic daily limit covers 800 resources, leaving 200 resources outside the monitoring scope.

**Licensing decision:** Fabrikam can leave 200 resources unmonitored or add Premium licenses. Security and compliance stakeholders determine that all 1,000 resources need daily monitoring because they affect tenant security posture, audit readiness, and operational consistency.

**Licensing calculation:** Each Premium license adds capacity for 10 resources per day. The 200-resource shortfall requires 20 Premium licenses.

**Outcome:** The additional licenses let Fabrikam include all 1,000 resources in daily drift detection and reporting. No critical configurations are excluded, and the team maintains consistent drift visibility across the tenant.

#### Use Premium capacity for large monthly snapshots

**Situation:** Northwind already has Premium licensing and needs broader visibility than daily monitoring provides. Its identity team wants to capture more than the Basic monthly limit of 20,000 configuration resources for reporting, audit evidence, and operational review.

**Licensing calculation:** Northwind has 100 Premium licenses. At 35 additional resources per month for each license, these licenses add capacity for 3,500 resources. Northwind can capture up to 23,500 configuration resources each month.

**How Northwind uses the capacity:** The team includes security policies, identity settings, role configurations, and other tenant resources in its snapshot scope. It schedules recurring snapshot jobs to preserve historical configuration data, compare how configurations change over time, and identify unexpected or risky changes.

**Outcome:** Northwind supports large-scale monthly configuration extraction and uses the historical data for audit, governance, and operational analysis.

### Governance relationships

Governance relationship licenses are required only in the governing tenant. The governed tenant doesn't need licenses. For example, when a service provider establishes a governance relationship with a customer, only administrators in the service provider tenant who configure the relationship need licenses.

Cross-tenant delegated administration requires Microsoft Entra P1, Microsoft Entra P2, or Microsoft Entra ID Governance. Custom multitenant application provisioning requires Microsoft Entra ID Governance.

One license is required for each administrator who configures governance relationships. The number of relationships doesn't affect the license count.

| Scenario | Calculation | Number of licenses |
| --- | --- | --- |
| One service provider administrator configures governance relationships with five customer tenants. | One license for the administrator who configures the relationships. The number of relationships and customer tenants doesn't add license requirements. | 1 |
| Three service provider administrators each configure cross-tenant delegated administration relationships with customers. | One license for each configuring administrator. | 3 |
| One administrator configures multitenant application provisioning from an organization's governing tenant. | One Microsoft Entra ID Governance license for the configuring administrator. The governed tenants don't need licenses. | 1 |

### Related tenants

One administrator enables Related tenants discovery for the tenant. After discovery is enabled, every administrator who uses Related tenants needs a license, whether they view results, trigger a refresh, or act on signals. The administrator who enables discovery also needs a license because they use the feature.

| Scenario | Calculation | Number of licenses |
| --- | --- | --- |
| Woodgrove Bank has 12 administrators. One administrator enables Related tenants discovery and is the only administrator who uses the results. | One license for the administrator who enables and uses Related tenants. | 1 |
| Contoso has 30 administrators. Five administrators use Related tenants after one of them enables discovery. Three trigger refreshes and act on signals, and two only view results. | One license for each of the five administrators who uses Related tenants. | 5 |
| Fabrikam has 50 administrators. Ten administrators use Related tenants, including the administrator who enables discovery, six who review signals, and three who only view results. | One license for each of the 10 administrators who uses Related tenants. Administrators who don't use the feature don't need licenses for it. | 10 |

### Secure tenant creation

Secure add-on tenant creation is available with Microsoft Entra Free for paid Microsoft customers. A premium Microsoft Entra license isn't required, but the customer's existing tenant must be associated with a paid Microsoft cloud subscription. Customers who use only a free tenant or trial subscription can't create more tenants from the Microsoft Entra admin center.

For more information about the general tenant creation requirements, see [Create a new tenant in Microsoft Entra ID](../../fundamentals/create-new-tenant).