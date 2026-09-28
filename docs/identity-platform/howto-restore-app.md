---
layout: Conceptual
title: 'How to: Restore or remove a recently deleted application with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-restore-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this how-to, you learn how to restore or permanently delete a recently deleted application registered with the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2023-06-21T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: aa21a33b-e4f0-70f9-eaf1-526eead150d4
document_version_independent_id: 6a686429-6ecd-f24f-fdf0-1dbedb1be1ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-restore-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-restore-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-restore-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 52c53e9f-1af4-638d-9845-510d8ee0dc9e
---

# How to: Restore or remove a recently deleted application with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

After you delete an app registration, the app remains in a suspended state for 30 days. During that 30-day window, the app registration can be restored, along with all its properties. After that 30-day window passes, app registrations can't be restored, and the permanent deletion process may be automatically started. This functionality only applies to applications associated to a directory. It isn't available for applications from a personal Microsoft account, which can't be restored.

You can view your deleted applications, restore a deleted application, or permanently delete an application using the **Entra ID** &gt; **App registrations** in the Microsoft Entra admin center.

Neither you nor Microsoft customer support can restore a permanently deleted application or an application deleted more than 30 days ago.

## Prerequisites

You must have one of the following roles to permanently delete applications.

- Application Administrator
- Cloud Application Administrator
- Hybrid Identity Administrator
- Application Owner

You must have one of the following roles to restore applications.

- Application Owner

## View your deleted applications

You can see all the applications in a soft deleted state. Only applications deleted less than 30 days ago can be restored.

To view your restorable applications:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using one of the roles listed in the prerequisites.
2. Browse to **Entra ID** &gt; **App registrations**, and then select the **Deleted applications** tab.

Review the list of applications. Only applications that have been deleted in the past 30 days are available to restore. If using the App registrations search preview, you can filter by the 'Deleted date' column to see only these applications.

## Restore a recently deleted application

When an app registration is deleted from the organization, the app is in a suspended state, and its configurations are preserved. When you restore an app registration, its configurations are also restored. However, if there were any organization-specific settings such as permission consents and user and group assignments for a certain organization stored in **Enterprise applications** for the application's home tenant, they're restored alongside the app registration.

To restore an application:

1. Go to the **Deleted applications** tab. Search for and select one of the applications deleted less than 30 days ago.
2. Select **Restore app registration**.

## Permanently delete an application

You can manually permanently delete an application from your organization. A permanently deleted application can't be restored by you, another administrator, or by Microsoft customer support. However, this doesn't permanently delete the corresponding service principal. The service principal can't be restored without having an active corresponding application, so the service principal can be manually deleted, which is also permanent. If no action is taken, the service principal will be permanently deleted 30 days after deleting the application.

To permanently delete an application:

1. Go to the **Deleted applications** tab. Search for and select one of the available applications.
2. Select **Delete permanently**.
3. Read the warning text and select **Yes**.