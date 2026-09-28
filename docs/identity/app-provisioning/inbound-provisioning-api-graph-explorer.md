---
layout: Conceptual
title: Quickstart API-driven inbound provisioning with Graph Explorer - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/inbound-provisioning-api-graph-explorer
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to get started quickly with API-driven inbound provisioning using Graph Explorer
ms.topic: how-to
ms.date: 2025-07-24T00:00:00.0000000Z
ms.reviewer: cmmdesai
locale: en-us
document_id: af907958-4514-58a5-ee5b-cba49cb05316
document_version_independent_id: 732a3501-c3ca-aa77-4ce6-ea87fbdd1bc1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/inbound-provisioning-api-graph-explorer.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/inbound-provisioning-api-graph-explorer
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/inbound-provisioning-api-graph-explorer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 927bedba-a2a4-b01f-46de-faa90f960c4f
---

# Quickstart API-driven inbound provisioning with Graph Explorer - Microsoft Entra ID | Microsoft Learn

This tutorial describes how you can quickly test [API-driven inbound provisioning](inbound-provisioning-api-concepts) with Microsoft Graph Explorer.

## Prerequisite

- You configured [API-driven inbound provisioning app](inbound-provisioning-api-configure-app).

Note

This provisioning API is primarily meant for use within an application or service. Tenant admins can either configure a service principal or managed identity to grant permission to perform the upload. There's no separate user-assignable Microsoft Entra built-in directory role for this API. Outside of applications that acquired `SynchronizationData-User.Upload` permission with admin consent, admin users with the [User Administrator](../role-based-access-control/permissions-reference#user-administrator) role can invoke the API. This tutorial shows how you can test the API with a User Administrator role in your test setup.

## Upload user data to the inbound provisioning API

1. Open a new browser tab or browser window.
2. Launch the URL https://aka.ms/ge to access Microsoft Graph Explorer.
3. Select the user profile icon to sign in.

    [![Image showing the user profile icon.](media/inbound-provisioning-api-graph-explorer/provisioning-user-profile-icon.png)](media/inbound-provisioning-api-graph-explorer/provisioning-user-profile-icon.png#lightbox)
4. Complete the login process with a user account that has [User Administrator](../role-based-access-control/permissions-reference#user-administrator) role access.
5. Upon successful login, the Tenant information shows your tenant name.

    [![Screenshot of Tenant name.](media/inbound-provisioning-api-graph-explorer/provisioning-tenant-name.png)](media/inbound-provisioning-api-graph-explorer/provisioning-tenant-name.png#lightbox)

    You're now ready to invoke the API.
6. In the API request panel, set the HTTP request type to **POST**.
7. Copy and paste the provisioning API endpoint retrieved from the provisioning app overview page.
8. Under the Request headers panel, add a new key value pair of **Content-Type = application/scim+json**. [![Screenshot of request header panel.](media/inbound-provisioning-api-graph-explorer/provisioning-request-header-panel.png)](media/inbound-provisioning-api-graph-explorer/provisioning-request-header-panel.png#lightbox)
9. Under the **Request body** panel, copy-paste the bulk request with SCIM Enterprise User Schema
10. Select on the **Run query** button to send the request to the provisioning API endpoint.
11. If the request is sent successfully, you'll get an `Accepted 202` response from the API endpoint.
12. Open the **Response headers** panel and copy the URL value of the location attribute. This points to the provisioning logs API endpoint that you can query to check the provisioning status of users present in the bulk request.

## Verify processing of bulk request payload

You can verify the processing either from the Microsoft Entra admin center or using Graph Explorer.

### Verify processing from Microsoft Entra admin center

1. Log in to [Microsoft Entra admin center](https://entra.microsoft.com) with at least [Application Administrator](https://go.microsoft.com/fwlink/?linkid=2247823) login credentials.
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Under all applications, use the search filter text box to find and open your API-driven provisioning application.
4. Open the Provisioning blade. The landing page displays the status of the last run.
5. Select **View provisioning logs** to open the provisioning logs blade. Alternatively, you can select the menu option **Monitor** &gt; **Provisioning logs**.

    [![Screenshot of provisioning logs in menu.](media/inbound-provisioning-api-curl-tutorial/access-provisioning-logs.png)](media/inbound-provisioning-api-curl-tutorial/access-provisioning-logs.png#lightbox)
6. Select any record in the provisioning logs to view additional processing details.
7. The provisioning log details screen displays all the steps executed for a specific user.

    - Under the **Import from API** step, see details of user data extracted from the bulk request.
    - The **Match user** step shows details of any user match based on the matching identifier. If a user match happens, then the provisioning service performs an update operation. If there's no user match, then the provisioning service performs a create operation.
    - The **Determine if User is in scope** step shows details of scoping filter evaluation. By default, all users are processed. If you set a scoping filter (example, process only users belonging to the Sales department), the evaluation details of the scoping filter displays in this step.
    - The **Provision User** step calls out the final processing step and changes applied to the user account.
    - Use the **Modified properties** tab to view attribute updates.

### Verify processing using provisioning logs API in Graph Explorer

You can inspect the processing using the provisioning logs API URL returned as part of the location response header in the provisioning API call.

1. In the Graph Explorer, **Request URL** text box copy-paste the location URL returned by the provisioning API endpoint or you can construct it using the format: `https://graph.microsoft.com/beta/auditLogs/provisioning/?$filter=jobid eq '<jobId>'` where you can retrieve the `jobId` from the provisioning app overview page.
2. Use the method **GET** and select **Run query** to retrieve the provisioning logs. By default, the response returned contains all log records.
3. You can set more filters to only retrieve data after a certain time frame or with a specific status value. `https://graph.microsoft.com/beta/auditLogs/provisioning/?$filter=jobid eq '<jobId> and statusInfo/status eq 'failure' and activityDateTime ge 2022-10-10T09:47:34Z` You can also check the status of the user by the `externalId` value used in your source system that is used as the source anchor / joining property. `https://graph.microsoft.com/beta/auditLogs/provisioning/?$filter=jobid eq '<jobId>' and sourceIdentity/id eq '701984'`

## Appendix

### Bulk request with SCIM Enterprise User Schema

The bulk request that follows uses the SCIM standard Core User and Enterprise User schema.

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