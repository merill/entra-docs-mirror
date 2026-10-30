---
layout: Conceptual
title: What are Microsoft Entra workbooks? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/overview-workbooks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to create and work with Microsoft Entra workbooks, for identity monitoring, alerts, and data visualization.
ms.topic: overview
ms.date: 2025-02-25T00:00:00.0000000Z
ms.reviewer: tspring
locale: en-us
document_id: 65c1f548-e9c9-3019-f044-8d5ca0ef3eb5
document_version_independent_id: 4b87ba39-af74-8063-9bae-ee28d0f2463a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/overview-workbooks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/overview-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/overview-workbooks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: d3681686-98f2-0bee-e4bb-f995c60b7e4e
---

# What are Microsoft Entra workbooks? - Microsoft Entra ID | Microsoft Learn

As an IT admin, you might need to see your Microsoft Entra tenant data as a visual representation that enables you to understand how your identity management environment is doing. This article gives you an overview of how you can use Azure Workbooks for Microsoft Entra ID to analyze your Microsoft Entra tenant data.

With Azure Workbooks for Microsoft Entra ID, you can:

- Query data from multiple sources in Azure
- Visualize data for reporting and analysis
- Combine multiple elements into a single interactive experience

Workbooks are found in Microsoft Entra ID and in Azure Monitor. The concepts, processes, and best practices are the same for both types of workbooks. Workbooks for Microsoft Entra ID, however, cover only those identity management scenarios that are associated with Microsoft Entra ID. Sign-ins, Conditional Access, multifactor authentication, and Identity Protection are scenarios included in the Workbooks for Microsoft Entra ID.

![Screenshot of the Microsoft Entra workbooks gallery.](media/overview-workbooks/workbooks-gallery.png)

For more information on workbooks for other Azure services, see [Azure Monitor workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview).

## How does it help me?

Workbooks are highly customizable, so you can make workbooks for any scenario. Public templates are added frequently, which provide a great starting point. Common scenarios for using workbooks include:

- Get shareable, at-a-glance summary reports about your Microsoft Entra tenant, and build your own custom reports.
- Find and diagnose sign-in failures, and get a trending view of your organization's sign-in health.
- Monitor Microsoft Entra logs for sign-ins, tenant administrator actions, provisioning, and risk together in a flexible, customizable format.
- Watch trends in your tenant’s usage of Microsoft Entra features such as Conditional Access, self-service password reset, and more.
- Know who's using legacy authentications to sign in to your environment.
- Understand the effect of your Conditional Access policies on your users' sign-in experience.

## Who should use it?

Because of the ability to customize workbooks, they can benefit many types of users. Typical personas that use workbooks are:

- **Reporting admin**: Someone who is responsible for creating reports on top of the available data and workbook templates
- **Tenant admins**: People who use the available reports to get insight and take action.
- **Workbook template builder**: Someone who "graduates" from the role of reporting admin by turning a workbook into a template for others with similar needs to use as a basis for creating their own workbooks.

## Public workbook templates

Public workbook templates are built, updated, and deprecated to reflect the needs of customers and the current Microsoft Entra services. Detailed guidance is available for several Microsoft Entra public workbook templates.

- [Authentication prompts analysis](workbook-authentication-prompts-analysis)
- [Conditional Access gap analyzer](workbook-conditional-access-gap-analyzer)
- [Cross-tenant access activity](workbook-cross-tenant-access-activity)
- [Multifactor authentication gaps](workbook-mfa-gaps)
- [Risk analysis](workbook-risk-analysis)
- [Sensitive Operations Report](workbook-sensitive-operations-report)
- [Sign-ins using legacy authentication](workbook-legacy-authentication)