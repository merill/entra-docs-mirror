---
layout: Conceptual
title: User Privacy and Microsoft Entra pass-through authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta-user-privacy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article deals with Microsoft Entra pass-through authentication and GDPR compliance.
keywords: Azure AD Connect Pass-through Authentication, GDPR, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: af1adc22-bfe9-96db-dc2c-438cf567791b
document_version_independent_id: 1c1a2df7-a3c5-17cf-b045-e823397c95f7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta-user-privacy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta-user-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta-user-privacy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 060cd8e1-d7ff-652d-4f82-cb3442ae9ddc
---

# User Privacy and Microsoft Entra pass-through authentication - Microsoft Entra ID | Microsoft Learn

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Overview

Microsoft Entra pass-through authentication creates the following log type, which can contain Personal Data:

- Microsoft Entra Connect trace log files.
- Authentication Agent trace log files.
- Windows Event log files.

Improve user privacy for Pass-through Authentication in two ways:

1. Upon request, extract data for a person and remove data from that person from the installations.
2. Ensure no data is retained beyond 48 hours.

We strongly recommend the second option as it is easier to implement and maintain. Following are the instructions for each log type:

### Delete Microsoft Entra Connect trace log files

Check the contents of **%ProgramData%\AADConnect** folder and delete the trace log contents (**trace-\*.log** files) of this folder within 48 hours of installing or upgrading Microsoft Entra Connect or modifying Pass-through Authentication configuration, as this action may create data covered by GDPR.

Important

Don’t delete the **PersistedState.xml** file in this folder, as this file is used to maintain the state of the previous installation of Microsoft Entra Connect and is used when an upgrade installation is done. This file will never contain any data about a person and should never be deleted.

You can either review and delete these trace log files using Windows Explorer or you can use the following PowerShell script to perform the necessary actions:

```
$Files = ((Get-Item -Path "$env:programdata\aadconnect\trace-*.log").VersionInfo).FileName 
 
Foreach ($file in $Files) { 
    {Remove-Item -Path $File -Force} 
}
```

Save the script in a file with the ".PS1" extension. Run this script as needed.

To learn more about related Microsoft Entra Connect GDPR requirements, see [this article](reference-connect-user-privacy).

### Delete Authentication Agent event logs

This product may also create **Windows Event Logs**. To learn more, please read [this article](/en-us/windows/win32/wes/windows-event-log).

To view logs related to the Pass-through Authentication Agent, open the **Event Viewer** application on the server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

### Delete Authentication Agent trace log files

You should regularly check the contents of **%ProgramData%\Microsoft\Azure AD Connect Authentication Agent\Trace** and delete the contents of this folder every 48 hours.

Important

If the Authentication Agent service is running, you'll not be able to delete the current log file in the folder. Stop the service before trying again. To avoid user sign-in failures, you should have already configured Pass-through Authentication for [high availability](how-to-connect-pta-quick-start#step-4-ensure-high-availability).

You can either review and delete these files using Windows Explorer or you can use the following script to perform the necessary actions:

```powershell
$Files = ((Get-ChildItem -Path "$env:programdata\microsoft\azure ad connect authentication agent\trace" -Recurse).VersionInfo).FileName 
 
Foreach ($file in $files) { 
    {Remove-Item -Path $File -Force} 
}
```

To schedule this script to run every 48 hours follow these steps:

1. Save the script in a file with the ".PS1" extension.
2. Open **Control Panel** and click on **System and Security**.
3. Under the **Administrative Tools** heading, click on “**Schedule Tasks**”.
4. In **Task Scheduler**, right-click on “**Task Schedule Library**” and click on “**Create Basic task…**”.
5. Enter the name for the new task and click **Next**.
6. Select “**Daily**” for the **Task Trigger** and click **Next**.
7. Set the recurrence to two days and click **Next**.
8. Select “**Start a program**” as the action and click **Next**.
9. Type “**PowerShell**” in the box for the Program/script, and in box labeled “**Add arguments (optional)**”, enter the full path to the script that you created earlier, then click **Next**.
10. The next screen shows a summary of the task you are about to create. Verify the values and click **Finish** to create the task:

### Note about Domain controller logs

If audit logging is enabled, this product may generate security logs for your Domain Controllers. To learn more about configuring audit policies, read this [article](/en-us/previous-versions/tn-archive/dd277403%28v=technet.10%29).