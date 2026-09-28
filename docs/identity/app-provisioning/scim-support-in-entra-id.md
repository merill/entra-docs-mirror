---
layout: Conceptual
title: SCIM support in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/scim-support-in-entra-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: Learn how Microsoft Entra ID supports the SCIM standard both as a provisioning client for SaaS applications and as a SCIM service provider through its SCIM APIs.
ms.topic: article
ms.date: 2026-03-31T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: 606b9a10-ac08-8ac9-c2f0-3afa594b9128
document_version_independent_id: 606b9a10-ac08-8ac9-c2f0-3afa594b9128
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/scim-support-in-entra-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/scim-support-in-entra-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/scim-support-in-entra-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ca569a95-4d4d-64f4-4655-3b42484a046f
---

# SCIM support in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID supports the **System for Cross‑domain Identity Management (SCIM) 2.0** standard in multiple ways, depending on the provisioning scenario. Microsoft Entra can act as:

- A **SCIM client**, provisioning users and groups from Microsoft Entra into partner applications.
- A **SCIM service provider**, exposing SCIM APIs that allow external systems to provision users and groups directly into Microsoft Entra.

This article provides an overview of SCIM support in Microsoft Entra ID and helps you understand which capabilities and documentation apply to your scenario.

## SCIM in Microsoft Entra ID at a glance

[![Diagram showing SCIM support scenarios in Microsoft Entra ID](media/scim-support-in-entra-id/scim-support-in-entra.png)](media/scim-support-in-entra-id/scim-support-in-entra.png#lightbox)

| Scenario | Role played by Microsoft Entra | Typical use case |
| --- | --- | --- |
| Provision users and groups to SaaS apps | SCIM client | Automatically create, update, and deprovision accounts in applications like ServiceNow, Zoom, or Dropbox |
| Provision users and groups into Microsoft Entra | SCIM service provider | Synchronize users from HR systems, partner platforms, or custom identity pipelines into Microsoft Entra ID |

## Entra as a SCIM client (app provisioning)

Microsoft Entra ID includes a built‑in provisioning service that acts as a **SCIM client**. In this model, Microsoft Entra ID sends SCIM requests to applications that expose SCIM‑compliant endpoints.

### What you can do

When acting as a SCIM client, Microsoft Entra ID can:

- Provision and deprovision users in third‑party applications
- Keep user attributes synchronized over time
- Create and manage groups and group memberships
- Support both cloud and on‑premises applications that expose SCIM endpoints
- Apply conditional logic and transformations using attribute mappings

This capability is commonly used by IT administrators to automate access lifecycle management for SaaS applications without writing custom synchronization code.

### Where to learn more

- [Develop a SCIM endpoint for user provisioning](use-scim-to-provision-users-and-groups)
- [App specific provisioning tutorials](/en-us/entra/identity/saas-apps/tutorial-list)
- [Known SCIM 2.0 compliance issues](application-provisioning-config-problem-scim-compatibility)

## Microsoft Entra as a SCIM service provider (SCIM APIs)

Microsoft Entra ID also acts as a **SCIM service provider** through its **SCIM 2.0 APIs**. In this model, external systems like HR systems can call SCIM API endpoints exposed by Microsoft Entra ID to manage identity data.

### What you can do

With Microsoft Entra ID SCIM APIs, you can:

- Create, read, update, and delete users in Microsoft Entra
- Create and manage security groups and Microsoft 365 groups
- Manage group memberships
- Discover supported schemas, resource types, and service capabilities using standard SCIM endpoints
- Integrate using existing SCIM clients, connectors, and automation frameworks

This capability is designed for **standards‑based identity lifecycle automation**, particularly when customers or partners already use SCIM to integrate with applications like HR apps, middleware services and other identity and access platforms.

### Common scenarios

- Synchronizing users from an HR system into Microsoft Entra ID
- Migrating identities from another identity provider into Microsoft Entra ID
- Using a single SCIM‑based provisioning pipeline across multiple platforms
- Enabling partners to provision identities into customer Microsoft Entra ID tenants using an industry‑standard protocol

### Where to learn more

- [Configure Microsoft Entra SCIM 2.0 APIs](enable-scim-api)
- [Microsoft Entra ID SCIM API endpoints](entra-id-scim-api-reference)
- [Microsoft Entra ID SCIM API schema](entra-id-scim-api-schema-documentation)

## Microsoft Graph vs. SCIM: when to use which

Microsoft Entra ID supports **both Microsoft Graph APIs and SCIM APIs** for managing users and groups. The right choice depends on your integration needs.

### Use Microsoft Graph when you need to:

- Access the full breadth of Microsoft identity, security, and Microsoft 365 capabilities
- Work with rich relationships and advanced identity features
- Build deeply integrated, Microsoft‑centric applications
- Use Microsoft‑specific concepts that go beyond lifecycle provisioning

### Use SCIM when you want to:

- Integrate using an **industry‑standard SCIM 2.0 protocol**
- Reuse existing SCIM clients, connectors, or provisioning frameworks
- Focus primarily on **user and group lifecycle management**
- Standardize identity provisioning across multiple platforms and identity providers

Many customers and partners use **both** approaches—SCIM for lifecycle synchronization and Microsoft Graph for richer Microsoft‑specific capabilities—depending on the scenario.

## Summary

Microsoft Entra ID provides flexible, standards‑based identity provisioning by supporting SCIM in two complementary roles:

- As a **SCIM client**, enabling provisioning from Microsoft Entra ID to business applications.
- As a **SCIM service provider**, enabling provisioning from business applications to Microsoft Entra ID through SCIM APIs.

Together with Microsoft Graph, these capabilities give customers and partners the choice to integrate with Microsoft Entra using the model that best fits their architecture, tooling, and long‑term identity strategy.