---
layout: Conceptual
title: Troubleshooting the configured permissions limits - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/troubleshoot-required-resource-access-limits
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn why some apps may exceed the limits on configured permissions and how to address this issue.
manager: pmwongera
ms.custom: 
ms.date: 2024-04-10T00:00:00.0000000Z
ms.reviewer: phsignor, jawoods
ms.topic: troubleshooting
locale: en-us
document_id: d61c18ad-1d42-7e6f-d8dc-d05648ca5c2f
document_version_independent_id: 4e6e15ba-ada3-6920-4c65-5f40a8d85dd2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/troubleshoot-required-resource-access-limits.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/troubleshoot-required-resource-access-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/troubleshoot-required-resource-access-limits.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a1210309-e63f-88df-ad30-93db9653f08e
---

# Troubleshooting the configured permissions limits - Microsoft identity platform | Microsoft Learn

The `RequiredResourceAccess` collection (RRA) on an application object contains all the configured API permissions that an app requires for its default consent request. This collection has various limits depending on which types of identities the app supports. For more information on the limits for supported account types, see [Validation differences by supported account types](supported-accounts-validation).

The limits on maximum permissions were updated in May 2022, so some apps may have more permissions in their RRA than are now allowed. In addition, apps that change their supported account types after configuring permissions may exceed the limits of the new setting. When apps exceed the configured permissions limit, no new permissions may be added until the number of permissions in the `RequiredResourceAccess` collection is brought back under the limits.

This document offers additional information and troubleshooting steps to resolve this issue.

## Identifying when an app has exceeded the `RequiredResourceAccess` limits

In general, all applications with more than 400 permissions have exceeded the configuration limits. Apps may also be subject to lower limits if they support sign-in for personal Microsoft accounts (MSA). An app that has exceeded the permission limits will receive the following error when trying to add more permissions in the Azure portal:

> 
> `Failed to save permissions for <AppName>. This configuration exceeds the global application object limit. Remove some items and retry your request.`

## Resolution steps

If the application isn't needed anymore, the first option you should consider is to delete the app registration entirely. (You can [restore recently deleted applications](../architecture/recover-from-deletions#applications-and-service-principals), in case you discover soon afterwards that it was still needed.)

If you still need the application or are unsure, the following steps will help you resolve this issue:

1. **Remove duplicate permissions.** In some cases, the same permission is listed multiple times. Review the required permissions and remove permissions that are listed two or more times. See the related PowerShell script on the additional resources section of this article.
2. **Remove unused permissions.** Review the permissions required by the application and compare them to what the application or service does. Remove permissions that are configured in the app registration, but which the application or service doesn’t require. For more information on how to review permissions, see [Review application permissions](../identity/enterprise-apps/manage-application-permissions)
3. **Remove redundant permissions.** In many APIs, including Microsoft Graph, some permissions aren't necessary when other more privileged permissions are included. For example, the Microsoft Graph permission User.Read.All (read all users) isn't needed when an application also has User.ReadWrite.All (read, create and update all users). To learn more about Microsoft Graph permissions, see [Microsoft Graph permissions reference](/en-us/graph/permissions-reference).

## Frequently asked questions (FAQ)

### *Why has Microsoft revised the limit on total permissions?*

This limit is important for two reasons:

- To help prevent an app from being configured to require more permissions than can be granted during consent.
- To keep the total size of the app registration within the limits required for stability and performance of the underlying storage platform.

### *What will happen if I don’t do anything?*

If your app exceeds the total permissions limit, you'll no longer be able to increase the total number of required permissions for your application.

### *Does the limit change how many permissions my application can be granted?*

No. This limit affects only the list of requested API permissions configured on the app registration. This is different from the list of permissions that have been granted to your application.

Even if it isn't listed in the required API permissions list, a delegated permission can still be requested dynamically by an application. Both delegated permissions and app roles (application permissions) can also be granted directly, using Microsoft Graph API or Microsoft Graph PowerShell.

### *Can the limit be raised for my application?*

No, the limit can't be raised for individual applications or organizations.

### *Are there other limits on the list of required API permissions?*

Yes. The limits can vary depending on the supported account types for the app. Apps that support personal Microsoft Accounts for sign-in (for example, Outlook.com, Hotmail.com, Xbox Live) generally have lower limits. See [Validation differences by supported account types](supported-accounts-validation) to learn more.