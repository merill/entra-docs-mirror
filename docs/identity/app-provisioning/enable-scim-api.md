---
layout: Conceptual
title: Enable the SCIM Provisioning API in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/enable-scim-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: Learn how to enable the SCIM Provisioning API feature in the Microsoft Entra admin center and link an Azure subscription for billing.
ms.topic: how-to
ms.date: 2026-09-04T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: 727a7c2c-87fc-af4f-f7bc-c2a8f36ea315
document_version_independent_id: 727a7c2c-87fc-af4f-f7bc-c2a8f36ea315
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/enable-scim-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/enable-scim-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/enable-scim-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 83cbb882-2053-3d40-abfb-aee74f961a66
---

# Enable the SCIM Provisioning API in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes how to enable the SCIM Provisioning API feature in the Microsoft Entra admin center. Once enabled, you can use the SCIM 2.0 protocol to automate the management of users and groups in your Microsoft Entra ID tenant.

Note

By enabling this feature, Microsoft Entra ID acts as the SCIM service provider (server), allowing external SCIM‑compatible clients—such as HR apps, identity platforms, orchestration tools, or custom automation frameworks—to provision and manage users and groups in Entra using standard SCIM operations at scale. This feature is intended for direct programmatic access to the SCIM API; if you want to use Entra ID's built-in [app provisioning](user-provisioning), [HR-driven provisioning](what-is-hr-driven-provisioning) or [API-driven provisioning](inbound-provisioning-api-concepts) capabilities, you don't need to enable it. For more details refer to [SCIM support in Entra ID](scim-support-in-entra-id).

For the full API reference, see [Microsoft Entra ID SCIM API reference](entra-id-scim-api-reference).

## Prerequisites

- An Entra ID P1 license or any license that contains Entra ID P1 (e.g., Entra ID P2, Microsoft 365 E3, Microsoft 365 E5, etc.)
- An active Azure subscription to link for billing.
- An admin with the [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) or [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) role to create an app registration with the permissions required to invoke the SCIM API.
- An admin with the [Billing Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#billing-administrator) role to enable SCIM API billing and link the Azure subscription.

## License and billing

The SCIM Provisioning API is a paid add-on that requires a subscription and billing configuration:

- **Cost:** See [API call pricing](https://aka.ms/EntraSCIMAPIPricing).
- **Billing:** Monthly, through a linked Azure subscription.

## Enable the SCIM Provisioning API

Use the following steps to turn on the SCIM Provisioning API from the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. In the left navigation, expand **ID Governance** and select **Dashboard**.
3. On the Dashboard page, locate the **SCIM Provisioning API** tile and select **Get Started**. If the feature was previously configured, the tile shows the current status and an **Edit** button instead.
4. In the **SCIM Provisioning API** pane that opens on the right side:

    1. Under **Link subscription**, select an **Azure subscription** from the dropdown.
    2. Select an existing **Resource group** or select **Create new** to create one.
    3. Review the **Billing Unit** details. Every SCIM Provisioning API call is billed.
    4. Select **Turn on**.
5. After the feature is enabled, the SCIM Provisioning API tile on the Dashboard updates to show **SCIM Provisioning API is enabled**.

## Set up credentials for the SCIM API client

After you enable the SCIM Provisioning API, set up the credentials that your SCIM client uses to authenticate. You can choose one of the following options.

Note

SCIM APIs operate exclusively in application context (app-only token) and do not support delegated, user-on-behalf-of scenarios. As a result, properties that require delegated authorization, such as `assignedLabels`, cannot be updated via SCIM.

### Option 1: Register an application (client credentials flow)

Register an application in your Microsoft Entra tenant, grant the required application permissions, and use the [OAuth 2.0 client credentials grant flow](/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow) to obtain an access token.

1. [Register an application with the Microsoft identity platform](/en-us/graph/auth-register-app-v2). Save the following values from the app registration:

    - The application ID (referred to as Object ID on the Microsoft Entra admin center).
    - A client secret (application password), a certificate, or a federated identity credential.
2. Under **API permissions**, select **Microsoft Graph** &gt; **Application permissions** and grant one or more of the following permissions depending on how you plan to use the SCIM APIs:

    | Permission | Description |
    | --- | --- |
    | `User.ReadBasic.All` | Least privileged read-only access to users' basic profile properties. Filtering is limited to properties in the basic profile. |
    | `User.Read.All` | Read-only access to all user properties supported by the SCIM API. |
    | `User.Create` | Create users without permission to update existing users. |
    | `User.ReadUpdate.All` | Read and update users without permission to create or delete users. |
    | `User.ReadWrite.All` | Read and write access to users. |
    | `User-Mail.ReadWrite.All` | Least privileged permission to update **emails[type eq "other"].value**, which maps to the *otherMails* user property. |
    | `User-Phone.ReadWrite.All` | Least privileged permission to update **phoneNumbers[type eq "mobile"].value** and **phoneNumbers[type eq "work"].value**, which map to the *mobilePhone* and *businessPhones* user properties, respectively. |
    | `User.EnableDisableAccount.All` | Least privileged permission to update the **active** SCIM attribute, which maps to the *accountEnabled* user property. |
    | `Group.Read.All` | Read-only access to groups. |
    | `Group.Create` | Create groups without permission to update existing groups. |
    | `GroupMember.ReadWrite.All` | Read and update group memberships without permission to update group properties. |
    | `Group.ReadWrite.All` | Read and write access to groups. |
    | `CustomSecAttributeAssignment.Read.All` | Read-only access to Custom Security Attributes on users. |
    | `CustomSecAttributeAssignment.ReadWrite.All` | Read and write access to Custom Security Attributes on users. |
    | `CustomSecAttributeDefinition.Read.All` | Read access to Custom Security Attributes schema. |
    | `User-LifeCycleInfo.ReadWrite.All` | Update lifecycle attributes like `employeeLeaveDateTime`. |

    Note

    For more information about these permissions, see the [Microsoft Graph permissions reference](/en-us/graph/permissions-reference).
3. Grant **Admin consent** for all assigned permissions.
4. Use the following HTTP request to obtain an access token, replacing the placeholder values to match your environment. For production usage, it's highly recommended to use client certificate or managed identity for authentication.

    **Request:**

    ```http
    POST https://login.microsoftonline.com/{tenant_id}/oauth2/v2.0/token HTTP/1.1
    Host: login.microsoftonline.com
    Content-Type: application/x-www-form-urlencoded
    
    client_id={client_id}&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret={client_secret}&grant_type=client_credentials
    ```

    **Response (200 OK):**

    ```json
    {
      "token_type": "Bearer",
      "expires_in": 3599,
      "access_token": "eyJhbGciOiJIUzI1NiJ9…"
    }
    ```
5. Include the access token in the `Authorization` header (Bearer scheme) when calling the SCIM API.

### Option 2: Use a managed identity

Assign a [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (system-assigned or user-assigned) to the Azure resource that hosts your SCIM client, and grant it the same Microsoft Graph application permissions listed in Option 1.

1. Enable a managed identity on your Azure resource (for example, a virtual machine or Azure Function).
2. Grant the managed identity the required Microsoft Graph application permissions listed in the table in Option 1.
3. At runtime, acquire an access token from the managed identity endpoint and include it in the `Authorization` header when calling the SCIM API.

For more information on acquiring tokens with a managed identity, see [How to use managed identities for Azure resources on an Azure VM to acquire an access token](/en-us/entra/identity/managed-identities-azure-resources/how-to-use-vm-token).

## Invoke SCIM API endpoints

After you set up credentials and obtain an access token, you can start calling SCIM API endpoints. The following example retrieves the service provider configuration for the Microsoft Entra ID SCIM implementation.

**Request:**

```http
GET https://graph.microsoft.com/rp/scim/serviceproviderconfig HTTP/1.1
Authorization: Bearer <access_token>
Accept: application/json
Host: graph.microsoft.com
```

**Response (200 OK):**

```json
{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:ServiceProviderConfig"],
  "documentationUri": "/graph/overview",
  "pagination": {
    "cursor": true,
    "index": false,
    "defaultPaginationMethod": "cursor",
    "defaultPageSize": 100,
    "maxPageSize": 1000
  },
  "patch": {
    "supported": true
  },
  "bulk": {
    "supported": false,
    "maxOperations": 0,
    "maxPayloadSize": 0
  },
  "filter": {
    "supported": true,
    "maxResults": 200
  }
}
```

For the full list of supported SCIM operations including user and group management, see the [Microsoft Entra ID SCIM API reference](entra-id-scim-api-reference).

## View SCIM API billing information

SCIM API usage is billed through the Azure subscription and resource group you linked when you enabled the feature. You can view accumulated costs and usage forecasts in the Azure portal using the **Cost analysis** blade.

### Prerequisites for viewing billing

You must have one of the following Azure roles on the linked resource group to access Cost analysis:

- **Owner**
- **Contributor**
- **Reader**
- **Cost Management Reader**

### Steps to view billing

1. Sign in to the [Azure portal](https://portal.azure.com).
2. In the top search bar, search for **Resource groups** and select it.
3. From the list of resource groups, select the resource group you linked when enabling SCIM API billing.
4. In the left navigation pane, expand **Cost Management** and select **Cost analysis**.
5. In the Cost analysis view:

    - Set the **Scope** to your resource group.
    - Set the **View** to **AccumulatedCosts**.
    - Set the date range to the month you want to review.
6. The chart shows your accumulated SCIM API spend over the selected period. The summary cards at the top show:

    - **Actual cost (USD)** – charges billed so far in the current period.
    - **Forecast** – projected total cost for the period based on current usage.
7. Use the breakdown tiles at the bottom to view costs by **Service name**, **Location**, and **Resource**. SCIM API charges appear under **Microsoft Entra** as the service name.