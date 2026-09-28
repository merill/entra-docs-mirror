---
layout: Conceptual
title: Convert external users to internal users - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/convert-external-users-internal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: You can convert users from external to internal without the need to recreate them.
ms.date: 2025-01-06T00:00:00.0000000Z
ms.topic: how-to
ms.workload: identity
ms.custom: sfi-image-nochange
ms.reviewer: yuank
locale: en-us
document_id: 87999564-0514-26cf-1b85-86f4a59d4c69
document_version_independent_id: 87999564-0514-26cf-1b85-86f4a59d4c69
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/convert-external-users-internal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/convert-external-users-internal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/convert-external-users-internal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: f8c3a06c-0d0a-2cef-42bc-44ef321d9df4
---

# Convert external users to internal users - Microsoft Entra ID | Microsoft Learn

## Overview

Enterprises, such as those going through reorganizations, mergers, and acquisitions, sometimes need to change the way they work with some or all of their existing users. In some cases, administrators need to change existing external users into internal ones.

External user conversion handles the conversion of external users into internal users without the need to delete existing user objects and create new ones. The preservation of the user objects allows users to keep their original account so that their access isn’t disrupted. A converted user's account maintains its history of activities intact as their relationship with the host organization changes.

- **Internal users** are users who authenticate with the local tenant.
- **External users** are users who authenticate via a method not managed by the host organization, such as another organization's Microsoft Entra ID, Google federation, or Microsoft account. Many external users have a *userType* of `guest`, but there's no formal relation between *userType* and how a user signs in. External users who have a *userType* of `member`, could also be eligible for conversion.

You can convert external users using [Microsoft Graph API](https://graph.microsoft.com) or the Microsoft Entra admin center.

## Convert external users

It's important to understand that the *userType* for `member` versus `guest` doesn't indicate where a user authenticates; instead, it only defines the level of permissions that a user has in the current tenant. You can update the *userType* for your users, but that alone doesn't change the users' external versus internal state. To change external users to internal users, see synced user conversion.

There are two types of external users that you can convert to internal:

- Cloud-only users
- Synced users

### Cloud user conversion

When a cloud user is converted from external to internal, administrators must specify a *UPN* and *password* for the user. Converting cloud users to synced users ensures that the user can authenticate with the current tenant.

### Synced user conversion

Synced user conversion allows you to convert a user from external to internal in Microsoft Entra ID. You can use [Microsoft Entra Connect](../hybrid/connect/whatis-azure-ad-connect) to synchronize your on-premises identities. When you convert a user from an external user to an internal user, the source of authority for the user continues to be on-premises, but the user authenticates as an internal user.

*Synced users* are users synced from on-premises. As these accounts are managed at the source, administrators are unable to specify the UPN for these users.

- Synced users where the tenant has Password Hash Sync (PHS) enabled, administrators are blocked from setting a new password during conversion.
- If the tenant uses federated authentication, administrators are blocked from setting a new password for synced users during conversion.
- In cases where the tenant is managed, meaning it uses cloud authentication, and the tenant doesn't have PHS enabled, administrators are required to specify a password during conversion.

## Test external user conversions

When testing external user conversions, use test accounts or accounts that wouldn't create a disruption if they were to become unavailable.

### Requirements

- Converting external users to internal users requires an account with at least the [user administrator](../role-based-access-control/permissions-reference#user-administrator) role assigned.
- Only users configured with an authentication method external to the host organization are eligible for conversion.

### Convert an external user

You can convert external users, such as cloud-only and synced users, to internal users using the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select an external user.
4. Select **Convert to internal user**.

    ![Screenshot showing the user properties with a red box around the Convert to Internal user option.](media/convert-external-users-internal/user-properties.png)
5. In the **Convert to internal user** section, you need to finalize a couple of steps:

    1. Provide a **user principal name (UPN)**. This value is the new UPN value for the user. For cloud-only users, the UPN domain must be one that is nonfederated. For on-premises synced users, you don't need to provide a UPN. The user continues to use the on-premises credentials.
    2. Check the box if you would like an autogenerated password.
    3. Check the box for **Change email address** to specify an optional new email address for cloud users.

    ![Screenshot showing the last set of options that must be chosen prior to converting an external user to an internal user.](media/convert-external-users-internal/convert.png)
6. After reviewing the options and making your selected choices, choose **Convert**.