---
layout: Conceptual
title: Opt out of Microsoft Entra Verified ID - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-opt-out
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to opt out of Microsoft Entra Verified ID.
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 444fa927-9a8d-25a3-398f-e7c0cc085d0b
document_version_independent_id: e9d28836-b1d8-0b09-5fdb-95902981b1fc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-opt-out.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-opt-out
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-opt-out.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: d3f06062-e0c5-5710-1734-46a71edbb966
---

# Opt out of Microsoft Entra Verified ID - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Opting out is the process of resetting your Microsoft Entra Verified ID environment.

## When do you need to opt out?

Opting out is a one-way operation. After the process finishes, your Microsoft Entra Verified ID environment is reset. You might need to opt out to:

- Enable new service capabilities.
- Reset your service configuration.
- Switch between the ION and web trust systems.

## What happens to your data?

When you finish opting out of the Microsoft Entra Verified ID service, the following actions occur:

- The decentralized identifier (DID) keys in Azure Key Vault are [soft deleted](/en-us/azure/key-vault/general/soft-delete-overview).
- The issuer object is deleted from the database.
- The tenant identifier is deleted from the database.
- All the verifiable credentials contracts are deleted from the database.

After an opt-out action takes place, you can't recover your DID or conduct any operations on your DID. This step is a one-way operation, and you need to onboard again. Onboarding again creates a new environment.

## Effect on existing verifiable credentials

All verifiable credentials already issued continue to exist. For the ION trust system, they aren't cryptographically invalidated because your DIDs remain resolvable through ION. However, when relying parties call the status API, they always receive a failure message.

## Opt out of Microsoft Entra Verified ID

1. From the **Azure portal**, search for verifiable credentials.
2. Select **Organization Settings** on the leftmost menu.
3. In the section **Reset your organization**, select **Delete all credentials and reset service**.

    ![Screenshot that shows the section on the Organization settings page where you reset your organization.](media/how-to-opt-out/settings-reset.png)
4. Read the warning message and select **Delete & opt out** to continue.

    ![Screenshot that shows Delete &amp; opt out.](media/how-to-opt-out/delete-and-opt-out.png)