---
layout: Conceptual
title: Microsoft Entra federation compatibility list - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-fed-compatibility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This page has non-Microsoft identity providers that can be used to implement single sign-on.
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: a93962f7-3776-f288-bb15-9347fd04d837
document_version_independent_id: 4295411d-66f1-6931-f6db-760a7fca1523
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-fed-compatibility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-fed-compatibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-fed-compatibility.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 81ea3fac-2a33-8644-32de-64dcf83e6c36
---

# Microsoft Entra federation compatibility list - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID provides single-sign on and enhanced application access security for Microsoft 365 and other Microsoft Online services for hybrid and cloud-only implementations without requiring any third-party solution. Microsoft 365, like most of Microsoft’s Online services, is integrated with Microsoft Entra ID for directory services, authentication, and authorization. Microsoft Entra ID also provides single sign-on to thousands of SaaS applications and on-premises web applications. See the Microsoft Entra ID [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) for supported SaaS applications.

## IDP Validation

If your organization uses a third-party federation solution, you can configure single sign-on for your on-premises Active Directory users with Microsoft Online services, such as Microsoft 365, provided the third-party federation solution is compatible with Microsoft Entra ID. For questions regarding compatibility, contact your identity provider. If you want to see a list of identity providers who have previously been tested for compatibility with Microsoft Entra ID, by Microsoft, see [Microsoft Entra identity provider compatibility docs](https://www.microsoft.com/download/details.aspx?id=56843).

Note

Microsoft no longer provides validation testing to independent identity providers for compatibility with Microsoft Entra ID. If you want to test your product for interoperability please refer to these [guidelines](https://www.microsoft.com/download/details.aspx?id=56843).