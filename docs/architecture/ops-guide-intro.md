---
layout: Conceptual
title: Microsoft Entra operations reference guide - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/ops-guide-intro
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: This operations reference guide describes the checks and actions you should take to secure and maintain identity and access management, authentication, governance, and operations
ms.topic: best-practice
ms.date: 2022-08-17T00:00:00.0000000Z
ms.reviewer: martinco
ms.subservice: architecture
locale: en-us
document_id: e8476858-0191-cc97-39c7-4d158a33d8ff
document_version_independent_id: a4d212bf-8193-4465-4c6f-2590ae9d401d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/ops-guide-intro.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/ops-guide-intro
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/ops-guide-intro.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 811e97df-13c9-62a6-23a3-d52d44b79f26
---

# Microsoft Entra operations reference guide - Microsoft Entra | Microsoft Learn

This operations reference guide describes the checks and actions you should take to secure and maintain the following areas:

- **[Identity and access management](ops-guide-iam)** - ability to manage the lifecycle of identities and their entitlements.
- **[Authentication management](ops-guide-auth)** - ability to manage credentials, define authentication experience, delegate assignment, measure usage, and define access policies based on enterprise security posture.
- **[Governance](ops-guide-govern)** - ability to assess and attest the access granted nonprivileged and privileged identities, audit, and control changes to the environment.
- **[Operations](ops-guide-ops)** - optimize the operations Microsoft Entra ID.

Some recommendations here might not be applicable to all customers' environment, for example, AD FS best practices might not apply if your organization uses password hash sync.

Note

These recommendations are current as of the date of publishing but can change over time. Organizations should continuously evaluate their identity practices as Microsoft products and services evolve over time. Recommendations can change when organizations subscribe to a different Microsoft Entra ID P1 or P2 license.

## Stakeholders

Each section in this reference guide recommends assigning stakeholders to plan and implement key tasks successfully. The following table outlines the list of all the stakeholders in this guide:

| Stakeholder | Description |
| --- | --- |
| IAM Operations Team | This team handles managing the day to day operations of the Identity and Access Management system |
| Productivity Team | This team owns and manages the productivity applications such as email, file sharing and collaboration, instant messaging, and conferencing. |
| Application Owner | This team owns the specific application from a business and usually a technical perspective in an organization. |
| InfoSec Architecture Team | This team plans and designs the Information Security practices of an organization. |
| InfoSec Operations Team | This team runs and monitors the implemented Information Security practices of the InfoSec Architecture team. |