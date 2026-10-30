---
layout: Conceptual
title: Troubleshoot inaccessible tenants - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/inaccessible-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Instructions about how to unblock a tenant.
ms.topic: troubleshooting
ms.date: 2025-01-15T00:00:00.0000000Z
ms.reviewer: Sunayana
ms.custom: sfi-image-nochange
locale: en-us
document_id: 686bd342-0d16-f681-7ed0-e0702354745c
document_version_independent_id: 686bd342-0d16-f681-7ed0-e0702354745c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/inaccessible-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/inaccessible-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/inaccessible-tenant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: db070987-fe41-3493-510f-d9315157806a
---

# Troubleshoot inaccessible tenants - Microsoft Entra | Microsoft Learn

## Overview

Configured tenants no longer in use might still generate costs for your organization. Making a tenant inaccessible due to inactivity helps reduce unnecessary expenses. This article discusses how to handle an inaccessible tenant, reactivation, and guidance for both administrators and application developers.

If you try to access the tenant, you receive a message similar to the example shown.

Error message `Error message: AADSTS5000225: This tenant has been blocked due to inactivity. To learn more about ...` is expected for tenants inaccessible due to inactivity.

[![Screenshot showing an error when tenant access blocked due to inactivity.](media/tenant-inaccessible/tenant-block.png)](media/tenant-inaccessible/tenant-block.png#lightbox)

Administrators can request a tenant to be reactivated within 20 days of the tenant entering an inactive state. Tenants that remain in this state for longer than 20 days are deleted.

Take the appropriate steps depending on your goals for the tenant and your role in the environment.

## Administrators

If you need to reactivate your tenant:

- Contact Microsoft, see the [global support phone numbers](https://support.microsoft.com/topic/global-customer-service-phone-numbers-c0389ade-5640-e588-8b0e-28de8afeb3f2).
- Refrain from submitting another assistance request while your existing case is in process and until you receive a response with a decision on this case.

If you don't plan to reactivate your tenant:

- The tenant is deleted after 20 days of being inaccessible due to inactivity and it isn't recoverable.
- Review [Microsoft's data protection policies](https://www.microsoft.com/trust-center/privacy/data-management#leave).

## Application owners/developers

- Minimize the number of authentication requests sent to this deactivated tenant until the tenant is reactivated.
- Refrain from submitting another assistance request. Microsoft contacts you once a decision is made.
- Review Microsoft's [data protection policies](https://www.microsoft.com/trust-center/privacy/data-management#leave).