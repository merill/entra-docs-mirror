---
layout: Conceptual
title: Configure permission classifications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-permission-classifications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to manage delegated permission classifications.
ms.topic: how-to
ms.date: 2025-03-03T00:00:00.0000000Z
ms.reviewer: phsignor, jawoods
ms.custom: no-azure-ad-ps-ref
zone_pivot_groups: enterprise-apps-all
locale: en-us
document_id: 1fa8e462-bbd4-622e-a073-f027406bb303
document_version_independent_id: b1915194-6e8e-8821-e287-9e4e85addf90
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-permission-classifications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-permission-classifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-permission-classifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 66dd5f33-4561-fb05-8cbb-a47c93ce7671
---

# Configure permission classifications - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure permissions classifications in Microsoft Entra ID. Permission classifications allow you to identify the impact that different permissions have based on your organization's policies and risk evaluations. For example, you can use permission classifications in consent policies to identify the set of permissions that users are allowed to consent to.

Three permission classifications are supported: "Low," "Medium" (preview), and "High" (preview). Currently, only delegated permissions that don't require admin consent can be classified.

The minimum permissions needed to do basic sign-in are `openid`, `profile`, `email`, and `offline_access`, which are all delegated permissions on the Microsoft Graph. With these permissions an app can read details of the signed-in user's profile, and can maintain this access even when the user is no longer using the app.

## Prerequisites

To configure permission classifications, you need:

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Application Administrator, or Cloud Application Administrator

## Manage permission classifications

::: zone pivot="portal"

Follow these steps to classify permissions using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Consent and permissions** &gt; **Permission classifications**.
3. Choose the tab for the permission classification you'd like to update.
4. Choose **Add permissions** to classify another permission.
5. Select the API and then select one or more delegated permissions.

In this example, we classify the minimum set of permission required for single sign-on:

![Permission classifications](media/configure-permission-classifications/permission-classifications.png)

::: zone-end

::: zone pivot="entra-powershell"

You can use the latest [Microsoft Entra PowerShell](/en-us/powershell/entra-powershell/?preserve-view=true&amp;view=entra-powershell) to classify permissions. Permission classifications are configured on the **ServicePrincipal** object of the API that publishes the permissions.

Run the following command to connect to Microsoft Entra PowerShell. To consent to the required scopes, sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```powershell
Connect-Entra -scopes "Policy.ReadWrite.PermissionGrant", "Application.Read.All"
```

### List the current permission classifications using Microsoft Entra PowerShell

1. Retrieve the **ServicePrincipal** object for the API. Here we retrieve the ServicePrincipal object for the Microsoft Graph API:

    ```powershell
    $serviceprincipal = Get-EntraServicePrincipal `
        -Filter "servicePrincipalNames/any(n:n eq 'https://graph.microsoft.com')"
    ```
2. Read the delegated permission classifications for the API:

    ```powershell
    Get-EntraServicePrincipalDelegatedPermissionClassification `
        -ServicePrincipalId $serviceprincipal.ObjectId | Format-Table Id, PermissionName, Classification
    ```

### Classify a permission as "Low impact" using Microsoft Entra PowerShell

1. Retrieve the **ServicePrincipal** object for the API. Here we retrieve the ServicePrincipal object for the Microsoft Graph API:

    ```powershell
    $serviceprincipal = Get-EntraServicePrincipal `
        -Filter "servicePrincipalNames/any(n:n eq 'https://graph.microsoft.com')"
    ```
2. Find the delegated permission you would like to classify:

    ```powershell
    $delegatedPermission = $serviceprincipal.oauth2PermissionScopes | Where-Object { $_.Value -eq "User.ReadBasic.All" }
    ```
3. Set the permission classification using the permission name and ID:

    ```powershell
    Add-EntraServicePrincipalDelegatedPermissionClassification `
       -ServicePrincipalId $serviceprincipal.ObjectId `
       -PermissionId $delegatedPermission.Id `
       -PermissionName $delegatedPermission.Value `
       -Classification "low"
    ```

### Remove a delegated permission classification using Microsoft Entra PowerShell

1. Retrieve the **ServicePrincipal** object for the API. Here we retrieve the ServicePrincipal object for the Microsoft Graph API:

    ```powershell
    $serviceprincipal = Get-EntraServicePrincipal `
        -Filter "servicePrincipalNames/any(n:n eq 'https://graph.microsoft.com')"
    ```
2. Find the delegated permission classification you wish to remove:

    ```powershell
    $classifications = Get-EntraServicePrincipalDelegatedPermissionClassification `
        -ServicePrincipalId $serviceprincipal.ObjectId
    $classificationToRemove = $classifications | Where-Object {$_.PermissionName -eq "User.ReadBasic.All"}
    ```
3. Delete the permission classification:

    ```powershell
    Remove-EntraServicePrincipalDelegatedPermissionClassification `
        -ServicePrincipalId $serviceprincipal.ObjectId `
        -Id $classificationToRemove.Id
    ```

::: zone-end

::: zone pivot="ms-powershell"

You can use [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/get-started?preserve-view=true&amp;view=graph-powershell-1.0), to classify permissions. Permission classifications are configured on the **ServicePrincipal** object of the API that publishes the permissions.

Run the following command to connect to Microsoft Graph PowerShell. To consent to the required scopes, sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```powershell
Connect-MgGraph -Scopes "Policy.ReadWrite.PermissionGrant", "Application.Read.All"
```

### List current permission classifications for an API using Microsoft Graph PowerShell

1. Retrieve the servicePrincipal object for the API:

    ```powershell
    $serviceprincipal = Get-MgServicePrincipal -Filter "displayName eq 'Microsoft Graph'" 
    ```
2. Read the delegated permission classifications for the API:

    ```powershell
    Get-MgServicePrincipalDelegatedPermissionClassification -ServicePrincipalId $serviceprincipal.Id 
    ```

### Classify a permission as "Low impact" using Microsoft Graph PowerShell

1. Retrieve the servicePrincipal object for the API:

    ```powershell
    $serviceprincipal = Get-MgServicePrincipal -Filter "displayName eq 'Microsoft Graph'" 
    ```
2. Find the delegated permission you would like to classify:

    ```powershell
    $delegatedPermission = $serviceprincipal.Oauth2PermissionScopes | Where-Object {$_.Value -eq "openid"} 
    ```
3. Set the permission classification:

    ```powershell
    $params = @{ 
       PermissionId = $delegatedPermission.Id 
       PermissionName = $delegatedPermission.Value 
       Classification = "Low"
    } 
    
    New-MgServicePrincipalDelegatedPermissionClassification -ServicePrincipalId $serviceprincipal.Id -BodyParameter $params 
    ```

### Remove a delegated permission classification using Microsoft Graph PowerShell

1. Retrieve the servicePrincipal object for the API:

    ```powershell
    $serviceprincipal = Get-MgServicePrincipal -Filter "displayName eq 'Microsoft Graph'" 
    ```
2. Find the delegated permission classification you wish to remove:

    ```powershell
    $classifications = Get-MgServicePrincipalDelegatedPermissionClassification -ServicePrincipalId $serviceprincipal.Id 
    
    $classificationToRemove = $classifications | Where-Object {$_.PermissionName -eq "openid"}
    ```
3. Delete the permission classification:

```powershell
Remove-MgServicePrincipalDelegatedPermissionClassification -DelegatedPermissionClassificationId $classificationToRemove.Id   -ServicePrincipalId $serviceprincipal.id 
```

::: zone-end

::: zone pivot="ms-graph"

To configure permissions classifications for an enterprise application, sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

You need to consent to the `Policy.ReadWrite.PermissionGrant` and `Application.Read.All` permissions.

Run the following queries on Microsoft Graph explorer to add a delegated permissions classification for an application.

### List current permission classifications for an API using Microsoft Graph API

List current permission classifications for an API using the following Microsoft Graph API call.

```http
GET https://graph.microsoft.com/v1.0/servicePrincipals(appId='00000003-0000-0000-c000-000000000000')/delegatedPermissionClassifications
```

### Classify a permission as "Low impact" using Microsoft Graph API

In the following example, we classify the permission as "low impact."

Add a delegated permission classification for an API using the following Microsoft Graph API call.

```http
POST https://graph.microsoft.com/v1.0/servicePrincipals(appId='00000003-0000-0000-c000-000000000000')/delegatedPermissionClassifications
Content-type: application/json

{
   "permissionId": "b4e74841-8e56-480b-be8b-910348b18b4c",
   "classification": "low"
}
```

### Remove a delegated permission classification using Microsoft Graph API

Run the following query on Microsoft Graph explorer to remove a delegated permissions classification for an API.

```http
DELETE https://graph.microsoft.com/v1.0/servicePrincipals(appId='00000003-0000-0000-c000-000000000000')/delegatedPermissionClassifications/QUjntFaOC0i-i5EDSLGLTAE
```

::: zone-end