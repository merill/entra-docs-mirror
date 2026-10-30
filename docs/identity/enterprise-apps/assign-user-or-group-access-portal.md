---
layout: Conceptual
title: Manage users and groups assignment to an application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/assign-user-or-group-access-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to assign and unassign users, and groups, for an app using Microsoft Entra ID for identity management.
ms.topic: how-to
ms.date: 2026-04-01T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps, no-azure-ad-ps-ref
zone_pivot_groups: enterprise-apps-all
locale: en-us
document_id: 163a1f88-c268-18aa-a1e6-89b4a11bfb01
document_version_independent_id: 1136a613-48f8-fb67-39d3-d9abdd351a0f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/assign-user-or-group-access-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/assign-user-or-group-access-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/assign-user-or-group-access-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c5cc1ba9-4b50-60c6-b2f0-5008adddafbc
---

# Manage users and groups assignment to an application - Microsoft Entra ID | Microsoft Learn

This article shows you how to assign users and groups to an enterprise application in Microsoft Entra ID. When you assign a user to an application, the application appears in the user's [My Apps](https://myapps.microsoft.com/) portal for easy access. If the application exposes app roles, you can also assign a specific app role to the user.

When you assign a group to an application, only users in the group have access. The assignment doesn't cascade to nested groups.

Group-based assignment requires Microsoft Entra ID P1 or P2 edition. Nested group memberships aren't currently supported. For more licensing requirements for the features discussed in this article, see the [Microsoft Entra pricing page](https://azure.microsoft.com/pricing/details/active-directory).

For greater control, certain types of enterprise applications can be configured to require user assignment. For more information on requiring user assignment for an app, see [Manage access to an application](what-is-access-management#requiring-user-assignment-for-an-app). Applications that require users to be assigned to the application must have their permissions consented by an administrator, even if the user consent policies for your directory would otherwise allow a user to consent on behalf of themselves.

Prior to integration with Microsoft Entra, your application may already have one or more users. Using the account discovery functionality, you can generate a report of all the users in your application, identify which users have matching accounts in Entra, and which users are local to your application with one click. Learn more about the account discovery functionality [here](../app-provisioning/how-to-account-discovery). This enables you to simplify onboarding to Entra, while also periodically monitoring for unauthorized access.

Note

If you encounter limitations when managing groups through the portal, such as with application access policy groups, consider using alternative methods like PowerShell or Microsoft Graph API.

## Prerequisites

To assign users to an enterprise application, you need:

- A Microsoft Entra account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator
    - User Administrator
    - Owner of the service principal.
- Microsoft Entra ID P1 or P2 for group-based assignment. For more licensing requirements for the features discussed in this article, see the [Microsoft Entra pricing page](https://azure.microsoft.com/pricing/details/active-directory).

::: zone pivot="portal"

## Assign users and groups to an application using the Microsoft Entra admin center

To assign a user or group account to an enterprise application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results.
4. Select **Users and groups**, and then select **Add user/group**.

    ![Assign user account to an application in your Microsoft Entra tenant.](media/add-application-portal-assign-users/assign-user.png)
5. On the **Add Assignment** pane, select **None Selected** under **Users and groups**.
6. Search for and select the user or group that you want to assign to the application. For example, `contosouser1@contoso.com` or `contosoteam1@contoso.com`.
7. Select **Select**.
8. Under **Select a role**, select the role that you want to assign to the user or group. If you haven't defined any roles yet, the default role is **Default Access**.
9. On the **Add Assignment** pane, select **Assign** to assign the user or group to the application.

## Unassign users, and groups, from an application

1. Follow the steps on the Assign users, and groups, to an application section to navigate to the **Users and groups** pane.
2. Search for and select the user or group that you want to unassign from the application.
3. Select **Remove** to unassign the user or group from the application.

::: zone-end

::: zone pivot="entra-powershell"

## Assign users and groups to an application using Microsoft Entra PowerShell

1. Sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Use the following script to assign a user to an application:

    ```powershell
    connect-entra -scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"
    # Assign the values to the variables
    $username = "<Your user's UPN>"
    $app_name = "<Your App's display name>"
    $app_role_name = "<App role display name>"
    
    # Get the user to assign, and the service principal for the app to assign to
    $user = Get-EntraUser -ObjectId "$username"
    $sp = Get-EntraServicePrincipal -Filter "displayName eq '$app_name'"
    $appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }
    
    # Assign the user to the app role
    New-EntraUserAppRoleAssignment -ObjectId $user.ObjectId -PrincipalId $user.ObjectId -ResourceId $sp.ObjectId -Id $appRole.Id
    ```

### Example

This example assigns the user Britta Simon to the Microsoft Workplace Analytics application using PowerShell.

1. In PowerShell, assign the corresponding values to the variables `$username`, `$app_name`, and `$app_role_name`.

    ```powershell
    connect-entra -scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"
    $username = "britta.simon@contoso.com"
    $app_name = "Workplace Analytics"
    ```
2. In this example, we don't know what is the exact name of the application role we want to assign to Britta Simon. Run the following commands to get the user (`$user`) and the service principal (`$sp`) using the user UPN and the service principal display names.

    ```powershell
    $user = Get-EntraUser -ObjectId "$username"
    $sp = Get-EntraServicePrincipal -Filter "displayName eq '$app_name'"
    ```
3. Run the following command to find the app roles exposed by the service principal

    ```powershell
    $appRoles = $sp.AppRoles
    # Display the app roles
    $appRoles | ForEach-Object {
        Write-Output "AppRole: $($_.DisplayName) - ID: $($_.Id)"
    }
    ```

    Note

    The default AppRole ID is `00000000-0000-0000-0000-000000000000`. This role is assigned when no specific AppRole is defined for a service principal.
4. Assign the AppRole name to the `$app_role_name` variable. In this example, we want to assign Britta Simon the Analyst (Limited access) Role.

    ```powershell
    $app_role_name = "Analyst (Limited access)"
    $appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }
    ```
5. Run the following command to assign the user to the app role.

    ```powershell
    New-EntraUserAppRoleAssignment -ObjectId $user.ObjectId -PrincipalId $user.ObjectId -ResourceId $sp.ObjectId -Id $appRole.Id
    ```

To assign a group to an enterprise app, replace `Get-EntraUser` with `Get-EntraGroup` and replace `New-EntraUserAppRoleAssignment` with `New-EntraGroupAppRoleAssignment`.

## Unassign users and groups from an application using Microsoft Entra PowerShell

1. Open an elevated Windows PowerShell command prompt.
2. Sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
3. Use the following script to remove a user and role from an application.

    ```powershell
    connect-entra -scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"
    # Store the proper parameters
    $user = Get-Entrauser -ObjectId "<objectId>"
    $spo = Get-EntraServicePrincipal -ObjectId "<objectId>"
    
    #Get the ID of role assignment
    $assignments = Get-EntraServicePrincipalAppRoleAssignedTo -ObjectId $spo.ObjectId | Where {$_.PrincipalDisplayName -eq $user.DisplayName}
    
    #if you run the following, it will show you what is assigned what
    $assignments | Select *
    
    #To remove the App role assignment run the following command.
    Remove-EntraServicePrincipalAppRoleAssignment -ObjectId $spo.ObjectId -AppRoleAssignmentId $assignments.ObjectId
    ```

## Remove all users who are assigned to the application using Microsoft Entra PowerShell

1. Open an elevated Windows PowerShell command prompt.

Use the following script to remove all users and groups assigned to the application.

```powershell
connect-entra -scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"
#Retrieve the service principal object ID.
$app_name = "<Your App's display name>"
$sp = Get-EntraServicePrincipal -Filter "displayName eq '$app_name'"

# Get Microsoft Entra App role assignments using objectId of the Service Principal
$assignments = Get-EntraServicePrincipalAppRoleAssignedTo -ObjectId $sp.ObjectId -All

# Remove all users and groups assigned to the application
$assignments | ForEach-Object {
    if ($_.PrincipalType -eq "User") {
        Remove-EntraUserAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.ObjectId
    } elseif ($_.PrincipalType -eq "Group") {
        Remove-EntraGroupAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.ObjectId
    }
}
```

::: zone-end

::: zone pivot="ms-powershell"

## Assign users and groups to an application using Microsoft Graph PowerShell

1. Open an elevated Windows PowerShell command prompt.
2. Run `Connect-MgGraph -Scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"` and sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
3. Use the following script to assign a user to an application:

    ```powershell
    #Assign the values to the variables
    $userId = "<Your user's ID>"
    $app_name = "<Your App's display name>"
    $app_role_name = "<App role display name>"
    $sp = Get-MgServicePrincipal -Filter "displayName eq '$app_name'"
    
    #Get the user, the service principal and appRole.
    $params = @{
    "PrincipalId" =$userId
    "ResourceId" =$sp.Id
    "AppRoleId" =($sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }).Id
    }
    #Assign the user to the AppRole
    New-MgUserAppRoleAssignment -UserId $userId -BodyParameter $params |
        Format-List Id, AppRoleId, CreationTime, PrincipalDisplayName,
        PrincipalId, PrincipalType, ResourceDisplayName, ResourceId
    ```

### Example

This example assigns the user Britta Simon to the Microsoft Workplace Analytics application using Microsoft Graph PowerShell.

1. In PowerShell, assign the corresponding values to the variables `$userId`, `$app_name`, and `$app_role_name`.

    ```powershell
    # Assign the values to the variables
    $userId = "<Britta Simon's user ID>"
    $app_name = "Workplace Analytics"
    ```
2. In this example, we don't know the exact name of the application role we want to assign to Britta Simon. Run the following command to get the service principal ($sp) using the service principal display name.

    ```powershell
    # Get the service principal for the app
    $sp = Get-MgServicePrincipal -Filter "displayName eq '$app_name'"
    ```
3. Run the following command to find the app roles exposed by the service principal.

    ```powershell
    # Get the app roles exposed by the service principal
    $appRoles = $sp.AppRoles
    # Display the app roles
    $appRoles | ForEach-Object {
        Write-Output "AppRole: $($_.DisplayName) - ID: $($_.Id)"
    }
    ```

    Note

    The default AppRole ID is `00000000-0000-0000-0000-000000000000`. This role is assigned when no specific AppRole is defined for a service principal.
4. Assign the role name to the `$app_role_name` variable. In this example, we want to assign Britta Simon the Analyst (Limited access) Role.

    ```powershell
    # Assign the values to the variables
    $app_role_name = "Analyst (Limited access)"
    $appRoleId = ($sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }).Id
    ```
5. Prepare the parameters and run the following command to assign the user to the app role.

    ```powershell
    # Prepare parameters for the role assignment
    $params = @{
        "PrincipalId" = $userId
        "ResourceId" = $sp.Id
        "AppRoleId" = $appRoleId
    }
    
    # Assign the user to the app role
    New-MgUserAppRoleAssignment -UserId $userId -BodyParameter $params |
        Format-List Id, AppRoleId, CreationTime, PrincipalDisplayName,
        PrincipalId, PrincipalType, ResourceDisplayName, ResourceId
    ```

To assign a group to an enterprise app, replace `Get-MgUser` with `Get-MgGroup` and replace `New-MgUserAppRoleAssignment` with `New-MgGroupAppRoleAssignment`.

For more information on how to assign a group to an application role, see the documentation for [New-MgGroupAppRoleAssignment](/en-us/powershell/module/microsoft.graph.applications/new-mggroupapproleassignment).

## Unassign users and groups from an application using Microsoft Graph PowerShell

1. Open an elevated Windows PowerShell command prompt.
2. Run `Connect-MgGraph -Scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"` and sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
3. Get the user and the service principal

    ```powershell
    $user = Get-MgUser -UserId <userid>
    $sp = Get-MgServicePrincipal -ServicePrincipalId <ServicePrincipalId>
    ```
4. Get the ID of the role assignment

    ```powershell
    $assignments = Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $sp.Id | Where {$_.PrincipalDisplayName -eq $user.DisplayName}
    ```
5. Run the following command to show the list of users assigned to the application

    ```powershell
    $assignments | Select *
    ```
6. Run the following command to remove the AppRole assignment.

    ```powershell
    Remove-MgServicePrincipalAppRoleAssignedTo -AppRoleAssignmentId  '<AppRoleAssignment-id>' -ServicePrincipalId $sp.Id
    ```

## Remove all users and groups assigned to the application using Microsoft Graph PowerShell

Run the following command to remove all users and groups assigned to the application.

```powershell
$assignments | ForEach-Object {
    if ($_.PrincipalType -in ("user", "Group")) {
        Remove-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $sp.Id -AppRoleAssignmentId $_.Id  }
}
```

::: zone-end

::: zone pivot="ms-graph"

## Assign users and groups to an application using Microsoft Graph API

1. To assign users and groups to an application, sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

    You need to consent to the following permissions:

    `Application.ReadWrite.All`, and `AppRoleAssignment.ReadWrite.All`.

    To grant an app role assignment, you need three identifiers:

    - `principalId`: The ID of the user or group to which you're assigning the app role.
    - `resourceId`: The ID of the resource servicePrincipal that defines the app role.
    - `appRoleId`: The ID of the appRole (defined on the resource service principal) to assign to a user or group.
2. Get the enterprise application. Filter by `DisplayName`.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals?$filter=displayName eq '{appDisplayName}'
    ```

    Record the following values from the response body:

    - Object ID of the enterprise application
    - AppRole ID that you assign to the user. If the application doesn't expose any roles, the user is assigned the default access role.

    Note

    The default AppRole ID is `00000000-0000-0000-0000-000000000000`. This role is assigned when no specific AppRole is defined for a service principal.
3. Get the user by filtering by the user's principal name. Record the object ID of the user.

    ```http
    GET https://graph.microsoft.com/v1.0/users/{userPrincipalName}
    ```
4. Assign the user to the application.

    ```http
    POST https://graph.microsoft.com/v1.0/servicePrincipals/{resource-servicePrincipal-id}/appRoleAssignedTo
    
    {
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "resourceId": "a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1",
    "appRoleId": "00000000-0000-0000-0000-000000000000"
    }
    ```

    In the example, both the `resource-servicePrincipal-id` and `resourceId` represent the enterprise application.

## Unassign users and groups from an application using Microsoft Graph API

To unassign all users and groups from the application, run the following query.

1. Get the enterprise application. Filter by `displayName`.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals?$filter=displayName eq '{appDisplayName}'
    ```
2. Get the list of `appRoleAssignments` for the application.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/{id}/appRoleAssignedTo
    ```
3. Remove the `appRoleAssignments` by specifying the `appRoleAssignment` ID.

    ```http
    DELETE https://graph.microsoft.com/v1.0/servicePrincipals/{resource-servicePrincipal-id}/appRoleAssignedTo/{appRoleAssignment-id}
    ```

Microsoft Graph Explorer doesn't support batch deletion of app role assignments directly. You need to delete each assignment individually. However, you can automate this process using Microsoft Graph PowerShell to iterate through and remove each assignment

::: zone-end