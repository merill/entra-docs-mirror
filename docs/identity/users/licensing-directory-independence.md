---
layout: Conceptual
title: Characteristics of multitenant interaction - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/licensing-directory-independence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Understanding the data independence of your Microsoft Entra organizations
ms.topic: how-to
ms.date: 2024-12-16T00:00:00.0000000Z
ms.custom: it-pro, sfi-ga-nochange
ms.reviewer: sumitp
locale: en-us
document_id: 4a916018-5100-91af-bc16-6aab0372bd48
document_version_independent_id: 2f526d40-8282-090c-430e-b2bf1d3ba7df
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/licensing-directory-independence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/licensing-directory-independence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/licensing-directory-independence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 05b4d28b-893a-7a13-4c45-7cd336281105
---

# Characteristics of multitenant interaction - Microsoft Entra ID | Microsoft Learn

## Overview

In Microsoft Entra ID, part of Microsoft Entra, each Microsoft Entra organization is fully independent: a peer that is logically independent from the other Microsoft Entra organizations that you manage. This independence between organizations includes resource independence, administrative independence, and synchronization independence. There's no parent-child relationship between organizations.

## Resource independence

- If you create or delete a Microsoft Entra resource in one organization, it has no effect on any resource in another organization, with the partial exception of external users.
- If you register one of your domain names with one organization, you can't use it for any other organization.

## Administrative independence

If a non-administrative user of organization 'Contoso' creates a test organization 'Test,' then:

- By default, the user who creates an organization is added as an external user to that new organization, and assigned the Global Administrator role.
- The administrators of organization 'Contoso' have no direct administrative privileges to organization 'Test,' unless an administrator of 'Test' specifically grants them these privileges.
- If you add or remove a Microsoft Entra role for a user in one organization, the change doesn't affect other roles. For example, roles that the user assigns in any other Microsoft Entra organization.

## Synchronization independence

You can configure each Microsoft Entra organization independently to get data synchronized from different AD forests, using the Microsoft Entra Connect tool. For more information on supported topologies when there are multiple Microsoft Entra tenants, see [topologies for Microsoft Entra Connect](../hybrid/connect/plan-connect-topologies).

## Add a Microsoft Entra organization

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Tenant Creator](../role-based-access-control/permissions-reference#tenant-creator).
2. Browse to **Entra ID** &gt; **Overview**.
3. Select **Manage tenants**.
4. Select **Create**.
5. Select **Workforce** and provide the requested information. Microsoft Entra ID creates a new organization and it appears in the list of organizations.

Note

Unlike other Azure resources, your Microsoft Entra organizations are not child resources of an Azure subscription. If your Azure subscription is canceled or expired, you can still access your Microsoft Entra organization's data using Azure PowerShell, the Microsoft Graph API, or the Microsoft 365 admin center. You can also [associate another subscription with the organization](../../fundamentals/how-subscriptions-associated-directory).

Note

Azure AD and MSOnline PowerShell modules are deprecated as of March 30, 2024. To learn more, read the [deprecation update](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270). After this date, support for these modules are limited to migration assistance to Microsoft Graph PowerShell SDK and security fixes. The deprecated modules will continue to function through March, 30 2025.

We recommend migrating to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) to interact with Microsoft Entra ID (formerly Azure AD). For common migration questions, refer to the [Migration FAQ](/en-us/powershell/azure/active-directory/migration-faq). *Note:* Versions 1.0.x of MSOnline may experience disruption after June 30, 2024.