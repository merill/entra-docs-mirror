---
layout: Conceptual
title: Preserve a group's organizational unit (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-preserve-group-organizational-unit-entra-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: mwongerapk
ms.reviewer: marshmacy
ms.subservice: hybrid-cloud-sync
ms.topic: how-to
ms.date: 2026-08-20T00:00:00.0000000Z
description: Set up the GroupDN directory extension so a group keeps its original organizational unit and common name after you convert its Source of Authority to Microsoft Entra ID.
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: e4d04717-e6bb-dbb1-accc-10d203929d4a
document_version_independent_id: e4d04717-e6bb-dbb1-accc-10d203929d4a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-preserve-group-organizational-unit-entra-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-preserve-group-organizational-unit-entra-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-preserve-group-organizational-unit-entra-to-active-directory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: c2490096-976c-b5dc-09fa-48bdeb951541
---

# Preserve a group's organizational unit (Preview) - Microsoft Entra ID | Microsoft Learn

When you convert a group's Source of Authority (SOA) to Microsoft Entra ID, the group's original organizational unit (OU) isn't detected automatically. Use the `GroupDN` directory extension to capture the group's distinguished name (DN) before you convert its SOA, then reference that extension in the OU and common name (CN) mapping expressions.

This article covers the one-time setup. Complete it **before** you convert the group to cloud-managed. For the mapping expressions that consume the extension, see [Preserve a group's original organizational unit](how-to-configure-entra-to-active-directory#preserve-a-groups-original-organizational-unit).

## Prerequisites

Complete the steps in [Prerequisites for provisioning from Microsoft Entra ID to Active Directory](how-to-prerequisites-provision-entra-to-active-directory) before you continue.

## Set up the GroupDN extension

Complete the following tasks in order, before you convert the group to cloud-managed.

### Change the group scope to Universal

To change the group scope to Universal:

1. Open **Active Directory Administrative Center**.
2. Select and hold (or right-click) the group, and then select **Properties**.
3. In the **Group** section, select **Universal** as the group scope.
4. Select **Save**.

### Create the extension

Cloud Sync only supports extensions created on the `CloudSyncCustomExtensionsApp` application. Create this application once per tenant if it doesn't already exist.

# [Graph PowerShell](#tab/ps)
1. Open an elevated PowerShell window and run the following commands to install modules and connect:

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser -Force
    Connect-MgGraph -Scopes "Application.ReadWrite.All","Directory.ReadWrite.All","Directory.AccessAsUser.All"
    ```
2. Check if the application exists. If it doesn't, create it, and ensure a service principal is present:

    ```powershell
    $tenantId = (Get-MgOrganization).Id
    $app = Get-MgApplication -Filter "identifierUris/any(uri:uri eq 'API://$tenantId/CloudSyncCustomExtensionsApp')"
    if (-not $app) {
      $app = New-MgApplication -DisplayName "CloudSyncCustomExtensionsApp" -IdentifierUris "API://$tenantId/CloudSyncCustomExtensionsApp"
    }
    $app
    
    $sp = Get-MgServicePrincipal -Filter "AppId eq '$($app.AppId)'"
    if (-not $sp) {
      $sp = New-MgServicePrincipal -AppId $app.AppId
    }
    $sp
    ```
3. Add a directory extension property named `GroupDN` — a string attribute on group objects:

    ```powershell
    New-MgApplicationExtensionProperty `
      -ApplicationId $app.Id `
      -Name "GroupDN" `
      -DataType "String" `
      -TargetObjects Group
    ```

# [Graph Explorer](#tab/ge)
1. Check if an application with the identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp` exists:

    ```http
    GET /applications?$filter=identifierUris/any(uri:uri eq 'api://<tenantId>/CloudSyncCustomExtensionsApp')
    ```
2. If the application doesn't exist, create it:

    ```http
    POST https://graph.microsoft.com/v1.0/applications
    Content-type: application/json
    
    {
      "displayName": "CloudSyncCustomExtensionsApp",
      "identifierUris": ["api://<tenant id>/CloudSyncCustomExtensionsApp"]
    }
    ```
3. Create the `GroupDN` directory extension (string type, for Group objects):

    ```http
    POST https://graph.microsoft.com/v1.0/applications/<ApplicationId>/extensionProperties
    Content-type: application/json
    
    {
      "name": "GroupDN",
      "dataType": "String",
      "isMultiValued": false,
      "targetObjects": [ "Group" ]
    }
    ```

---

For more information, see [Directory extensions for provisioning Microsoft Entra ID to Active Directory](custom-attribute-mapping-entra-to-active-directory).

### Map distinguishedName to the GroupDN extension

Tell Cloud Sync to populate the extension with the group's distinguished name (DN) from Active Directory. This captures the group's full DN (CN + OU path) in Microsoft Entra ID.

1. Open **Entra ID** &gt; **Entra Connect** &gt; **Cloud Sync**.
2. Select your **AD to Microsoft Entra ID** configuration.
3. Go to **Attribute mappings** and set **Object type** to **Group**.
4. Add a new attribute mapping:
    - **Mapping type**: Direct
    - **Source attribute**: `distinguishedName`
    - **Target attribute**: `extension_<appIdWithoutHyphens>_GroupDN`
5. Save the schema to trigger a sync.

### Verify the mapping and convert SOA

After a sync runs, verify that the extension property is populated with the DN by using Microsoft Graph PowerShell:

```powershell
$groupDisplayName = 'My Security Group'
$clientId = $app.AppId
$propName = "extension_{0}_GroupDN" -f ($clientId -replace "-","")
$grp = Get-MgGroup -Filter "displayName eq '$groupDisplayName'" -ConsistencyLevel eventual
Get-MgGroup -GroupId $grp.Id -Property "id,displayName,$propName" |
  Select-Object id, displayName, @{n=$propName; e={$_."$propName"}}
```

Once the DN is stored in the extension, [convert the group's Source of Authority to Microsoft Entra ID](../how-to-group-source-of-authority-configure). The group becomes cloud-managed while its original DN is preserved in the extension for use in the OU and CN mapping expressions that follow.