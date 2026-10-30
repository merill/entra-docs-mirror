---
layout: Conceptual
title: AADCloudSyncTools PowerShell module for Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/reference-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to install the Microsoft Entra Connect cloud provisioning agent.
ms.custom: no-azure-ad-ps-ref, msecd-doc-authoring-1024
ms.topic: how-to
ms.date: 2026-08-21T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 23c548e7-2ce5-259f-de2a-09f8ef731c0d
document_version_independent_id: 162a109d-ee93-e361-299f-ea371c8239c8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/reference-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/reference-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/reference-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2ce14715-d7be-b607-3d7a-345c5fa2ef31
---

# AADCloudSyncTools PowerShell module for Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn

The AADCloudSyncTools module provides a set of useful tools that can help you manage your deployments of Microsoft Entra Cloud Sync.

## Prerequisites

You can automatically install all the prerequisites for the AADCloudSyncTools module by using `Install-AADCloudSyncToolsPrerequisites`. You'll do that in the next section of this article.

Here are some details about what you need:

- The AADCloudSyncTools module uses Microsoft Authentication Library (MSAL) authentication, so it requires installation of the MSAL.PS module. To verify the installation, in a PowerShell window, run `Get-module MSAL.PS -ListAvailable`. If the module is installed correctly, you'll get a response. If necessary, you can use `Install-AADCloudSyncToolsPrerequisites` to install the latest version of MSAL.PS.
- Although the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) module is not required for any functionality of the AADCloudSyncTools module, it is useful. So it's automatically installed when you use `Install-AADCloudSyncToolsPrerequisites`.
- Installing modules from the PowerShell Gallery requires Transport Layer Security (TLS) 1.2 enforcement. The cmdlet `Install-AADCloudSyncToolsPrerequisites` sets TLS 1.2 enforcement before installing all the prerequisites. To ensure that you can manually install modules, set the following in the PowerShell session before using the cmdlet:

    ```
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
    ```
- The AADCloudSyncTools module might not work correctly if the Microsoft Entra Connect cloud provisioning agent is not running or the configuration wizard has not finished successfully.

## Install the AADCloudSyncTools PowerShell module

1. Open Windows PowerShell with administrative privileges.
2. Run `Import-module -Name "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Utility\AADCloudSyncTools"`.
3. To verify that the module was imported, run `Get-module AADCloudSyncTools`.

    You should now see information about the module.
4. To install the AADCloudSyncTools module prerequisites, run `Install-AADCloudSyncToolsPrerequisites`.
5. On the first run, the PowerShellGet module will be installed if it's not present. To load the new PowerShellGet module, close the PowerShell window and open a new PowerShell session with administrative privileges.
6. Import the module again by running `Import-module -Name "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Utility\AADCloudSyncTools"`.
7. Run `Install-AADCloudSyncToolsPrerequisites` again to install the MSAL and Microsoft Graph PowerShell modules.

    All prerequisites should now be installed.

    ![Screenshot of the notification in the PowerShell window that says the prerequisites were installed successfully.](media/reference-powershell/install-1.png)
8. Every time you want to use the AADCloudSyncTools module in a new PowerShell session, run the following command:

    ```
    Import-module "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Utility\AADCloudSyncTools"
    ```

## AADCloudSyncTools cmdlets

Note

Before using AADCloudSyncTools module make sure the Microsoft Entra Connect cloud provisioning agent is running and the configuration wizard has finished successfully. To troubleshoot wizard issues, you can find trace logs in the folder *C:\ProgramData\Microsoft\Azure AD Connect Provisioning Agent\Trace*, see [Cloud sync troubleshooting](how-to-troubleshoot) for more information.

### Connect-AADCloudSyncTools

This cmdlet uses the MSAL.PS module to request a token for the Microsoft Entra administrator to access Microsoft Graph.

### Export-AADCloudSyncToolsLogs

This cmdlet exports and packages all the troubleshooting data in a compressed file, as follows:

1. Sets verbose tracing and starts collecting data from the provisioning agent (same as `Start-AADCloudSyncToolsVerboseLogs`).
2. Stops data collection after three minutes and disables verbose tracing (same as `Stop-AADCloudSyncToolsVerboseLogs`).
3. Collects Event Viewer logs for the last 24 hours.
4. Compresses all the agent logs, verbose logs, and Event Viewer logs into a .zip file in the user's *Documents* folder.

You can use the following options to fine-tune your data collection:

- `SkipVerboseTrace` to only export current logs without capturing verbose logs (default = false).
- `TracingDurationMins` to specify a different capture duration (default = 3 minutes).
- `OutputPath` to specify a different output path (default = user’s Documents folder).

### Get-AADCloudSyncToolsInfo

This cmdlet shows Microsoft Entra tenant details and the state of internal variables.

### Get-AADCloudSyncToolsJob

This cmdlet uses Microsoft Graph to get Microsoft Entra service principals and returns the sync job's information. You can also call it by using the specific sync job ID as a parameter.

### Get-AADCloudSyncToolsJobSchedule

This cmdlet uses Microsoft Graph to get Microsoft Entra service principals and returns the sync job's schedule. You can also call it by using the specific sync job ID as a parameter.

### Get-AADCloudSyncToolsJobSchema

This cmdlet uses Microsoft Graph to get Microsoft Entra service principals and returns the sync job's schema.

### Get-AADCloudSyncToolsJobScope

This cmdlet uses Microsoft Graph to get the sync job's schema for the provided sync job ID and outputs all filter groups' scopes.

### Get-AADCloudSyncToolsJobSettings

This cmdlet uses Microsoft Graph to get Microsoft Entra service principals and returns the sync job's settings. You can also call it by using the specific sync job ID as a parameter.

### Get-AADCloudSyncToolsJobStatus

This cmdlet uses Microsoft Graph to get Microsoft Entra service principals and returns the sync job's status. You can also call it by using the specific sync job ID as a parameter.

### Get-AADCloudSyncToolsServicePrincipal

This cmdlet uses Microsoft Graph to get the service principals for Microsoft Entra ID and/or Azure Service Fabric. Without parameters, it will return only Microsoft Entra service principals.

### Install-AADCloudSyncToolsPrerequisites

This cmdlet checks for the presence of PowerShellGet v2.2.4.1 or later, the Microsoft Graph PowerShell module, and the MSAL.PS module. It installs these items if they're missing.

### Invoke-AADCloudSyncToolsGraphQuery

This cmdlet invokes a web request for the URI, method, and body specified as parameters.

### Restart-AADCloudSyncToolsJob

This cmdlet restarts a full synchronization.

### Resume-AADCloudSyncToolsJob

This cmdlet continues synchronization from the previous watermark.

### Start-AADCloudSyncToolsVerboseLogs

This cmdlet modifies *AADConnectProvisioningAgent.exe.config* to enable verbose tracing and restarts the AADConnectProvisioningAgent service. You can use `-SkipServiceRestart` to prevent service restart, but any configuration changes will not take effect. You can find these trace logs in the folder *C:\ProgramData\Microsoft\Azure AD Connect Provisioning Agent\Trace*.

### Stop-AADCloudSyncToolsVerboseLogs

This cmdlet modifies *AADConnectProvisioningAgent.exe.config* to disable verbose tracing and restarts the AADConnectProvisioningAgent service. You can use `-SkipServiceRestart` to prevent service restart, but any configuration changes will not take effect.

### Suspend-AADCloudSyncToolsJob

This cmdlet pauses synchronization.

### Disable-AADCloudSyncToolsDirSyncAccidentalDeletionPrevention

Disables accidentalDeletionPrevention tenant feature

```powershell
Disable-AADCloudSyncToolsDirSyncAccidentalDeletionPrevention -tenantId <TenantId>
```

This cmdlet requires `TenantId` of the Microsoft Entra tenant. It will verify if Accidental Deletion Prevention feature, set on the tenant with Microsoft Entra Connect (ADSync, not cloud sync), is enabled and disables it.

#### Example:

```powershell
Disable-AADCloudSyncToolsDirSyncAccidentalDeletionPrevention -tenantId "aaaabbbb-0000-cccc-1111-dddd2222eeee"
```