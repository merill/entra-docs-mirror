---
layout: Conceptual
title: Known issues in external tenants - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/troubleshooting-known-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about known issues in external tenants.
ms.topic: concept-article
ms.date: 2025-07-07T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 0bf9d718-d2b0-5028-beab-f8c1690c01cd
document_version_independent_id: 634f32d6-a186-bf61-adbe-8baa1c67d21e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/troubleshooting-known-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/troubleshooting-known-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/troubleshooting-known-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 634c1931-1f09-6252-2787-6977cf08a400
---

# Known issues in external tenants - Microsoft Entra External ID | Microsoft Learn

This article describes known issues that you may experience when you use Microsoft Entra External ID for your external-facing apps, and provides help to resolve these issues.

## Tenant creation and management

### Using your admin email to create a local customer account prevents you from administering the tenant

If you're the admin who created the external tenant and you use the same email address as your admin account to create a local customer account in that same tenant, you can't sign in directly to the tenant with admin privileges.

**Cause**: Using your tenant admin email to create a customer account via self-service sign-up creates a second user with the same email address, but with customer-level privileges. When you sign in to the tenant via `https://entra.microsoft.com/<tenantID>` or `<tenantName>.onmicrosoft.com`, the least-privileged account takes precedence, and you're signed in as the customer instead of the admin. You have insufficient privileges to manage the tenant.

**Workaround**: Take one of the following actions.

- When creating a local customer account, use a different email address than the one used by the admin who created the tenant.
- If you've already created a customer account with the same email address as the admin, sign out of the admin center, and then use `https://entra.microsoft.com` instead of `https://entra.microsoft.com/<tenantID>` or `<tenantName>.onmicrosoft.com` to sign in with the correct admin account.

## Token version in Web API

### Error when running a web API

When you create your own web API in an external tenant (without using the app creation scripts in the web API samples), and then run it and send an access token, you enable logging and see the following error:

`IDX20804: Unable to retrieve document from: https://<tenant>.ciamlogin.com/common/discovery/keys`

**Cause**: This error occurs if you haven't set the accepted access token version to 2.

**Workaround**: Do the following.

1. Go to the app registration for your application.
2. Choose to edit the manifest.
3. Change the **accessTokenAcceptedVersion** property from null to **2**.