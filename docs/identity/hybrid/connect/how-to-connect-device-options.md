---
layout: Conceptual
title: 'Microsoft Entra Connect: Device options - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-device-options
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document details device options available in Microsoft Entra Connect
editor: billmath
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: e95fac4e-0780-82ea-75b6-6396f7ceaed2
document_version_independent_id: 1932b404-8654-e8c9-d149-987e43523d62
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-device-options.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-device-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-device-options.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3bf4b5a3-3bc1-0152-2388-1d27ce67898f
---

# Microsoft Entra Connect: Device options - Microsoft Entra ID | Microsoft Learn

The following documentation provides information about the various device options available in Microsoft Entra Connect. You can use Microsoft Entra Connect to configure the following two operations:

- **Microsoft Entra hybrid join**: If your environment has an on-premises AD footprint and you want the benefits of Microsoft Entra ID, you can implement Microsoft Entra hybrid joined devices. These devices are joined both to your on-premises Active Directory, and your Microsoft Entra ID.
- **Device writeback**: Device writeback is used to enable Conditional Access based on devices to AD FS (2012 R2 or higher) protected devices

## Configure device options in Microsoft Entra Connect

1. Run Microsoft Entra Connect. In the **Additional tasks** page, select **Configure device options**. Click **Next**. ![Configure device options](media/how-to-connect-device-options/deviceoptions.png)

    The **Overview** page displays the details. ![Overview](media/how-to-connect-device-options/deviceoverview.png)

    Note

    The new Configure device options is available only in version 1.1.819.0 and newer.
2. After providing the credentials for Microsoft Entra ID, you can chose the operation to be performed on the Device options page. ![Device operations](media/how-to-connect-device-options/deviceoptionsselection.png)