---
layout: Conceptual
title: Restore a soft deleted enterprise application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/restore-application
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Restore a soft deleted enterprise application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-02-28T00:00:00.0000000Z
ms.reviewer: sureshja
ms.custom: enterprise-apps, no-azure-ad-ps-ref
zone_pivot_groups: enterprise-apps-minus-portal
locale: en-us
document_id: 49f59a37-d380-b534-fd24-995e89b0d7b2
document_version_independent_id: 6ae0b7e9-3673-21b6-709e-0d36024bdf99
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/restore-application.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/restore-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/restore-application.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b26e20e3-ec9b-9ef9-f59e-6678d64cafc2
---

# Restore a soft deleted enterprise application - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to restore a soft deleted enterprise application in your Microsoft Entra tenant. Soft deleted enterprise applications can be restored from the recycle bin within the first 30 days after their deletion. After the 30-day window, the enterprise application is permanently deleted and can't be restored.

If you deleted an [application registration](../../identity-platform/howto-remove-app) in its home tenant through app registrations in the Microsoft Entra admin center, the enterprise application, which is its corresponding service principal also got deleted.

If you restore the deleted application registration through the Microsoft Entra admin center, its corresponding service principal, is also restored. You therefore be able to recover the service principal's previous configurations, except its previous policies such as Conditional Access policies, which aren't restored.

## Prerequisites

To restore an enterprise application, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator
    - owner of the service principal.
- A [soft deleted enterprise application](delete-application-portal) in your tenant.

Take the following steps to recover a recently deleted enterprise application. For more information on frequently asked questions about deletion and recovery of applications, see [Deleting and recovering applications FAQs](delete-recover-faq).

::: zone pivot="entra-powershell"

## View restorable enterprise applications using Microsoft Entra PowerShell

Make sure you're using the [Microsoft Entra PowerShell](/en-us/powershell/entra-powershell/?preserve-view=true&amp;view=entra-powershell) module.

You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

1. Run the following command to view the recently deleted enterprise application.

    ```powershell
    Connect-Entra -Scopes 'Application.Read.All'
    Get-EntraDeletedServicePrincipal
    ```

Replace ID with the object ID of the service principal that you want to restore.

::: zone-end

::: zone pivot="ms-powershell"

## View restorable enterprise applications using Microsoft Graph PowerShell

1. Run `connect-MgGraph -Scopes "Application.ReadWrite.All"`. You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. To view the recently deleted enterprise applications, run the following command.

    ```powershell
    Get-MgDirectoryDeletedItem -DirectoryObjectId <id>
    ```

Replace ID with the object ID of the service principal that you want to restore.

::: zone-end

::: zone pivot="ms-graph"

## View restorable enterprise applications using Microsoft Graph API

View and restore recently deleted enterprise applications using [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer). You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

To get the list of deleted enterprise applications in your tenant, run the following query.

```http
GET https://graph.microsoft.com/v1.0/directory/deletedItems/microsoft.graph.servicePrincipal
```

From the list of deleted service principals generated, record the ID of the enterprise application you want to restore.

Alternatively, if you want to get the specific enterprise application that was deleted, fetch the deleted service principal and filter the results by the client's application ID (appId) property using the following syntax:

`https://graph.microsoft.com/v1.0/directory/deletedItems/microsoft.graph.servicePrincipal?$filter=appId eq '{appId}'`. Once you retrieved the object ID of the deleted service principal, proceed to restore it.

::: zone-end

::: zone pivot="entra-powershell"

## Restore an enterprise app using Microsoft Entra PowerShell

1. To restore the soft-deleted enterprise application, run the following command:

    ```powershell
    Connect-Entra -Scopes 'Application.ReadWrite.All'
    #get the deleted service principal by filtering by the display name.
    $deletedServicePrincipal = Get-EntraDeletedServicePrincipal -Filter "DisplayName eq 'test-App1-Deleted'"
    
    #assign the value returned to a variable and restore the deleted service principal
    $Id = $deletedServicePrincipal.Id
    Restore-EntraDeletedDirectoryObject -Id $deletedServicePrincipal.Id
    ```

::: zone-end

::: zone pivot="ms-powershell"

## Restore an enterprise app using Microsoft Graph PowerShell

1. To restore the enterprise application, run the following command:

    ```powershell
    Restore-MgDirectoryDeletedItem -DirectoryObjectId <id>
    ```

Replace ID with the object ID of the service principal that you want to restore.

::: zone-end

::: zone pivot="ms-graph"

## Restore an enterprise app using Microsoft Graph API

To restore the enterprise application, run the following query:

```http
POST https://graph.microsoft.com/v1.0/directory/deletedItems/{id}/restore
```

Replace ID with the object ID of the service principal that you want to restore.

::: zone-end

Soft-deleted managed identity service principals can be viewed but can't be recovered or permanently deleted by customers.

Warning

Permanently deleting an enterprise application is an irreversible action. Any present configurations on the app are lost. Carefully review the details of the enterprise application to be sure you still want to hard delete it.

::: zone pivot="entra-powershell"

## Permanently delete an enterprise app using Microsoft Entra PowerShell

To permanently delete a soft deleted enterprise application, run the following command:

```powershell
   Connect-Entra -Scopes 'Application.ReadWrite.All'
   #get the deleted service principal by filtering by the display name.
   $deletedServicePrincipal = Get-EntraDeletedServicePrincipal -Filter "DisplayName eq 'test-App1-Deleted'"

   #assign the value returned to a variable and permanently delete the service principal
   $Id = $deletedServicePrincipal.Id
   Remove-EntraDeletedDirectoryObject -Id $deletedServicePrincipal.Id
```

::: zone-end

::: zone pivot="ms-powershell"

## Permanently delete an enterprise app using Microsoft Graph PowerShell

1. To permanently delete the soft deleted enterprise application, run the following command:

    ```powershell
    Remove-MgDirectoryDeletedItem -DirectoryObjectId <id>
    ```

::: zone-end

::: zone pivot="ms-graph"

## Permanently delete an enterprise app using Microsoft Graph API

To permanently delete a soft deleted enterprise application, run the following query in Microsoft Graph explorer.

```http
DELETE https://graph.microsoft.com/v1.0/directory/deletedItems/{object-id}
```

::: zone-end