---
layout: Conceptual
title: Configure multitenant organization policy templates using Microsoft Graph API - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/multi-tenant-organization-configure-templates
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.reviewer: hafowler
ms.service: entra-id
ms.subservice: multitenant-organizations
manager: dougeby
description: Configure cross-tenant access and identity synchronization policy templates for multitenant organizations using the Microsoft Graph API. Covers automatic redemption, inbound sync, and template management.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 1d89d378-6396-0f39-b3da-1cba4f915c8f
document_version_independent_id: 397ee545-b655-6eb4-6e39-5941d4d332d9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/multi-tenant-organization-configure-templates.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/multi-tenant-organization-configure-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/multi-tenant-organization-configure-templates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 50477c1f-aa2b-4e02-795a-5d5a441b8673
---

# Configure multitenant organization policy templates using Microsoft Graph API - Microsoft Entra ID | Microsoft Learn

## Overview

This article describes how to configure a policy template for your multitenant organization.

## Prerequisites

- For license information, see [License requirements](multi-tenant-organization-overview#license-requirements).
- [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) role to configure cross-tenant access settings and templates for the multitenant organization.
- [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator) role to consent to required permissions.

## Cross-tenant access policy partner template

The [cross-tenant access partner configuration](../../external-id/cross-tenant-access-settings-b2b-collaboration) handles trust settings and automatic user consent settings between partner tenants. For example, you can use these settings to trust multifactor authentication claims for inbound users from the target partner tenant. With the template in an unconfigured state, partner configurations for partner tenants in the multitenant organization won't be amended, with all trust settings passed through from default settings. However, if you configure the template, then partner configurations will be amended corresponding to the policy template.

### Configure inbound and outbound automatic redemption

To specify which trust settings and automatic user consent settings to apply to your policy template, use the [Update multiTenantOrganizationPartnerConfigurationTemplate](/en-us/graph/api/multitenantorganizationpartnerconfigurationtemplate-update) API. If you create or join a multitenant organization using the Microsoft 365 admin center, this configuration is handled automatically.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationPartnerConfiguration

{
    "inboundTrust": {
        "isMfaAccepted": true,
        "isCompliantDeviceAccepted": true,
        "isHybridAzureADJoinedDeviceAccepted": true
    },
    "automaticUserConsentSettings": {
        "inboundAllowed": true,
        "outboundAllowed": true
    },
    "templateApplicationLevel": "newPartners,existingPartners"
}
```

### Disable the partner configuration template for existing partners

To apply this template only to new multitenant organization members and exclude existing partners, set the `templateApplicationLevel` parameter to new partners only.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationPartnerConfiguration

{
    "inboundTrust": {
        "isMfaAccepted": true,
        "isCompliantDeviceAccepted": true,
        "isHybridAzureADJoinedDeviceAccepted": true
    },
    "automaticUserConsentSettings": {
        "inboundAllowed": true,
        "outboundAllowed": true
    },
    "templateApplicationLevel": "newPartners"
}
```

### Disable the partner configuration template completely

To disable the template completely, set the `templateApplicationLevel` parameter to null.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationPartnerConfiguration

{
    "inboundTrust": {
        "isMfaAccepted": true,
        "isCompliantDeviceAccepted": true,
        "isHybridAzureADJoinedDeviceAccepted": true
    },
    "automaticUserConsentSettings": {
        "inboundAllowed": true,
        "outboundAllowed": true
    },
    "templateApplicationLevel": ""
}
```

### Reset the partner configuration template

To reset the template to its default state (decline all trust and automatic user consent), use the [multiTenantOrganizationPartnerConfigurationTemplate: resetToDefaultSettings](/en-us/graph/api/multitenantorganizationpartnerconfigurationtemplate-resettodefaultsettings) API.

```http
POST https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationPartnerConfiguration/resetToDefaultSettings
```

## Cross-tenant synchronization template

The identity synchronization policy governs [cross-tenant synchronization](cross-tenant-synchronization-overview), which allows you to share users and groups across tenants in your organization. You can use these settings to allow inbound user synchronization. With the template in an unconfigured state, the identity synchronization policy for partner tenants in the multitenant organization won't be amended. However, if you configure the template, then the identity synchronization policy will be amended corresponding to the policy template.

### Configure inbound user synchronization

To allow inbound user synchronization in the policy template, use the [Update multiTenantOrganizationIdentitySyncPolicyTemplate](/en-us/graph/api/multitenantorganizationidentitysyncpolicytemplate-update) API. If you create or join a multitenant organization using the Microsoft 365 admin center, this configuration is handled automatically.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationIdentitySynchronization

{
    "userSyncInbound": {
        "isSyncAllowed": true
    },
    "templateApplicationLevel": "newPartners,existingPartners"
}
```

### Disable the synchronization template for existing partners

To apply this template only to new multitenant organization members and exclude existing partners, set the `templateApplicationLevel` parameter to new partners only.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationIdentitySynchronization

{
    "userSyncInbound": {
        "isSyncAllowed": true
    },
    "templateApplicationLevel": "newPartners"
}
```

### Disable the synchronization template completely

To disable the template completely, set the `templateApplicationLevel` parameter to null.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationIdentitySynchronization

{
    "userSyncInbound": {
        "isSyncAllowed": true
    },
    "templateApplicationLevel": ""
}
```

### Reset the synchronization template

To reset the template to its default state (decline inbound synchronization), use the [multiTenantOrganizationIdentitySyncPolicyTemplate: resetToDefaultSettings](/en-us/graph/api/multitenantorganizationidentitysyncpolicytemplate-resettodefaultsettings) API.

**Request**

```http
POST https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/templates/multiTenantOrganizationIdentitySynchronization/resetToDefaultSettings
```