---
layout: Conceptual
title: Service limits and restrictions - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/reference-service-limits
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about the service limits and restrictions in an external tenant.
ms.topic: reference
ms.date: 2025-07-07T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: be7fee42-fd78-bd4d-a524-5fe35f1cc031
document_version_independent_id: be7fee42-fd78-bd4d-a524-5fe35f1cc031
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/reference-service-limits.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/reference-service-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/reference-service-limits.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 89b2b233-cf9c-550e-ccc3-db4a909dc13e
---

# Service limits and restrictions - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article outlines the service limits and usage constraints of Microsoft Entra External ID for external tenants, which is Microsoft’s latest customer identity and access management (CIAM) solution. If you’re looking for the full set of Microsoft Entra ID service limits, see [Microsoft Entra service limits and restrictions](/en-us/entra/identity/users/directory-service-limits-restrictions).

## User/consumption related limits

The number of users able to authenticate through an external tenant is gated through request limits. The following table illustrates the request limits for your tenant.

| Category | Limit |
| --- | --- |
| Maximum requests per IP per external tenant | 20 per second |
| Maximum requests per external tenant | 200 per second |
| Maximum requests per external trial tenant | 20 per second |

## Endpoint request usage

Microsoft Entra External ID is compliant with [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749), [OpenID Connect (OIDC)](https://openid.net/certification/) protocols. The following table lists the endpoints and the number of requests consumed by each endpoint.

| Endpoint | Endpoint type | Requests consumed |
| --- | --- | --- |
| /oauth2/v2.0/authorize | Dynamic | Varies |
| /oauth2/v2.0/token | Static | 1 |
| /.well-known/openid-config | Static | 1 |
| /discovery/v2.0/keys | Static | 1 |
| /oauth2/v2.0/logout | Static | 1 |

## Token issuance rate

Each type of user flow provides a unique user experience and consumes a different number of requests. The token issuance rate of a user flow is dependent on the number of requests consumed by both the static and dynamic endpoints. The following table shows the number of requests consumed at a dynamic endpoint for each user flow.

| User flow | Requests consumed |
| --- | --- |
| Sign up | 6 |
| Sign in | 4 |
| Password reset | 4 |

When you add more features to a user flow, such as multifactor authentication, more requests are consumed. The following table shows how many additional requests are consumed when a user interacts with one of these features.

| Feature | Additional requests consumed |
| --- | --- |
| Email one-time password | 2 |

To obtain the token issuance rate per second for your user flow:

1. Use the previous tables to add the total number of requests consumed at the dynamic endpoint.
2. Add the number of requests expected at the static endpoints based on your application type.
3. Use the following formula to calculate the token issuance rate per second.

```
Tokens/sec = 200/requests-consumed
```

## Configuration limits for Microsoft Entra ID for external configuration tenants

The following table lists the administrative configuration limits in the Microsoft Entra External ID service.

| Category | Limit |
| --- | --- |
| Number of scopes per application | 1000 |
| Number of custom attributes per user | 100 |
| Number of redirect URLs per application | 100 |
| Number of sign-out URLs per application | 1 |
| String limit per attribute | 250 Chars |
| Number of external tenants per subscription | 20 |
| Total number of objects (user accounts and applications) per trial tenant (can't be extended) | 10000 |
| Total number of objects (user accounts and applications) per tenant. If you want to increase this limit, contact [Microsoft Support](/en-us/entra/identity-platform/developer-support-help-options?toc=%2Fentra%2Fexternal-id%2Ftoc.json&amp;bc=%2Fentra%2Fexternal-id%2Fbreadcrumb%2Ftoc.json#create-an-azure-support-request). | 300,000 |
| Number of [custom authentication extensions](/en-us/entra/identity-platform/custom-extension-overview) | 100 |
| Number of event listener policies | 249 |
| Maximum custom authentication extension timeout | 2,000 ms |
| Maximum custom authentication extension retries | 1 |
| Maximum custom authentication extension requests per second, combined across all extensions in the tenant | 50 |

## Telephony throttling limits

The following table lists the service limits we implement to prevent outages and slowdowns. [Learn more](../../identity/authentication/concept-mfa-telephony-fraud)

| Limit | Texts every 15 minutes | Texts every 60 minutes | Texts every 24 hours | Texts every seven days |
| --- | --- | --- | --- | --- |
| Limits based on IP address | 100 texts | 300 texts | 500 texts | No limit |
| Limits based on phone number | 15 texts | 20 texts | 30 texts | 50 texts |
| Limits based on tenant | 500 texts | 1500 texts | 5,000 texts | No limit |

## Capability support by scale and deployment mode

The following table shows which Microsoft Graph capabilities are available based on your tenant's directory scale and deployment mode.

| Capability area | Standard mode\* | HSC mode |
| --- | --- | --- |
| Advanced directory queries (filtering, sorting, count, search, transitive membership) | Supported | Not supported |
| Change-based (delta) queries | Supported | Not supported |
| SCIM outbound user provisioning | Supported | Not supported |

\* The features listed in this table are supported in standard mode for tenants with up to 15 million directory objects.

Note

These capabilities aren't available in HSC mode regardless of directory size. HSC mode prioritizes stability and throughput at scale over query-heavy or event-driven directory operations.