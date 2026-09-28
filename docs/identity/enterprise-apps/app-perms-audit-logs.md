---
layout: Conceptual
title: View Activity logs of application permissions - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/app-perms-audit-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Understand how to view the activity logs of what permissions are being granted and revoked for applications in my directory.
ms.topic: how-to
ms.date: 2025-04-28T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps
locale: en-us
document_id: 4acb34d9-8bd3-36e6-baf6-eda079a0aa50
document_version_independent_id: 4acb34d9-8bd3-36e6-baf6-eda079a0aa50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/app-perms-audit-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/app-perms-audit-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/app-perms-audit-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 2db38114-3a6d-c544-7e08-66e31338eadc
---

# View Activity logs of application permissions - Microsoft Entra ID | Microsoft Learn

Microsoft Entra is a platform that allows you to create and manage applications for your organization. You can grant different permissions to your applications, such as accessing data, or performing actions. It's important to review these permissions periodically to ensure they remain appropriate and secure.

One way to review permissions granted to your apps is by using activity logs, which record the activities and events that occur in your Microsoft Entra applications. Activity logs help you to monitor the usage and performance of your applications, and to identify any potential issues or risks. By reviewing the activity logs, you can see what permissions your applications have and whether they're complying with your policies and expectations.

In this article, you:

- View activity logs to see API permission granting and removing activity for a specific application.
- View activity logs to see API permission granting and removing activity for all applications.
- Understand which audit logs are used to track granting and removing API permissions from app to app.

## Prerequisites

To view Activity Logs for applications, you need:

- A user account. If you don't already have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Reports Reader, Security Reader, Security Administrator, Global Reader

## How to view permission audit logs for all applications in your directory

Only certain events recorded in the Activity Logs are needed to see application permission activity. To view all events using the Microsoft Entra admin center, Take the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with at least a [Reports reader](../role-based-access-control/permissions-reference#reports-reader) role
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. In the left-hand navigation underneath **Activity**, browse to **Audit logs**.
4. Filter the audit logs by using the information included in the Audit logs section to select only the needed logs to view permission activity for your applications.
5. Use **Manage view** on the top command bar to edit the columns shown. Select the **Date** column to view more detailed information per audit log.

## How to view permission audit logs for a specific resource application

It can be helpful to deep dive into the activity of a resource application to see which applications already have access through API permissions. For example, you might want to monitor the activity logs for the Microsoft Graph application, so you can see when permissions are granted for the resources it protects.

To view the activity logs for a resource application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with at least a [Reports reader](../role-based-access-control/permissions-reference#reports-reader) role
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Search for the resource application that owns the permission. For example, if you want to view which applications were awarded the Microsoft Graph `Mail.Read` permission in the last 30 days, search for *Microsoft Graph*.
4. In the left-hand navigation underneath **Activity**, browse to **Audit logs**.
5. Filter the audit logs by using the information included in the Audit logs section to select only the needed logs to view permission activity for your applications.
6. Use **Manage view** on the top command bar to edit the columns shown. Select the **Date** column to view more detailed information per audit log.

## Audit logs

The following table outlines the scenarios and audit values available for the granting and revoking of permissions granted to apps.

| Scenario | Audit Service | Audit Category | Audit Activity | Audit Actor | Audit log limitations |
| --- | --- | --- | --- | --- | --- |
| Granting app-only access to an app | Core Directory | ApplicationManagement | Add app role assignment to the service principal | User context |  |
| Revoking app-only access to an app | Core Directory | ApplicationManagement | Remove app role assignment from the service principal | User context |  |
| Granting delegated access to an app | Core Directory | ApplicationManagement | Add delegated permission grant | User context |  |
| User grants consent to an application | Core Directory | ApplicationManagement | Consent to application | User context |  |