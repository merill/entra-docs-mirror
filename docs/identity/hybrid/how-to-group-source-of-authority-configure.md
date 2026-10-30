---
layout: Conceptual
title: Configure Group Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/how-to-group-source-of-authority-configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to convert group management from Active Directory Domain Services to Microsoft Entra ID by using Group Source of Authority (SOA).
ms.subservice: hybrid-cloud-sync
ms.topic: how-to
ms.date: 2025-10-13T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 82090af7-7979-65a5-c0bb-59d9e51f2d1d
document_version_independent_id: 82090af7-7979-65a5-c0bb-59d9e51f2d1d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/how-to-group-source-of-authority-configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/how-to-group-source-of-authority-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/how-to-group-source-of-authority-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: a2d396ea-55d7-4dc7-d305-80a676a5362a
---

# Configure Group Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article explains the prerequisites and steps to configure Group Source of Authority (SOA), how to revert changes, and limitations. For more information about Group SOA, see [Embrace cloud-first posture: Convert Group Source of Authority to the cloud](concept-source-of-authority-overview).

## Prerequisites

| Requirement | Description |
| --- | --- |
| **Roles** | [Hybrid Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-administrator) is required to call the Microsoft Graph APIs to read and update SOA of groups.[Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) or [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) is required to grant user consent to the required permissions to Microsoft Graph Explorer or the app used to call the Microsoft Graph APIs. |
| **Permissions** | For apps calling into the onPremisesSyncBehavior Microsoft Graph API, the Group-OnPremisesSyncBehavior.ReadWrite.All permission scope needs to be granted. For more information, see how to grant this permission to Graph Explorer or an existing app in your tenant. |
| **License needed** | Microsoft Entra Free license. |
| **Sync client** | Before applying SOA, make sure you are on a supported version of your sync client so the client will honor the SOA setting. If you use Connect Sync, upgrade to the minimum version [2.5.76.0](/en-us/entra/identity/hybrid/connect/reference-connect-version-history#25760). If you use Cloud Sync, upgrade to minimum version [1.1.1370.0](/en-us/entra/identity/hybrid/cloud-sync/reference-version-history#1113700). |
| **Provisioning to AD DS (optional)** | To provision a SOA converted group from Microsoft Entra ID to Active Directory Domain Services (AD DS), you need to use Cloud Sync. You also need to complete steps to prepare the groups for provisioning to AD DS with their original OU path. For more information, see [Prepare groups for Group SOA conversion and provisioning](concept-group-source-of-authority-guidance#prepare-groups-for-group-soa-conversion-and-provisioning). |

### Download Connect Sync client

1. Download Connect Sync build version [2.5.76.0](/en-us/entra/identity/hybrid/connect/reference-connect-version-history#25760) or later.
2. Go to **Programs** in Control Panel and confirm the version of Microsoft Entra Connect Sync.

### Download Cloud Sync client

1. Download Cloud Sync build version [1.1.1370.0](/en-us/entra/identity/hybrid/cloud-sync/reference-version-history#1113700) or later.
2. Learn how to [identify the agent's current version](/en-us/azure/active-directory/hybrid/cloud-sync/how-to-automatic-upgrade).
3. Follow the [instructions to configure provisioning from AD DS to Microsoft Entra ID](/en-us/entra/identity/hybrid/cloud-sync/how-to-configure).

## Grant permission to apps

You can grant permission in the Microsoft Entra admin center or in Graph Explorer. This highly privileged operation requires the Application Administrator or Cloud Application Administrator role. You can also grant consent by using PowerShell. For more information, see [Grant consent on behalf of a single user](/en-us/entra/identity/enterprise-apps/grant-consent-single-user?pivots=ms-graph).

### Custom apps

Follow these steps to grant `Group-OnPremisesSyncBehavior.ReadWrite.All` permission to the corresponding app. For more information about how to add new permissions to your app registration and grant consent, see [Update an app's requested permissions in Microsoft Entra ID](/en-us/entra/identity-platform/howto-update-permissions).

### Use Microsoft Entra admin center to grant permission to apps

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Enterprise Applications** &gt; ***App name***.
3. Select **Permissions** &gt; **Grant admin consent for *tenant name***.
4. Sign in again as an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
5. Review the list of permissions that require your consent, and select **Accept**.
6. You can see the list of permissions that you granted:

    ![Screenshot of how to grant permission.](media/how-to-group-source-of-authority-configure/permission.png)

### Use Graph Explorer to grant permission to apps

1. Open [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and sign in as an [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) or [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Select the profile icon, and select **Consent to permissions**.
3. Search for Group-OnPremisesSyncBehavior, and select **Consent** for the permission.

[![Screenshot of how to grant consent to Group-OnPremisesSyncBehavior.ReadWrite permission.](media/how-to-group-source-of-authority-configure/consent.png)](media/how-to-group-source-of-authority-configure/consent.png#lightbox)

## Prepare groups for Group SOA conversion and provisioning

If you want to provision the group back to AD DS, plan to complete the following steps to preserve the OU Path and set it in the **Group Provision to AD** configuration with the right mapping:

1. Change the group scope for the AD DS groups to Universal.
2. Create a tenant-scoped directory extension property for groups.
3. Map an on-premises value, such as the distinguished name (DN), directly into the extension property.
4. Verify the property value using Microsoft Graph.
5. Convert the Source of Authority (SOA) when ready.
6. Use custom expressions to ensure Cloud Sync provisions groups back to AD DS with the same CN and OU values.

For more information, see [Provision groups to Active Directory Domain Services by using Microsoft Entra Cloud Sync](cloud-sync/how-to-configure-entra-to-active-directory).

## Convert SOA for a test group

Follow these steps to convert the SOA for a test group:

1. Create a security group or a mail-enabled distribution group in AD for testing and add group members. You can also use a group that is synced to Microsoft Entra ID by using Connect Sync.
2. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
3. Verify that the group appears in the Microsoft Entra admin center as a synced group.
4. Use Microsoft Graph API to convert the SOA of the group object (*isCloudManaged*=true). Open [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and sign in with an appropriate user role, such as Groups admin.
5. Let's check the existing SOA status. We didn’t update the SOA yet, so the *isCloudManaged* attribute value should be false. Replace the *{ID}* in the following examples with the object ID of your group. For more information about this API, see [Get onPremisesSyncBehavior](/en-us/graph/api/onpremisessyncbehavior-get).

    ```https
    GET https://graph.microsoft.com/v1.0/groups/{ID}/onPremisesSyncBehavior?$select=isCloudManaged
    ```

    ![Screenshot of how to use Microsoft Graph Explorer to get the SOA value of a group.](media/how-to-group-source-of-authority-configure/get-group.png)
6. Confirm that the synced group is read-only. Because the group is managed on-premises, any write attempts to the group in the cloud fail. The error message differs for mail-enabled groups, but updates still aren't allowed.

    Note

    If this API fails with 403, use the **Modify permissions** tab to grant consent to the required Group.ReadWrite.All permission.

    ```https
    PATCH https://graph.microsoft.com/v1.0/groups/{ID}/
       {
         "DisplayName": "Group1 Name Updated"
       }   
    ```

    ![Screenshot of an attempt to update a group to verify it's read-only.](media/how-to-group-source-of-authority-configure/try-update.png)
7. Search the Microsoft Entra admin center for the group. Verify that all group fields are greyed out, and that source is Windows Server AD DS:

    ![Screenshot of basic group properties.](media/how-to-group-source-of-authority-configure/basic.png)

    ![Screenshot of advanced group properties.](media/how-to-group-source-of-authority-configure/properties.png)
8. Now you can update the SOA of group to be cloud-managed. Run the following operation in Microsoft Graph Explorer for the group object you want to convert to the cloud. For more information about this API, see [Update onPremisesSyncBehavior](/en-us/graph/api/onpremisessyncbehavior-update).

    ```https
    PATCH https://graph.microsoft.com/v1.0/groups/{ID}/onPremisesSyncBehavior
       {
         "isCloudManaged": true
       }   
    ```

    ![Screenshot of PATCH operation to update group properties.](media/how-to-group-source-of-authority-configure/switch.png)
9. To validate the change, call GET to verify *isCloudManaged* is true.

    ```https
    GET https://graph.microsoft.com/v1.0/groups/{ID}/onPremisesSyncBehavior?$select=isCloudManaged
    ```

    ![Screenshot of GET call to verify group properties.](media/how-to-group-source-of-authority-configure/cloud-managed.png)
10. Confirm the change in the Audit Logs. To access Audit Logs in the Azure portal, open **Manage Microsoft Entra ID** &gt; **Monitoring** &gt; **Audit Logs**, or search for *audit logs*. Select **Change Source of Authority from AD to cloud** as the activity.

    ![Screenshot of change to group properties in Audit Logs.](media/how-to-group-source-of-authority-configure/audit.png)
11. Check that the group can be updated in the cloud.

    ```https
    PATCH https://graph.microsoft.com/v1.0/groups/{ID}/
       {
         "DisplayName": "Group1 Name Updated"
       }   
    ```

    ![Screenshot of a retry to change group properties.](media/how-to-group-source-of-authority-configure/retry-update.png)
12. Open Microsoft Entra admin center and confirm that the group **Source** property is **Cloud**.

    ![Screenshot of how to confirm group source property.](media/how-to-group-source-of-authority-configure/source-cloud.png)

## Connect Sync client

1. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
2. To look at the group object with converted SOA, in the **Synchronization Service Manager**, go to **Connectors**:

    ![Screenshot of Connectors.](media/how-to-group-source-of-authority-configure/connectors.png)
3. Right-click **Active Directory Domain Services Connector**. Search for the group by the relative domain name (RDN) setting "CN=&lt;GroupName&gt;":

    ![Screenshot of how to search for RDN.](media/how-to-group-source-of-authority-configure/search.png)
4. Double-click the searched entry, and select **Lineage** &gt; **Metaverse Object Properties**.

    ![Screenshot of how to view lineage.](media/how-to-group-source-of-authority-configure/lineage.png)
5. Select **Connectors** and double-click the **Entra ID object** with "CN={&lt;Alphanumeric Characters&gt;}".
6. You can see that the **blockOnPremisesSync** property is set to true on the Entra ID object. This property value means that any changes made in the corresponding AD DS object don't flow to the Entra ID object:

    ![Screenshot of how to block data flow.](media/how-to-group-source-of-authority-configure/block.png)
7. Let’s update the on-premises group object. We'll change the group name from *SecGroup1* to *SecGroup1.1*:

    ![Screenshot of how to change the object name.](media/how-to-group-source-of-authority-configure/change-name.png)
8. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
9. Open Event viewer and filter the Application log for event ID 6956. This event ID is reserved to inform the customers that the object isn't synced to the cloud because the SOA of the object is in the cloud.

    ![Screenshot of event ID 6956.](media/how-to-group-source-of-authority-configure/event-6956.png)

## Bulk updates for Group SOA

You can use the following PowerShell script to automate Group SOA updates by using app-based authentication.

```powershell
<#
.SYNOPSIS
    Updates groups to set isCloudManaged parameter to true for on-premises synchronized groups.

.DESCRIPTION
    This script reads a file containing group Ids, checks each group's OnPremisesSyncEnabled property,
    and if true, calls the onPremisesSyncBehavior API to set isCloudManaged to true.

.PARAMETER FilePath
    Mandatory. Path to the file containing group Ids (one per line).

.PARAMETER WhatIf
    Boolean parameter. When true (default), shows what would be done without making actual changes.

.EXAMPLE
    .\Update-GroupSoA.ps1 -FilePath "C:\temp\groups.txt"
    .\Update-GroupSoA.ps1 -FilePath "C:\temp\groups.txt" -WhatIf $false

.NOTES
    Requires Microsoft.Graph PowerShell module to be installed and appropriate permissions.
    Required Graph permissions: Group.ReadWrite.All, Group-OnPremisesSyncBehavior.ReadWrite.All

    Input file should contain one group Id (GUID) per line.
#>

[CmdletBinding()]
param(
    [Parameter(Mandatory = $true)]
    [string]$FilePath,

    [Parameter(Mandatory = $false)]
    [bool]$WhatIf = $true
)

# Import Groups module
try {
    $moduleName = "Microsoft.Graph.Groups"
    if (-not (Get-Module -Name $moduleName)) {
        Import-Module -Name $moduleName
    }
    Write-Host "Successfully imported Microsoft Graph modules."
}
catch {
    Write-Error "Failed to import Microsoft Graph modules. Please ensure Microsoft.Graph PowerShell SDK is installed."
    Write-Host "Install with: Install-Module Microsoft.Graph -Scope CurrentUser"
    exit 1
}

# Connect to MS Graph
$context = Get-MgContext
if (-not $context) {
    Connect-MgGraph -Scopes 'Group.ReadWrite.All', 'Group-OnPremisesSyncBehavior.ReadWrite.All'
}

# Validate input file
if (-not (Test-Path $FilePath)) {
    Write-Error "Input file not found: $FilePath"
    exit 1
}

Write-Host "Starting group update process using $FilePath (WhatIf: $WhatIf)..."
Write-Host "-----------------------------------"

# Read group Ids from file
$groupGuids = Get-Content $FilePath

if ($groupGuids.Count -eq 0) {
    Write-Error "No group Ids found in the input file."
    exit 1
}

Write-Host "Found $($groupGuids.Count) group Ids to process."

# Initialize counters for summary
$totalGroups = $groupGuids.Count
$processedCount = 0
$updatedCount = 0
$skippedCount = 0
$errorCount = 0

# Process each group
foreach ($groupId in $groupGuids) {
    $processedCount++
    Write-Host "`nProcessing $groupId ($processedCount/$totalGroups)"

    try {
        $group = Get-MgGroup -GroupId $groupId -Property "Id,DisplayName,OnPremisesSyncEnabled"

        Write-Host "Group Name: $($group.DisplayName)"
        Write-Host "OnPremisesSyncEnabled: $($group.OnPremisesSyncEnabled)"

        if ($group.OnPremisesSyncEnabled -eq $true) {
            $actionDescription = "Set isCloudManaged to true for group '$($group.DisplayName)'"

            if ($WhatIf) {
                Write-Host "Skipping since WhatIf is enabled: $actionDescription"
                $skippedCount++
            }
            else {
                try {
                    # Call the onPremisesSyncBehavior API to set isCloudManaged to true
                    $body = @{
                        isCloudManaged = $true
                    }

                    $uri = "https://graph.microsoft.com/v1.0/groups/$groupId/onPremisesSyncBehavior"
                    Invoke-MgGraphRequest -Uri $uri -Method PATCH -Body ($body | ConvertTo-Json) -ContentType "application/json"

                    Write-Host "SUCCESS: Updated group to cloud-managed"
                    $updatedCount++
                }
                catch {
                    Write-Host "ERROR: Failed to update group: $_"
                    $errorCount++
                }
            }
        }
        else {
            Write-Host "SKIPPED: Group is not on-premises synchronized"
            $skippedCount++
        }
    }
    catch {
        Write-Host "ERROR: Failed to retrieve group information: $_"
        $errorCount++
    }
}

Write-Host "`n-----------------------------------"
Write-Host "SUMMARY"
Write-Host "-----------------------------------"
Write-Host "Total groups processed: $totalGroups"
Write-Host "Successfully updated: $updatedCount"
Write-Host "Skipped (not sync-enabled or WhatIf): $skippedCount"
Write-Host "Errors encountered: $errorCount"

Write-Host "`nScript completed."
```

### Status of attributes after you convert SOA

The following table explains the status for *isCloudManaged* and *onPremisesSyncEnabled* attributes after you convert the SOA of an object.

| Admin step | isCloudManaged value | onPremisesSyncEnabled value | Description |
| --- | --- | --- | --- |
| Admin syncs an object from AD DS to Microsoft Entra ID | `false` | `true` | When an object is originally synchronized to Microsoft Entra ID, the *onPremisesSyncEnabled* attribute is set to `true` and *isCloudManaged* is set to `false`. |
| Admin converts the source of authority (SOA) of the object to the cloud | `true` | `null` | After an admin converts the SOA of an object to the cloud, the *isCloudManaged* attribute becomes set to `true` and the *onPremisesSyncEnabled* attribute value is set to `null`. |
| Admin rolls back the SOA operation | `false` | `null` | If an admin converts the SOA back to AD, the *isCloudManaged* is set to `false` and *onPremisesSyncEnabled* is set to `null` until the sync client takes over the object. |
| Admin creates a cloud native object in Microsoft Entra ID | `false` | `null` | If an admin creates a new cloud-native object in Microsoft Entra ID, *isCloudManaged* is set to `false` and *onPremisesSyncEnabled* is set to `null`. |

## Roll back SOA update

Important

Make sure that the groups that you roll back have no cloud references. Remove cloud users from SOA converted groups, and remove these groups from access packages before you roll back the group to AD DS. The sync client takes over the object in the next sync cycle. For a sample PowerShell script to identify and remove cloud users from groups, see: [Script to identify cloud members (users) of a group](how-to-group-source-of-authority-configure#script-to-identify-cloud-members-users-of-a-group).

You can run this operation to roll back the SOA update and revert the SOA to on-premises.

```https
PATCH https://graph.microsoft.com/v1.0/groups/{ID}/onPremisesSyncBehavior
   {
     "isCloudManaged": false
   }   
```

![Screenshot of API call to revert SOA.](media/how-to-group-source-of-authority-configure/rollback.png)

Note

The change of *isCloudManaged* to `false` allows an AD DS object that's in scope for sync to be taken over by Connect Sync the next time it runs. Until the next time Connect Sync runs, the object can be edited in the cloud. The rollback of SOA is finished only after *both* the API call and the next scheduled or forced run of Connect Sync are complete.

### Validate the change in the Audit Logs

Select activity as **Undo changes to Source of Authority from AD DS to cloud**:

![Screenshot of Undo Changes in Audit Logs.](media/how-to-group-source-of-authority-configure/audit-undo-changes.png)

## Validate in Connect Sync client

1. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
2. Open the object in the **Synchronization Server Manager** (details are in the Connect Sync Client section). You can see the state of the Microsoft Entra ID connector object is **Awaiting Export Confirmation** and *blockOnPremisesSync* = false, which means the object SOA is taken over by the on-premises again.

    ![Screenshot of an object awaiting export.](media/how-to-group-source-of-authority-configure/await-export.png)

## Limitations

- **No reconciliation support for AD DS groups**: An AD DS admin (or an application with sufficient permissions) can directly modify an AD DS group. If Group SOA is converted for the group, or if cloud security group provisioning to AD DS is enabled, those local AD changes aren't reflected in Microsoft Entra ID. When a change to the cloud security group is made, any local AD DS changes are overwritten when group provisioning to AD DS runs.
- **No dual write allowed**: After you start to manage the memberships for the converted group (say cloud group A) from Microsoft Entra ID, and you provision this group to AD as a nested group under another AD DS group (OnPremGroupB) that's in scope for sync to Microsoft Entra ID, the membership references of group A aren't synced when sync happens for OnPremGroupB. The membership references aren't synced because the sync client doesn't know the cloud group membership references. This behavior is by design.
- **No SOA conversion of nested groups**: If there are nested groups in AD DS, and you want to convert the SOA of the parent group or top group to Microsoft Entra ID, only the parent group SOA is converted. Nested groups in the parent group continue to be AD DS groups. You need to convert the SOA of any nested groups one-by-one. We recommend you start with the group that is lowest in the hierarchy, and move up the tree.
- **No support for extension attributes (1-15)**: Extension attributes 1–15 aren't supported on cloud security groups and aren't supported after SOA is converted.

## Script to identify cloud members (users) of a group

The following script can be used to identify and remove cloud users from groups:

```powershell
<#
.SYNOPSIS
    Finds cloud users in an Entra ID group and optionally removes them.

.DESCRIPTION
    This script pages through all users in a specified Entra ID group, identifies cloud users
    (users where onPremisesSyncEnabled is not set to true), and prints their details.
    Optionally removes these users from the group if removeUsers is set to true.

.PARAMETER GroupId
    The GUID of the Entra ID group to process. This parameter is required.

.PARAMETER RemoveUsers
    Boolean flag to indicate whether to remove cloud users from the group. 
    Default is false (optional parameter).

.EXAMPLE
    .\Find-CloudUsersInGroup.ps1 -GroupId "12345678-1234-1234-1234-123456789012"
    .\Find-CloudUsersInGroup.ps1 -GroupId "12345678-1234-1234-1234-123456789012" -RemoveUsers $true

.NOTES
    Requires Microsoft.Graph PowerShell module to be installed and appropriate permissions.
    Required Graph permissions: Group.Read.All, GroupMember.Read.All, User.Read.All and GroupMember.ReadWrite.All (if removing users)
#>

[CmdletBinding()]
param(
    [Parameter(Mandatory = $true)]
    [System.Guid]$GroupId,

    [Parameter(Mandatory = $false)]
    [bool]$RemoveUsers = $false
)

# Import required modules
try {
    $moduleName = "Microsoft.Graph.Groups"
    if (-not (Get-Module -Name $moduleName)) {
        Import-Module -Name $moduleName
    }
    $moduleName = "Microsoft.Graph.Users"
    if (-not (Get-Module -Name $moduleName)) {
        Import-Module -Name $moduleName
    }
    Write-Host "Microsoft Graph modules imported successfully"
}
catch {
    Write-Error "Failed to import Microsoft Graph modules. Please install Microsoft.Graph PowerShell module."
    Write-Error "Run: Install-Module Microsoft.Graph -Scope CurrentUser"
    exit 1
}

# Connect to MS Graph and verify the group exists
$context = Get-MgContext
if (-not $context) {
    Connect-MgGraph -Scopes 'Group.Read.All','GroupMember.Read.All','GroupMember.ReadWrite.All','User.Read.All'
}

$group = Get-MgGroup -GroupId $GroupId -Property "Id,DisplayName,MailEnabled"
Write-Host "Processing group: $($group.DisplayName) (ID: $GroupId)"

if ($group.MailEnabled -eq $true) {
    Write-Warning "The specified group is mail-enabled. Users can only be identified using this script. To remove users, use Exchange."
}

# Initialize counters
$totalUsers = 0
$cloudUsers = 0
$removedUsers = 0

Write-Host "`nStarting to process group users..."

try {
    # Get all group members that are users
    $usersInGroup = Get-MgGroupMemberAsUser -GroupId $GroupId -All -Property "Id"

    if ($usersInGroup.Count -ge 1) {
        $totalUsers = $usersInGroup.Count
        Write-Host "Found $totalUsers total users in the group"
    }
    else {
        Write-Host "No users found in the group"
        exit 0
    }
}
catch {
    Write-Error "Failed to retrieve group users: $($_.Exception.Message)"
    exit 1
}

Write-Host "`nProcessing each user to identify cloud users..."
Write-Host "-----------------"

# Process each user
foreach ($user in $usersInGroup) {
    try {
        # Get detailed user information
        $user = Get-MgUser -UserId $user.Id -Property "Id,DisplayName,UserPrincipalName,OnPremisesSyncEnabled"

        # Check if user is a cloud user
        $isCloudUser = -not $user.OnPremisesSyncEnabled

        if ($isCloudUser) {
            $cloudUsers++

            # Print cloud user details
            Write-Host "Cloud User Found:"
            Write-Host "  Object ID: $($user.Id)"
            Write-Host "  Display Name: $($user.DisplayName)"
            Write-Host "  User Principal Name: $($user.UserPrincipalName)"
            Write-Host "  OnPremisesSyncEnabled: $($user.OnPremisesSyncEnabled)"

            # Remove user from group if requested
            if ($RemoveUsers) {
                Remove-MgGroupMemberByRef -GroupId $GroupId -DirectoryObjectId $user.Id -ErrorAction Stop
                Write-Host "REMOVED from group"
                $removedUsers++
            }
        }
    }
    catch {
        Write-Warning "Failed to process User ID $($user.Id): $($_.Exception.Message)"
    }
}

# Summary
Write-Host "-----------------"
Write-Host "SUMMARY:"
Write-Host "-----------------"
Write-Host "Total group users processed: $totalUsers"
Write-Host "Cloud users identified: $cloudUsers"
if ($RemoveUsers) {
    Write-Host "Cloud users successfully removed: $removedUsers"
}

if ($cloudUsers -eq 0) {
    Write-Host "No cloud users found in this group."
}

Write-Host "`nScript completed."
```

This script is being provided as an example and should not be considered as official guidance on how to identify and remove cloud users from group memberships.

## Scope a group for SOA operations within an Administrative Unit

To scope a group for Source of Authority operations within an Administrative Unit, do the following steps:

1. Create a unit to use as the scope for the group. For steps on creating a unit, see: [Create an administrative unit](../role-based-access-control/admin-units-manage#create-an-administrative-unit).
2. Add the group as a Hybrid Identity Administrator within the scope. [![Screenshot of assigning a hybrid admin role to an Administrative unit scope.](media/how-to-user-source-of-authority-configure/assign-scope-role.png)](media/how-to-user-source-of-authority-configure/assign-scope-role.png#lightbox)
3. Add the group to the unit. For information on this, see: [Add users, groups, or devices to an administrative unit](../role-based-access-control/admin-units-members-add).
4. Transfer the SOA of a group within the scope of the unit. For a guide on transferring the SOA of groups, see: [Convert SOA for a test group](how-to-group-source-of-authority-configure#convert-soa-for-a-test-group).