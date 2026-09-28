---
layout: Conceptual
title: Microsoft Entra Connect Health instructions data retrieval - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-data-retrieval
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This page describes how to retrieve data from Microsoft Entra Connect Health.
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
locale: en-us
document_id: 1f38e6c1-d262-48f7-03fe-96f42b7b5c15
document_version_independent_id: 49b2dd2e-534f-b0c2-f3c1-39215cc9ba3d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-data-retrieval.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-data-retrieval
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-data-retrieval.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 28a7738b-2cda-ab08-7f67-6b3980f5b1fd
---

# Microsoft Entra Connect Health instructions data retrieval - Microsoft Entra ID | Microsoft Learn

This document describes how to use Microsoft Entra Connect to retrieve data from Microsoft Entra Connect Health.

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Retrieve email addresses configured for health alerts

To retrieve the email addresses for all of your users that are configured in Microsoft Entra Connect Health to receive alerts, use the following steps.

1. Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth).
2. Select **Sync errors**.
3. Select **Notification settings** on the command bar.
4. In the notification settings panel, review whether Global Administrators receive notifications and the addresses listed under the custom email recipients section.

[![Screenshot of the Connect Health notification settings panel with callouts for enabling email, choosing recipients, and saving changes.](media/how-to-connect-health-data-retrieval/connect-health-notification-settings.png)](media/how-to-connect-health-data-retrieval/connect-health-notification-settings.png#lightbox)

## Retrieve all sync errors

To retrieve a list of all sync errors, use the following steps.

1. Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), and then select **Sync errors**.
2. Select **Export** on the command bar. The browser downloads a CSV file that contains the recorded sync errors.