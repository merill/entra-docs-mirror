---
layout: Conceptual
title: Disable user sign-in for application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/disable-user-sign-in-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to prevent users from signing in to an application in Microsoft Entra ID and prevent tokens from being issued.
ms.topic: how-to
ms.date: 2025-03-03T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: it-pro, enterprise-apps, no-azure-ad-ps-ref
ms.collection: M365-identity-device-management
zone_pivot_groups: enterprise-apps-all
locale: en-us
document_id: 7f07ca31-dd65-9b05-186b-429eb48f91f8
document_version_independent_id: 3229b6cb-5833-cc86-ac18-95ce512182ff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/disable-user-sign-in-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/disable-user-sign-in-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/disable-user-sign-in-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 702d5b77-b026-1c6a-91ee-040b4470747a
---

# Disable user sign-in for application - Microsoft Entra ID | Microsoft Learn

There might be situations while configuring or managing an application where you don't want tokens to be issued for an application. Or, you might want to block an application that you don't want your employees to try to access. To block user access to an application, you can disable user sign-in for the application, which prevents all tokens from being issued for that application.

In this article, you learn how to prevent users from signing in to an application in Microsoft Entra ID through both the Microsoft Entra admin center and PowerShell. If you're looking for how to block specific users from accessing an application, use [user or group assignment](assign-user-or-group-access-portal).

Note

The steps in this article disable user sign-in for a single tenant. If you need to globally disable an application across all tenants (for multitenant apps), consider [deactivating the application](deactivate-application-portal) instead, which prevents all token issuance globally.

## Prerequisites

To disable user sign-in, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator
    - owner of the service principal

::: zone pivot="portal"

## Disable user sign-in using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Search for the application you want to disable a user from signing in, and select the application.
4. Select **Properties**.
5. Select **No** for **Enabled for users to sign-in?**.
6. Select **Save**.

::: zone-end

::: zone pivot="entra-powershell"

## Disable user sign-in using Microsoft Entra PowerShell

You might know the AppId of an app that doesn't appear on the Enterprise apps list. For example, if you delete the app or the service principal isn't yet created because Microsoft preauthorizes it. You can manually create the service principal for the app and then disable it by using the following Microsoft Entra PowerShell cmdlet.

Ensure you install the Microsoft Entra PowerShell module. In case you're prompted to install a NuGet module or the new Microsoft Entra PowerShell V2 module, type Y and press ENTER. You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```PowerShell
# Connect to Microsoft Entra PowerShell
Connect-Entra -scopes "Application.ReadWrite.All"

# The AppId of the service principal to be disabled
$appId = "{AppId}"

# Disable the service principal
$servicePrincipal = Get-EntraServicePrincipal -Filter "appId eq '$appId'"
Set-EntraServicePrincipal -ObjectId $servicePrincipal.ObjectId -AccountEnabled $false
```

::: zone-end

::: zone pivot="ms-powershell"

## Disable user sign-in using Microsoft Graph PowerShell

You might know the AppId of an app that doesn't appear on the Enterprise apps list. For example, if you delete the app or the service principal isn't yet created due to the app because Microsoft preauthorizes it. You can manually create the service principal for the app and then disable it by using the following Microsoft Graph PowerShell cmdlet.

Ensure you install the Microsoft Graph module (use the command `Install-Module Microsoft.Graph`). You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```powershell
# Connect to Microsoft Graph PowerShell
Connect-MgGraph -Scopes "Application.ReadWrite.All"

# Get the AppId of the service principal to be disabled  
$appId = "{AppId}"  
$servicePrincipal = Get-MgServicePrincipal -Filter "appId eq '$appId'"  

# Disable the service principal
Update-MgServicePrincipal -ServicePrincipalId $servicePrincipal.Id -AccountEnabled:$false 
```

::: zone-end

::: zone pivot="ms-graph"

## Disable user sign-in using Microsoft Graph API

You might know the AppId of an app that doesn't appear on the Enterprise apps list. For example, if you delete the app or the service principal isn't yet created due to the app because Microsoft preauthorizes it. You can manually create the service principal for the app and then disable it by using the following Microsoft Graph call.

To disable sign-in to an application, sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

You need to consent to the `Application.ReadWrite.All` permission.

Run the following query to disable user sign-in to an application.

```http
PATCH https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444

Content-type: application/json

{
    "accountEnabled": false
}
```

::: zone-end