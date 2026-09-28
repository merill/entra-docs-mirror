---
layout: Conceptual
title: Microsoft Entra Connect Single Object Sync  - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-single-object-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to synchronize one object from Active Directory to Microsoft Entra ID for troubleshooting.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 9897bb52-2f1d-a182-292f-b45129105a70
document_version_independent_id: 6a6aef13-e3d3-d1bb-33ca-6faa1f339c00
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-single-object-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-single-object-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-single-object-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 320f651b-3243-f39a-9ec8-1930c8444374
---

# Microsoft Entra Connect Single Object Sync  - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra Connect Single Object Sync tool is a PowerShell cmdlet that can be used to synchronize an individual object from Active Directory to Microsoft Entra ID. The report generated can be used to investigate and troubleshoot per object synchronization issues.

Note

The tool supports synchronization from Active Directory to Microsoft Entra ID. It does not support synchronization from Microsoft Entra ID to Active Directory.

The tool supports synchronizing an Object Modification Add and Update. It does not support synchronizing an Object Modification Delete.

## How it works

The Single Object Sync tool requires an Active Directory distinguished name as input to find the source connector and partition for import. It exports the changes to Microsoft Entra ID. The tool generates a JSON output similar to the **provisioningObjectSummary** resource type.

The Single Object Sync tool performs the following steps:

1. Determine if Object's (source) Domain (Active Directory Connector and Partition) in sync scope.
2. Determine if Object's (target) Domain (Microsoft Entra Connector and Partition) in sync scope.
3. Determine if Object's Organizational Unit in sync scope.
4. Determine if Object is accessible using connector account credentials.
5. Determine if Object's Type in sync scope.
6. Determine if Object is in sync scope if Group Filtering enabled.
7. Import Object from Active Directory to Active Directory Connector Space.
8. Import Object from Microsoft Entra ID to Microsoft Entra Connector Space.
9. Sync Object from Active Directory Connector Space.
10. Export Object from Microsoft Entra Connector Space to Microsoft Entra ID.

In addition to the JSON output, the tool generates an HTML report that has all the details of the synchronization operation. The HTML report is located in **C:\ProgramData\AADConnect\ADSyncObjectDiagnostics\ ADSyncSingleObjectSyncResult-&lt;date&gt;.htm**. This HTML report can be shared with the support team to do further troubleshooting, if needed.

The HTML report has the following:

| Tab | Description |
| --- | --- |
| Steps | Outlines the steps taken to synchronize an object. Each step contains details for troubleshooting. The Import, Sync, and Export steps contain additional attribute info such as name, is multi-valued, type, value, value add, value delete, operation, sync rule, mapping type and data source. |
| Troubleshooting & Recommendation | Provides the error code and reason. The error information is available only if a failure happens. |
| Modified Properties | Shows the old value and the new value. If there's no old value or if the new value is deleted, that cell is blank. For multivalued attributes, it shows the count. The attribute name is a link to Steps tab: Export Object from Microsoft Entra Connector Space to Microsoft Entra ID: Attribute Info that contains additional details of the attribute such as name, is multi-valued, type, value, value add, value delete, operation, sync rule, mapping type and data source. |
| Summary | Provides an overview of what happened and identifiers for the object in the source and target systems. |

## Prerequisites

In order to use the Single Object Sync tool, you need to use the following:

- 2021 March release ([1.6.4.0](reference-connect-version-history#1640)) of Microsoft Entra Connect or later.
- [PowerShell 5.0](/en-us/powershell/scripting/windows-powershell/whats-new/what-s-new-in-windows-powershell-50)

### Run the Single Object Sync tool

To run the Single Object Sync tool, perform the following steps:

1. Open a new Windows PowerShell session on your Microsoft Entra Connect server with the Run as Administrator option.
2. Set the [execution policy](/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy) to RemoteSigned or Unrestricted.
3. Disable the sync scheduler after verifying that no synchronization operations are running.

    `Set-ADSyncScheduler -SyncCycleEnabled $false`
4. Import the AdSync Diagnostics module

    `Import-module -Name "C:\Program Files\Microsoft Azure AD Sync\Bin\ADSyncDiagnostics\ADSyncDiagnostics.psm1"`
5. Invoke the Single Object Sync cmdlet.

    `Invoke-ADSyncSingleObjectSync -DistinguishedName "CN=testobject,OU=corp,DC=contoso,DC=com" | Out-File -FilePath ".\output.json"`
6. Re-enable the Sync Scheduler.

    `Set-ADSyncScheduler -SyncCycleEnabled $true`

| Single Object Sync Input Parameters | Description |
| --- | --- |
| DistinguishedName | This is a required string parameter. This is the Active Directory object’s distinguished name that needs synchronization and troubleshooting. |
| StagingMode | This is an optional switch parameter. This parameter can be used to prevent exporting the changes to Microsoft Entra ID.**Note**: The cmdlet commits the sync operation. **Note**: Microsoft Entra Connect Staging server won't export the changes to Microsoft Entra ID. |
| NoHtmlReport | This is an optional switch parameter. This parameter can be used to prevent generating the HTML report. |

## Single Object Sync throttling

The Single Object Sync tool **is** intended for investigating and troubleshooting per object synchronization issues. It is **not** intended to replace the synchronization cycle run by the Scheduler. The import from Microsoft Entra ID and export to Microsoft Entra ID are subject to throttling limits. Please retry after 5 minutes, if you reach the throttling limit.