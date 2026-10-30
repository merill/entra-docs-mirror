---
layout: Conceptual
title: Create collections on the My Apps portal - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/access-panel-collections
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Use My Apps collections to Customize My Apps pages for a simpler My Apps experience for your users. Organize applications into groups with separate tabs.
ms.topic: how-to
ms.date: 2024-09-30T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.reviewer: lenalepa
ms.custom: enterprise-apps
locale: en-us
document_id: 97b489b7-9f8c-d46a-8699-c2b791b0a3be
document_version_independent_id: b75539dc-8803-cc28-af48-539799858daf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/access-panel-collections.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/access-panel-collections
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/access-panel-collections.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: add10899-dc30-fe53-94ab-e6891ce2e79a
---

# Create collections on the My Apps portal - Microsoft Entra ID | Microsoft Learn

Your users can use the My Apps portal to view and start the cloud-based applications they have access to. By default, all the applications a user can access are listed together on a single page. To better organize this page for your users, if you have a Microsoft Entra ID P1 or P2 license you can set up collections. With a collection, you can group together applications that are related. For example, by job role, task, or project and display them on a separate tab. A collection essentially applies a filter to the applications a user can already access, so the user sees only those applications in the collection that have been assigned to them.

Note

This article covers how an admin can enable and create collections. For information for the end user about how to use the My Apps portal and collections, see [Access and use collections](https://support.microsoft.com/account-billing/organize-apps-using-collections-in-the-my-apps-portal-2dae6b8a-d8b0-4a16-9a5d-71ed4d6a6c1d).

## Prerequisites

To create collections on the My Apps portal, you need:

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, Application Administrator, or owner of the service principal.

## Create a collection

To create a collection, you must have a Microsoft Entra ID P1 or P2 license.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Under **Manage**, select **App launchers**.
4. Select **New collection**. In the **New collection** page, enter a **Name** for the collection (we recommend not using "collection" in the name). Then enter a **Description**.
5. Select the **Applications** tab. Select **+ Add application**, and then in the **Add applications** page, select all the applications you want to add to the collection, or use the **Search** box to find applications.

    ![Add an application to the collection](media/acces-panel-collections/add-applications.png)
6. When you're finished adding applications, select **Add**. The list of selected applications appears. You can use the arrows to change the order of applications in the list.
7. Select the **Owners** tab. Select **+ Add users and groups**, and then in the **Add users and groups** page, select the users or groups you want to assign ownership to. When you're finished selecting users and groups, choose **Select**.
8. Select the **Users and groups** tab. Select **+ Add users and groups**, and then in the **Add users and groups** page, select the users or groups you want to assign the collection to. Or use the **Search** box to find users or groups. When you're finished selecting users and groups, choose **Select**.
9. Select **Review + Create**. The properties for the new collection appear.

Note

Admin collections are managed through the [Microsoft Entra admin center](https://entra.microsoft.com), not from [My Apps portal](https://myapps.microsoft.com). For example, if you assign users or groups as an owner, then they can only manage the collection through the Microsoft Entra admin center.

Note

There is a known issue with Office apps in collections. If you already have at least one Office app in a collection and want to add more, follow these steps:

1. Select the collection you'd like to manage, then select the **Applications** tab.
2. Remove all Office apps from the collection but do not save the changes.
3. Select **+ Add application**.
4. In the **Add applications** page, select all the Office apps you want to add to the collection (including the ones that you removed in step 2).
5. When you're finished adding applications, select **Add**. The list of selected applications appears. You can use the arrows to change the order of applications in the list.
6. Select **Save** to apply the changes.

## View audit logs

The Audit logs record My Apps collections operations, including collection creation end-user actions. The following events are generated from My Apps:

- Create admin collection
- Edit admin collection
- Delete admin collection
- Self-service application adding (end user)
- Self-service application deletion (end user)

You can access audit logs in the [Microsoft Entra admin center](https://entra.microsoft.com) by selecting **Entra ID** &gt; **Enterprise apps** &gt; **Audit logs** in the Activity section. For **Service**, select **My Apps**.

## Get support for My Account pages

From the My Apps page, a user can select **My account** &gt; **View account** to open their account settings. On the Microsoft Entra ID **My Account** page, users can manage their security info, devices, passwords, and more. They can also access their Office account settings.

In case you need to submit a support request for an issue with the Microsoft Entra account page or the Office account page, follow these steps so your request is routed properly:

- For issues with the **Microsoft Entra ID "My Account"** page, open a support request from within the Microsoft Entra admin center. Go to **Microsoft Entra admin center** &gt; **Learn & support** &gt; **New support request**.
- For issues with the **Office "My account"** page, open a support request from within the Microsoft 365 admin center. Go to **Microsoft 365 admin center** &gt; **Support**.