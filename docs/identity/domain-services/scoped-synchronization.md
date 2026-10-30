---
layout: Conceptual
title: Scoped synchronization for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/scoped-synchronization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to use the Microsoft Entra admin center to configure scoped synchronization from Microsoft Entra ID to a Microsoft Entra Domain Services managed domain
ms.assetid: 9389cf0f-0036-4b17-95da-80838edd2225
ms.topic: how-to
ms.date: 2025-02-05T00:00:00.0000000Z
locale: en-us
document_id: 9aa065e4-a8b1-5986-8778-b63d5c509db8
document_version_independent_id: d28e4ec6-17e6-446c-89fc-7a8658d13185
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/scoped-synchronization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/scoped-synchronization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/scoped-synchronization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 085e3ca6-cc18-0087-ccf5-a6348453ef9c
---

# Scoped synchronization for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

To provide authentication services, Microsoft Entra Domain Services synchronizes users and groups from Microsoft Entra ID. In a hybrid environment, users and groups from an on-premises Active Directory Domain Services (AD DS) environment can be first synchronized to Microsoft Entra ID using Microsoft Entra Connect, and then synchronized to a Domain Services managed domain.

By default, all users and groups from a Microsoft Entra directory are synchronized to a managed domain. If only some users need to use Domain Services, you can instead choose to synchronize only groups of users. You can filter synchronization for groups on-premises, cloud only, or both.

This article shows you how to configure scoped synchronization and then change or disable the set of scoped users using the Microsoft Entra admin center. You can also [complete these steps using PowerShell](powershell-scoped-synchronization).

![Screenshot of group filter option.](media/scoped-synchronization/filter.png)

## Before you begin

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, complete the tutorial to [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
- You need [Application Administrator](/en-us/azure/active-directory/roles/permissions-reference#application-administrator) and [Groups Administrator](/en-us/azure/active-directory/roles/permissions-reference#groups-administrator) Microsoft Entra roles in your tenant to change the Domain Services synchronization scope.

## Scoped synchronization overview

By default, all users and groups from a Microsoft Entra directory are synchronized to a managed domain. You can scope synchronization to only user accounts that were created in Microsoft Entra ID, or synchronize all users.

If only a few groups of users need to access the managed domain, you can select **Filter by group entitlement** to synchronize only those groups. This scoped synchronization is only group-based. When you configure group-based scoped synchronization, only the user accounts that belong to the groups you specify are synchronized to the managed domain. Nested groups aren't synchronized; only the groups you specify get synchronized.

You can change the synchronization scope before or after you create the managed domain. The scope of synchronization is defined by a service principal with the application identifier `2565bd9d-da50-47d4-8b85-4c97f669dc36`. To prevent scope loss, don't delete or change the service principal. If it is accidentally deleted, the synchronization scope can't be recovered.

Keep in mind the following caveats if you change the synchronization scope:

- A full synchronization occurs.
- Objects that are no longer required in the managed domain are deleted. New objects are created in the managed domain.

To learn more about the synchronization process, see [Understand synchronization in Microsoft Entra Domain Services](synchronization).

## Enable scoped synchronization

To enable scoped synchronization in the Microsoft Entra admin center, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Microsoft Entra Domain Services**. Choose your managed domain, such as *aaddscontoso.com*.
2. Select **Synchronization** from the menu on the left-hand side.
3. For *Synchronization scope*, select **All** or **Cloud Only**.
4. To filter synchronization for selected groups, click **Show selected groups**, choose whether to synchronize cloud-only groups, on-premises groups, or both. For example, the following screenshot shows how to synchronize only three groups that were created in Microsoft Entra ID. Only users who belong to those groups will have their accounts synchronized to Domain Services.

    ![Screenshot that shows filter by cloud-only groups.](media/scoped-synchronization/cloud-only-groups.png)
5. To add groups, click **Add groups**, then search for and choose the groups to add.
6. When all changes are made, select **Save synchronization scope**.

Changing the scope of synchronization causes the managed domain to resynchronize all data. Objects that are no longer required in the managed domain are deleted, and resynchronization may take some time to complete.

## Modify scoped synchronization

To modify the list of groups whose users should be synchronized to the managed domain, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Microsoft Entra Domain Services**. Choose your managed domain, such as *aaddscontoso.com*.
2. Select **Synchronization** from the menu on the left-hand side.
3. To add a group, choose **+ Add groups** at the top, then choose the groups to add.
4. To remove a group from the synchronization scope, select it from the list of currently synchronized groups and choose **Remove groups**.
5. When all changes are made, select **Save synchronization scope**.

Changing the scope of synchronization causes the managed domain to resynchronize all data. Objects that are no longer required in the managed domain are deleted, and resynchronization may take some time to complete.

## Disable scoped synchronization

To disable group-based scoped synchronization for a managed domain, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Microsoft Entra Domain Services**. Choose your managed domain, such as *aaddscontoso.com*.
2. Select **Synchronization** from the menu on the left-hand side.
3. Clear the check box for **Show selected groups**, and click **Save synchronization scope**.

Changing the scope of synchronization causes the managed domain to resynchronize all data. Objects that are no longer required in the managed domain are deleted, and resynchronization may take some time to complete.