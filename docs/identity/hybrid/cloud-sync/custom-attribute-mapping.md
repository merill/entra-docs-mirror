---
layout: Conceptual
title: Microsoft Entra Cloud Sync directory extensions and custom attribute mapping - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/custom-attribute-mapping
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article provides information on custom attribute mapping in cloud sync.
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 2bbc90dc-3d2c-7a9a-7699-740398b0ed3f
document_version_independent_id: 137f80e4-7d00-a04e-0922-bcf595357960
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/custom-attribute-mapping.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/custom-attribute-mapping
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/custom-attribute-mapping.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 8d7c5067-3e11-2ac2-fa6c-8b82e17c046a
---

# Microsoft Entra Cloud Sync directory extensions and custom attribute mapping - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID must contain all the data (attributes) required to create a user profile when provisioning user accounts from Microsoft Entra ID to a line of business (LOB), [SaaS app](../../saas-apps/tutorial-list), or on-premises application. You can use directory extensions to extend the schema in Microsoft Entra ID with your own attributes. This feature enables you to build LOB apps by consuming attributes that you continue to manage on-premises, provision users from Active Directory to Microsoft Entra ID or SaaS apps, and use extension attributes in Microsoft Entra ID and Microsoft Entra ID Governance features such as dynamic membership groups or Group provisioning to Active Directory.

For more information on directory extensions, see [Using directory extension attributes in claims](../../../identity-platform/schema-extensions), [Microsoft Entra Connect Sync: directory extensions](../connect/how-to-connect-sync-feature-directory-extensions), and [Syncing extension attributes for Microsoft Entra application provisioning](../../app-provisioning/user-provisioning-sync-attributes-for-mapping).

You can see the available attributes by using [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).

Note

In order to discover new Active Directory extension attributes, the provisioning agent needs to be restarted. You should restart the agent after the directory extensions have been created. For Microsoft Entra extension attributes, the agent doesn't need to be restarted.

## Syncing directory extensions for Microsoft Entra Cloud Sync

You can use [directory extensions](/en-us/graph/api/resources/extensionproperty?view=graph-rest-1.0&amp;preserve-view=true) to extend the synchronization schema directory definition in Microsoft Entra ID with your own attributes.

Important

Directory extension for Microsoft Entra Cloud Sync is only supported for applications with the identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp` and the [Tenant Schema Extension App](../connect/how-to-connect-sync-feature-directory-extensions#configuration-changes-in-azure-ad-made-by-the-wizard) created by Microsoft Entra Connect.

### Create application and service principal for directory extension

You need to create an [application](/en-us/graph/api/resources/application) with the identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp` if it doesn't exist and create a service principal for the application if it doesn't exist.

# [Graph PowerShell](#tab/ps)
1. Check if application with the identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp` exists:

    ```powershell
    $tenantId = (Get-MgOrganization).Id
    
    Get-MgApplication -Filter "identifierUris/any(uri:uri eq 'API://$tenantId/CloudSyncCustomExtensionsApp')"
    ```

    For more information, see [Get-MgApplication](/en-us/powershell/module/microsoft.graph.applications/get-mgapplication).
2. If the application doesn't exist, use the `$tenantId` variable from previous step to create the application with identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp`:

    ```powershell
    New-MgApplication -DisplayName "CloudSyncCustomExtensionsApp" -IdentifierUris "API://$tenantId/CloudSyncCustomExtensionsApp"
    ```

    For more information, see [New-MgApplication](/en-us/powershell/module/microsoft.graph.applications/new-mgapplication).
3. Use the `$tenantId` variable from previous step to check if the service principal exists for the application with identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp`:

    ```powershell
    $appId = (Get-MgApplication -Filter "identifierUris/any(uri:uri eq 'API://$tenantId/CloudSyncCustomExtensionsApp')").AppId
    
    Get-MgServicePrincipal -Filter "AppId eq '$appId'"
    ```

    For more information, see [Get-MgServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/get-mgserviceprincipal).
4. If a service principal doesn't exist, use the `$appId variable` from the previous step to create a new service principal for the application with identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp`:

    ```powershell
    New-MgServicePrincipal -AppId $appId
    ```

    For more information, see [New-MgServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/new-mgserviceprincipal).
5. Use the `$tenantId` variable from previous step to create a directory extension in Microsoft Entra ID. For example, a new extension called 'GroupDN', of string type, for Group objects:

    ```powershell
    $appObjId = (Get-MgApplication -Filter "identifierUris/any(uri:uri eq 'API://$tenantId/CloudSyncCustomExtensionsApp')").Id
    
    New-MgApplicationExtensionProperty -ApplicationId $appObjId -Name GroupDN -DataType String -TargetObjects Group
    ```

# [Graph Explorer](#tab/ge)
1. Check if application with the identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp` exists.

    ```https
    GET /applications?$filter=identifierUris/any(uri:uri eq 'api://<tenantId>/CloudSyncCustomExtensionsApp')
    ```

    For more information, see [Get application](/en-us/graph/api/application-get?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true)
2. If the application doesn't exist, create the application with identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp`:

    ```https
    POST https://graph.microsoft.com/v1.0/applications
    Content-type: application/json
    
    {
    "displayName": "CloudSyncCustomExtensionsApp",
    "identifierUris": ["api://<tenant id>/CloudSyncCustomExtensionsApp"]
    }
    ```

    For more information, see [create application](/en-us/graph/api/application-post-applications?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true).
3. Check if the service principal exists for the application with identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp`:

    ```
    GET /servicePrincipals?$filter=(appId eq '{appId}')
    ```

    For more information, see [get service principal](/en-us/graph/api/serviceprincipal-get?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true)
4. If a service principal doesn't exist, create a new service principal for the application with identifier URI `API://<tenantId>/CloudSyncCustomExtensionsApp`:

    ```https
    POST https://graph.microsoft.com/v1.0/servicePrincipals
    Content-type: application/json
    
    {
    "appId": 
    "<application appId>"
    }
    ```

    For more information, see [create servicePrincipal](/en-us/graph/api/serviceprincipal-post-serviceprincipals?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true).
5. Create a directory extension in Microsoft Entra ID. For example, a new extension called 'GroupDN', of string type, for Group objects:

    ```https
    POST https://graph.microsoft.com/v1.0/applications/<ApplicationId>/extensionProperties
    Content-type: application/json
    
    {
      "name": "GroupDN",
      "dataType": "String",
      "isMultiValued": false,
      "targetObjects": [
          "Group"
      ]
    }    
    ```

---

You can create directory extensions in Microsoft Entra ID in several different ways, as described in the following table:

| Method | Description | URL |
| --- | --- | --- |
| MS Graph | Create extensions using Microsoft Graph | [Create extensionProperty](/en-us/graph/api/application-post-extensionproperty?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) |
| PowerShell | Create extensions using PowerShell | [New-MgApplicationExtensionProperty](/en-us/powershell/module/microsoft.graph.applications/new-mgapplicationextensionproperty) |
| Using cloud sync and Microsoft Entra Connect | Create extensions using Microsoft Entra Connect | [Create an extension attribute using Microsoft Entra Connect](../../app-provisioning/user-provisioning-sync-attributes-for-mapping#create-an-extension-attribute-using-azure-ad-connect) |
| Customizing attributes to sync | Information on customizing, which attributes to synch | [Customize which attributes to synchronize with Microsoft Entra ID](../connect/how-to-connect-sync-feature-directory-extensions#select-which-attributes-to-synchronize-with-microsoft-entra-id) |

## Use attribute mapping to map Directory Extensions

If you extended Active Directory to include custom attributes, you can add these attributes and map them to users.

To discover and map attributes, select **Add attribute mapping** and the attributes become available in the drop-down under **source attribute**. Fill in the type of mapping you want and select **Apply**. [![Custom attribute mapping](media/custom-attribute-mapping/schema-1.png)](media/custom-attribute-mapping/schema-1.png#lightbox)

For information on new attributes that are added and updated in Microsoft Entra ID see the [`user` resource type](/en-us/graph/api/resources/user?view=graph-rest-1.0#properties&amp;preserve-view=true) and consider subscribing to [change notifications](/en-us/graph/change-notifications-overview).

For more information on extension attributes, see [Syncing extension attributes for Microsoft Entra Application Provisioning](../../app-provisioning/user-provisioning-sync-attributes-for-mapping).