---
layout: FAQ
title: Deletion and recovery of applications FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/delete-recover-faq
summary: >
  <p>The following are some frequently asked questions (FAQs) on deletion and recovery of applications.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Find answers to frequently asked questions (FAQs) about recovering deleted apps and service principals.
ms.topic: faq
ms.date: 2024-02-21T00:00:00.0000000Z
ms.reviewer: sureshja
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps
locale: en-us
document_id: a33ad28a-a75d-7fda-df48-8f0f3791f92d
document_version_independent_id: d4b12b27-7a46-8ef1-d3b5-55eca981724c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/delete-recover-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/delete-recover-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/delete-recover-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: c8ad75bb-15c0-71da-803b-570f96eec4c9
---

# Deletion and recovery of applications FAQ - Microsoft Entra ID | Microsoft Learn

The following are some frequently asked questions (FAQs) on deletion and recovery of applications.

## When I create applications, and get a Directory\_QuotaExceeded error, how can I avoid this problem?

> 
> A nonadmin user can create no more than 250 Microsoft Entra resources that include applications and service principals. Both active resources and deleted resources that are available to restore count toward this quota. Even if you delete more applications that you don't need, they still add count to the quota. To free up the quota, you need to [permanently delete](restore-application) objects in the deleted items container.
> 
> For more information about the service limits, see [Azure resource management](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits?msclkid=6cb6cc54c68711ec93eb9539fce3cc28#azure-active-directory-limits).

## Where can I find all the deleted applications and service principals?

> 
> Soft-deleted application and service principal objects go into the deleted items container and remain available to restore for up to 30 days. After 30 days, they're permanently deleted, thus freeing up the quota.
> 
> To learn how to view deleted application objects through the Microsoft Entra admin center, see [View restorable applications](../../identity-platform/howto-restore-app#view-your-deleted-applications).
> 
> Deleted service principals can't be viewed through the Microsoft Entra admin center. To learn how to view your restorable service principals using PowerShell or Microsoft Graph API, see [View restorable service principals](restore-application).

## How do I restore deleted applications or service principals?

> 
> To learn how to restore recently deleted application registrations through the Microsoft Entra admin center, see [Restore application registrations](../../identity-platform/howto-restore-app). If the application registration and its corresponding service principal got deleted, the service principal is also restored.
> 
> To learn how to restore recently deleted service principals, see [Restore service principals](restore-application). This method is also applicable for restoring recently deleted application registrations using PowerShell or Microsoft Graph API.

## How do I permanently delete soft deleted applications or service principals?

> 
> To permanently delete application registrations through the Microsoft Entra admin center, see [Permanently delete an application](../../identity-platform/howto-restore-app#permanently-delete-an-application).
> 
> To permanently delete a service principal, see [Permanently delete a service principal](restore-application). This method is also applicable for permanently deleting application registrations using PowerShell or Microsoft Graph API.

## Can I configure the interval in which applications and service principals are permanently deleted by Microsoft Entra ID?

> 
> No. You can't configure the periodicity of hard deletion.

## Are managed identities soft-deleted?

> 
> Yes, Managed identities are soft-deleted. You can view the soft-deleted managed identity service principal from the recycle bin within 30 days after deletion, but you can't restore or permanently delete it. The managed identity service principal is permanently deleted after 30 days. For more information on how to view soft-deleted managed identities service principals, see [View deleted service principals](restore-application).

## I can't see the provisioning data from a recovered service principal. How can I recover it?

> 
> After recovering a service principal, you may initially see the error in the following screenshot. This issue resolves itself between 40 mins and 1 day. If you'd like the provisioning job to start immediately, you can hit restart to force the provisioning service to run again. Hitting restart triggers an initial cycle that can take time for customers with 100 K+ users or group memberships.
> 
> ![Screenshot of recovering user provisioning data.](media/delete-application-portal/recover-user-provisioning.png)

## I recovered my application that was configured for application proxy. I can't see app proxy configurations after the recovery. How can I recover it back?

> 
> App proxy configurations can't be recovered through the portal UI. Use the API to recover app proxy settings. Expect a delay of up to 24 hours as the app proxy data gets synced back.

## I can't see the policies I set on the service principal object after the recovery. How can I recover them?

> 
> Policies can't be recovered currently. When you restore a service principal, you have to configure the policies again.