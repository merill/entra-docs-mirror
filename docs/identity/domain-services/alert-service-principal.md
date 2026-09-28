---
layout: Conceptual
title: Resolve service principal alerts in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/alert-service-principal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot service principal configuration alerts for Microsoft Entra Domain Services
ms.assetid: f168870c-b43a-4dd6-a13f-5cfadc5edf2c
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.topic: troubleshooting
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 18099591-fa99-1845-8386-b28adf7d702e
document_version_independent_id: 58ebfe11-e88f-59e9-671a-3a771a8dd950
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/alert-service-principal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/alert-service-principal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/alert-service-principal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 9ca57c5a-6cea-872f-aa34-017e68e7cd89
---

# Resolve service principal alerts in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

[Service principals](/en-us/azure/active-directory/develop/app-objects-and-service-principals) are applications that the Azure platform uses to manage, update, and maintain a Microsoft Entra Domain Services managed domain. If a service principal is deleted, functionality in the managed domain is impacted.

This article helps you troubleshoot and resolve service principal-related configuration alerts.

## Alert AADDS102: Service principal not found

### Alert message

*A Service Principal required for Microsoft Entra Domain Services to function properly has been deleted from your Microsoft Entra directory. This configuration impacts Microsoft's ability to monitor, manage, patch, and synchronize your managed domain.*

If a required service principal is deleted, the Azure platform can't perform automated management tasks. The managed domain may not correctly apply updates or take backups.

### Check for missing service principals

To check which service principal is missing and must be recreated, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Enterprise applications**. Choose *All applications* from the **Application Type** drop-down menu, then select **Apply**.
2. Search for each of the following application IDs. For Azure Global, search for AppId value `2565bd9d-da50-47d4-8b85-4c97f669dc36`. For other Azure clouds, search for AppId value `6ba9a5d4-8456-4118-b521-9c5ca10cdf84`. If no existing application is found, follow the *Resolution* steps to create the service principal or re-register the namespace.

    | Application ID | Resolution |
    | --- | --- |
    | 2565bd9d-da50-47d4-8b85-4c97f669dc36 | Recreate a missing service principal |
    | 443155a6-77f3-45e3-882b-22b3a8d431fb | Re-register the `Microsoft.AAD` namespace |
    | abba844e-bc0e-44b0-947a-dc74e5d09022 | Re-register the `Microsoft.AAD` namespace |
    | d87dcbc6-a371-462e-88e3-28ad15ec4e64 | Re-register the `Microsoft.AAD` namespace |

### Recreate a missing Service Principal

If application ID *2565bd9d-da50-47d4-8b85-4c97f669dc36* is missing from your Microsoft Entra directory in Azure Global, use Microsoft Graph PowerShell to complete the following steps. For other Azure clouds, use AppId value *6ba9a5d4-8456-4118-b521-9c5ca10cdf84*. For more information, see [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

1. If needed, install the Microsoft Graph PowerShell module and import it as follows:

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```
2. Now recreate the service principal using the [New-MgServicePrincipal][/powershell/module/microsoft.graph.applications/new-mgserviceprincipal] cmdlet:

    ```powershell
    New-MgServicePrincipal -AppId "2565bd9d-da50-47d4-8b85-4c97f669dc36"
    ```

The managed domain's health automatically updates itself within two hours and removes the alert.

### Re-register the Microsoft Entra namespace

If application ID `443155a6-77f3-45e3-882b-22b3a8d431fb`, `abba844e-bc0e-44b0-947a-dc74e5d09022`, or `d87dcbc6-a371-462e-88e3-28ad15ec4e64` is missing from your Microsoft Entra directory, complete the following steps to re-register the `Microsoft.AAD` resource provider for your Azure subscription:

1. In the [Azure portal](https://portal.azure.com), search for and select **Subscriptions**.
2. Choose the subscription associated with your managed domain.
3. From the left-hand navigation expand **Settings**, then select **Resource Providers**.
4. Search for `Microsoft.AAD`, then select **Re-register**.

The managed domain's health automatically updates itself within two hours and removes the alert.

## Alert AADDS105: Password synchronization application is out of date

### Alert message

*The service principal with the application ID "d87dcbc6-a371-462e-88e3-28ad15ec4e64" was deleted and then recreated. The recreation leaves behind inconsistent permissions on Microsoft Entra Domain Services resources needed to service your managed domain. Synchronization of passwords on your managed domain could be affected.*

Domain Services automatically synchronizes user accounts and credentials from Microsoft Entra ID. If there's a problem with the Microsoft Entra application used for this process, credential synchronization between Domain Services and Microsoft Entra ID fails.

### Resolution

To recreate the Microsoft Entra application used for credential synchronization, use Microsoft Graph PowerShell to complete the following steps. For more information, see [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

1. If needed, install the Microsoft Graph PowerShell module and import it as follows:

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```
2. Now delete the old application and object using the following PowerShell cmdlets:

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    Connect-MgGraph -Scopes "Application.ReadWrite.All"
    $app = Get-MgApplication -Filter "DisplayName eq 'Azure AD Domain Services Sync'"
    Remove-MgApplication -ApplicationId $app.Id   
    ```

After you delete both applications, the Azure platform automatically recreates them and tries to resume password synchronization. The managed domain's health automatically updates itself within two hours and removes the alert.