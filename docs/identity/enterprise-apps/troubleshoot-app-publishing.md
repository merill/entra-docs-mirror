---
layout: Conceptual
title: Your sign-in was blocked - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/troubleshoot-app-publishing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Troubleshoot a blocked sign-in to the Microsoft Application Network portal.
ms.topic: troubleshooting
ms.date: 2025-04-29T00:00:00.0000000Z
ms.reviewer: jeedes
ms.custom: enterprise-apps
locale: en-us
document_id: c9cc3885-a2f5-9b7f-95d9-02ed72cb44bb
document_version_independent_id: 97e4341c-0b15-7e0d-fb24-f0a32a6444f1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/troubleshoot-app-publishing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/troubleshoot-app-publishing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/troubleshoot-app-publishing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d30c295c-cf98-ca02-f4e8-f613c6621900
---

# Your sign-in was blocked - Microsoft Entra ID | Microsoft Learn

This article provides information for resolving a blocked sign-in to the Microsoft Application Network portal.

## Symptoms

The user sees this message when trying to sign in to the Microsoft Application Network portal.

![Screenshot that shows a blocked sign-in to the portal.](media/howto-app-gallery-listing/blocked.png)

## Cause

The guest user is federated to a home tenant that is also a Microsoft Entra tenant. The guest user is at high risk. High risk users aren't allowed to access resources. All high risk users (employees, guests, or vendors) must remediate their risk to access resources. For guest users, this user risk comes from the home tenant and the policy comes from the resource tenant.

## Solutions

- MFA registered guest users remediate their own user risk. The guest user [resets or changes a secured password](https://aka.ms/sspr) at their home tenant (this needs MFA and self service password reset (SSPR) at the home tenant). The secured password change or reset must be initiated on Microsoft Entra ID and not on-premises.
- Guest users have their administrators remediate their risk. In this case, the administrator resets a password (temporary password generation). The guest user's administrator can go to https://aka.ms/RiskyUsers and select **Reset password**.
- Guest users have their administrators dismiss their risk. The admin can go to https://aka.ms/RiskyUsers and select **Dismiss user risk**. However, the administrator must do the due diligence to make sure the risk assessment was a false positive before dismissing the user risk. Otherwise, resources are put at risk by suppressing a risk assessment without investigation.