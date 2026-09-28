---
layout: Conceptual
title: Scoped synchronization using PowerShell for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/powershell-scoped-synchronization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to use Microsoft Graph PowerShell to configure scoped synchronization from Microsoft Entra ID to a Microsoft Entra Domain Services managed domain
ms.topic: how-to
ms.date: 2025-05-22T00:00:00.0000000Z
ms.reviewer: wanjikumugo
ms.custom: has-azure-ad-ps-ref, devx-track-azurepowershell, azure-ad-ref-level-one-done
locale: en-us
document_id: f1074050-fc02-0063-613e-5745ef95f2bc
document_version_independent_id: 726aecc7-0dd9-e0cc-9ad8-64900ed048b0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/powershell-scoped-synchronization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/powershell-scoped-synchronization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/powershell-scoped-synchronization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ed14edcc-3114-9e3a-cb3d-f50c6ca573f2
---

# Scoped synchronization using PowerShell for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

To provide authentication services, Microsoft Entra Domain Services synchronizes users and groups from Microsoft Entra ID. In a hybrid environment, users and groups from an on-premises Active Directory Domain Services (AD DS) environment can be first synchronized to Microsoft Entra ID using Microsoft Entra Connect, and then synchronized to Domain Services.

By default, all users and groups from a Microsoft Entra directory are synchronized to a Domain Services managed domain. If you have specific needs, you can instead choose to synchronize only a defined set of users.

This article shows you how to create a managed domain that uses scoped synchronization and then change or disable the set of scoped users using MS Graph PowerShell. You can also [complete these steps using the Microsoft Entra admin center](scoped-synchronization).

## Before you begin

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, complete the tutorial to [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
- You need [Application Administrator](/en-us/azure/active-directory/roles/permissions-reference#application-administrator) and [Groups Administrator](/en-us/azure/active-directory/roles/permissions-reference#groups-administrator) Microsoft Entra roles in your tenant to change the Domain Services synchronization scope.

## Scoped synchronization overview

By default, all users and groups from a Microsoft Entra directory are synchronized to a managed domain. If only a few users need to access the managed domain, you can synchronize only those user accounts. This scoped synchronization is group-based. When you configure group-based scoped synchronization, only the user accounts that belong to the groups you specify are synchronized to the managed domain. Nested groups aren't synchronized, only the specific groups you select.

You can change the synchronization scope before or after you create the managed domain. The scope of synchronization is defined by a service principal with the application identifier 2565bd9d-da50-47d4-8b85-4c97f669dc36. To prevent scope loss, don't delete or change the service principal. If it is accidentally deleted, the synchronization scope can't be recovered.

Keep in mind the following caveats if you change the synchronization scope:

- A full synchronization occurs.
- Objects that are no longer required in the managed domain are deleted. New objects are created in the managed domain.

To learn more about the synchronization process, see [Understand synchronization in Microsoft Entra Domain Services](synchronization).

## PowerShell script for scoped synchronization

To configure scoped synchronization using PowerShell, first save the following script to a file named `Select-GroupsToSync.ps1`.

This script configures Domain Services to synchronize selected groups from Microsoft Entra ID. All user accounts that are part of the specified groups are synchronized to the managed domain.

This script is used in the additional steps in this article.

```powershell
param (
    [Parameter(Position = 0)]
    [String[]]$groupsToAdd
)

Connect-MgGraph -Scopes "Directory.Read.All","AppRoleAssignment.ReadWrite.All"
$sp = Get-MgServicePrincipal -Filter "AppId eq '2565bd9d-da50-47d4-8b85-4c97f669dc36'"
$role = $sp.AppRoles | where-object -FilterScript {$_.DisplayName -eq "User"}

Write-Output "`n****************************************************************************"

Write-Output "Total group-assignments need to be added: $($groupsToAdd.Count)"
$newGroupIds = New-Object 'System.Collections.Generic.HashSet[string]'
foreach ($groupName in $groupsToAdd)
{
    try
    {
        $group = Get-MgGroup -Filter "DisplayName eq '$groupName'"
        $newGroupIds.Add($group.Id)

        Write-Output "Group-Name: $groupName, Id: $($group.Id)"
    }
    catch
    {
        Write-Error "Failed to find group: $groupName. Exception: $($_.Exception)."
    }
}

Write-Output "****************************************************************************`n"
Write-Output "`n****************************************************************************"

$currentAssignments = Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $sp.Id -All:$true
Write-Output "Total current group-assignments: $($currentAssignments.Count), SP-ObjectId: $($sp.Id)"

$currAssignedObjectIds = New-Object 'System.Collections.Generic.HashSet[string]'
foreach ($assignment in $currentAssignments)
{
    Write-Output "Assignment-ObjectId: $($assignment.PrincipalId)"

    if ($newGroupIds.Contains($assignment.PrincipalId) -eq $false)
    {
        Write-Output "This assignment is not needed anymore. Removing it! Assignment-ObjectId: $($assignment.PrincipalId)"
        Remove-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $sp.Id -AppRoleAssignmentId $assignment.Id
    }
    else
    {
        $currAssignedObjectIds.Add($assignment.PrincipalId)
    }
}

Write-Output "****************************************************************************`n"
Write-Output "`n****************************************************************************"

foreach ($id in $newGroupIds)
{
    try
    {
        if ($currAssignedObjectIds.Contains($id) -eq $false)
        {
            Write-Output "Adding new group-assignment. Role-Id: $($role.Id), Group-Object-Id: $id, ResourceId: $($sp.Id)"
            $appRoleAssignment = @{
                "principalId"= $Id
                "resourceId"= $sp.Id
                "appRoleId"= $role.Id
            }
            New-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $sp.Id -BodyParameter $appRoleAssignment 
        }
        else
        {
            Write-Output "Group-ObjectId: $id is already assigned."
        }
    }
    catch
    {
        Write-Error "Exception occurred assigning Object-ID: $id. Exception: $($_.Exception)."
    }
}

Write-Output "****************************************************************************`n"
```

## Enable scoped synchronization

To enable group-based scoped synchronization for a managed domain, complete the following steps:

1. First set *"filteredSync" = "Enabled"* on the Domain Services resource, then update the managed domain.

    A [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) is needed to manage this feature.

    Sign in to your Microsoft Entra tenant using the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands) cmdlet:

    ```powershell
    # Connect to your Entra ID tenant
    Connect-MgGraph -Scopes "Application.ReadWrite.All","Group.ReadWrite.All"
    
    # Retrieve the Microsoft Entra DS resource.
    $DomainServicesResource = Get-AzResource -ResourceType "Microsoft.AAD/DomainServices"
    
    # Enable group-based scoped synchronization.
    $enableScopedSync = @{"filteredSync" = "Enabled"}
    
    # Update the Microsoft Entra DS resource
    Set-AzResource -Id $DomainServicesResource.ResourceId -Properties $enableScopedSync
    ```
2. Now specify the list of groups whose users should be synchronized to the managed domain.

    Run the `Select-GroupsToSync.ps1` script and specify the list of groups to sync. In the following example, the groups to synchronize are *GroupName1* and *GroupName2*.

    Warning

    You must include the *AAD DC Administrators* group in the list of groups for scoped synchronization. If you don't include this group, the managed domain is unusable.

    ```powershell
    .\Select-GroupsToSync.ps1 -groupsToAdd @("AAD DC Administrators", "GroupName1", "GroupName2")
    ```

Changing the scope of synchronization causes the managed domain to resynchronize all data. Objects that are no longer required in the managed domain are deleted, and resynchronization may take a long time to complete.

## Modify scoped synchronization

To modify the list of groups whose users should be synchronized to the managed domain, run `Select-GroupsToSync.ps1` script and specify the new list of groups to sync.

In the following example, the groups to synchronize no longer includes *GroupName2*, and now includes *GroupName3*.

Warning

You must include the *AAD DC Administrators* group in the list of groups for scoped synchronization. If you don't include this group, the managed domain is unusable.

A [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) is needed to manage this feature.

Sign in to your Microsoft Entra tenant using the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands) cmdlet.

```powershell
.\Select-GroupsToSync.ps1 -groupsToAdd @("AAD DC Administrators", "GroupName1", "GroupName3")
```

Changing the scope of synchronization causes the managed domain to resynchronize all data. Objects that are no longer required in the managed domain are deleted, and resynchronization may take a long time to complete.

## Disable scoped synchronization

To disable group-based scoped synchronization for a managed domain, set *"filteredSync" = "Disabled"* on the Domain Services resource, then update the managed domain. When complete, all users and groups are set to synchronize from Microsoft Entra ID.

A [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) is needed to manage this feature.

Sign in to your Microsoft Entra tenant using the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands) cmdlet:

```powershell
# Connect to your Entra ID tenant
Connect-MgGraph -Scopes "Application.ReadWrite.All","Group.ReadWrite.All"

# Retrieve the Microsoft Entra DS resource.
$DomainServicesResource = Get-AzResource -ResourceType "Microsoft.AAD/DomainServices"

# Disable group-based scoped synchronization.
$disableScopedSync = @{"filteredSync" = "Disabled"}

# Update the Microsoft Entra DS resource
Set-AzResource -Id $DomainServicesResource.ResourceId -Properties $disableScopedSync
```

Changing the scope of synchronization causes the managed domain to resynchronize all data. Objects that are no longer required in the managed domain are deleted, and resynchronization may take a long time to complete.