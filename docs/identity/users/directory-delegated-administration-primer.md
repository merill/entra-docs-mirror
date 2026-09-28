---
layout: Conceptual
title: Delegated administration in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/directory-delegated-administration-primer
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: The relationship between older delegated admin permissions and new granular delegated admin permissions in Microsoft Entra ID
keywords: 
ms.reviewer: yuank
ms.date: 2024-12-13T00:00:00.0000000Z
ms.topic: overview
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-ga-nochange
locale: en-us
document_id: 51bb8ff2-61c3-0d70-7cb8-b582768ad148
document_version_independent_id: 9d0e108e-d99b-fe95-1e0c-3cf9bf951dbe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/directory-delegated-administration-primer.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/directory-delegated-administration-primer
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/directory-delegated-administration-primer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 60fa21f5-a100-c64a-7615-b18f9ee2f771
---

# Delegated administration in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Managing permissions for external partners is a key part of your security posture. The administrator portal experience in Microsoft Entra ID, part of Microsoft Entra, now includes capabilities so that an administrator can see the relationships that their Microsoft Entra tenant has with Microsoft Cloud Service Providers (CSP) who can manage the tenant. This permissions model is called delegated administration. This article introduces the Microsoft Entra administrator to the relationship between the old Delegated Admin Permissions (DAP) permission model and the new [Granular Delegated Admin Permissions (GDAP)](/en-us/partner-center/gdap-introduction) permission model.

## Delegated administration relationships

Delegated administration relationships enable technicians at a Microsoft CSP to administer Microsoft services such as Microsoft 365, Dynamics 365, and Azure on behalf of your organization. These technicians administer these services for you using the same roles and permissions as your organization's own administrators. These roles are assigned to security groups in the CSP’s Microsoft Entra tenant, which is why CSP technicians don’t need user accounts in your tenant in order to administer services for you.

There are two types of delegated administration relationships that are visible in the Azure portal experience. The newer type of delegated admin relationship is known as Granular Delegated Admin Permission. The older type of relationship is known as Delegated Admin Permission. You can see both types of relationship if you sign in to the Azure portal and then select **Delegated administration**.

## Granular delegated admin permission

When a Microsoft CSP creates a GDAP relationship request for your tenant, a Global Administrator needs to approve the request. The GDAP relationship request specifies:

- The CSP partner tenant
- The roles that the partner needs to delegate to their technicians
- The expiration date

If you have GDAP relationships in your tenant, you see a notification banner on the **Delegated Administration** page in the Microsoft Entra admin center. Select the notification banner to see and manage GDAP relationships in the **Partners** page in Microsoft Admin Center.

## Delegated admin permission

All DAP relationships enable the CSP to delegate Global Administrator and Helpdesk Administrator roles to their technicians. Unlike a GDAP relationship, a DAP relationship persists until you or your CSP revokes them.

If you have any DAP relationships in your tenant, you can see them in the list on the **Delegated Administration** page in the Azure portal. To remove a DAP relationship for a CSP, follow the link to the **Partners** page in the Microsoft Admin Center.