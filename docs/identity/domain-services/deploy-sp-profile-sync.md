---
layout: Conceptual
title: Enable SharePoint User Profile service with Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/deploy-sp-profile-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to configure a Microsoft Entra Domain Services managed domain to support profile synchronization for SharePoint Server
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: f95ecc6f-90c2-338c-cb74-f202da4afd4b
document_version_independent_id: b7c5da87-33d9-e82d-f3f5-20ab9e970c58
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/deploy-sp-profile-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/deploy-sp-profile-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/deploy-sp-profile-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/dc29fde7-b949-4135-9273-ad8e4a53d516
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/25d6050c-71f5-4b48-8bc7-575debd6530a
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 485fe3b0-5f50-a535-8d2a-e3a98af728bb
---

# Enable SharePoint User Profile service with Domain Services - Microsoft Entra ID | Microsoft Learn

SharePoint Server includes a service to synchronize user profiles. This feature allows user profiles to be stored in a central location and accessible across multiple SharePoint sites and farms. To configure the SharePoint Server user profile service, the appropriate permissions must be granted in a Microsoft Entra Domain Services managed domain. For more information, see [user profile synchronization in SharePoint Server](/en-us/SharePoint/administration/user-profile-service-administration).

This article shows you how to configure Domain Services to allow the SharePoint Server user profile sync service.

## Before you begin

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, complete the tutorial to [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
- A Windows Server management VM that is joined to the Domain Services managed domain.
    - If needed, complete the tutorial to [create a management VM](tutorial-create-management-vm).
- A user account that's a member of the *Microsoft Entra DC administrators* group in your Microsoft Entra tenant.
- The SharePoint service account name for the user profile synchronization service. For more information about the *Profile Synchronization account*, see [Plan for administrative and service accounts in SharePoint Server](/en-us/sharepoint/security-for-sharepoint-server/plan-for-administrative-and-service-accounts). To get the *Profile Synchronization account* name from the SharePoint Central Administration website, click **Application Management** &gt; **Manage service applications** &gt; **User Profile service application**. For more information, see [Configure profile synchronization by using SharePoint Active Directory Import in SharePoint Server](/en-us/SharePoint/administration/configure-profile-synchronization-by-using-sharepoint-active-directory-import).

## Service accounts overview

In a managed domain, a security group named *Microsoft Entra DC Service Accounts* exists as part of the *Users* organizational unit (OU). Members of this security group are delegated the following privileges:

- **Replicate Directory Changes** privilege on the root DSE.
- **Replicate Directory Changes** privilege on the *Configuration* naming context (`cn=configuration` container).

The *Microsoft Entra DC Service Accounts* security group is also a member of the built-in group *Pre-Windows 2000 Compatible Access*.

When added to this security group, the service account for SharePoint Server user profile synchronization service is granted the required privileges to work correctly.

## Enable support for SharePoint Server user profile sync

The service account for SharePoint Server needs adequate privileges to replicate changes to the directory and let SharePoint Server user profile sync work correctly. To provide these privileges, add the service account used for SharePoint user profile synchronization to the *Microsoft Entra DC Service Accounts* group.

From your Domain Services management VM, complete the following steps:

Note

To edit group membership in a managed domain, you must be signed in to a user account that's a member of the *AAD DC Administrators* group.

1. From the Start screen, select **Administrative Tools**. A list of available management tools is shown that were installed in the tutorial to [create a management VM](tutorial-create-management-vm).
2. To manage group membership, select **Active Directory Administrative Center** from the list of administrative tools.
3. In the left pane, choose your managed domain, such as *aaddscontoso.com*. A list of existing OUs and resources is shown.
4. Select the **Users** OU, then choose the *Microsoft Entra DC Service Accounts* security group.
5. Select **Members**, then choose **Add...**.
6. Enter the name of the SharePoint service account, then select **OK**. In the following example, the SharePoint service account is named *spadmin*:

    ![Add the SharePoint service account to the Microsoft Entra DC Service Accounts security group](media/deploy-sp-profile-sync/add-member-to-aad-dc-service-accounts-group.png)