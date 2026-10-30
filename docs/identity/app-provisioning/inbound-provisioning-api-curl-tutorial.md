---
layout: Conceptual
title: Quickstart for API-driven inbound provisioning with cURL - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/inbound-provisioning-api-curl-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This tutorial provides step-by-step instructions so you can get started with API-driven inbound provisioning using cURL.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: cmmdesai
locale: en-us
document_id: de216396-0262-c3f0-fb2f-86db613cd1cf
document_version_independent_id: 6ad22cff-3675-47ed-05d0-9c599e92bb95
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/inbound-provisioning-api-curl-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/inbound-provisioning-api-curl-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/inbound-provisioning-api-curl-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 2566ff86-459d-c401-b15c-3b8444b7b734
---

# Quickstart for API-driven inbound provisioning with cURL - Microsoft Entra ID | Microsoft Learn

## Introduction

[cURL](https://curl.se/) is a popular, free, open-source, command-line tool used by API developers, and it's [available by default on Windows 10/11](https://curl.se/windows/microsoft.html). This tutorial describes how you can quickly test [API-driven inbound provisioning](inbound-provisioning-api-concepts) with cURL.

## Pre-requisites

- You configured [API-driven inbound provisioning app](inbound-provisioning-api-configure-app).
- You [configured a service principal and it has access](inbound-provisioning-api-grant-access) to the inbound provisioning API. Make note of the `ClientId` and `ClientSecret` of your service principal app for use in this tutorial.

## Upload user data to the inbound provisioning API

1. Retrieve the **client\_id** and **client\_secret** of the service principal that has access to the inbound provisioning API.
2. Use OAuth **client\_credentials** grant flow to get an access token. Replace the variables `[yourClientId]`, `[yourClientSecret]` and `[yourTenantId]` with values applicable to your setup and run the following cURL command. Copy the access token value generated 

    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=[yourClientId]&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=[yourClientSecret]&grant_type=client_credentials" "https://login.microsoftonline.com/[yourTenantId]/oauth2/v2.0/token"
    ```
3. Copy the bulk request with SCIM Enterprise User Schema and save the contents in a file called `scim-bulk-upload-users.json`.
4. Replace the variable `[InboundProvisioningAPIEndpoint]` with the provisioning API endpoint associated with your provisioning app. Use the `[AccessToken]` value from the previous step and run the following curl command to upload the bulk request to the provisioning API endpoint. 

    ```
    curl -v "[InboundProvisioningAPIEndpoint]" -d @scim-bulk-upload-users.json -H "Authorization: Bearer [AccessToken]" -H "Content-Type: application/scim+json"
    ```
5. Upon successful upload, you receive HTTP 202 Accepted response code.
6. The provisioning service starts processing the bulk request payload immediately and you can see the provisioning details by accessing the provisioning logs of the inbound provisioning app.

## Verify processing of the bulk request payload

1. Log in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](https://go.microsoft.com/fwlink/?linkid=2247823).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Under all applications, use the search filter text box to find and open your API-driven provisioning application.
4. Open the Provisioning blade. The landing page displays the status of the last run.
5. Select **View provisioning logs** to open the provisioning logs blade. Alternatively, you can select the menu option **Monitor** &gt; **Provisioning logs**.

    [![Screenshot of provisioning logs in menu.](media/inbound-provisioning-api-curl-tutorial/access-provisioning-logs.png)](media/inbound-provisioning-api-curl-tutorial/access-provisioning-logs.png#lightbox)
6. Select any record in the provisioning logs to view more processing details.
7. The provisioning log details screen displays all the steps executed for a specific user.

    - Under the **Import from API** step, see details of user data extracted from the bulk request.
    - The **Match user** step shows details of any user match based on the matching identifier. If a user match happens, then the provisioning service performs an update operation. If there's no user match, then the provisioning service performs a create operation.
    - The **Determine if User is in scope** step shows details of scoping filter evaluation. By default, all users are processed. If you set a scoping filter (example, process only users belonging to the Sales department), the evaluation details of the scoping filter displays in this step.
    - The **Provision User** step calls out the final processing step and changes applied to the user account.
    - Use the **Modified properties** tab to view attribute updates.

## Appendix

View this section for information on the bulk request with SCIM Enterprise User Schema.

### Bulk request with SCIM Enterprise User Schema

The bulk request shown as follows uses the SCIM standard Core User and Enterprise User Schema.

**Request body**

```http
{
    "schemas": ["urn:ietf:params:scim:api:messages:2.0:BulkRequest"],
    "Operations": [
    {
        "method": "POST",
        "bulkId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
        "path": "/Users",
        "data": {
            "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User",
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"],
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
              "streetAddress": "100 Universal City Plaza",
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
            }
        }
    },
    {
        "method": "POST",
        "bulkId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
        "path": "/Users",
        "data": {
            "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User",
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"],
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
                 "employeeNumber": "701985",
                 "costCenter": "4130",
                 "organization": "Universal Studios",
                 "division": "Theme Park",
                 "department": "Tour Operations",
                 "manager": {
                     "value": "701984",
                     "displayName": "Barbara Jensen"
                 }
            }
        }
    }
],
    "failOnErrors": null
}
```