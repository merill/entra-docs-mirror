---
layout: Conceptual
title: Bulk operations service limitations - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/bulk-operations-service-limitations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about Microsoft Entra bulk operations related to users, groups, and devices in the Microsoft Entra admin portal could time out and fail on large tenants.
ms.topic: how-to
ms.date: 2025-12-05T00:00:00.0000000Z
ms.reviewer: krbain
ms.custom: it-pro
locale: en-us
document_id: 6b163e51-c881-f713-727d-976a629483ba
document_version_independent_id: 6b163e51-c881-f713-727d-976a629483ba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/bulk-operations-service-limitations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/bulk-operations-service-limitations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/bulk-operations-service-limitations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 19b0fb5b-b8dc-5b5e-99e1-74e11bed8990
---

# Bulk operations service limitations - Microsoft Entra | Microsoft Learn

## Overview

Bulk operations in Microsoft Entra ID enable you to perform actions on multiple entities, such as users, groups, and devices, at once. These actions can include creating, deleting, or updating multiple records in a single operation. Bulk operations can greatly streamline administrative tasks and improve efficiency.

Bulk operations in the Microsoft Entra admin portal could time out and fail on large tenants. This limitation is a known issue due to scaling limitations.

Tip

A new bulk operations experience is now available in preview that provides enhanced performance and removes scaling limitations for large tenants. For more information, see [Bulk operations in Microsoft Entra ID (Preview)](bulk-operations).

Note

When performing bulk operations, such as import or create, you might encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, split the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, you're essentially limiting the data returned by the bulk operation.

## Bulk operations workaround

A workaround for this issue is to use PowerShell to make direct Microsoft Graph API calls. For bulk user and group download failures, we recommend using the PowerShell cmdlets `GET-MgGroup -All` and `GET-MgUser -All`.

The following PowerShell code examples are for bulk operations related to:

- Users
- Groups
- Devices

## Users

The following sections describe limitations for user bulk operations.

### Download all users

```azurepowershell
# Import the Microsoft Graph module 
Import-Module Microsoft.Graph 

# Authenticate to Microsoft Graph (you may need to provide your credentials) 
Connect-MgGraph -Scopes "User.Read.All" 

# Get all users using Get-MgUser 
$users = Get-MgUser -All -ConsistencyLevel eventual -Property Id, DisplayName, UserPrincipalName,UserType,OnPremisesSyncEnabled,CompanyName,CreationType 

# Specify the output CSV file path 
$outputCsvPath = "C:\\Users\\YourUsername\\Documents\\Users.csv"  

# Create a custom object to store user data 
$userData = @() 

# Loop through each user and collect relevant data 
foreach ($user in $users) { 
    $userObject = [PSCustomObject]@{ 
        Id = $user.Id 
        DisplayName = $user.DisplayName 
        UserPrincipalName = $user.UserPrincipalName 
        UserType = $user.UserType 
        OnPremisesSyncEnabled = $user.OnPremisesSyncEnabled 
        CompanyName = $user.CompanyName 
        CreationType = $user.CreationType 
    } 
    $userData += $userObject 
} 

# Export user data to a CSV file 
$userData | Export-Csv -Path $outputCsvPath -NoTypeInformation 

# Disconnect from Microsoft Graph 
Disconnect-MgGraph 

Write-Host "User data exported to $outputCsvPath" 
```

### Create users

```azurepowershell
# Import the Microsoft Graph module 
Import-Module Microsoft.Graph 

# Authenticate to Microsoft Graph (you may need to provide your credentials) 
Connect-MgGraph -Scopes "User.ReadWrite.All" 

# Specify the path to the CSV file containing user data 
$csvFilePath = "C:\\Path\\To\\Your\\Users.csv" 

# Read the CSV file (adjust the column names as needed) 
$usersData = Import-Csv -Path $csvFilePath 

# Loop through each row in the CSV and create users \
foreach ($userRow in $usersData) { 
    $userParams = @{ 
        DisplayName = $userRow.'Name [displayName] Required' 
        UserPrincipalName = $userRow.'User name [userPrincipalName] Required' 
        PasswordProfile = @{ 
            Password = $userRow.'Initial password [passwordProfile] Required' 
        } 
        AccountEnabled = $true 
        MailNickName = $userRow.mailNickName 
    } 
    try { 
        New-MgUser @userParams 
        Write-Host "User $($userRow.UserPrincipalName) created successfully." 
    } catch { 
        Write-Host "Error creating user $($userRow.UserPrincipalName): $($_.Exception.Message)" 
    } 
} 

# Disconnect from Microsoft Graph 
Disconnect-MgGraph 

Write-Host "Bulk user creation completed." 
```

Note

Make sure your CSV file contains the necessary columns (for example, `DisplayName`, `UserPrincipalName`). Also, adjust the script to match the actual column names in your CSV file.

### Delete users

```azurepowershell
# Import the Microsoft Graph module 
Import-Module Microsoft.Graph 

# Authenticate to Microsoft Graph (you may need to provide your credentials) 
Connect-MgGraph -Scopes "User.ReadWrite.All" 

# Specify the path to the CSV file containing user data 
$csvFilePath = "C:\\Path\\To\\Your\\Users.csv" 

# Read the CSV file (adjust the column names as needed) 
$usersData = Import-Csv -Path $csvFilePath 

# Loop through each row in the CSV and delete users 
foreach ($userRow in $usersData) { 
    try { 
        Remove-MgUser -UserId $userRow.UserPrincipalName -Confirm:$false 
        Write-Host "User $($userRow.UserPrincipalName) deleted successfully." 
    } catch { 
        Write-Host "Error deleting user $($userRow.UserPrincipalName): $($_.Exception.Message)" 
    } 
} 

# Disconnect from Microsoft Graph 
Disconnect-MgGraph 

Write-Host "Bulk user deletion completed." 
```

Note

Make sure your CSV file contains the necessary columns (for example, `UserPrincipalName`). Also, adjust the script to match the actual column names in your CSV file.

## Groups

The following sections describe limitations for group bulk operations.

### Bulk download all groups

```azurepowershell
Import-Module Microsoft.Graph.Groups 

 # Authenticate to Microsoft Graph (you may need to provide your credentials) 
 Connect-MgGraph -Scopes "Group.Read.All" 

 # Get the group members 
 $groups = Get-MgGroup -All | Select displayName, Id, groupTypes,mail 

 # Create a custom object to store group data 
$groupData = @() 

# Loop through each group and collect relevant data 
foreach ($group in $groups) { 
    if ($group.groupTypes -contains "Unified"){$groupType = "Microsoft 365"} 
    else {$groupType = "Security"} 
    if ($group.groupTypes -contains "DynamicMembership"){$membershipType = "Dynamic"} 
    else {$membershipType = "Assigned"} 
    $groupObject = [PSCustomObject]@{ 
        Id = $group.Id 
        DisplayName = $group.displayName 
        Mail = $group.mail 
        GroupType = $groupType 
        MembershipType = $membershipType 
    }   
    $groupData += $groupObject 
} 

 # Specify the output CSV file path 
 $outputCsvPath = "C:\\Users\\<YourUsername>\\Documents\\Groups.csv" 

 $groupData| Export-Csv -Path $outputCsvPath -NoTypeInformation 
 
 Write-Host "Group members exported to $outputCsvPath" 
```

### Bulk download members of a group

```azurepowershell
Import-Module Microsoft.Graph.Groups 

 # Authenticate to Microsoft Graph (you may need to provide your credentials) 
 Connect-MgGraph -Scopes "Group.Read.All,GroupMember.Read.All" 

 # Set the group ID of the group whose members you want to download 
 $groupId = "your_group_id" 

 # Get the group members 
 $members = Get-MgGroupMember -GroupId $groupId -All | select * -ExpandProperty additionalProperties | Select-Object @( 
                'id'     
                @{  Name       = 'userPrincipalName' 
                    Expression = { $_.AdditionalProperties["userPrincipalName"] } 
                } 
                @{  Name = 'displayName' 
                Expression = { $_.AdditionalProperties["displayName"] } 
                } 
            ) 

 # Specify the output CSV file path 
 $outputCsvPath = "C:\\Users\\YourUserName\\Documents\\GroupMembers.csv" 

 $members| Export-Csv -Path $outputCsvPath -NoTypeInformation 

# Disconnect from Microsoft Graph 
Disconnect-MgGraph 

 Write-Host "Group members exported to $outputCsvPath"  
```

### Add members in bulk

```azurepowershell
Import-Module Microsoft.Graph.Groups 

 # Authenticate to Microsoft Graph (you may need to provide your credentials) 
 Connect-MgGraph -Scopes "GroupMember.ReadWrite.All" 

# Import the CSV file 
$members = Import-Csv -Path "C:\path\to\your\file.csv" 

# Define the Group ID 
$groupId = "your-group-id" 

# Iterate over each member and add them to the group 
foreach ($member in $members) { 
    try{ 
        New-MgGroupMember -GroupId $groupId -DirectoryObjectId $member.memberObjectId 
  	 Write-Host "Added $($member.memberObjectId) to the group."  
    } 
    Catch{ 
        Write-Host "Error adding member $($member.memberObjectId):$($_.Exception.Message)" 
    } 
} 

# Disconnect from Microsoft Graph 
Disconnect-MgGraph 
```

### Remove members in bulk

```azurepowershell
Import-Module Microsoft.Graph.Groups 

 # Authenticate to Microsoft Graph (you may need to provide your credentials) 
 Connect-MgGraph -Scopes "GroupMember.ReadWrite.All" 

# Import the CSV file 
$members = Import-Csv -Path "C:\path\to\your\file.csv" 

# Define the Group ID 
$groupId = "your-group-id" 

# Iterate over each member and remove them from the group
foreach ($member in $members) { 
    try{ 
        Remove-MgGroupMemberByRef -GroupId $groupId -DirectoryObjectId $member.memberObjectId \
        Write-Host "Removed $($member.memberObjectId) from the group." 
    } 
    Catch{ 
        Write-Host "Error removing member $($member.memberObjectId):$($_.Exception.Message)" 
    } 
} 

# Disconnect from Microsoft Graph 
Disconnect-MgGraph 
```

## Devices

The following sections describe limitations for device bulk operations.

### Bulk download all devices

```azurepowershell
Import-Module Microsoft.Graph 

 # Authenticate to Microsoft Graph (you may need to provide your credentials) 
 Connect-MgGraph -Scopes "Device.Read.All" 

 # Get all devices  
 $devices = Get-MgDevice -All |select displayName,deviceId,operatingSystem,operatingSystemVersion,isManaged,isCompliant,mdmAppId,registeredOwners,TrustType 

 # Specify the output CSV file path 
 $outputCsvPath = "C:\\Users\\YourUserName\\Documents\\Devices.csv" 

 $devices| Export-Csv -Path $outputCsvPath -NoTypeInformation 

 Write-Host "Devices exported to $outputCsvPath"  
```