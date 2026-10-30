---
layout: Conceptual
title: 'How to: Remove a registered app from the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-remove-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to remove an application registered with the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2023-06-21T00:00:00.0000000Z
ms.reviewer: sureshja
ms.topic: how-to
locale: en-us
document_id: 0871c918-f43d-42e6-b294-0784c6c76cb6
document_version_independent_id: c7b0c0e7-6b7c-04b8-8775-3a079c1fa98f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-remove-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-remove-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-remove-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4065f9f4-9f2d-b931-fb47-da704d8a48e7
---

# How to: Remove a registered app from the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

Enterprise developers and software-as-a-service (SaaS) providers who have registered applications with the Microsoft identity platform may need to remove an application's registration.

Tip

Before permanently removing an application, consider [deactivating it](../identity/enterprise-apps/deactivate-application-portal) instead. Deactivation prevents token issuance while preserving the application configuration for investigation or potential reactivation, making it a less destructive alternative to deletion.

In the following sections, you learn how to:

- Remove an application authored by you or your organization
- Remove an application authored by another organization

## Prerequisites

- An [application registered in your Microsoft Entra tenant](quickstart-register-app)

## Remove an application authored by you or your organization

Applications that you or your organization have registered are represented by both an application object and service principal object in your tenant. For more information, see [Application objects and service principal objects](app-objects-and-service-principals).

Note

Deleting an application will also delete its service principal object in the application's home directory. For multitenant applications, service principal objects in other directories will not be deleted.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations** and then select the application that you want to configure. Once you've selected the app, you see the application's **Overview** page.
4. From the **Overview** page, select **Delete**.
5. Read the deletion consequences. Check the box if one appears at the bottom of the pane.
6. Select **Delete** to confirm that you want to delete the app.

## Remove an application authored by another organization

If you're viewing **App registrations** in the context of a tenant, a subset of the applications that appear under the **All apps** tab are from another tenant and were registered into your tenant during the consent process. More specifically, they're represented by only a service principal object in your tenant, with no corresponding application object. For more information on the differences between application and service principal objects, see [Application and service principal objects in Microsoft Entra ID](app-objects-and-service-principals).

In order to remove an application’s access to your directory (after having granted consent), the company administrator must remove its service principal. The administrator must have at least the [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator) access. To learn how to delete a service principal, see [Delete an enterprise application](../identity/enterprise-apps/delete-application-portal).