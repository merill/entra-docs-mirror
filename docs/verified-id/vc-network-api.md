---
layout: Conceptual
title: Microsoft Entra Verified ID Network API - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/vc-network-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to use the Microsoft Entra Verified ID Network API
documentationCenter: ''
ms.topic: reference
ms.date: 2025-01-30T00:00:00.0000000Z
locale: en-us
document_id: c9c9f112-7562-b258-c347-414e13136e29
document_version_independent_id: bae8f594-c267-d351-f054-526c0ea54693
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/vc-network-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/vc-network-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/vc-network-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: c2d1a31d-8a70-180a-6035-8e873ec7139c
---

# Microsoft Entra Verified ID Network API - Microsoft Entra Verified ID | Microsoft Learn

## Overview

The Microsoft Entra Verified ID Network API enables you to search for published credentials in the [Microsoft Entra Verified ID Network](how-use-vcnetwork).

Note

The API is intended for developers comfortable with RESTful APIs.

## Base URL

The Microsoft Entra Verified ID Network API is served over HTTPS. All URLs referenced in the documentation have the following base: `https://verifiedid.did.msidentity.com`.

## Authentication

The API is protected through Microsoft Entra ID and uses OAuth2 bearer tokens. Grant the app registration the API Permission for `Verifiable Credentials Service Admin` and use scope `6a8b4b39-c021-437c-b060-5a14a3fd65f3/full_access` when acquiring the access token.

## Search for issuers

Use this API to search for issuers available in the Microsoft Entra Verified ID Network. You can search for issuers by their **linked domain** name. The value supplied for the `filter` parameter is used to find issuers that onboarded to Microsoft Entra Verified ID and have a verified linked domain. Currently you can only filter by `linkeddomainurls` and with operator `like`. There's a maximum of 15 issuers in the response.

#### HTTP request

`GET /v1.0/verifiableCredentialsNetwork/authorities?filter=linkeddomainurls%20like%20Woodgrove`

#### Request headers

| Header | Value |
| --- | --- |
| Authorization | Bearer (token). Required |
| Content-Type | application/json |

#### Request parameters

| Parameter | Value |
| --- | --- |
| filter | linkeddomainurls like Woodgrove |

#### Return message

```json
HTTP/1.1 200 OK
Content-type: application/json

[
  {
    "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
    "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
    "did": "did:web:bank.woodgrove.com...<SNIP>...",
    "name": "WoodgroveBank",
    "linkedDomainUrls": [
      "https://bank.woodgrove.com/"
    ]
  },
  {
    "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
    "tenantId": "bbbbcccc-1111-dddd-2222-eeee3333ffff",
    "did": "did:web:woodgrove.com...<SNIP>...",
    "name": "Woodgrove",
    "linkedDomainUrls": [
      "https://woodgrove.com/"
    ]
  }
]
```

## Search for published credential types by an issuer

This API is used to search for published credential types for a specific issuer. You need to know the issuer's `tenantId` and `issuerId`. The return message is a collection of published credential types and their respective claims. There's a maximum of 100 credential types in the response.

#### HTTP request

`GET /v1.0/tenants/:tenantId/verifiableCredentialsNetwork/authorities/:issuerId/contracts/`

#### Request headers

| Header | Value |
| --- | --- |
| Authorization | Bearer (token). Required |
| Content-Type | application/json |

#### Request parameters

| Parameter | Value |
| --- | --- |
| tenantId | TenantId obtained from the search by linked domain name |
| issuerId | IssuerId obtained from the search by linked domain name |

#### Return message

```json
HTTP/1.1 200 OK
Content-type: application/json

[
  {
    "name": "Verified employee 1",
    "types": [
      "VerifiedEmployee"
    ],
    "claims": [
      "displayName",
      "givenName",
      "jobTitle",
      "preferredLanguage",
      "surname",
      "mail",
      "revocationId",
      "photo"
    ]
  }
]
```