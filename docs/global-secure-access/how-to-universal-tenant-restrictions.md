---
layout: Conceptual
title: Global Secure Access and Universal Tenant Restrictions - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-universal-tenant-restrictions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn about how Global Secure Access helps secure access to your corporate network by restricting access to external tenants.
ms.topic: how-to
ms.date: 2026-07-29T00:00:00.0000000Z
ms.reviewer: dhruvinrshah
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1c527722-0c12-6428-798f-835ba0ace45c
document_version_independent_id: bf796e9d-d5f8-14f6-21fb-ccf7663cdc5b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-universal-tenant-restrictions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-universal-tenant-restrictions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-universal-tenant-restrictions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 15e43df2-c760-1217-2f4e-930da3166962
---

# Global Secure Access and Universal Tenant Restrictions - Global Secure Access | Microsoft Learn

## Overview

Universal Tenant Restrictions (UTR) enhance the functionality of [tenant restrictions v2 (TRv2)](https://aka.ms/tenant-restrictions-enforcement). UTR applies tenant restrictions policies to any devices with the GSA client or on the GSA Remote Network, without having to steer network traffic through company-managed proxy service.

When you enable UTR, Microsoft Entra ID tenant restrictions policy is applied to all applications protected by Entra ID. Users on your devices with GSA or GSA Remote Networks can only sign in to tenants and applications authorized in your TRv2 policy.

## Prerequisites

- Administrators who interact with Global Secure Access features must have the [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) to manage those features.
- Global Secure Access requires a license. For details, see [Licensing overview](overview-what-is-global-secure-access#licensing-overview).
- You must enable a [Microsoft traffic profile](concept-microsoft-traffic-profile). Fully qualified domain names (FQDNs) and IP addresses of Entra ID services must be configured to 'Tunnel'.
- You must deploy [Global Secure Access clients](concept-clients) or configure [remote network connectivity](concept-remote-network-connectivity).

## Configure the TRv2 policy

Before you can use UTR, you must configure both the default tenant restrictions and tenant restrictions for any specific partners.

For more information about configuring these policies, see [Set up tenant restrictions v2](/en-us/azure/active-directory/external-identities/tenant-restrictions-v2).

## Enable Universal Tenant Restrictions

After you create the TRv2 policies, you can use Global Secure Access to apply tagging for TRv2. An administrator who has both the [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference) and [Security Administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator) roles must take the following steps to enable enforcement with Global Secure Access:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Go to **Global Secure Access** &gt; **Settings** &gt; **Session Management**.
3. On the **Universal Tenant Restrictions** tab, turn on the **Enable Tenant Restrictions for Microsoft Entra ID and Microsoft Graph** toggle.

## Try universal tenant restrictions

Tenant restrictions aren't enforced when a user (or a guest user) tries to access resources in the tenant where the policies are configured. Tenant restrictions v2 policies are processed only when an identity from a different tenant attempts to sign in or accesses resources.

For example, if you configure a tenant restrictions v2 policy in the tenant contoso.com to block all organizations except fabrikam.com, the policy applies according to this table:

| User | Type | Tenant | Tenant restrictions v2 policy processed? | Authenticated access allowed? |
| --- | --- | --- | --- | --- |
| `alice@contoso.com` | Member | contoso.com | No (same tenant) | Yes |
| `alice@fabrikam.com` | Member | fabrikam.com | Yes | Yes (tenant allowed by policy) |
| `bob@northwindtraders.com` | Member | northwindtraders.com | Yes | No (tenant not allowed by policy) |
| `bob_northwindtraders.com#EXT#@contoso.com` | Guest | contoso.com | No (guest user) | Yes |

## Known limitations

If you enabled universal tenant restrictions and you access the Microsoft Entra admin center for a tenant on the tenant restrictions v2 allow list, you might get an "Access denied" error. To correct this error, add the following feature flag to the Microsoft Entra admin center: `?feature.msaljs=true&exp.msaljsexp=true`.

For example, assume that you work for Contoso. Fabrikam, a partner tenant, is on the allow list. You might get the error message for the Fabrikam tenant's Microsoft Entra admin center.

If you received the "Access denied" error message for the URL `https://entra.microsoft.com/`, add the feature flag as follows: `https://entra.microsoft.com/?feature.msaljs%253Dtrue%2526exp.msaljsexp%253Dtrue#home`.

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).