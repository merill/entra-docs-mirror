---
layout: Conceptual
title: Assign, update, list, or remove custom security attributes for a user - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-custom-security-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Assign, update, list, or remove custom security attributes for a user in Microsoft Entra ID.
ms.date: 2026-05-11T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, no-azure-ad-ps-ref, sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 43c892af-3e7a-7475-bea4-e49d33afc7a6
document_version_independent_id: 88355bde-bac2-943e-08f8-fd5f2ecf707b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-custom-security-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-custom-security-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-custom-security-attributes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1997df67-ca9c-e630-5e7b-125a7432948b
---

# Assign, update, list, or remove custom security attributes for a user - Microsoft Entra ID | Microsoft Learn

## Overview

[Custom security attributes](../../fundamentals/custom-security-attributes-overview) in Microsoft Entra ID, part of Microsoft Entra, are business-specific attributes (key-value pairs) that you can define and assign to Microsoft Entra objects. For example, you can assign custom security attribute to filter your employees or to help determine who gets access to resources. This article describes how to assign, update, list, or remove custom security attributes for Microsoft Entra ID.

## Prerequisites

To assign or remove custom security attributes for a user in your Microsoft Entra tenant, you need:

- [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator)
- Microsoft.Graph module when using [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation)
- Connect to Microsoft Graph with the required scope:

    ```PowerShell
    Connect-MgGraph -Scopes "CustomSecAttributeAssignment.ReadWrite.All"
    ```

Important

By default, [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

## Assign custom security attributes to a user

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Make sure that you have defined custom security attributes. For more information, see [Add or deactivate custom security attribute definitions in Microsoft Entra ID](../../fundamentals/custom-security-attributes-add).
3. Browse to **Identity** &gt; **Users** &gt; **All users**.
4. Find and select the user you want to assign custom security attributes to.
5. In the Manage section, select **Custom security attributes**.
6. Select **Add assignment**.
7. In **Attribute set**, select an attribute set from the list.
8. In **Attribute name**, select a custom security attribute from the list.
9. Depending on the properties of the selected custom security attribute, you can enter a single value, select a value from a predefined list, or add multiple values.

    - For freeform, single-valued custom security attributes, enter a value in the **Assigned values** box.
    - For predefined custom security attribute values, select a value from the **Assigned values** list.
    - For multi-valued custom security attributes, select **Add values** to open the **Attribute values** pane and add your values. When finished adding values, select **Done**.

    [![Screenshot showing assigning a custom security attribute to a user.](media/users-custom-security-attributes/users-attributes-assign.png)](media/users-custom-security-attributes/users-attributes-assign.png#lightbox)
10. When finished, select **Save** to assign the custom security attributes to the user.

## Update custom security attribute assignment values for a user

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Identity** &gt; **Users** &gt; **All users**.
3. Find and select the user that has a custom security attribute assignment value you want to update.
4. In the Manage section, select **Custom security attributes**.
5. Find the custom security attribute assignment value you want to update.

    Once you have assigned a custom security attribute to a user, you can only change the value of the custom security attribute. You can't change other properties of the custom security attribute, such as attribute set or attribute name.
6. Depending on the properties of the selected custom security attribute, you can update a single value, select a value from a predefined list, or update multiple values.
7. When finished, select **Save**.

## Filter users based on custom security attribute assignments

You can filter the list of custom security attributes assigned to users on the All users page.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Assignment Reader](../role-based-access-control/permissions-reference#attribute-assignment-reader).
2. Browse to **Identity** &gt; **Users** &gt; **All users**.
3. Select **Add filter** to open the Add filter pane.
4. Select **Custom security attributes**.
5. Select your attribute set and attribute name.
6. For **Operator**, you can select equals (**==**), not equals (**!=**), or **starts with**.
7. For **Value**, enter or select a value.

    [![Screenshot showing a custom security attribute filter for users.](media/users-custom-security-attributes/users-attributes-filter.png)](media/users-custom-security-attributes/users-attributes-filter.png#lightbox)
8. To apply the filter, select **Apply**.

## Remove custom security attribute assignments from a user

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Identity** &gt; **Users** &gt; **All users**.
3. Find and select the user that has the custom security attribute assignments you want to remove.
4. In the Manage section, select **Custom security attributes**.
5. Add check marks next to all the custom security attribute assignments you want to remove.
6. Select **Remove assignment**.

## PowerShell or Microsoft Graph API

To manage custom security attribute assignments for users in your Microsoft Entra organization, you can use PowerShell or Microsoft Graph API. The following examples can be used to manage assignments.

### Assign a custom security attribute with a string value to a user

The following example assigns a custom security attribute with a string value to a user.

- Attribute set: `Engineering`
- Attribute: `ProjectDate`
- Attribute data type: String
- Attribute value: `"2024-11-15"`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "ProjectDate" = "2024-11-15"
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "ProjectDate":"2024-11-15"
        }
    }
}
```

---

### Assign a custom security attribute with a multi-string value to a user

The following example assigns a custom security attribute with a multi-string value to a user.

- Attribute set: `Engineering`
- Attribute: `Project`
- Attribute data type: Collection of Strings
- Attribute value: `["Baker","Cascade"]`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Project@odata.type" = "#Collection(String)"
        "Project" = @("Baker","Cascade")
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
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

---

### Assign a custom security attribute with an integer value to a user

The following example assigns a custom security attribute with an integer value to a user.

- Attribute set: `Engineering`
- Attribute: `NumVendors`
- Attribute data type: Integer
- Attribute value: `4`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "NumVendors@odata.type" = "#Int32"
        "NumVendors" = 4
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "NumVendors@odata.type":"#Int32",
            "NumVendors":4
        }
    }
}
```

---

### Assign a custom security attribute with a multi-integer value to a user

The following example assigns a custom security attribute with a multi-integer value to a user.

- Attribute set: `Engineering`
- Attribute: `CostCenter`
- Attribute data type: Collection of Integers
- Attribute value: `[1001,1003]`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "CostCenter@odata.type" = "#Collection(Int32)"
        "CostCenter" = @(1001,1003)
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "CostCenter@odata.type":"#Collection(Int32)",
            "CostCenter":[1001,1003]
        }
    }
}
```

---

### Assign a custom security attribute with a Boolean value to a user

The following example assigns a custom security attribute with a Boolean value to a user.

- Attribute set: `Engineering`
- Attribute: `Certification`
- Attribute data type: Boolean
- Attribute value: `true`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Certification" = $true
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "Certification":true
        }
    }
}
```

---

### Update a custom security attribute assignment with an integer value for a user

The following example updates a custom security attribute assignment with an integer value for a user.

- Attribute set: `Engineering`
- Attribute: `NumVendors`
- Attribute data type: Integer
- Attribute value: `8`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "NumVendors@odata.type" = "#Int32"
        "NumVendors" = 8
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "NumVendors@odata.type":"#Int32",
            "NumVendors":8
        }
    }
}
```

---

### Update a custom security attribute assignment with a Boolean value for a user

The following example updates a custom security attribute assignment with a Boolean value for a user.

- Attribute set: `Engineering`
- Attribute: `Certification`
- Attribute data type: Boolean
- Attribute value: `false`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Certification" = $false
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "Certification":false
        }
    }
}
```

---

### Update a custom security attribute assignment with a multi-string value for a user

The following example updates a custom security attribute assignment with a multi-string value for a user.

- Attribute set: `Engineering`
- Attribute: `Project`
- Attribute data type: Collection of Strings
- Attribute value: `("Alpine","Baker")`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Project@odata.type" = "#Collection(String)"
        "Project" = @("Alpine","Baker")
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "Project@odata.type":"#Collection(String)",
            "Project":["Alpine","Baker"]
        }
    }
}
```

---

### Get the custom security attribute assignments for a user

The following example gets the custom security attribute assignments for a user.

# [PowerShell](#tab/ms-powershell)
[Get-MgUser](/en-us/powershell/module/microsoft.graph.users/get-mguser)

```powershell
$userAttributes = Get-MgUser -UserId $userId -Property "customSecurityAttributes"
$userAttributes.CustomSecurityAttributes.AdditionalProperties | Format-List
$userAttributes.CustomSecurityAttributes.AdditionalProperties.Engineering
$userAttributes.CustomSecurityAttributes.AdditionalProperties.Marketing
```

```Output
Key   : Engineering
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [Project@odata.type, #Collection(String)], [Project, System.Object[]],
        [ProjectDate, 2024-11-15]…}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [EmployeeId, GS45897]}

Key                   Value
---                   -----
@odata.type           #microsoft.graph.customSecurityAttributeValue
Project@odata.type    #Collection(String)
Project               {Baker, Alpine}
ProjectDate           2024-11-15
NumVendors            8
CostCenter@odata.type #Collection(Int32)
CostCenter            {1001, 1003}
Certification         False

Key         Value
---         -----
@odata.type #microsoft.graph.customSecurityAttributeValue
EmployeeId  KX45897
```

If there are no custom security attributes assigned to the user or if the calling principal doesn't have access, the response will be empty.

# [Microsoft Graph](#tab/ms-graph)
[Get user](/en-us/graph/api/user-get)

```http
GET https://graph.microsoft.com/v1.0/users/{id}?$select=customSecurityAttributes
```

```http
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users(customSecurityAttributes)/$entity",
    "customSecurityAttributes": {
        "Engineering": {
            "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
            "Project@odata.type": "#Collection(String)",
            "Project": [
                "Baker",
                "Alpine"
            ],
            "ProjectDate": "2024-11-15",
            "NumVendors": 8,
            "CostCenter@odata.type": "#Collection(Int32)",
            "CostCenter": [
                1001,
                1003
            ],
            "Certification": false
        },
        "Marketing": {
            "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
            "EmployeeId": "GS45897"
        }
    }
}
```

If there are no custom security attributes assigned to the user or if the calling principal doesn't have access, the response will look like:

```http
{
    "customSecurityAttributes": null
}
```

---

### List all users and any custom security attribute assignments

The following example lists all users and any custom security attribute assignments. Because this example uses only `$select` (no `$filter`, `$search`, `$count`, or `$orderby`), advanced query parameters aren't required. The List examples later in this article that use `$filter` on `customSecurityAttributes` do require `ConsistencyLevel=eventual` and `$count=true`. For more information, see [Advanced query capabilities on directory objects](/en-us/graph/aad-advanced-queries).

# [PowerShell](#tab/ms-powershell)
[Get-MgUser](/en-us/powershell/module/microsoft.graph.users/get-mguser)

```powershell
$userAttributes = Get-MgUser -All -Property "id,displayName,customSecurityAttributes"
$userAttributes | select Id,DisplayName,CustomSecurityAttributes
$userAttributes.CustomSecurityAttributes.AdditionalProperties | Format-List
```

```Output
Id                                   DisplayName CustomSecurityAttributes
--                                   ----------- ------------------------
00aa00aa-bb11-cc22-dd33-44ee44ee44ee Alain
11bb11bb-cc22-dd33-ee44-55ff55ff55ff Joe         Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
22cc22cc-dd33-ee44-ff55-66aa66aa66aa Isabella    Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
33dd33dd-ee44-ff55-aa66-77bb77bb77bb Jiya        Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
44ee44ee-ff55-aa66-bb77-88cc88cc88cc Admin

Key   : Engineering
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [Project@odata.type, #Collection(String)], [Project, System.Object[]],
        [CostCenter@odata.type, #Collection(Int32)], [CostCenter, System.Object[]], [Certification, True]}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [EmployeeId, QN26904]}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [AppCountry@odata.type, #Collection(String)], [AppCountry, System.Object[]]}

Key   : Engineering
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [ProjectDate, 2026-04-23]}
```

# [Microsoft Graph](#tab/ms-graph)
[List users](/en-us/graph/api/user-list)

```http
GET https://graph.microsoft.com/v1.0/users?$select=id,displayName,customSecurityAttributes
```

If your tenant has more users than fit in a single page, the response includes an `@odata.nextLink` property. Follow that link to retrieve the next page of results. For more information, see [Paging Microsoft Graph data in your app](/en-us/graph/paging).

```http
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users(id,displayName,customSecurityAttributes)",
    "value": [
        {
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
            "displayName": "Alain",
            "customSecurityAttributes": null
        },
        {
            "id": "11bb11bb-cc22-dd33-ee44-55ff55ff55ff",
            "displayName": "Joe",
            "customSecurityAttributes": {
                "Engineering": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "Project@odata.type": "#Collection(String)",
                    "Project": [
                        "Baker",
                        "Cascade"
                    ],
                    "CostCenter@odata.type": "#Collection(Int32)",
                    "CostCenter": [
                        1001
                    ],
                    "Certification": true
                },
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "EmployeeId": "QN26904"
                }
            }
        },
        {
            "id": "22cc22cc-dd33-ee44-ff55-66aa66aa66aa",
            "displayName": "Isabella",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "AppCountry@odata.type": "#Collection(String)",
                    "AppCountry": [
                        "France"
                    ]
                }
            }
        },
        {
            "id": "33dd33dd-ee44-ff55-aa66-77bb77bb77bb",
            "displayName": "Jiya",
            "customSecurityAttributes": {
                "Engineering": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "ProjectDate": "2026-04-23"
                }
            }
        },
        {
            "id": "44ee44ee-ff55-aa66-bb77-88cc88cc88cc",
            "displayName": "Admin",
            "customSecurityAttributes": null
        }
    ]
}
```

---

### List all users with a custom security attribute assignment that equals a value

The following example lists all users with a custom security attribute assignment that equals a value. It retrieves users with a custom security attribute named `AppCountry` with a value that equals `Canada`. The filter value is case sensitive. You must add `ConsistencyLevel=eventual` in the request or the header. You must also include `$count=true` to ensure the request is routed correctly.

- Attribute set: `Marketing`
- Attribute: `AppCountry`
- Filter: AppCountry eq 'Canada'

# [PowerShell](#tab/ms-powershell)
[Get-MgUser](/en-us/powershell/module/microsoft.graph.users/get-mguser)

```powershell
$userAttributes = Get-MgUser -CountVariable CountVar -Property "id,displayName,customSecurityAttributes" -Filter "customSecurityAttributes/Marketing/AppCountry eq 'Canada'" -ConsistencyLevel eventual
$userAttributes | select Id,DisplayName,CustomSecurityAttributes
$userAttributes.CustomSecurityAttributes.AdditionalProperties | Format-List
```

```Output
Id                                   DisplayName CustomSecurityAttributes
--                                   ----------- ------------------------
00aa00aa-bb11-cc22-dd33-44ee44ee44ee Jiya        Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
11bb11bb-cc22-dd33-ee44-55ff55ff55ff Jana        Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue

Key   : Engineering
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [Datacenter@odata.type, #Collection(String)], [Datacenter, System.Object[]]}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [AppCountry@odata.type, #Collection(String)], [AppCountry, System.Object[]],
        [EmployeeId, KX19476]}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [AppCountry@odata.type, #Collection(String)], [AppCountry, System.Object[]],
        [EmployeeId, GS46982]}
```

# [Microsoft Graph](#tab/ms-graph)
[List users](/en-us/graph/api/user-list)

```http
GET https://graph.microsoft.com/v1.0/users?$count=true&$select=id,displayName,customSecurityAttributes&$filter=customSecurityAttributes/Marketing/AppCountry eq 'Canada'
ConsistencyLevel: eventual
```

```http
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users(id,displayName,customSecurityAttributes)",
    "@odata.count": 2,
    "value": [
        {
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
            "displayName": "Jiya",
            "customSecurityAttributes": {
                "Engineering": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "Datacenter@odata.type": "#Collection(String)",
                    "Datacenter": [
                        "India"
                    ]
                },
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "AppCountry@odata.type": "#Collection(String)",
                    "AppCountry": [
                        "India",
                        "Canada"
                    ],
                    "EmployeeId": "KX19476"
                }
            }
        },
        {
            "id": "11bb11bb-cc22-dd33-ee44-55ff55ff55ff",
            "displayName": "Jana",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "AppCountry@odata.type": "#Collection(String)",
                    "AppCountry": [
                        "Canada",
                        "Mexico"
                    ],
                    "EmployeeId": "GS46982"
                }
            }
        }
    ]
}
```

---

### List all users with a custom security attribute assignment that starts with a value

The following example lists all users with a custom security attribute assignment that starts with a value. It retrieves users with a custom security attribute named `EmployeeId` with a value that starts with `GS`. The filter value is case sensitive. You must add `ConsistencyLevel=eventual` in the request or the header. You must also include `$count=true` to ensure the request is routed correctly.

- Attribute set: `Marketing`
- Attribute: `EmployeeId`
- Filter: EmployeeId startsWith 'GS'

# [PowerShell](#tab/ms-powershell)
[Get-MgUser](/en-us/powershell/module/microsoft.graph.users/get-mguser)

```powershell
$userAttributes = Get-MgUser -CountVariable CountVar -Property "id,displayName,customSecurityAttributes" -Filter "startsWith(customSecurityAttributes/Marketing/EmployeeId,'GS')" -ConsistencyLevel eventual
$userAttributes | select Id,DisplayName,CustomSecurityAttributes
$userAttributes.CustomSecurityAttributes.AdditionalProperties | Format-List
```

```Output
Id                                   DisplayName CustomSecurityAttributes
--                                   ----------- ------------------------
22cc22cc-dd33-ee44-ff55-66aa66aa66aa Chandra     Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
11bb11bb-cc22-dd33-ee44-55ff55ff55ff Jana        Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
33dd33dd-ee44-ff55-aa66-77bb77bb77bb Joe         Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [EmployeeId, GS36348]}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [AppCountry@odata.type, #Collection(String)], [AppCountry, System.Object[]],
        [EmployeeId, GS46982]}

Key   : Engineering
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [Project@odata.type, #Collection(String)], [Project, System.Object[]],
        [ProjectDate, 2024-11-15]…}

Key   : Marketing
Value : {[@odata.type, #microsoft.graph.customSecurityAttributeValue], [EmployeeId, GS45897]}
```

# [Microsoft Graph](#tab/ms-graph)
[List users](/en-us/graph/api/user-list)

```http
GET https://graph.microsoft.com/v1.0/users?$count=true&$select=id,displayName,customSecurityAttributes&$filter=startsWith(customSecurityAttributes/Marketing/EmployeeId,'GS')
ConsistencyLevel: eventual
```

```http
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users(id,displayName,customSecurityAttributes)",
    "@odata.count": 3,
    "value": [
        {
            "id": "22cc22cc-dd33-ee44-ff55-66aa66aa66aa",
            "displayName": "Chandra",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "EmployeeId": "GS36348"
                }
            }
        },
        {
            "id": "11bb11bb-cc22-dd33-ee44-55ff55ff55ff",
            "displayName": "Jana",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "AppCountry@odata.type": "#Collection(String)",
                    "AppCountry": [
                        "Canada",
                        "Mexico"
                    ],
                    "EmployeeId": "GS46982"
                }
            }
        },
        {
            "id": "33dd33dd-ee44-ff55-aa66-77bb77bb77bb",
            "displayName": "Joe",
            "customSecurityAttributes": {
                "Engineering": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "Project@odata.type": "#Collection(String)",
                    "Project": [
                        "Baker",
                        "Alpine"
                    ],
                    "ProjectDate": "2024-11-15",
                    "NumVendors": 8,
                    "CostCenter@odata.type": "#Collection(Int32)",
                    "CostCenter": [
                        1001,
                        1003
                    ],
                    "Certification": false
                },
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "EmployeeId": "GS45897"
                }
            }
        }
    ]
}
```

---

### List all users with a custom security attribute assignment that doesn't equal a value

The following example lists all users with a custom security attribute assignment that doesn't equal a value. It retrieves users with a custom security attribute named `AppCountry` with a value that doesn't equal `Canada`. The filter value is case sensitive. You must add `ConsistencyLevel=eventual` in the request or the header. You must also include `$count=true` to ensure the request is routed correctly.

- Attribute set: `Marketing`
- Attribute: `AppCountry`
- Filter: AppCountry ne 'Canada'

# [PowerShell](#tab/ms-powershell)
[Get-MgUser](/en-us/powershell/module/microsoft.graph.users/get-mguser)

```powershell
$userAttributes = Get-MgUser -CountVariable CountVar -Property "id,displayName,customSecurityAttributes" -Filter "customSecurityAttributes/Marketing/AppCountry ne 'Canada'" -ConsistencyLevel eventual
$userAttributes | select Id,DisplayName,CustomSecurityAttributes
```

```Output
Id                                   DisplayName              CustomSecurityAttributes
--                                   -----------              ------------------------
22cc22cc-dd33-ee44-ff55-66aa66aa66aa Chandra                  Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
44ee44ee-ff55-aa66-bb77-88cc88cc88cc Isabella                 Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
00aa00aa-bb11-cc22-dd33-44ee44ee44ee Alain                    Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
33dd33dd-ee44-ff55-aa66-77bb77bb77bb Joe                      Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
00aa00aa-bb11-cc22-dd33-44ee44ee44ee Dara                     Microsoft.Graph.PowerShell.Models.MicrosoftGraphCustomSecurityAttributeValue
```

# [Microsoft Graph](#tab/ms-graph)
[List users](/en-us/graph/api/user-list)

```http
GET https://graph.microsoft.com/v1.0/users?$count=true&$select=id,displayName,customSecurityAttributes&$filter=customSecurityAttributes/Marketing/AppCountry ne 'Canada'
ConsistencyLevel: eventual
```

```http
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users(id,displayName,customSecurityAttributes)",
    "@odata.count": 47,
    "value": [
        {
            "id": "22cc22cc-dd33-ee44-ff55-66aa66aa66aa",
            "displayName": "Chandra",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "EmployeeId": "GS36348"
                }
            }
        },
        {
            "id": "44ee44ee-ff55-aa66-bb77-88cc88cc88cc",
            "displayName": "Isabella",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "AppCountry@odata.type": "#Collection(String)",
                    "AppCountry": [
                        "France"
                    ]
                }
            }
        },
        {
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
            "displayName": "Alain",
            "customSecurityAttributes": {
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "AppCountry@odata.type": "#Collection(String)",
                    "AppCountry": [
                        "Germany",
                        "Japan"
                    ]
                }
            }
        },
        {
            "id": "33dd33dd-ee44-ff55-aa66-77bb77bb77bb",
            "displayName": "Joe",
            "customSecurityAttributes": {
                "Engineering": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "Project@odata.type": "#Collection(String)",
                    "Project": [
                        "Baker",
                        "Alpine"
                    ],
                    "ProjectDate": "2024-11-15",
                    "NumVendors": 8,
                    "CostCenter@odata.type": "#Collection(Int32)",
                    "CostCenter": [
                        1001,
                        1003
                    ],
                    "Certification": false
                },
                "Marketing": {
                    "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
                    "EmployeeId": "GS45897"
                }
            }
        },
        {
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
            "displayName": "Dara",
            "customSecurityAttributes": null
        }
    ]
}
```

---

### Remove a single-valued custom security attribute assignment from a user

The following example removes a single-valued custom security attribute assignment from a user by setting the value to null.

- Attribute set: `Engineering`
- Attribute: `ProjectDate`
- Attribute value: `null`

# [PowerShell](#tab/ms-powershell)
[Invoke-MgGraphRequest](/en-us/powershell/microsoftgraph/authentication-commands#using-invoke-mggraphrequest)

```powershell
$params = @{
    "customSecurityAttributes" = @{
        "Engineering" = @{
            "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
            "ProjectDate" = $null
        }
    }
}
Invoke-MgGraphRequest -Method PATCH -Uri "https://graph.microsoft.com/v1.0/users/$userId" -Body $params
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "ProjectDate":null
        }
    }
}
```

---

### Remove a multi-valued custom security attribute assignment from a user

The following example removes a multi-valued custom security attribute assignment from a user by setting the value to an empty collection.

- Attribute set: `Engineering`
- Attribute: `Project`
- Attribute value: `[]`

# [PowerShell](#tab/ms-powershell)
[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)

```powershell
$customSecurityAttributes = @{
    "Engineering" = @{
        "@odata.type" = "#Microsoft.DirectoryServices.CustomSecurityAttributeValue"
        "Project" = @()
    }
}
Update-MgUser -UserId $userId -CustomSecurityAttributes $customSecurityAttributes
```

# [Microsoft Graph](#tab/ms-graph)
[Update user](/en-us/graph/api/user-update)

```http
PATCH https://graph.microsoft.com/v1.0/users/{id}
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

---

## Frequently asked questions

**Where are custom security attribute assignments for users supported?**

Custom security attribute assignments for users are supported in Microsoft Entra admin center, PowerShell, and Microsoft Graph APIs. Custom security attribute assignments aren't supported in My Apps or Microsoft 365 admin center.

**Who can view the custom security attributes assigned to a user?**

Only users that have been assigned the Attribute Assignment Administrator or Attribute Assignment Reader roles at tenant scope can view custom security attributes assigned to any users in the tenant. Users can't view the custom security attributes assigned to their own profile or other users. Guests can't view the custom security attributes regardless of the guest permissions set on the tenant.

**Do I need to create an app to add custom security attribute assignments?**

No, custom security attributes can be assigned to user objects without requiring an application.

**Why do I keep getting an error trying to save custom security attribute assignments?**

You don't have permissions to assign custom security attributes to users. Make sure that you are assigned the Attribute Assignment Administrator role.

**Can I assign custom security attributes to guests?**

Yes, custom security attributes can be assigned to members or guests in your tenant.

**Can I assign custom security attributes to directory synced users?**

Yes, directory synced users from an on-premises Active Directory can be assigned custom security attributes.

**Are custom security attribute assignments available for rules for dynamic membership groups?**

No, custom security attributes assigned to users aren't supported for configuring rules for dynamic membership groups.

**Are custom security attributes the same as the custom attributes in B2C tenants?**

No, custom security attributes aren't supported in B2C tenants and aren't related to B2C features.