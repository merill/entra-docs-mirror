---
layout: Conceptual
title: Troubleshoot registered, hybrid, and Microsoft Entra joined Windows machines - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/troubleshoot-device-windows-joined
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: This article helps you troubleshoot Microsoft Entra hybrid joined Windows 10 and Windows 11 devices.
ms.topic: troubleshooting
ms.date: 2025-07-27T00:00:00.0000000Z
ms.reviewer: jogro
ms.custom: sfi-image-nochange
locale: en-us
document_id: e606575a-2b56-5a1b-fae4-660bcc75c1b5
document_version_independent_id: 46e358c6-2fce-fc77-366d-04abf156f9d2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/troubleshoot-device-windows-joined.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/troubleshoot-device-windows-joined
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/troubleshoot-device-windows-joined.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: a8bbe588-5b1c-6945-747e-4d3b86ee948f
---

# Troubleshoot registered, hybrid, and Microsoft Entra joined Windows machines - Microsoft Entra ID | Microsoft Learn

If you have a Windows 11 or Windows 10 device that isn't working with Microsoft Entra ID correctly, start your troubleshooting here.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Devices** &gt; **All devices** &gt; **Diagnose and solve problems**.
3. Select **Troubleshoot** under the **Windows 10+ related issue** troubleshooter. [![A screenshot showing the Windows troubleshooter located in the diagnose and solve pane.](media/troubleshoot-device-windows-joined/devices-troubleshoot-windows.png)](media/troubleshoot-device-windows-joined/devices-troubleshoot-windows.png#lightbox)
4. Select **instructions** and follow the steps to download, run, and collect the required logs for the troubleshooter to analyze.
5. Return to the Microsoft Entra admin center when you collect and zip the `authlogs` folder and contents.
6. Select **Browse** and choose the zip file you wish to upload. [![A screenshot showing how to browse to select the logs gathered in the previous step to allow the troubleshooter to make recommendations.](media/troubleshoot-device-windows-joined/devices-troubleshoot-windows-upload.png)](media/troubleshoot-device-windows-joined/devices-troubleshoot-windows-upload.png#lightbox)

The troubleshooter will review the contents of the file you uploaded and provide suggested next steps. These next steps might include links to documentation or contacting support for further assistance.