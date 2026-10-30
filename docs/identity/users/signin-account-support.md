---
layout: Conceptual
title: Does my Microsoft Entra sign-in page accept Microsoft accounts - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/signin-account-support
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: How on-screen messaging reflects username lookup during sign-in
ms.topic: concept-article
ms.date: 2024-12-16T00:00:00.0000000Z
ms.reviewer: kexia
ms.custom: it-pro
locale: en-us
document_id: b52c065e-d4b3-04d9-281d-cb939ce96eb1
document_version_independent_id: eecedd28-cf9d-0524-fd1d-9424062f5cba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/signin-account-support.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/signin-account-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/signin-account-support.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 07c9a67c-495b-a2e4-2668-69ae2061935e
---

# Does my Microsoft Entra sign-in page accept Microsoft accounts - Microsoft Entra ID | Microsoft Learn

## Overview

The Microsoft 365 sign-in page for Microsoft Entra ID, part of Microsoft Entra, supports work or school accounts and Microsoft accounts, but depending on the user's situation, it could be one or the other or both. For example, the Microsoft Entra sign-in page supports:

- Apps that accept sign-ins from both types of account
- Organizations that accept guests

## Identification

You can tell if the sign-in page your organization uses supports Microsoft accounts by looking at the hint text in the username field. If the hint text says "Email, phone, or Skype", the sign-in page supports Microsoft accounts.

![Screenshot of the difference between account sign-in pages.](media/signin-account-support/ui-prompt.png)

[Additional sign-in options work only for personal Microsoft accounts](https://azure.microsoft.com/updates/microsoft-account-signin-options/), and can't be used for signing in to work or school account resources.