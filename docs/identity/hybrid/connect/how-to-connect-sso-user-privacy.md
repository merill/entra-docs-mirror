---
layout: Conceptual
title: User Privacy and Microsoft Entra seamless single sign-on - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sso-user-privacy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article deals with Microsoft Entra seamless SSO and GDPR compliance.
keywords: what is Azure AD Connect, GDPR, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 6e904a4c-fd13-09bc-7402-90fcc96dbd15
document_version_independent_id: 991649f2-e3da-be43-2acf-d93ce947cab4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sso-user-privacy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sso-user-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sso-user-privacy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 33a925b3-4b03-ec21-00db-a36b3912a31a
---

# User Privacy and Microsoft Entra seamless single sign-on - Microsoft Entra ID | Microsoft Learn

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Overview

Microsoft Entra seamless SSO creates the following log type, which can contain Personal Data:

- Microsoft Entra Connect trace log files.

Improve user privacy for Seamless SSO in two ways:

1. Upon request, extract data for a person and remove data from that person from the installations.
2. Ensure no data is retained beyond 48 hours.

We strongly recommend the second option as it is easier to implement and maintain. See following instructions for each log type:

### Delete Microsoft Entra Connect trace log files

Check the contents of **%ProgramData%\AADConnect** folder and delete the trace log contents (**trace-\*.log** files) of this folder within 48 hours of installing or upgrading Microsoft Entra Connect or modifying Seamless SSO configuration, as this action may create data covered by GDPR.

Important

Don’t delete the **PersistedState.xml** file in this folder, as this file is used to maintain the state of the previous installation of Microsoft Entra Connect and is used when an upgrade installation is done. This file will never contain any data about a person and should never be deleted.

You can either review and delete these trace log files using Windows Explorer or you can use the following PowerShell script to perform the necessary actions:

```powershell
$Files = ((Get-Item -Path "$env:programdata\aadconnect\trace-*.log").VersionInfo).FileName 
 
Foreach ($file in $Files) { 
    {Remove-Item -Path $File -Force} 
}
```

Save the script in a file with the ".PS1" extension. Run this script as needed.

To learn more about related Microsoft Entra Connect GDPR requirements, see [this article](reference-connect-user-privacy).

### Note about Domain controller logs

If audit logging is enabled, this product may generate security logs for your Domain Controllers. To learn more about configuring audit policies, read this [article](/en-us/previous-versions/tn-archive/dd277403%28v=technet.10%29).