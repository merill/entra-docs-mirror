---
layout: Conceptual
title: Manage custom security attributes for an application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/custom-security-attributes-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Assign, update, list, or remove custom security attributes for an application that is registered with your Microsoft Entra tenant.
ms.topic: how-to
ms.date: 2025-03-05T00:00:00.0000000Z
ms.reviewer: rolyon
zone_pivot_groups: enterprise-apps-minus-legacy-powershell
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: c8fd49e8-cf05-b223-5a23-5bab621c464b
document_version_independent_id: 84d4ca91-ab6b-4036-e259-fd9c4ce7fa44
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/custom-security-attributes-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/custom-security-attributes-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/custom-security-attributes-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 4bc74f5d-eeed-998f-eca0-d9a44d52dda9
---

# Manage custom security attributes for an application - Microsoft Entra ID | Microsoft Learn

[Custom security attributes](../../fundamentals/custom-security-attributes-overview) in Microsoft Entra ID are business-specific attributes (key-value pairs) that you can define and assign to Microsoft Entra objects. For example, you can assign custom security attribute to filter your applications or to help determine who gets access. This article describes how to assign, update, list, or remove custom security attributes for Microsoft Entra enterprise applications.

## Prerequisites

To assign or remove custom security attributes for an application in your Microsoft Entra tenant, you need:

- A Microsoft Entra account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator) role.
- Make sure you have existing custom security attributes. To learn how to create a security attribute, see [Add or deactivate custom security attributes in Microsoft Entra ID](../../fundamentals/custom-security-attributes-add).

Important

By default, [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

## Assign, update, list, or remove custom attributes for an application

Learn how to work with custom attributes for applications in Microsoft Entra ID.

### Assign custom security attributes to an application

::: zone pivot="portal"

Undertake the following steps to assign custom security attributes through the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Find and select the application you want to add a custom security attribute to.
4. In the Manage section, select **Custom security attributes**.
5. Select **Add assignment**.
6. In **Attribute set**, select an attribute set from the list.
7. In **Attribute name**, select a custom security attribute from the list.
8. Depending on the properties of the selected custom security attribute, you can enter a single value, select a value from a predefined list, or add multiple values.

    - For freeform, single-valued custom security attributes, enter a value in the **Assigned values** box.
    - For predefined custom security attribute values, select a value from the **Assigned values** list.
    - For multi-valued custom security attributes, select **Add values** to open the **Attribute values** pane and add your values. When finished adding values, select **Done**.

    [![Screenshot shows how to assign a custom security attribute to an application.](media/custom-security-attributes-apps/apps-attributes-assign.png)](media/custom-security-attributes-apps/apps-attributes-assign.png#lightbox)
9. When finished, select **Save** to assign the custom security attributes to the application.

### Update custom security attribute assignment values for an application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Find and select the application that has a custom security attribute assignment value you want to update.
4. In the Manage section, select **Custom security attributes**.
5. Find the custom security attribute assignment value you want to update.

    Once you assigned a custom security attribute to an application, you can only change the value of the custom security attribute. You can't change other properties of the custom security attribute, such as attribute set or custom security attribute name.
6. Depending on the properties of the selected custom security attribute, you can update a single value, select a value from a predefined list, or update multiple values.
7. When finished, select **Save**.

### Filter applications based on custom security attributes

You can filter the list of custom security attributes assigned to applications on the **All applications** page.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Attribute Assignment Reader](../role-based-access-control/permissions-reference#attribute-assignment-reader).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **Add filters** to open the Pick a field pane.

    If you don't see **Add filters**, select the banner to enable the Enterprise applications search preview.
4. For **Filters**, select **Custom security attribute**.
5. Select your attribute set and attribute name.
6. For **Operator**, you can select equals (**==**), not equals (**!=**), or **starts with**.
7. For **Value**, enter or select a value.
8. To apply the filter, select **Apply**.

### Remove custom security attribute assignments from applications

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Find and select the application that has the custom security attribute assignments you want to remove.
4. In the **Manage** section, select **Custom security attributes (preview)**.
5. Add check marks next to all the custom security attribute assignments you want to remove.
6. Select **Remove assignment**.

::: zone-end

::: zone pivot="ms-powershell"

### Microsoft Graph PowerShell

To manage custom security attribute assignments for applications in your Microsoft Entra organization, you can use Microsoft Graph PowerShell. The following commands can be used to manage assignments.

### Assign a custom security attribute with a multi-string value to an application (service principal) using Microsoft Graph PowerShell

Use the [Update-MgServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/update-mgserviceprincipal) command to assign a custom security attribute with a multi-string value to an application (service principal).

Given the values

- Attribute set: `Engineering`
- Attribute: `ProjectDate`
- Attribute data type: String
- Attribute value: `"2024-11-15"`

```powershell
#Retrieve the servicePrincipal

$ServicePrincipal = (Get-MgServicePrincipal -Filter "displayName eq 'TestApp'").Id

$customSecurityAttributes = @{
    Engineering = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "ProjectDate" ="2024-11-15"
    }
}
Update-MgServicePrincipal -ServicePrincipalId $ServicePrincipal -CustomSecurityAttributes $customSecurityAttributes
```

### Update a custom security attribute with a multi-string value for an application (service principal) using Microsoft Graph PowerShell

Provide the new set of attribute values that you would like to reflect on the application. In this example, we're adding one more value for project attribute.

Given the values

- Attribute set: `Engineering`
- Attribute: `Project`
- Attribute data type: Collection of Strings
- Attribute value: `["Baker","Cascade"]`

```powershell
$customSecurityAttributes = @{
    Engineering = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Project@odata.type" = "#Collection(String)"
        "Project" = @(
            "Baker"
            "Cascade"
        )
    }
}
Update-MgServicePrincipal -ServicePrincipalId $ServicePrincipal -CustomSecurityAttributes $customSecurityAttributes
```

### Filter applications based on custom security attributes using Microsoft Graph PowerShell

This example filters a list of applications with a custom security attribute assignment that equals the specified value.

```powershell
$appAttributes = Get-MgServicePrincipal -CountVariable CountVar -Property "id,displayName,customSecurityAttributes" -Filter "customSecurityAttributes/Engineering/Project eq 'Baker'" -ConsistencyLevel eventual
$appAttributes | select Id,DisplayName,CustomSecurityAttributes  | Format-List
$appAttributes.CustomSecurityAttributes.AdditionalProperties | Format-List
```

```Output
Id                       : aaaaaaaa-bbbb-cccc-1111-222222222222
DisplayName              : TestApp
CustomSecurityAttributes : Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue

Key   : Engineering
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [ProjectDate, 2024-11-15], [Project@odata.type, #Collection(String)], [Project, System.Object[]]}
```

### Remove custom security attribute assignments from applications using Microsoft Graph PowerShell

In this example, we remove a custom security attribute assignment that supports single values.

```powershell

$params = @{
    "customSecurityAttributes" = @{
        "Engineering" = @{
            "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
            "ProjectDate" = $null
        }
    }
}
Invoke-MgGraphRequest -Method PATCH -Uri "https://graph.microsoft.com/v1.0/servicePrincipals/$ServicePrincipal" -Body $params
```

In this example, we remove a custom security attribute assignment that supports multiple values.

```powershell
$customSecurityAttributes = @{
    Engineering = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Project" = @()
    }
}
Update-MgServicePrincipal -ServicePrincipalId $ServicePrincipal -CustomSecurityAttributes $customSecurityAttributes
```

::: zone-end

::: zone pivot="ms-graph"

### Microsoft Graph API

To manage custom security attribute assignments for applications in your Microsoft Entra organization, you can use the Microsoft Graph API. Make the following API calls to manage assignments.

For other similar Microsoft Graph API examples for users, see [Assign, update, list, or remove custom security attributes for a user](../users/users-custom-security-attributes#powershell-or-microsoft-graph-api) and [Examples: Assign, update, list, or remove custom security attribute assignments using the Microsoft Graph API](/en-us/graph/custom-security-attributes-examples).

### Assign a custom security attribute with a multi-string value to an application (service principal) using Microsoft Graph API

Use the [Update servicePrincipal](/en-us/graph/api/serviceprincipal-update) API to assign a custom security attribute with a string value to an application.

Given the values

- Attribute set: `Engineering`
- Attribute: `Project`
- Attribute data type: String
- Attribute value: `"Baker"`

```http
PATCH https://graph.microsoft.com/v1.0/servicePrincipals/{id}
Content-type: application/json

{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "Project@odata.type":"#Collection(String)",
            "Project": "Baker"
        }
    }
}
```

### Update a custom security attribute with a multi-string value for an application (service principal) using Microsoft Graph API

Provide the new set of attribute values that you would like to reflect on the application. In this example, we're adding one more value for project attribute.

```http
PATCH https://graph.microsoft.com/v1.0/servicePrincipals/{id}
Content-type: application/json

{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "Project@odata.type":"#Collection(String)",
            "Project":["Baker","Cascade"]
        }
    }
}
```

### Filter applications based on custom security attributes using Microsoft Graph API

This example filters a list of applications with a custom security attribute assignment that equals the specified value. The filter value is case sensitive. You must add `ConsistencyLevel=eventual` in the request or the header. You must also include `$count=true` to ensure the request is routed correctly.

```http
GET https://graph.microsoft.com/v1.0/servicePrincipals?$count=true&$select=id,displayName,customSecurityAttributes&$filter=customSecurityAttributes/Engineering/Project eq 'Baker'
ConsistencyLevel: eventual
```

### Remove custom security attribute assignments from an application using Microsoft Graph API

In this example, we remove a custom security attribute assignment that supports multiple values.

```http
PATCH https://graph.microsoft.com/v1.0/servicePrincipals/{id}
Content-type: application/json

{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "Project":[]
        }
    }
}
```

::: zone-end