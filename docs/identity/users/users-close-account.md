---
layout: Conceptual
title: Close a work or school account in an unmanaged Microsoft Entra organization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-close-account
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: How to close your work or school account in an unmanaged Microsoft Entra ID.
ms.topic: how-to
ms.date: 2021-05-04T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 84276ec1-e345-25fd-1ca6-a5e2dd407963
document_version_independent_id: c8b3495d-1c71-ea8f-6e0c-99453596b88d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-close-account.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-close-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-close-account.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cd0e63f1-f02c-7437-39b7-1926491762dd
---

# Close a work or school account in an unmanaged Microsoft Entra organization - Microsoft Entra ID | Microsoft Learn

## Overview

If you're a user in an unmanaged organization (tenant) in Microsoft Entra ID, and you no longer need to use apps from that organization or maintain any association with it, you can close your account at any time. An unmanaged organization doesn't have an administrator. Users in an unmanaged organization can close their accounts on their own, without contacting an administrator.

Users in an unmanaged organization are often created during self-service sign-up. An example of this occurring is when an information worker in an organization signs up for a free service. For more information about self-service sign-up, see [What is self-service sign-up for Microsoft Entra ID?](directory-self-service-signup).

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Before you begin

Before you can close your account, you'll need to confirm the following items:

- Make sure you're a user of an unmanaged Microsoft Entra organization. You can't close your account if you belong to a managed organization. If you belong to a managed organization and want to close your account, you must contact your administrator. For information about how to determine whether you belong to an unmanaged organization, see [Delete the user from Unmanaged Tenant](/en-us/power-automate/privacy-dsr-delete#delete-the-user-from-unmanaged-tenant).
- Save any data you want to keep. For information about how to submit an export request, see [Accessing and exporting system-generated logs for Unmanaged Tenants](/en-us/power-platform/admin/powerapps-privacy-dsr-guide-systemlogs#accessing-and-exporting-system-generated-logs-for-unmanaged-tenants).

Warning

Closing your account is irreversible. When you close your account, the service removes all personal data. You won't have access to your account and you'll no longer have access to the data associated with your account.

## Close your account

To close an unmanaged work or school account, follow these steps:

1. Sign in to [close your account](https://portal.azure.com/#blade/Microsoft_AAD_IAM/PrivacyDataRequests), using the account that you want to close.
2. On **My data requests**, select **Close account**.

    ![My data requests - Close account](media/users-close-account/close-account.png)
3. Review the confirmation message and then select **Yes**.

    ![My data requests - Confirm close](media/users-close-account/confirm-close.png)