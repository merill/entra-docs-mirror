---
layout: Conceptual
title: 'Microsoft Entra Connect: Pass-through Authentication - Current limitations - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta-current-limitations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes the current limitations of Microsoft Entra pass-through authentication
keywords: Azure AD Connect Pass-through Authentication, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 20292fdc-9a8d-95a0-7cb4-3f20f759d970
document_version_independent_id: 8f8b5634-b575-4a97-57d5-2a6e9a4854e0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta-current-limitations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta-current-limitations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta-current-limitations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 53dc65fe-fcaf-a905-d2fd-dc0ebffa915b
---

# Microsoft Entra Connect: Pass-through Authentication - Current limitations - Microsoft Entra ID | Microsoft Learn

## Supported scenarios

The following scenarios are supported:

- User sign-ins to web browser-based applications.
- User sign-ins to legacy Office client applications and Office applications that support [modern authentication](https://www.microsoft.com/en-us/microsoft-365/blog/2015/11/19/updated-office-365-modern-authentication-public-preview): Office 2013 and 2016 versions.
- User sign-ins to legacy protocol applications such as PowerShell version 1.0 and others.
- Microsoft Entra joins for Windows 10 and later devices.
- Hybrid Microsoft Entra joins for Windows 10 and later devices.

## Unsupported scenarios

The following scenarios *aren't* supported:

- Detection of users with [leaked credentials](../../../id-protection/overview-identity-protection).
- Microsoft Entra Domain Services needs Password Hash Synchronization to be enabled on the tenant. Therefore tenants that use Pass-through Authentication *only* don't work for scenarios that need Microsoft Entra Domain Services.
- Pass-through Authentication isn't integrated with [Microsoft Entra Connect Health](whatis-azure-ad-connect).
- Signing in to Microsoft Entra joined (AADJ) devices with a temporary or expired password isn't supported for Pass-through authentication users. The error "the sign-in method you're trying to use isn't allowed" will appear. These users must sign in to a browser to update their temporary password.

Important

As a workaround for unsupported scenarios *only* (except Microsoft Entra Connect Health integration), enable Password Hash Synchronization on the [Optional features](how-to-connect-install-custom#optional-features) page in the Microsoft Entra Connect wizard.

Note

Enabling Password Hash Synchronization gives you the option to failover authentication if your on-premises infrastructure is disrupted. This failover from Pass-through Authentication to Password Hash Synchronization isn't automatic. You'll need to switch the sign-in method manually using Microsoft Entra Connect. If the server running Microsoft Entra Connect goes down, you'll require help from Microsoft Support to turn off Pass-through Authentication.