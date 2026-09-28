---
layout: Conceptual
title: Remove personal data - Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-remove-personal-data
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Remove personal data from connectors installed on devices for Microsoft Entra application proxy.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 56046976-d2a2-6956-8ca6-8743d1a5269f
document_version_independent_id: 167a8e60-7da9-02a1-90ab-c501bedeeaa0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-remove-personal-data.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-remove-personal-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-remove-personal-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1ba5dfd4-ac17-30e9-3bb3-12b58e34ca1e
---

# Remove personal data - Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra application proxy requires that you install connectors on your devices, which means that there might be personal data on your devices. This article provides steps for how to delete that personal data to improve privacy.

## Where is the personal data?

It's possible for application proxy to write personal data to the following log types:

- connector event logs
- Windows event logs

## Remove personal data from Windows event logs

For information on how to configure data retention for the Windows event logs, see the Windows event log settings documentation. For more information about Windows event logs, see [Using Windows Event Log](/en-us/windows/win32/wes/using-windows-event-log).

Note

For information about viewing or deleting personal data, please review Microsoft's guidance on the [Windows data subject requests for the GDPR](/en-us/microsoft-365/compliance/gdpr-dsr-windows) site. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Remove personal data from connector event logs

To ensure the application proxy logs don't have personal data, you can either:

- Delete or view data when needed, or
- Turn off logging

Use the following sections to remove personal data from connector event logs. You must complete the removal process for all devices on which the connector is installed.

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

### View or export specific data

To view or export specific data, search for related entries in each of the connector event logs. The logs are located at `C:\ProgramData\Microsoft\Microsoft AAD private network connector\Trace`.

Since the logs are text files, you can use [findstr](/en-us/windows-server/administration/windows-commands/findstr) to search for text entries related to a user.

To find personal data, search log files for UserID.

To find personal data logged by an application that uses Kerberos Constrained Delegation, search for these components of the username type:

- On-premises user principal name
- Username part of user principal name
- Username part of on-premises user principal name
- On-premises security accounts manager (SAM) account name

### Delete specific data

To delete specific data:

1. Generate a new log file. Restart the Microsoft Entra private network connector service. The new log file enables you to delete or modify the old log files.
2. Follow the View or export specific data process described previously to find information that needs to be deleted. Search all of the connector logs.
3. Either delete the relevant log files or selectively delete the fields that contain personal data. You can also delete all old log files if you don’t need them anymore.

### Turn off connector logs

One option to ensure the connector logs don't contain personal data is to turn off the log generation. To stop generating connector logs, remove the following highlighted line from `C:\Program Files\Microsoft Entra private network connector\MicrosoftEntraPrivateNetworkConnectorService.exe.config`.

![Screenshot that shows a code snippet with the highlighted code to remove.](media/application-proxy-remove-personal-data/01.png)