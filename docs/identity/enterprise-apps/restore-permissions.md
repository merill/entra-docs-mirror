---
layout: Conceptual
title: Restore revoked permissions granted to applications in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/restore-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to review and restore revoked permissions for an application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2023-07-05T00:00:00.0000000Z
ms.reviewer: phsignor, jawoods
ms.collection: M365-identity-device-management
zone_pivot_groups: delegated-app-permissions
ms.custom: enterprise-apps
locale: en-us
document_id: 08eae9d8-7818-6bac-c6a1-5cd3bf5c456e
document_version_independent_id: e5bf8edc-023d-9201-1e77-7cde5d106e7d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/restore-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/restore-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/restore-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 479cd606-27e2-da3d-7898-d8a95ec8726a
---

# Restore revoked permissions granted to applications in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to restore previously revoked permissions that were granted to an application. You can restore permissions for an application that was granted permissions to access your organization's data. You can also restore permissions for an application that was granted permissions to act as a user.

Currently, restoring permissions is only possible through Microsoft Graph PowerShell and Microsoft Graph API calls. You can't restore permissions through the Microsoft Entra admin center. In this article, you learn how to restore permissions using Microsoft Graph PowerShell.

## Prerequisites

To restore previously revoked permissions for an application, you need:

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, Application Administrator.
- A Service principal owner who isn't an administrator is able to invalidate refresh tokens.

## Restore revoked permissions for an application

You can try different methods for restoring permissions:

- Use the **Grant admin consent** button on the **Permissions** page for the app to apply consent again. This consent applies the set of permissions that the app's developer originally requested in the app manifest.

Note

Regranting admin consent will remove any granted permissions that are not part of the default set configured by the developer.

- If you know the specific permission that was revoked, you can grant it again manually using [PowerShell](/en-us/powershell/microsoftgraph/tutorial-grant-delegated-api-permissions?view=graph-powershell-1.0&amp;preserve-view=true) or the [Microsoft Graph API](/en-us/graph/permissions-grant-via-msgraph?tabs=http&amp;pivots=grant-delegated-permissions).
- If you don't know the revoked permissions, you can use the scripts provided in this article to detect and restore revoked permissions.

First, set the servicePrincipalId value in the script to the ID value for the enterprise app whose permissions you want to restore. This ID is also called the `object ID` in the Microsoft Entra admin center **Enterprise applications** page.

Then, run each script with `$ForceGrantUpdate = $false` in order to see a list of delegated or app-only permissions that maybe have been removed. Even if the permissions have already been restored, revoke events from your audit logs may still appear in the script results.

Leave `$ForceGrantUpdate` set to `$true` if you want the script to attempt to restore any revoked permissions it detects. The scripts ask for confirmation, but don't ask for individual approval for each permission that it restores.

Be cautious when granting permissions to apps. To learn more on how to evaluate permissions, see [Evaluate permissions](manage-consent-requests#evaluate-a-request-for-tenant-wide-admin-consent).

::: zone pivot="delegated-perms"

### Restore delegated permissions

```powershell
# WARNING: Setting $ForceGrantUpdate to true will modify permission grants without
# prompting for confirmation. This can result in unintended changes to your
# application's security settings. Use with caution!
$ForceGrantUpdate = $false

# Set the start and end dates for the audit log search
# If setting date use yyyy-MM-dd format
# endDate is set to tomorrow to include today's audit logs
$startDate = (Get-Date).AddDays(-7).ToString('yyyy-MM-dd')
$endDate = (Get-Date).AddDays(1).ToString('yyyy-MM-dd')

# Set the service principal ID
$servicePrincipalId = "aaaaaaaa-bbbb-cccc-1111-222222222222"

Write-Host "Searching for audit logs between $startDate and $endDate" -ForegroundColor Green
Write-Host "Searching for audit logs for service principal $servicePrincipalId" -ForegroundColor Green

if ($ForceGrantUpdate -eq $true) {
    Write-Host "WARNING: ForceGrantUpdate is set to true. This will modify permission grants without prompting for confirmation. This can result in unintended changes to your application's security settings. Use with caution!" -ForegroundColor Red
    $continue = Read-Host "Do you want to continue? (Y/N)"
    if ($continue -eq "Y" -or $continue -eq "y") {
        Write-Host "Continuing..."
    } else {
        Write-Host "Exiting..."
        exit
    }
}

# Connect to MS Graph
Connect-MgGraph -Scopes "AuditLog.Read.All","DelegatedPermissionGrant.ReadWrite.All" -ErrorAction Stop | Out-Null

# Create a hashtable to store the OAuth2PermissionGrants
$oAuth2PermissionGrants = @{}

function Merge-Scopes($oldScopes, $newScopes) {
    $oldScopes = $oldScopes.Trim() -split '\s+'
    $newScopes = $newScopes.Trim() -split '\s+'
    $mergedScopesArray = $oldScopes + $newScopes | Select-Object -Unique
    $mergedScopes = $mergedScopesArray -join ' '
    return $mergedScopes.Trim()
}

# Function to merge scopes if multiple OAuth2PermissionGrants are found in the audit logs
function Add-Scopes($resourceId, $newScopes) {
    if($oAuth2PermissionGrants.ContainsKey($resourceId)) {
        $oldScopes = $oAuth2PermissionGrants[$resourceId]
        $oAuth2PermissionGrants[$resourceId] = Merge-Scopes $oldScopes $newScopes
    }
    else {
        $oAuth2PermissionGrants[$resourceId] = $newScopes
    }
}

function Get-ScopeDifference ($generatedScope, $currentScope) {
    $generatedScopeArray = $generatedScope.Trim() -split '\s+'
    $currentScopeArray = $currentScope.Trim() -split '\s+'
    $difference = $generatedScopeArray | Where-Object { $_ -notin $currentScopeArray }
    $difference = $difference -join ' '
    return $difference.Trim()
}

# Set the filter for the audit log search
$filterOAuth2PermissionGrant = "activityDateTime ge $startDate and activityDateTime le $endDate" +
    " and Result eq 'success'" +
    " and ActivityDisplayName eq 'Remove delegated permission grant'" +
    " and targetResources/any(x: x/id eq '$servicePrincipalId')"
try {
    # Retrieve the audit logs for removed OAuth2PermissionGrants
    $oAuth2PermissionGrantsAuditLogs = Get-MgAuditLogDirectoryAudit -Filter $filterOAuth2PermissionGrant -All -ErrorAction Stop
}
catch {
    Disconnect-MgGraph | Out-Null
    throw $_
}

# Remove User Delegated Permission Grants
$oAuth2PermissionGrantsAuditLogs = $oAuth2PermissionGrantsAuditLogs | Where-Object {
    -not ($_.TargetResources.ModifiedProperties.OldValue -eq '"Principal"')
}

# Merge duplicate OAuth2PermissionGrants from AuditLogs using Add-Scopes
foreach ($auditLog in $oAuth2PermissionGrantsAuditLogs) {
    $resourceId = $auditLog.TargetResources[0].Id
    # We only want to process OAuth2PermissionGrant Audit Logs where $servicePrincipalId is the clientId not the resourceId
    if ($resourceId -eq $servicePrincipalId) {
        continue
    }
    $oldScope = $auditLog.TargetResources[0].ModifiedProperties | Where-Object { $_.DisplayName -eq "DelegatedPermissionGrant.Scope" } | Select-Object -ExpandProperty OldValue
    if ($oldScope -eq $null) {
        $oldScope = ""
    }
    $oldScope = $oldScope.Replace('"', '')
    $newScope = $auditLog.TargetResources[0].ModifiedProperties | Where-Object { $_.DisplayName -eq "DelegatedPermissionGrant.Scope" } | Select-Object -ExpandProperty NewValue
    if ($newScope -eq $null) {
        $newScope = ""
    }
    $newScope = $newScope.Replace('"', '')
    $scope = Merge-Scopes $oldScope $newScope
    Add-Scopes $resourceId $scope
}

$permissionCount = 0
foreach ($resourceId in $oAuth2PermissionGrants.keys) {
    $scope = $oAuth2PermissionGrants[$resourceId]
    $params = @{
        clientId = $servicePrincipalId
        consentType = "AllPrincipals"
        resourceId = $resourceId
        scope = $scope
    }

    try {
        $currentOAuth2PermissionGrant = Get-MgOauth2PermissionGrant -Filter "clientId eq '$servicePrincipalId' and consentType eq 'AllPrincipals' and resourceId eq '$resourceId'" -ErrorAction Stop
        $action = "Creating"
        if ($currentOAuth2PermissionGrant -ne $null) {
            $action = "Updating"
        }
        Write-Host "--------------------------"
        if ($ForceGrantUpdate -eq $true) {
            Write-Host "$action OAuth2PermissionGrant with the following parameters:"
        } else {
            Write-Host "Potentially removed OAuth2PermissionGrant scopes with the following parameters:"
        }
        Write-Host "    clientId: $($params.clientId)"
        Write-Host "    consentType: $($params.consentType)"
        Write-Host "    resourceId: $($params.resourceId)"
        if ($currentOAuth2PermissionGrant -ne $null) {
            $scopeDifference = Get-ScopeDifference $scope $currentOAuth2PermissionGrant.Scope
            if ($scopeDifference -eq "") {
                Write-Host "OAuth2PermissionGrant already exists with the same scope" -ForegroundColor Yellow
                if ($ForceGrantUpdate -eq $true) {
                    Write-Host "Skipping Update" -ForegroundColor Yellow
                }
                continue
            }
            else {
                Write-Host "    scope diff: '$scopeDifference'"
            }
        }
        else {
            Write-Host "    scope: '$($params.scope)'"
        }
        if ($ForceGrantUpdate -eq $true -and $currentOAuth2PermissionGrant -eq $null) {
            New-MgOauth2PermissionGrant -BodyParameter $params -ErrorAction Stop | Out-Null
            Write-Host "OAuth2PermissionGrant was created successfully" -ForegroundColor Green
        }
        if ($ForceGrantUpdate -eq $true -and $currentOAuth2PermissionGrant -ne $null) {
            Write-Host "    Current Scope: '$($currentOAuth2PermissionGrant.scope)'" -ForegroundColor Yellow
            Write-Host "    Merging with scopes from audit logs" -ForegroundColor Yellow
            $params.scope = Merge-Scopes $currentOAuth2PermissionGrant.scope $params.scope
            Write-Host "    New Scope: '$($params.scope)'" -ForegroundColor Yellow
            Update-MgOauth2PermissionGrant -OAuth2PermissionGrantId $currentOAuth2PermissionGrant.id -BodyParameter $params -ErrorAction Stop | Out-Null
            Write-Host "OAuth2PermissionGrant was updated successfully" -ForegroundColor Green
        }
        $permissionCount++
    }
    catch {
        Disconnect-MgGraph | Out-Null
        throw $_
    }
}

Disconnect-MgGraph | Out-Null

if ($ForceGrantUpdate -eq $true) {
    Write-Host "--------------------------"
    Write-Host "$permissionCount OAuth2PermissionGrants were created/updated successfully" -ForegroundColor Green
} else {
    Write-Host "--------------------------"
    Write-Host "$permissionCount OAuth2PermissionGrants were found" -ForegroundColor Green
}

```

::: zone-end

::: zone pivot="app-perms"

### Restore app-only permissions

Note

Granting app-only Microsoft Graph permissions requires the Privileged Role Administrator role.

```powershell
# WARNING: Setting $ForceGrantUpdate to true will modify permission grants without
# prompting for confirmation. This can result in unintended changes to your
# application's security settings. Use with caution!
$ForceGrantUpdate = $false

# Set the start and end dates for the audit log search
# If setting date use yyyy-MM-dd format
# endDate is set to tomorrow to include today's audit logs
$startDate = (Get-Date).AddDays(-7).ToString('yyyy-MM-dd')
$endDate = (Get-Date).AddDays(1).ToString('yyyy-MM-dd')

# Set the service principal ID
$servicePrincipalId = "aaaaaaaa-bbbb-cccc-1111-222222222222"

Write-Host "Searching for audit logs between $startDate and $endDate" -ForegroundColor Green
Write-Host "Searching for audit logs for service principal $servicePrincipalId" -ForegroundColor Green

if ($ForceGrantUpdate -eq $true) {
    Write-Host "WARNING: ForceGrantUpdate is set to true. This will modify permission grants without prompting for confirmation. This can result in unintended changes to your application's security settings. Use with caution!" -ForegroundColor Red
    $continue = Read-Host "Do you want to continue? (Y/N)"
    if ($continue -eq "Y" -or $continue -eq "y") {
        Write-Host "Continuing..."
    } else {
        Write-Host "Exiting..."
        exit
    }
}

# Connect to MS Graph
Connect-MgGraph -Scopes "AuditLog.Read.All","Application.Read.All","AppRoleAssignment.ReadWrite.All" -ErrorAction Stop | Out-Null

# Set the filter for the audit log search
$filterAppRoleAssignment = "activityDateTime ge $startDate and activityDateTime le $endDate" + 
    " and Result eq 'success'" +
    " and ActivityDisplayName eq 'Remove app role assignment from service principal'" +
    " and targetResources/any(x: x/id eq '$servicePrincipalId')"

try {
    # Retrieve the audit logs for removed AppRoleAssignments
    $appRoleAssignmentsAuditLogs = Get-MgAuditLogDirectoryAudit -Filter $filterAppRoleAssignment -All -ErrorAction Stop
}
catch {
    Disconnect-MgGraph | Out-Null
    throw $_
}

$permissionCount = 0
foreach ($auditLog in $appRoleAssignmentsAuditLogs) {
    $resourceId = $auditLog.TargetResources[0].Id
    # We only want to process AppRoleAssignments Audit Logs where $servicePrincipalId is the principalId not the resourceId
    if ($resourceId -eq $servicePrincipalId) {
        continue
    }
    $appRoleId = $auditLog.TargetResources[0].ModifiedProperties | Where-Object { $_.DisplayName -eq "AppRole.Id" } | Select-Object -ExpandProperty OldValue
    $appRoleId = $appRoleId.Replace('"', '')
    $params = @{
        principalId = $servicePrincipalId
        resourceId = $resourceId
        appRoleId = $appRoleId
    }

    try {
        $sp = Get-MgServicePrincipal -ServicePrincipalId $resourceId
        $appRole = $sp.AppRoles | Where-Object { $_.Id -eq $appRoleId }

        Write-Host "--------------------------"
        if ($ForceGrantUpdate -eq $true) {
            Write-Host "Creating AppRoleAssignment with the following parameters:"
        } else {
            Write-Host "Potentially removed AppRoleAssignment with the following parameters:"
        }
        Write-Host "    principalId: $($params.principalId)"
        Write-Host "    resourceId: $($params.resourceId)"
        Write-Host "    appRoleId: $($params.appRoleId)"
        Write-Host "    appRoleValue: $($appRole.Value)"
        Write-Host "    appRoleDisplayName: $($appRole.DisplayName)"
        if ($ForceGrantUpdate -eq $true) {
            New-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $servicePrincipalId -BodyParameter $params -ErrorAction Stop | Out-Null
            Write-Host "AppRoleAssignment was created successfully" -ForegroundColor Green
        }
        $permissionCount++
    }
    catch {
        if ($_.Exception.Message -like "*Permission being assigned already exists on the object*") {
            Write-Host "AppRoleAssignment already exists skipping creation" -ForegroundColor Yellow
        }
        else {
            Disconnect-MgGraph | Out-Null
            throw $_
        }
    }
}

Disconnect-MgGraph | Out-Null

if ($ForceGrantUpdate -eq $true) {
    Write-Host "--------------------------"
    Write-Host "$permissionCount AppRoleAssignments were created successfully" -ForegroundColor Green
} else {
    Write-Host "--------------------------"
    Write-Host "$permissionCount AppRoleAssignments were found" -ForegroundColor Green
}

```

::: zone-end