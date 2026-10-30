---
layout: Conceptual
title: Provision custom security attributes from HR sources - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/provision-custom-security-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to provision custom security attributes from HR sources.
ms.topic: troubleshooting
ms.date: 2025-06-24T00:00:00.0000000Z
ms.reviewer: chmutali
locale: en-us
document_id: 81b7b6f3-ecc4-8692-43eb-430b6b0bb852
document_version_independent_id: 81b7b6f3-ecc4-8692-43eb-430b6b0bb852
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/provision-custom-security-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/provision-custom-security-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/provision-custom-security-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f62ec327-405e-5b76-54b3-723dba17a6ff
---

# Provision custom security attributes from HR sources - Microsoft Entra ID | Microsoft Learn

Custom security attribute provisioning enables customers to set custom security attributes automatically using Microsoft Entra inbound provisioning capabilities. With this feature, you can source values for custom security attributes from authoritative sources, such as those from HR systems. Custom security attribute provisioning supports the following sources: Workday, SAP SuccessFactors, and other integrated HR systems that use API-driven provisioning. The provisioning target is your Microsoft Entra ID tenant.

![Diagram of custom security attributes architecture.](media/provision-custom-security-attributes/about-custom-security-attributes.png)

## Custom security attributes

Custom security attributes in Microsoft Entra ID are business-specific attributes (key value pairs) that you can define and assign to Microsoft Entra objects. These attributes can be used to store information, categorize objects, or enforce fine-tuned access control over specific Azure resources. To learn more about custom security attributes, see [What are custom security attributes in Microsoft Entra ID?](../../fundamentals/custom-security-attributes-overview).

## Prerequisites

To provision custom security attributes, you must meet the following prerequisites:

- A Microsoft Entra ID Premium P1 license to configure one of the following inbound provisioning apps:
    - [Workday to Microsoft Entra ID user provisioning](../saas-apps/workday-inbound-cloud-only-tutorial)
    - [SAP SuccessFactors to Microsoft Entra ID user provisioning](../saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial)
    - [API-driven provisioning to Microsoft Entra ID](inbound-provisioning-api-configure-app)
- Active custom security attributes in your tenant for discovery during the attribute mapping process. Before using this feature, you must [create custom security attribute sets](../../fundamentals/custom-security-attributes-add) in your Microsoft Entra ID tenant. The provisioning service supports setting single free-form and predefined values for custom security attributes of type `String`, `Integer`, and `Boolean`.
- To configure custom security attributes in the attribute mapping of your inbound provisioning app, sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user who is assigned the Microsoft Entra roles of [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) and [Attribute Provisioning Administrator](../role-based-access-control/permissions-reference#attribute-provisioning-administrator):
    - **Application Administrator** is required to create and update the provisioning app.
    - **Attribute Provisioning Administrator** is required to add or remove custom security attributes in the attribute mapping section of the provisioning app.

## Known limitations

- Provisioning multi-valued custom security attributes isn't supported.
- Provisioning deactivated custom security attributes isn't supported.
- With the [Attribute Log Reader](../role-based-access-control/permissions-reference#attribute-log-reader) role, you can't view the custom security attribute value in the provisioning logs.

## Configuring your provisioning app with custom security attributes

Before you begin, [follow these steps](../../fundamentals/custom-security-attributes-add) to add custom security attributes in your Microsoft Entra ID tenant and map custom security attributes in your inbound provisioning app.

### Define custom security attributes in your Microsoft Entra ID tenant

In the [Microsoft Entra admin center](https://entra.microsoft.com), access the option to add custom security attributes from **Entra ID** &gt; **Custom security attributes**. You need to have at least an **Attribute Definition Administrator** role to complete this task.

This example includes custom security attributes that you could add to your tenant. Use the attribute set `HRConfidentialData` and then add the following attributes to:

- EEOStatus (String)
- FLSAStatus (String)
- PayGrade (String)
- PayScaleType (String)
- IsRehire (Boolean)
- EmployeeLevel (Integer)

[![Screenshot of custom security active attributes.](media/provision-custom-security-attributes/active-attributes.png)](media/provision-custom-security-attributes/active-attributes-expanded.png#lightbox)

### Map custom security attributes in your inbound provisioning app

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user who has both [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) and [Attribute Provisioning Administrator](../role-based-access-control/permissions-reference#attribute-provisioning-administrator) role permissions.
2. Go to **Enterprise Applications**, then open your inbound provisioning app.
3. Open the **Provisioning** screen.

    ![Screenshot of the provisioning Overview screen.](media/provision-custom-security-attributes/provisioning-overview.png)

    Note

    This guidance displays screen captures of API-driven provisioning to Microsoft Entra ID. If you’re using Workday or SuccessFactors provisioning apps, then you'll see Workday and SuccessFactors related attributes and configurations.
4. Select **Edit provisioning**.

    ![Screenshot of the Edit provisioning screen.](media/provision-custom-security-attributes/edit-provisioning.png)
5. Select **Attribute mapping** to open the attribute mapping screen.

    ![Screenshot of the attribute mapping screen.](media/provision-custom-security-attributes/attribute-mapping.png)
6. Define source attributes that you want to store sensitive HR data, then select the **Advanced Options** dropdown to open the attribute list.
7. Select **Edit attribute list for API** to identify those attributes that you want to test.

    ![Screenshot of the Edit attribute list for API screen.](media/provision-custom-security-attributes/show-advanced-options.png)

    - Test custom security attributes provisioning with the *Inbound Provisioning* API by defining a SCIM schema namespace: `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa`. Be sure to include the following attributes:

        - `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:EEOStatus`
        - `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:FLSAStatus`
        - `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:PayGrade`
        - `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:PayScaleType`
        - `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:isRehire`
        - `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:EmployeeLevel`

    ![Screenshot of the SCIM schema namespace option.](media/provision-custom-security-attributes/attributes-to-test.png)

    Note

    You can define your own SCIM schema namespace to represent sensitive HR data in your SCIM payload. Make sure it starts with `urn:ietf:params:scim:schemas:extension`.

    - If you're using Workday or SuccessFactors as your HR source, update the attribute list with API expressions to retrieve HR data to store is in the custom security attributes list.
    - If you want to retrieve the same set of HR data from SuccessFactors, use the following API expressions:

        - `$.employmentNav.results[0].jobInfoNav.results[0].eeoClass`
        - `$.employmentNav.results[0].jobInfoNav.results[0].flsaStatus`
        - `$.employmentNav.results[0].jobInfoNav.results[0].payGradeNav.name`
        - `$.employmentNav.results[0].jobInfoNav.results[0].payScaleType`

    [![Screenshot of the API expressions available to select.](media/provision-custom-security-attributes/api-expressions.png)](media/provision-custom-security-attributes/api-expressions-expanded.png#lightbox)
8. Save the schema changes.
9. From the **Attribute mapping** screen, select **Add new mapping**.

    [![Screenshot of the Add new mapping options.](media/provision-custom-security-attributes/add-new-mapping.png)](media/provision-custom-security-attributes/add-new-mapping-expanded.png#lightbox)

    - The custom security attributes display in the format `CustomSecurityAttributes.<AttributeSetName>_<AttributeName>`.
10. Add the following mappings, then save the changes:

    | API source attribute | Microsoft Entra ID target attribute |
    | --- | --- |
    | urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:EEOStatus | CustomSecurityAttributes.HRConfidentialData\_EEOStatus |
    | urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:FLSAStatus | CustomSecurityAttributes.HRConfidentialData\_FLSAStatus |
    | urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:PayGrade | CustomSecurityAttributes.HRConfidentialData\_PayGrade |
    | urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:PayScaleType | CustomSecurityAttributes.HRConfidentialData\_PayScaleType |
    | urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:isRehire | CustomSecurityAttributes.HRConfidentialData\_IsRehire |
    | urn:ietf:params:scim:schemas:extension:microsoft:entra:csa:EmployeeLevel | CustomSecurityAttributes.HRConfidentialData\_EmployeeLevel |

## Test custom security attributes provisioning

Once you've mapped HR source attributes to the custom security attributes, use the following method to test the flow of custom security attributes data. The method you choose depends upon your provisioning app type.

- If your job uses either Workday or SuccessFactors as its source, then use the [On-demand provisioning](provision-on-demand) capability to test the custom security attributes data flow.
- If your job uses API-driven provisioning, then send SCIM bulk payload to the *bulkUpload* API endpoint of your job.

### Test with SuccessFactors provisioning app

In this example, SAP SuccessFactors attributes are mapped to custom security attributes as shown here:

![Screenshot of SAP attribute mapping options.](media/provision-custom-security-attributes/sap-attribute-mapping.png)

1. Open the SuccessFactors provisioning job, then select **Provision on demand**.

![Screenshot of the Microsoft Entra ID overview with Provision on demand selection.](media/provision-custom-security-attributes/provision-on-demand.png)

1. In the **Select a user** box, enter the *personIdExternal* attribute of the user that you want to test.

    The provisioning logs display the custom security attributes that you set.

    ![Screenshot of the Modified attributes screen.](media/provision-custom-security-attributes/modified-attributes.png)

    Note

    The source and target values of custom security attributes are redacted in the provisioning logs.
2. In the **Custom security attributes** screen of the user's Microsoft Entra ID profile, you can view the actual values set for that user. You need at least the [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator) or [Attribute Assignment Reader](../role-based-access-control/permissions-reference#attribute-assignment-reader) role to view this data.

    [![Screenshot of the assigned values column in the Custom security attributes screen.](media/provision-custom-security-attributes/assigned-values.png)](media/provision-custom-security-attributes/assigned-values-expanded.png#lightbox)

### Test with the API-driven provisioning app

1. Create a SCIM bulk request payload that includes values for custom security attributes.

    ![Screenshot of the SCIM bulk request payload code.](media/provision-custom-security-attributes/scim-bulk-request.png)

    - To access the full SCIM payload, see Sample SCIM payload.
2. Copy the *bulkUpload* API URL from the provisioning job overview page.

    ![Screenshot of the Provisioning API endpoint of the payload.](media/provision-custom-security-attributes/provisioning-job-overview.png)
3. Use either [Graph Explorer](inbound-provisioning-api-graph-explorer) or [cURL](inbound-provisioning-api-curl-tutorial), then post the SCIM payload to the *bulkUpload* API endpoint.

    ![Screenshot of the API request and response of the payload.](media/provision-custom-security-attributes/api-request-response.png)

    - If there are no errors in the SCIM payload format, you receive an **Accepted** status.
    - Wait a few minutes, then check the provisioning logs of your API-driven provisioning job.
4. The custom security attribute displays as in the following example.

    ![Screenshot of the custom security attributes entry.](media/provision-custom-security-attributes/entry-export-add.png)

    Note

    The source and target values of custom security attributes get redacted in the provisioning logs. To view the actual values set for the user, go the user's Microsoft Entra ID profile. You view the data in the **Custom security attributes** screen. You need at least the Attribute Assignment Administrator or Attribute Assignment Reader role to view this data.

    [![Screenshot of the Custom security attributes screen for the user.](media/provision-custom-security-attributes/user-custom-security-attributes.png)](media/provision-custom-security-attributes/user-custom-security-attributes-expanded.png#lightbox)

#### Sample SCIM payload with custom security attributes

This sample SCIM bulk request includes custom fields under the extension `urn:ietf:params:scim:schemas:extension:microsoft:entra:csa` that can be mapped to custom security attributes.

```json
{
    "schemas": ["urn:ietf:params:scim:api:messages:2.0:BulkRequest"],
    "Operations": [{
            "method": "POST",
            "bulkId": "897401c2-2de4-4b87-a97f-c02de3bcfc61",
            "path": "/Users",
            "data": {
                "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User",
                    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User",
                    "urn:ietf:params:scim:schemas:extension:microsoft:entra:csa"],
                "id": "2819c223-7f76-453a-919d-413861904646",
                "externalId": "701984",
                "userName": "bjensen@example.com",
                "name": {
                    "formatted": "Ms. Barbara J Jensen, III",
                    "familyName": "Jensen",
                    "givenName": "Barbara",
                    "middleName": "Jane",
                    "honorificPrefix": "Ms.",
                    "honorificSuffix": "III"
                },
                "displayName": "Babs Jensen",
                "nickName": "Babs",
                "emails": [{
                        "value": "bjensen@example.com",
                        "type": "work",
                        "primary": true
                    }
                ],
                "addresses": [{
                        "type": "work",
                        "streetAddress": "234300 Universal City Plaza",
                        "locality": "Hollywood",
                        "region": "CA",
                        "postalCode": "91608",
                        "country": "USA",
                        "formatted": "100 Universal City Plaza\nHollywood, CA 91608 USA",
                        "primary": true
                    }
                ],
                "phoneNumbers": [{
                        "value": "555-555-5555",
                        "type": "work"
                    }
                ],
                "userType": "Employee",
                "title": "Tour Guide",
                "preferredLanguage": "en-US",
                "locale": "en-US",
                "timezone": "America/Los_Angeles",
                "active": true,
                "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
                    "employeeNumber": "701984",
                    "costCenter": "4130",
                    "organization": "Universal Studios",
                    "division": "Theme Park",
                    "department": "Tour Operations",
                    "manager": {
                        "value": "89607",
                        "$ref": "../Users/26118915-6090-4610-87e4-49d8ca9f808d",
                        "displayName": "John Smith"
                    }
                },
                "urn:ietf:params:scim:schemas:extension:microsoft:entra:csa": {
                    "EEOStatus":"Semi-skilled",
                    "FLSAStatus":"Non-exempt",
                    "PayGrade":"IC-Level5",
                    "PayScaleType":"Revenue-based",				"IsRehire": false,				"EmployeeLevel": 64					
                }
            }
        }, {
            "method": "POST",
            "bulkId": "897401c2-2de4-4b87-a97f-c02de3bcfc61",
            "path": "/Users",
            "data": {
                "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User",
                    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User",
                    "urn:ietf:params:scim:schemas:extension:microsoft:entra:csa" ],
                "id": "2819c223-7f76-453a-919d-413861904646",
                "externalId": "701985",
                "userName": "Kjensen@example.com",
                "name": {
                    "formatted": "Ms. Kathy J Jensen, III",
                    "familyName": "Jensen",
                    "givenName": "Kathy",
                    "middleName": "Jane",
                    "honorificPrefix": "Ms.",
                    "honorificSuffix": "III"
                },
                "displayName": "Kathy Jensen",
                "nickName": "Kathy",
                "emails": [{
                        "value": "kjensen@example.com",
                        "type": "work",
                        "primary": true
                    }
                ],
                "addresses": [{
                        "type": "work",
                        "streetAddress": "100 Oracle City Plaza",
                        "locality": "Hollywood",
                        "region": "CA",
                        "postalCode": "91618",
                        "country": "USA",
                        "formatted": "100 Oracle City Plaza\nHollywood, CA 91618 USA",
                        "primary": true
                    }
                ],
                "phoneNumbers": [{
                        "value": "555-555-5545",
                        "type": "work"
                    }
                ],
                "userType": "Employee",
                "title": "Tour Lead",
                "preferredLanguage": "en-US",
                "locale": "en-US",
                "timezone": "America/Los_Angeles",
                "active": true,
                "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
                    "employeeNumber": "701984",
                    "costCenter": "4130",
                    "organization": "Universal Studios",
                    "division": "Theme Park",
                    "department": "Tour Operations",
                    "manager": {
                        "value": "89607",
                        "$ref": "../Users/26118915-6090-4610-87e4-49d8ca9f808d",
                        "displayName": "John Smith"
                    }
                },
                "urn:ietf:params:scim:schemas:extension:microsoft:entra:csa": {
                    "EEOStatus":"Skilled",
                    "FLSAStatus":"Exempt",
                    "PayGrade":"Manager-Level2",
                    "PayScaleType":"Profit-based",				"IsRehire": true,				"EmployeeLevel": 63
                }
                
            }
        }
    ],
    "failOnErrors": null
}
```

## Provision custom security attributes for hybrid users

Hybrid users are provisioned from HR systems first in on-premises Active Directory and then synchronized to Microsoft Entra ID using Entra Connect Sync or Cloud Sync. Custom security attributes can be assigned to hybrid users, and these attributes are only present on the Microsoft Entra ID profile of the hybrid user.

This section describes the provisioning topology to auto provision custom security attributes for hybrid users. It uses Workday as the trusted HR source. However, the same topology can also be used with SuccessFactors and API-driven provisioning.

Let’s say Workday is your HR system of record for identities. To set custom security attributes on hybrid users sourced from Workday, configure two provisioning apps:

- **Workday to on-premises Active Directory provisioning:** This provisioning app creates and updates hybrid users in on-premises Active Directory. It only processes normal attributes from Workday.
- **Workday to Microsoft Entra ID provisioning:** Configure this provisioning app to only process **Update** operations and restrict the attribute mapping to only include custom security attributes as target attributes.

With this topology, here is how the end-to-end flow works:

![Flow diagram of how custom security attribute mapping works for hybrid users.](media/provision-custom-security-attributes/custom-security-attributes-end-to-end-flow.png)

1. The **Workday-to-AD provisioning** app imports the core user profile from Workday.
2. The app creates/updates the user account in on-premises Active Directory using the Employee ID as the matching identifier.
3. Microsoft Entra Connect Sync / Cloud Sync synchronizes the user profile to Microsoft Entra ID.
4. If you’ve configured Workday Writeback, email or phone number information is written back to Workday.
5. The **Workday-to-Microsoft Entra ID provisioning** app is configured to only process updates and set confidential attributes as custom security attributes. Use **Edit schema** under the **Advanced Options** dropdown to remove default attribute mappings like `accountEnabled` and `isSoftDeleted` that are not relevant in this scenario.

![Screenshot of attribute mapping for hybrid users.](media/provision-custom-security-attributes/attribute-mapping-hybrid.png)

This configuration assigns the custom security attributes to hybrid users synchronized to Microsoft Entra ID from on-premises Active Directory.

Note

The above configuration relies on three different sync cycles to complete in a specific order. If the hybrid user profile is not available in Microsoft Entra ID, when the **Workday-to-Microsoft Entra ID provisioning** job runs, then the update operation fails, and is retried during the next execution. If you’re using the **API-driven provisioning-to-Microsoft Entra ID** app, then you have better control on timing the execution of the custom security attribute update.

## API permissions for custom security attributes provisioning

This feature introduces the following new Graph API permissions. This functionality enables you to access and modify provisioning app schemas that contain custom security attribute mappings, either directly or on behalf of the signed-in user.

1. **CustomSecAttributeProvisioning.ReadWrite.All**: This permission grants the calling app ability to read and write the attribute mapping that contains custom security attributes. This permission with `Application.ReadWrite.OwnedBy` or `Synchronization.ReadWrite.All` or `Application.ReadWrite.All` (from least to highest privilege) is required to edit a provisioning app that contains custom security attributes mappings. This permission enables you to get the complete schema that includes the custom security attributes and to update or reset the schema with custom security attributes.
2. **CustomSecAttributeProvisioning.Read.All**: This permission grants the calling app ability to read the attribute mapping and the provisioning logs that contain custom security attributes. This permission with `Synchronization.Read.All` or `Application.Read.All` (from least to highest privilege) is required to view the custom security attributes names and values in the protected resources.

If an app doesn't have the `CustomSecAttributeProvisioning.ReadWrite.All` permission or the `CustomSecAttributeProvisioning.Read.All` permission, it's not able to access or modify provisioning apps that contain custom security attributes. Instead, an error message or redacted data appears.

## Troubleshoot custom security attributes provisioning

| Issue | Troubleshoot steps |
| --- | --- |
| Custom Security Attributes aren't showing up in the *Target attributes* mapping drop-down list. | - Ensure that you're adding custom security attributes to a provisioning app that supports custom security attributes.  - Ensure that the logged-in user is assigned the role [Attribute Provisioning Administrator](../role-based-access-control/permissions-reference#attribute-provisioning-administrator) (for edit access) or [Attribute Provisioning Reader](../role-based-access-control/permissions-reference#attribute-provisioning-reader) (for view access). |
| Error returned when you reset or update the provisioning app schema. `HTTP 403 Forbidden - InsufficientAccountPermission Provisioning schema has custom security attributes. The account does not have sufficient permissions to perform this operation.` | Ensure that the logged-in user is assigned the role [Attribute Provisioning Administrator](../role-based-access-control/permissions-reference#attribute-provisioning-administrator). |
| Unable to remove custom security attributes present in an attribute mapping. | Ensure that the logged in user is assigned the role [Attribute Provisioning Administrator](../role-based-access-control/permissions-reference#attribute-provisioning-administrator). |
| The attribute mapping table has rows where the string `redacted` appears under source and target attributes. | This behavior is by design if the logged-in user doesn't have [Attribute Provisioning Administrator](../role-based-access-control/permissions-reference#attribute-provisioning-administrator) or [Attribute Provisioning Reader](../role-based-access-control/permissions-reference#attribute-provisioning-reader) role. Assigning one of these roles displays the custom security attribute mappings. |
| Error returned `The provisioning service does not support setting custom security attributes of type boolean and integer. Unable to set CSA attribute`. | Remove the integer/Boolean custom security attribute from the provisioning app attribute mapping. |
| Error returned `The provisioning service does not support setting custom security attributes that are deactivated. Unable to set CSA attribute <attribute name>`. | There was an attempt to update a deactivated custom security attribute. Remove the deactivated custom security attribute from the provisioning app attribute mapping. |