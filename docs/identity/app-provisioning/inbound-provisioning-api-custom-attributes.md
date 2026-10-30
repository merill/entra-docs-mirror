---
layout: Conceptual
title: Extend API-driven provisioning to sync custom attributes - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/inbound-provisioning-api-custom-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to extend API-driven inbound provisioning to sync custom attributes.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: cmmdesai
ms.custom: sfi-image-nochange
locale: en-us
document_id: a59dad83-c2cb-fc27-bfa0-2dbf91303166
document_version_independent_id: a9a1c464-5de2-e955-dbd1-3f5418c9f293
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/inbound-provisioning-api-custom-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/inbound-provisioning-api-custom-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/inbound-provisioning-api-custom-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ead80ac7-602b-feff-3cff-91c764f67195
---

# Extend API-driven provisioning to sync custom attributes - Microsoft Entra ID | Microsoft Learn

By default, API-driven provisioning apps support processing attributes that are part of the standard SCIM Core User and Enterprise User schema. Your system of record may have custom attributes that you may want to include as part of API-driven provisioning. This advanced tutorial describes how to extend your API-driven provisioning app to process additional custom attributes.

Note

Before trying this advanced scenario, we recommend verifying that your out-of-the-box provisioning app configuration works as expected using one of the following API clients [Graph Explorer](inbound-provisioning-api-graph-explorer), [cURL](inbound-provisioning-api-curl-tutorial).

## Example scenario

You have configured API-driven provisioning app. You're provisioning app is successfully consuming the attributes that are part of the standard SCIM Core User and Enterprise User schema and provisioning users in Microsoft Entra ID. You now want to send two custom attributes `HireDate` and `JobCode` from your HR system to the inbound provisioning API endpoint. You'd like to map these two custom attributes to Microsoft Entra attributes `employeeHireDate` and `jobTitle`.

## Step 1 - Extend the provisioning app schema

In this step, we'll add the two attributes "HireDate" and "JobCode" that are not part of the standard SCIM schema to the provisioning app and use them in the provisioning data flow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](https://go.microsoft.com/fwlink/?linkid=2247823).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Open your API-driven provisioning app.
4. Open the **Provisioning** blade.
5. Click on the **Edit Provisioning** button.
6. Expand the **Mappings** section and click on the attribute mapping link. [![Screenshot of edit attribute mapping.](media/inbound-provisioning-api-custom-attributes/edit-attribute-mapping.png)](media/inbound-provisioning-api-custom-attributes/edit-attribute-mapping.png#lightbox)
7. On the **Attribute Mapping** page, select the **Advanced Options** dropdown and then select **Edit target User attributes**. [![Screenshot of edit API attribute list.](media/inbound-provisioning-api-custom-attributes/edit-api-attribute-list.png)](media/inbound-provisioning-api-custom-attributes/edit-api-attribute-list.png#lightbox)
8. Scroll down to the end of the **Edit Attribute List** page.
9. Add the following two attributes to the list as SCIM schema extensions. You can use your own SCIM schema namespace. `urn:ietf:params:scim:schemas:extension:contoso:1.0:User:HireDate``urn:ietf:params:scim:schemas:extension:contoso:1.0:User:JobCode`[![Screenshot of adding custom attributes.](media/inbound-provisioning-api-custom-attributes/add-custom-attributes.png)](media/inbound-provisioning-api-custom-attributes/add-custom-attributes.png#lightbox)
10. **Save** your changes

Note

If you'd like to add only a few additional attributes to the provisioning app, use Microsoft Entra admin center to extend the schema. If you'd like to add more custom attributes (let's say 20+ attributes), then we recommend using the [`UpdateSchema` mode of the CSV2SCIM PowerShell script](inbound-provisioning-api-powershell#extending-provisioning-job-schema) which automates the above manual process.

## Step 2 - Map the custom attributes

Let's now add these extensions to the provisioning app attribute mapping.

1. Click on the **Add New Mapping** link on the **Attribute mapping** page. [![Screenshot of add new mapping.](media/inbound-provisioning-api-custom-attributes/add-new-mapping.png)](media/inbound-provisioning-api-custom-attributes/add-new-mapping.png#lightbox)
2. Map the `urn:ietf:params:scim:schemas:extension:contoso:1.0:User:HireDate` attribute to `employeeHireDate`. Click **OK**. [![Screenshot of hire date mapping.](media/inbound-provisioning-api-custom-attributes/hire-date-mapping.png)](media/inbound-provisioning-api-custom-attributes/hire-date-mapping.png#lightbox)
3. Next, select the existing mapping for `title` and click on it to edit the mapping.
4. Edit the attribute mapping to an expression that will include the `urn:ietf:params:scim:schemas:extension:contoso:1.0:User:JobCode` as part of the `jobTitle` Microsoft Entra attribute.

    ```
      Join("", [title], "(", [urn:ietf:params:scim:schemas:extension:contoso:1.0:User:JobCode], ")")
    ```

    [![Screenshot of job title mapping.](media/inbound-provisioning-api-custom-attributes/job-title-mapping.png)](media/inbound-provisioning-api-custom-attributes/job-title-mapping.png#lightbox)

    With this expression mapping, if the `title` is "Tour Lead" and `JobCode`is "TL-1001", then the Microsoft Entra attribute `jobTitle` will be set to "Tour Lead (TL-1001)".
5. Save the attribute mappings.

## Step 3 - Upload bulk request with custom attributes

1. Open your API client (Graph Explorer / cURL).
2. Copy-paste the bulk request with custom attributes.
3. Send the bulk request to your provisioning API endpoint URL. [![Screenshot of bulk upload request.](media/inbound-provisioning-api-custom-attributes/upload-bulk-request.png)](media/inbound-provisioning-api-custom-attributes/upload-bulk-request.png#lightbox)
4. After some time, you can check the provisioning logs to verify the attribute change. [![Screenshot of provisioning logs.](media/inbound-provisioning-api-custom-attributes/verify-provisioning-logs.png)](media/inbound-provisioning-api-custom-attributes/verify-provisioning-logs.png#lightbox)
5. You can also verify the change in the Microsoft Entra user profile. The value for `Employee hire date` reflects your tenant time zone. [![Screenshot of user profile.](media/inbound-provisioning-api-custom-attributes/verify-user-profile.png)](media/inbound-provisioning-api-custom-attributes/verify-user-profile.png#lightbox)

## Appendix

### Bulk request with custom attributes

The bulk request includes the custom attributes configured in the steps above.

**Request body**

```http
{
    "schemas": ["urn:ietf:params:scim:api:messages:2.0:BulkRequest"],
    "Operations": [
    {
        "method": "POST",
        "bulkId": "701984",
        "path": "/Users",
        "data": {
            "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User",
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User",
            "urn:ietf:params:scim:schemas:extension:contoso:1.0:User"],
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
            "emails": [
            {
              "value": "bjensen@example.com",
              "type": "work",
              "primary": true
            }
            ],
            "addresses": [
            {
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
            "phoneNumbers": [
            {
              "value": "555-555-5555",
              "type": "work"
            }
            ],
            "userType": "Employee",
            "title": "Tour Guide",
            "preferredLanguage": "en-US",
            "locale": "en-US",
            "timezone": "America/Los_Angeles",
            "active":true,
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
                "employeeNumber": "701984",
                "costCenter": "4130",
                "organization": "Universal Studios",
                "division": "Theme Park",
                "department": "Tour Operations",
                "manager": {
                  "value": "89607",
                  "displayName": "John Smith"
                 }
            },
            "urn:ietf:params:scim:schemas:extension:contoso:1.0:User": {
                "HireDate": "2021-05-01T00:00:00-05:00",
                "JobCode": "TG-1001"
            }            
        }
    },
    {
        "method": "POST",
        "bulkId": "701985",
        "path": "/Users",
        "data": {
            "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User",
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User",
            "urn:ietf:params:scim:schemas:extension:contoso:1.0:User"],
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
            "emails": [
            {
              "value": "kjensen@example.com",
              "type": "work",
              "primary": true
            }
            ],
            "addresses": [
            {
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
            "phoneNumbers": [
            {
              "value": "555-555-5545",
              "type": "work"
            }
            ],
            "userType": "Employee",
            "title": "Tour Lead",
            "preferredLanguage": "en-US",
            "locale": "en-US",
            "timezone": "America/Los_Angeles",
            "active":true,
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
              "employeeNumber": "701984",
              "costCenter": "4130",
              "organization": "Universal Studios",
              "division": "Theme Park",
              "department": "Tour Operations",
              "manager": {
                "value": "701984",
                "displayName": "Barbara Jensen"
             }
            },
            "urn:ietf:params:scim:schemas:extension:contoso:1.0:User": {
                "HireDate": "2022-07-15T00:00:00-05:00",
                "JobCode": "TL-1003"
            }            
        }
    }
],
    "failOnErrors": null
}
```