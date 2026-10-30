---
layout: Conceptual
title: What is the Microsoft Entra Connect Administration Agent - Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-aadc-admin-agent
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Describes the tools that are used to synchronize and monitor your on-premises environment with Microsoft Entra ID.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: a2820699-005d-daa9-e4c1-447d349724ff
document_version_independent_id: 7305384a-340c-0a95-d9fa-242dafbff605
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/whatis-aadc-admin-agent.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/whatis-aadc-admin-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/whatis-aadc-admin-agent.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a555a5ef-be63-d76f-5330-8427c58e3408
---

# What is the Microsoft Entra Connect Administration Agent - Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra Connect Administration Agent is a component of Microsoft Entra Connect that can be installed on a Microsoft Entra Connect server. The agent is used to collect specific data from your hybrid Active Directory environment. The collected data helps a Microsoft support engineer troubleshoot issues when you open a support case.

Note

The Microsoft Entra Connect Administration Agent is no longer part of the Microsoft Entra Connect installation, and it can't be used with Microsoft Entra Connect version 2.1.12.0 or later.

The Microsoft Entra Connect Administration Agent waits for specific requests for data from Microsoft Entra ID. The agent then takes the requested data from the sync environment and sends it to Microsoft Entra ID, where it's presented to the Microsoft support engineer.

The information that the Microsoft Entra Connect Administration Agent retrieves from your environment isn't stored. The information is shown only to the Microsoft support engineer to help them investigate and troubleshoot a Microsoft Entra Connect-related support case.

By default, the Microsoft Entra Connect Administration Agent isn't installed on the Microsoft Entra Connect server. To assist with support cases, you must install the agent to collect data.

## Install the Microsoft Entra Connect Administration Agent

To install the Microsoft Entra Connect Administration Agent on the Microsoft Entra Connect server, first be sure you meet some prerequisites, and then install the agent.

Prerequisites:

- Microsoft Entra Connect is installed on the server.
- Microsoft Entra Connect Health is installed on the server.

![Screenshot that shows the admin agent on the server.](media/whatis-aadc-admin-agent/adminagent0.png)

The Microsoft Entra Connect Administration Agent binaries are placed on the Microsoft Entra Connect server.

To install the agent:

1. Open PowerShell as administrator.
2. Go to the directory where the application is located: `cd "C:\Program Files\Microsoft Azure Active Directory Connect\Tools"`.
3. Run `ConfigureAdminAgent.ps1`.

When prompted, enter your Microsoft Entra Hybrid Identity Administrator credentials. These credentials should be the same credentials you entered during Microsoft Entra Connect installation.

Note

The `ConfigureAdminAgent.ps1` script is no longer included in Microsoft Entra Connect version 2.1.12.0 or later. The Microsoft Entra Connect Administration Agent itself is deprecated and cannot be installed on these versions.

After the agent is installed, you'll see the following two new programs in **Add/Remove Programs** in Control Panel on your server:

![Screenshot that shows the Add/Remove Programs list that includes the new programs you added.](media/whatis-aadc-admin-agent/adminagent1.png)

## What data in my sync service is visible to the Microsoft support engineer?

When you open a support case, the Microsoft support engineer can see this information for a specific user:

- The relevant data in Windows Server Active Directory (Windows Server AD).
- The Windows Server AD connector space on the Microsoft Entra Connect server.
- The Microsoft Entra connector space on the Microsoft Entra Connect server.
- The metaverse in the Microsoft Entra Connect server.

The Microsoft support engineer can't change any data in your system, and they can't see any passwords.

## What if I don't want the Microsoft support engineer to access my data?

After the agent is installed, if you don't want the Microsoft support engineer to access your data for a support call, you can disable the functionality by modifying the service config file:

1. In Notepad, open *C:\Program Files\Microsoft Azure AD Connect Administration Agent\AzureADConnectAdministrationAgentService.exe.config*.
2. Disable the **UserDataEnabled** setting as shown in the following example. If the **UserDataEnabled** setting exists and is set to **true**, set it to **false**. If the setting doesn't exist, add the setting.

    ```xml
    <appSettings>
      <add key="TraceFilename" value="ADAdministrationAgent.log" />
      <add key="UserDataEnabled" value="false" />
    </appSettings>
    ```
3. Save the config file.
4. Restart the Microsoft Entra Connect Administration Agent service as shown in the following figure:

    ![Screenshot that shows how to restart the Microsoft Entra Connect Administrator Agent service.](media/whatis-aadc-admin-agent/adminagent2.png)