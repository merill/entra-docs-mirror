---
layout: Conceptual
title: 'Quickstart: Create and assign a user account - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal-assign-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Create a user account and assign it to an enterprise application in your Microsoft Entra tenant. Begin managing access efficiently today
ms.topic: quickstart
ms.date: 2025-03-21T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: mode-other, enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 05f5a57c-9ddc-3075-5aa0-4561d19eff69
document_version_independent_id: 28541e41-3915-d0b8-10e5-f7d1c2fc40d2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/add-application-portal-assign-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/add-application-portal-assign-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/add-application-portal-assign-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a681bb30-f611-c7b6-5378-ad5d88103ac9
---

# Quickstart: Create and assign a user account - Microsoft Entra ID | Microsoft Learn

In this quickstart, you use the Microsoft Entra admin center to create a user account in your Microsoft Entra tenant. After you create the account, you can assign it to the enterprise application that you added to your tenant.

We recommend that you use a nonproduction environment to test the steps in this quickstart.

## Prerequisites

To create a user account and assign it to an enterprise application, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, or owner of the service principal. You need the User Administrator role to manage users.
- Completion of the steps in [Quickstart: Add an enterprise application](add-application-portal).

## Create a user account

To create a user account in your Microsoft Entra tenant:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**
3. Select **New user** at the top of the pane and then, select **Create new user**.
4. In the **User principal name** field, enter the username of the user account. For example, `b.simon@contoso.com`. Be sure to change `contoso.com` to the name of your tenant domain.
5. In the **Display name** field, enter the name of the user of the account. For example, `B.Simon`.
6. Enter the details required for the user under the **Groups and roles**, **Settings**, and **Job info** sections.
7. Select **Create**.

## Assign a user account to an enterprise application

To assign a user account to an enterprise application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**. For example, select the application that you created in the previous quickstart named **Microsoft Entra SAML Toolkit 1**.
3. In the left pane, select **Users and groups**, and then select **Add user/group**.

    [![Assign user account to an application in your Microsoft Entra tenant.](media/add-application-portal-assign-users/assign-user.png)](media/add-application-portal-assign-users/assign-user.png#lightbox)
4. On the **Add Assignment** pane, select **None Selected** under **Users and groups**.
5. Search for and select the user that you want to assign to the application. For example, `b.simon@contoso.com`.
6. Select **Select**.
7. Select **None Selected** under **Select a role** and then select the role that you want to assign to the user. For example, **Standard User**.
8. Select **Select**.
9. Select **Assign** at the bottom of the pane to assign the user to the application.

After you assign the user to the application, ensure you set the application to be visible to the user. To make it visible to assigned users, select **Properties** in the left pane, and then set **Visible to users?** to **Yes**.

## Clean up resources

If you're planning to complete the next quickstart, keep the application that you created. Otherwise, you can consider deleting it to clean up your tenant.