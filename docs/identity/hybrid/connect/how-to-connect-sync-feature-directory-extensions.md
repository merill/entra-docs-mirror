---
layout: Conceptual
title: 'Microsoft Entra Connect Sync: Directory extensions - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes the directory extensions feature in Microsoft Entra Connect.
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0cc5c0d2-f57a-d462-01f0-f185362681bc
document_version_independent_id: 0d99a6af-1382-963c-d163-04492eb596b3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 57151345-3fe1-60cf-0bde-7e199706c25e
---

# Microsoft Entra Connect Sync: Directory extensions - Microsoft Entra ID | Microsoft Learn

You can use directory extensions to extend the schema in Microsoft Entra ID with your own attributes from on-premises Active Directory. This feature enables you to build LOB apps by consuming attributes that you continue to manage on-premises. These attributes can be consumed through [extensions](/en-us/graph/extensibility-overview). You can see the available attributes by using [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/overview) or [Microsoft Entra PowerShell](/en-us/powershell/entra-powershell/overview). Currently, no Microsoft 365 workload consumes these attributes, but you can use this feature with dynamic group memberships in Microsoft Entra ID.

## Select which attributes to synchronize with Microsoft Entra ID

You configure which extended attributes you want to synchronize using Microsoft Entra Connect configuration wizard, in the custom settings.

![Schema extension wizard](media/how-to-connect-sync-feature-directory-extensions/extension2.png)

The wizard shows the attributes that are valid candidates to be used with Directory Extensions:

- User and Group object types
- Single-valued attributes: String, Boolean, Integer, Binary
- Multi-valued attributes: String, Binary

## Important considerations when using Directory Extensions

- The list of attributes is read from the Active Directory schema during initial installation of Microsoft Entra Connect. If you extend the Active Directory schema with more custom attributes, you must [refresh the schema](how-to-connect-installation-wizard#refresh-directory-schema) before these new attributes are visible.
- If you exported a configuration that contains a custom rule used to synchronize directory extension attributes and you attempt to import this rule into a new or existing installation of Microsoft Entra Connect, the rule is created during import, but the directory extension attributes won't be mapped. You need to re-select the directory extension attributes and re-associate them with the rule or recreate the rule entirely to fix this.
- Not all features in Microsoft Entra ID support multi-valued extension attributes. Refer to the documentation of the feature in which you plan to use these attributes to confirm they're supported.
- An object in Microsoft Entra ID can have up to 100 directory extension attribute values. For multi‑valued attributes, each individual value counts toward this 100‑value limit.
- The maximum length of a string attribute value is 256 characters. If an attribute value exceeds this limit, the sync engine truncates the value.
- It's not supported to sync constructed attributes, such as msDS-UserPasswordExpiryTimeComputed. If you upgrade from an old version of Microsoft Entra Connect you may still see these attributes show up in the installation wizard, you shouldn't enable them as its value won't sync to Microsoft Entra ID. [Learn mode](/en-us/openspecs/windows_protocols/ms-adts/a3aff238-5f0e-4eec-8598-0a59c30ecd56).
- It's not supported to sync non-replicated attributes, such as badPwdCount, Last-Logon, and Last-Logoff, as their values don't sync to Microsoft Entra ID.
- It's not supported to manage on-premises Directory Extensions outside of Microsoft Entra Connect wizard. Manually editing or cloning the sync rules for Directory Extensions can cause synchronization issues.
- It's not supported to sync attribute values from Microsoft Entra Connect to extension attributes that aren't created by Microsoft Entra Connect. Doing so may produce performance issues and unexpected results.

## Configuration changes in Microsoft Entra ID made by the wizard

During installation of Microsoft Entra Connect, an application is registered where these attributes are configured. You can see this application in the [Microsoft Entra admin center](https://entra.microsoft.com), with the name **Tenant Schema Extension App**. Make sure you select **All Applications** to see this app.

![Schema extension app](media/how-to-connect-sync-feature-directory-extensions/extension3new.png)

Note

The **Tenant Schema Extension App** is a system-only application that can't be deleted. Deleting the Service Principal associated with **Tenant Schema Extension App** breaks the synchronization. To recover Directory Extensions synchronization, restore the soft-deleted Service Principal or re-create a new one.

## Viewing extended attributes in Microsoft Entra ID

The format of extended attributes is `extension_{ApplicationId}_<attributeName>`, where ApplicationId is the application identifier of your *Tenant Schema Extension App*. You need this value for all other scenarios in this topic.

### Using the Microsoft Graph API

These attributes are available through Microsoft Graph API, by using [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer#).

In the Microsoft Graph API, you need to ask for the attributes to be returned. Explicitly select the attributes like this:

```
https://graph.microsoft.com/beta/users/abbie.spencer@fabrikamonline.com?$select=extension_9d98ed114c4840d298fad781915f27e4_employeeID,extension_9d98ed114c4840d298fad781915f27e4_division
```

For more information, see [Microsoft Graph: Use query parameters](/en-us/graph/query-parameters#select-parameter).

### Using the Microsoft Graph PowerShell SDK

1. Get the **Tenant Schema Extension App** application:

```powershell
Get-MgApplication -Filter "DisplayName eq 'Tenant Schema Extension App'"
```

1. List all extension attributes for the **Tenant Schema Extension App**:

```powershell
Get-MgDirectoryObjectAvailableExtensionProperty
```

1. List all extension attributes for a user object:

```powershell
(Get-MgBetaUser -UserId "<Id or UserPrincipalName>").AdditionalProperties

```

### Using the Microsoft Entra PowerShell

1. Get the **Tenant Schema Extension App** application identifier:

```powershell
Get-EntraApplication -SearchString "Tenant Schema Extension App"
```

1. List all extension attributes for **Tenant Schema Extension App** application:

```powershell
Get-EntraExtensionProperty | Where-Object {$_.AppDisplayName -eq 'Tenant Schema Extension App'}
```

1. List all extension attributes for a user object:

```powershell
Get-EntraUserExtension -UserId "<Id or UserPrincipalName>"
```

## Use the attributes in dynamic membership groups

One of the most useful scenarios is to use extension attributes in dynamic security or Microsoft 365 groups.

1. Create a new group in Microsoft Entra ID. Give it a name and make sure the **Membership type** is **Dynamic User**.

    ![Screenshot with a new group](media/how-to-connect-sync-feature-directory-extensions/dynamicgroup1.png)
2. Select to **Add dynamic query**. When you look at the properties, these extended attributes are missing because you need to add them first. Click **Get custom extension properties**, enter the Application ID, and click **Refresh properties**.

    ![Screenshot where directory extensions have been added](media/how-to-connect-sync-feature-directory-extensions/dynamicgroup2.png)
3. Open the property drop-down and note that the attributes you added are now visible.

    ![Screenshot with new attributes showing up in the UI](media/how-to-connect-sync-feature-directory-extensions/dynamicgroup3.png)
4. To suit your requirements, complete the expression. In our example, the rule is set to:

    `(user.extension_9d98ed114c4840d298fad781915f27e4_division -eq "Sales and marketing")`
5. After the group is created, give Microsoft Entra some time to populate the members and then review the members.

    ![Screenshot with members in the dynamic group](media/how-to-connect-sync-feature-directory-extensions/dynamicgroup4.png)