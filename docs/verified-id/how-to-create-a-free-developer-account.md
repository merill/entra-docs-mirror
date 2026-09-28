---
layout: Conceptual
title: Create a Microsoft Entra developer tenant - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-create-a-free-developer-account
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to create a developer tenant for testing Microsoft Entra Verified ID.
ms.topic: how-to
ms.date: 2026-03-09T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 58a9537e-1377-6b90-667e-becc6d1399a0
document_version_independent_id: 96e4ee73-6da2-e2bd-2a8c-a33a01e6fbe1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-create-a-free-developer-account.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-create-a-free-developer-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-create-a-free-developer-account.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3c65eca4-2096-6103-b728-efdcacb78109
---

# Create a Microsoft Entra developer tenant - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Note

The requirement of a Microsoft Entra ID P2 license was removed in early May 2021. The Microsoft Entra ID Free tier is now supported.

## Create a Microsoft Entra tenant for development

You can create a Microsoft Entra tenant for development and testing in either of the following ways:

- **Microsoft 365 Developer Program** — Join the [Microsoft 365 Developer Program](https://aka.ms/o365devprogram) to get a sandbox tenant with E5 licenses, configured users, groups, and mailboxes. A qualifying subscription or program membership is required — see [who qualifies](/en-us/office/developer-program/microsoft-365-developer-program-faq#who-qualifies-for-a-microsoft-365-e5-developer-subscription-) for details.
- **Free Microsoft Entra tenant** — [Create a new tenant](../identity-platform/quickstart-create-new-tenant) with an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account). This gives you Microsoft Entra ID Free tier. You can then [activate a free trial of Microsoft Entra ID P1 or P2](../fundamentals/get-started-premium) if needed for testing.

Important

The Microsoft 365 Developer Program requires a qualifying subscription or program membership. Eligible members include Visual Studio Enterprise or Professional subscribers, ISV Success Program or Microsoft AI Cloud Partner Program participants, and Premier or Unified Support customers. For more information, see the [Microsoft 365 Developer Program eligibility update](https://devblogs.microsoft.com/microsoft365dev/stay-ahead-of-the-game-with-the-latest-updates-to-the-microsoft-365-developer-program/) and [Who qualifies for a Microsoft 365 E5 developer subscription?](/en-us/office/developer-program/microsoft-365-developer-program-faq#who-qualifies-for-a-microsoft-365-e5-developer-subscription-). If you don't qualify, use the free tenant option instead.

### Sign up for the Microsoft 365 Developer Program

If you have a qualifying subscription or program membership and decide to sign up for the Microsoft 365 Developer Program, follow these steps:

1. On the [Microsoft 365 Developer Program](https://aka.ms/o365devprogram) page, select **Join now**.
2. Sign in with a new Microsoft account or use an existing (work) account.
3. On the sign-up page, select your region, enter a company name, and accept the terms and conditions of the program.
4. Select **Next**.
5. Select **Set up subscription**. Specify the region where you want to create your new tenant, create a username and domain, and enter a password. This step creates a new tenant and the first administrator of the tenant.
6. Enter the security information needed to protect the administrator account of your new tenant. This step sets up multifactor authentication for the account.

At this point, you've created a tenant with 25 E5 user licenses. The E5 licenses include Microsoft Entra ID P2 licenses. Optionally, you can add sample data packs with users, groups, mail, and SharePoint to help you test in your development environment. For the verifiable credential issuing service, these data packs aren't required.