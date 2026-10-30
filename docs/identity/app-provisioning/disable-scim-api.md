---
layout: Conceptual
title: Disable the SCIM Provisioning API in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/disable-scim-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: Learn how to disable the SCIM Provisioning API feature in the Microsoft Entra admin center to stop all API access and billing.
ms.topic: how-to
ms.date: 2026-03-31T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: 39dab906-7e06-8adf-6987-8825cab7f8ad
document_version_independent_id: 39dab906-7e06-8adf-6987-8825cab7f8ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/disable-scim-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/disable-scim-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/disable-scim-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 7465e260-c800-083e-dbb8-8a27f47afc02
---

# Disable the SCIM Provisioning API in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

If you no longer need programmatic SCIM access, you can turn off the SCIM Provisioning API to stop all API access and billing.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. In the left navigation, expand **ID Governance** and select **Dashboard**.
3. On the Dashboard page, locate the **SCIM Provisioning API** tile and select **Edit**.
4. In the **SCIM Provisioning API** pane, select **Turn off**.
5. Confirm the action when prompted. After the feature is turned off, all SCIM API calls to the tenant return an error and billing stops.

## Verify that the SCIM API is disabled

Use the following steps to validate that the disable operation was successful.

1. Obtain an app-only access token that previously worked for SCIM API calls.
2. Send a GET request to any SCIM endpoint. For example, call the user read endpoint:

```http
GET https://graph.microsoft.com/rp/scim/users/{id}
Authorization: Bearer {token}
Accept: application/json
```

1. Confirm that the API returns **HTTP 400 Bad Request**.
2. Confirm that the response includes an error message similar to the following:

```text
No 'scimapiconsumptions' resource found for TenantId: {tenantId}. Please ensure 'SCIM Provisioning API' feature is enabled and only one 'scimapiconsumptions' resource exists.
```

If you receive this error, the SCIM APIs are now disabled in your tenant.