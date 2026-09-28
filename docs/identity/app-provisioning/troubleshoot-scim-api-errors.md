---
layout: Conceptual
title: Troubleshoot Microsoft Entra ID SCIM API errors - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/troubleshoot-scim-api-errors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: Troubleshoot common errors encountered when calling Microsoft Entra ID SCIM APIs for user and group management.
ms.topic: troubleshooting
ms.date: 2026-03-31T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: d3a70d7a-a63a-1f15-0a17-e1ceff93c412
document_version_independent_id: d3a70d7a-a63a-1f15-0a17-e1ceff93c412
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/troubleshoot-scim-api-errors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/troubleshoot-scim-api-errors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/troubleshoot-scim-api-errors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c8a387c3-7df1-90a6-5170-0d478ac84396
---

# Troubleshoot Microsoft Entra ID SCIM API errors - Microsoft Entra ID | Microsoft Learn

This article helps troubleshoot common issues encountered when calling the Microsoft Entra ID SCIM APIs for user and group management.

## Error: 401 – Invalid authentication token

### Symptoms

SCIM API requests return:

```
HTTP 401 Unauthorized
```

### Cause

The request does not include a valid access token in the HTTP `Authorization` header.

### Resolution

1. Confirm that the request includes a Bearer token in the HTTP `Authorization` header.
2. Validate the access token by using https://jwt.ms/
3. Verify the following token claims:
    - `iat`
    - `exp`
4. If the issue persists:
    - Collect details of the failing API call
    - Create a support ticket

## Error: 403 – Forbidden

### Symptoms

SCIM API requests return:

```
HTTP 403 Forbidden
```

### Cause

The app registration used by the SCIM API client does not have the required API permissions or does not have admin consent granted.

### Resolution

1. Review the app registration used by the SCIM API client.
2. Confirm that the Microsoft Graph API permissions as documented in [Microsoft Entra ID SCIM API reference](entra-id-scim-api-reference) are assigned:
3. Confirm that **Admin Consent** has been granted for all assigned permissions.
4. If the issue persists:
    - Collect API request details
    - Create a support ticket

## Error: 404 – Resource not found

### Symptoms

The following API calls return:

```
HTTP 404 Not Found
```

- `GET /users/{id}`
- `GET /groups/{id}`

### Cause

The `{id}` value in the request does not resolve to a valid user or group object in the Microsoft Entra ID tenant.

### Resolution

1. Confirm that the `{id}` value exists in the Microsoft Entra ID tenant.
2. If the issue persists:
    - Collect API request details
    - Create a support ticket

## Error: 400 – Bad request

### Symptoms

SCIM API requests return:

```
HTTP 400 Bad Request
```

This error may occur during:

- User create or update operations (`POST /Users` or `PATCH /Users`)
- Group create or update operations (`POST /Groups` or `PATCH /Groups`)
- User or Group filter queries (`GET`)

### Cause

The request payload or query parameters do not meet the constraints defined for the SCIM API or reference invalid SCIM schema attributes.

### Resolution

1. For `POST`operations:
    - Ensure all required attributes are included in the request payload.
2. For `PATCH`operations:
    - Ensure that the request complies with SCIM API constraints.
3. For `GET`operations:
    - Confirm that only supported API filters are used.
4. Ensure that request attributes map to valid Microsoft Entra SCIM schema attributes.
5. Resend the request with corrections.
6. If the issue persists:
    - Collect API request details
    - Create a support ticket

## Error: 400 – SCIM Provisioning API feature not enabled

### Symptoms

SCIM API requests return:

```http
HTTP 400 Bad Request
```

```json
{
  "schemas": [
    "urn:ietf:params:scim:api:messages:2.0:Error"
  ],
  "detail": "No 'scimapiconsumptions' resource found for TenantId: <tenant-id>. Please ensure 'SCIM Provisioning API' feature is enabled and only one 'scimapiconsumptions' resource exists.",
  "status": "400"
}
```

### Cause

The SCIM Provisioning API feature is not enabled in the Microsoft Entra admin center, or the billing subscription required for the feature has not been linked. The Azure resource is created when an administrator turns on the feature and links an Azure subscription for billing. Without this resource, the SCIM service rejects all API calls.

### Resolution

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Navigate to **ID Governance** &gt; **Dashboard**.
3. On the **SCIM Provisioning API** tile, select **Get Started** (or **Edit** if previously configured).
4. Link an Azure subscription, select a resource group, and select **Turn on**.
5. After the feature is enabled, retry the SCIM API request.

For detailed steps, see [Enable the SCIM Provisioning API](enable-scim-api).

## Error: 500 – Internal server error

### Symptoms

SCIM API requests return:

```
HTTP 500 Internal Server Error
```

### Cause

An unexpected server-side error occurred while processing the SCIM API request.

### Resolution

1. Collect details of the failing API call.
2. Create a support ticket.

## Error: 504 – Gateway timeout

### Symptoms

SCIM API requests return:

```
HTTP 504 Gateway Timeout
```

### Cause

Intermittent 504 responses may be returned by the SCIM service.

### Resolution

1. Collect details of the failing API calls and time window for the errors.
2. Create a support ticket if the issue persists.

## SCIM API error code reference

The following table lists all error codes that the Microsoft Entra ID SCIM APIs can return. Use this table to identify the error and its cause when troubleshooting SCIM API requests.

Note

Not all error codes apply to every API endpoint. For example, `BadRequest` (400) interpretation could vary depending on the request payload associated with the API endpoint. Refer to the [Microsoft Entra ID SCIM API reference](entra-id-scim-api-reference) for endpoint-specific details.

| Error | Condition | HTTP Status Code |
| --- | --- | --- |
| BadRequest | Request payload or query parameters don't meet SCIM API constraints, required attributes are missing, or invalid SCIM schema attributes are referenced. | 400 |
| BadRequest | SCIM Provisioning API feature is not enabled or the billing subscription is not linked. The error detail references a missing Azure resource. | 400 |
| BadRequest | HTTP Accept header for application/json is missing | 400 |
| InvalidAuthenticationToken | Access token is empty or invalid. | 401 |
| InsufficientPrivileges | Insufficient permission to complete the operation. | 403 |
| ResourceNotFound | Invalid URN or the specified resource doesn't exist in the tenant. | 404 |
| InternalServerException | Service failed to process the request. | 500 |
| GatewayTimeout | The SCIM service didn't respond within the expected time. | 504 |