---
layout: Conceptual
title: Global Secure Access licensing for guest users - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-licensing-guest-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how Global Secure Access licensing works for guest users, including MAU billing, billable features, and multitenant organization scenarios.
ms.topic: reference
ms.date: 2026-04-09T00:00:00.0000000Z
ms.reviewer: cagautham
ai-usage: ai-assisted
locale: en-us
document_id: 16c53ab5-acad-6f7a-47f5-46d997d914da
document_version_independent_id: 16c53ab5-acad-6f7a-47f5-46d997d914da
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-licensing-guest-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-licensing-guest-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-licensing-guest-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3afb0e46-d793-782f-c95d-2dcd1a4d9a9c
---

# Global Secure Access licensing for guest users - Global Secure Access | Microsoft Learn

This article outlines the pricing structure for Microsoft Entra Private Access licensing for guest users. It also describes how to link your tenant to an Azure subscription to ensure correct billing and feature access.

## Monthly active users (MAU) billing model

Global Secure Access uses Monthly Active User (MAU) licensing for guest users. This model is different from licensing for employees. For complete details on licensing for employees, see [Global Secure Access licensing overview](overview-what-is-global-secure-access#licensing-overview).

Under the guest billing model, guests are identified by a `userType` of `Guest` regardless of where the user authenticates. A `userType` of `Guest` is the default `userType` for all B2B invitation methods and can also be set by an identity administrator. Monthly active usage for Global Secure Access is measured when a guest user initiates at least one sign-in during a given month to Microsoft Entra Private Access tunnels using the Global Secure Access client solution. For pricing details, see the [Microsoft Entra External ID pricing page](https://www.microsoft.com/en-us/security/pricing/microsoft-entra-external-id/).

## Billable access features

Guest users are only billed when they actively sign in to the Global Secure Access client for Private Access.

You can identify sign-ins that are billed to Microsoft Entra Private Access for guests by looking at your sign-in logs. Under **Microsoft Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**, each billable sign-in has these properties:

- **User type**: Guest
- **Cross tenant access type**: B2B collaboration
- **Application**: Global Secure Access Client
- **Client app**: Mobile Apps and Desktop clients

Note

These sign-in log filters are provided as guidance for identifying billable guest usage. Contact your Microsoft account team if you need detailed billing validation.

## Link your tenant to a subscription

Global Secure Access external user access licensing is supported through Microsoft Entra External ID subscription linking. The administrator must link the subscription in the resource tenant so guest users can access private resources and usage is billed correctly.

To link the subscription in the resource tenant, follow the steps in [Link a workforce tenant to a subscription](../external-id/external-identities-pricing#link-your-azure-ad-tenant-to-a-subscription).

If you need help with billing or subscription linking, contact your Microsoft account team for details.

## Global Secure Access guest user licensing FAQs

**Does guest billing apply to all guest users, including those within the first 50,000 Monthly Active Users (MAU)?**

The 50,000 free Monthly Active Users (MAU) allowance applies exclusively to external users utilizing Microsoft Entra ID P1 and P2. However, this MAU allowance doesn't extend to products like Microsoft Entra ID Governance for guests or Global Secure Access for guests.

**Does guest billing apply to all internal guest users as well?**

Yes, guest billing applies to all users with a `userType` of `Guest`. It applies to internal and external guest users.