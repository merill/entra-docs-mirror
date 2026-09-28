---
layout: Conceptual
title: Limitations in multitenant organizations - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/multi-tenant-organization-known-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.reviewer: hafowler
ms.service: entra-id
ms.subservice: multitenant-organizations
manager: dougeby
description: Learn about the limitations when you work with multitenant organizations in Microsoft Entra ID.
ms.topic: troubleshooting
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 18796183-0c8c-be38-8321-d6f0c9f467e3
document_version_independent_id: 9add98e0-9608-5452-beaf-7edb3e79a1f8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/multi-tenant-organization-known-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/multi-tenant-organization-known-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/multi-tenant-organization-known-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dfc5822f-13ae-3e97-5c6c-04e7698ce229
---

# Limitations in multitenant organizations - Microsoft Entra ID | Microsoft Learn

## Overview

This article describes limitations to be aware of when you work with multitenant organization functionality across Microsoft Entra ID and Microsoft 365. To provide feedback about the multitenant organization functionality on UserVoice, see [Microsoft Entra UserVoice](https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789?category_id=360892). UserVoice is closely monitored to improve the service.

## Scope

The limitations described in this article have the following scope.

| Scope | Description |
| --- | --- |
| In scope | - Microsoft Entra administrator limitations related to multitenant organizations to support seamless collaboration experiences in new Microsoft Teams, with reciprocally provisioned B2B members- Microsoft Entra administrator limitations related to multitenant organizations to support seamless collaboration experiences in Microsoft Viva Engage, with centrally provisioned B2B members |
| Related scope | - Microsoft 365 admin center limitations related to multitenant organizations- Microsoft 365 multitenant organization people search experiences- Cross-tenant synchronization limitations related to Microsoft 365 |
| Out of scope | - Cross-tenant synchronization unrelated to Microsoft 365- End user experiences in Viva Engage- Tenant migration or consolidation |
| Unsupported scenarios | - Multitenant organizations across education tenants involving student scenarios- Multitenant organizations in Microsoft 365 Government- Seamless collaboration experience across multitenant organizations in classic Teams- Self-service for multitenant organizations larger than 100 tenants- Multitenant organizations in Azure Government or Microsoft Azure operated by 21Vianet- Multitenant organizations is available within GCC, GCC-H, and DOD clouds. However, the multitenant organizations tenants can ONLY have tenants which are within the same cloud. Cross-cloud multitenant organizations isn't supported. |

## Create or join a multitenant organization using the Microsoft 365 admin center

- After creating a multitenant organization in Microsoft 365 admin center, you'll see Microsoft admin center created cross-tenant synchronization configurations with the names `MTO_Sync_<TenantID>`. Refrain from editing or changing the name if you want Microsoft 365 admin center to recognize the configurations as created and managed by Microsoft 365 admin center.
- Synchronization jobs created with Microsoft Entra ID won't appear in Microsoft 365 admin center. Microsoft 365 admin center will indicate an **Outbound sync status** of **Not configured**. This is expected behavior. There's no supported pattern for Microsoft 365 admin center to take control of cross-tenant synchronization jobs created in Microsoft Entra admin center.

## Cross-tenant access settings

- Cross-tenant synchronization in Microsoft Entra ID doesn't support establishing a cross-tenant synchronization configuration before the tenant in question allows inbound synchronization in their cross-tenant access settings for identity synchronization.
- Therefore, prior to multitenant organization creation, the usage of the cross-tenant access settings template for identity synchronization is encouraged, with `userSyncInbound` set to true.
- Similarly, prior to multitenant organization creation, the usage of the cross-tenant access settings template for partner configurations is encouraged with `automaticUserConsentSettings.inboundAllowed` and `automaticUserConsentSettings.outboundAllowed` set to true.

## Join requests

- There are multiple reasons why a join request might fail. If the Microsoft 365 admin center doesn't indicate why a join request isn't succeeding, try examining the join request response by using the Microsoft Graph APIs or Microsoft Graph Explorer.
- If you followed the correct sequence to create a multitenant organization and add a tenant to the multitenant organization, and the added tenant's join request keeps failing, submit a support request in the Microsoft Entra or Microsoft 365 admin center.

## Options to provision your external member users

- If you're already using Microsoft Entra cross-tenant synchronization, for various [multi-hub multi-spoke topologies](cross-tenant-synchronization-topology), you don't need to use the Microsoft 365 admin center share users functionality. Instead, you might want to continue using your existing Microsoft Entra cross-tenant synchronization jobs.
- If you haven't previously used Microsoft Entra cross-tenant synchronization, and you intend to establish a [collaborating user set](multi-tenant-organization-microsoft-365#collaborating-user-set) topology where the same set of users is shared to all multitenant organization tenants, you might want to use the Microsoft 365 admin center share users functionality.
- If you already have your own at-scale user provisioning engine, you can utilize the new multitenant organization benefits while continuing to use your own engine to manage the lifecycle of your employees.
- If you need to create individual external member users in a host tenant rather than creating them through a provisioning engine from a source tenant, see [How to create, invite, and delete users](../../fundamentals/how-to-create-delete-users#users-in-workforce-tenants).

## Cross-tenant synchronization in Microsoft Entra admin center

- For enterprise organizations with complex identity configurations, use cross-tenant synchronization in Microsoft Entra admin center.
- By default, new B2B users are provisioned as B2B members, while existing B2B guests remain B2B guests. You can opt to convert B2B guests into B2B members by setting [**Apply this mapping** to **Always**](cross-tenant-synchronization-configure#step-9-review-attribute-mappings).
- By default, `showInAddressList` is synchronized into a target tenant as true. You might adjust this attribute mapping to match your organizations' needs.
- The at-scale provisioning of B2B users might collide with contact objects. The handling or conversion of contact objects isn't currently supported.
- Using cross-tenant synchronization to target hybrid identities that have been converted to B2B users isn't currently supported.

## Synchronize users in Microsoft 365 admin center

- For smaller multitenant organizations, consider using Microsoft 365 admin center to [synchronize users into multiple tenants](/en-us/microsoft-365/enterprise/sync-users-multi-tenant-orgs) of your multitenant organization.
- To share users, Microsoft 365 admin center creates multiple cross-tenant synchronization jobs, one per target tenant, keeping the same user scope for all jobs.
- After the Microsoft 365 admin center created the cross-tenant synchronization jobs, you might adjust attribute mappings in Microsoft Entra admin center to match your organizations' needs.

## B2B guests or B2B members managed in the host tenant

- The promotion of B2B guests to B2B members represents a strategic decision by multitenant organizations to consider B2B members as trusted users of the organization. Review the [default permissions](../../fundamentals/users-default-permissions) for B2B members.
- As your organization rolls out the multitenant organization functionality including provisioning of B2B users across multitenant organization tenants, you might want to provision some users as B2B guests, while provisioning other users as B2B members.
- To promote B2B guests to B2B members, a host tenant administrator can change the [userType](../../fundamentals/how-to-manage-user-profile-info#add-or-change-profile-information), assuming the property isn't recurringly synchronized.

## B2B guests or B2B members managed using cross-tenant synchronization

- If cross-tenant synchronization is used to recurringly synchronize the [userType](../../fundamentals/how-to-manage-user-profile-info#add-or-change-profile-information) property, a source tenant administrator can amend the [attribute mappings](cross-tenant-synchronization-configure#step-9-review-attribute-mappings).
- You might want to establish two Microsoft Entra cross-tenant synchronization configurations in the source tenant, one with userType attribute mappings configured to B2B guest, and another with userType attribute mappings configured to B2B member, each with [**Apply this mapping** set to **Always**](cross-tenant-synchronization-configure#step-9-review-attribute-mappings).
- By moving a user from one configuration's scope to the other, you can easily control who will be a B2B guest or a B2B member in the target tenant. Using this approach, you might also want to disable [Target Object Actions for Delete](cross-tenant-synchronization-configure#step-8-optional-define-who-is-in-scope-for-provisioning-with-scoping-filters).

## Global address list managed in the host tenant

- The [showInAddressList](/en-us/graph/api/resources/user#properties) property of a B2B user can be updated with [User Administrator](../role-based-access-control/permissions-reference#user-administrator) privileges in Microsoft Graph Explorer or Microsoft Graph PowerShell.
- Updating the [showInAddressList](/en-us/graph/api/resources/user#properties) property on the user object will also update the hide recipients from address lists setting in Microsoft Exchange Online.
- The [hide recipients from address lists](/en-us/exchange/address-books/address-lists/manage-address-lists#hide-recipients-from-address-lists) setting, if configured to differ from the [showInAddressList](/en-us/graph/api/resources/user#properties) property, takes precedence in determining address list visibility.
- If the [hide recipients](/en-us/exchange/address-books/address-lists/manage-address-lists#hide-recipients-from-address-lists) setting isn't configurable in [Exchange admin center](/en-us/exchange/address-books/address-lists/manage-address-lists#use-the-new-eac-to-hide-recipients-from-address-lists) due to user type Guest, it can be configured in PowerShell using the [HiddenFromAddressListsEnabled](/en-us/powershell/module/exchange/set-mailuser#-hiddenfromaddresslistsenabled) property.
- For more information, see [Add guests to the global address list](/en-us/microsoft-365/solutions/per-group-guest-access#add-guests-to-the-global-address-list).

## Global address list managed using cross-tenant synchronization

- If cross-tenant synchronization is used to synchronize the property, [showInAddressList](/en-us/graph/api/resources/user#properties) in a source tenant **can** be used to control address list visibility in a target tenant.
- On the other hand, [hide recipient from address lists](/en-us/exchange/address-books/address-lists/manage-address-lists#hide-recipients-from-address-lists) in the source tenant **can't** be used to affect address list visibility in a target tenant.

## Microsoft apps

- In [SharePoint OneDrive](/en-us/sharepoint/) user interfaces, when sharing a file with *People in Fabrikam*, the current user interfaces might be counterintuitive, because B2B members in Fabrikam from Contoso count toward *People in Fabrikam*.
- In Microsoft 365 admin center, [Microsoft Forms](/en-us/office365/servicedescriptions/microsoft-forms-service-description), Microsoft OneNote, and Microsoft Planner, B2B member users might not be supported.
- In [Microsoft Power BI](/en-us/fabric/enterprise/powerbi/service-admin-entra-b2b#who-can-you-invite), B2B member support is currently in preview. B2B guest users can continue to access Power BI dashboards.
- In [Microsoft Power Apps](/en-us/power-platform/), [Microsoft Dynamics 365](/en-us/dynamics365/), and related workloads, B2B member users might have restricted functionality. For more information, see [Invite users with Microsoft Entra B2B collaboration](/en-us/power-platform/admin/invite-users-azure-active-directory-b2b-collaboration).
- In Microsoft Purview, multitenant organization capabilities aren't yet supported. For more information, see existing functionalities for [external users and labeled content](/en-us/purview/sensitivity-labels-office-apps#support-for-external-users-and-labeled-content) and [external collaboration using sensitivity labels](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/secure-external-collaboration-using-sensitivity-labels/ba-p/1680498).
- In Microsoft Intune, multitenant organization capabilities aren't yet supported. For more information, see existing functionalities to [trust compliant device claims from external organizations](../../external-id/cross-tenant-access-settings-b2b-collaboration#to-change-inbound-trust-settings-for-mfa-and-device-claims).

## B2B users or B2B members

- As part of a multitenant organization, [reset redemption for an already redeemed B2B user](../../external-id/reset-redemption-status) is currently disabled.
- The at-scale provisioning of B2B users might collide with contact objects. The handling or conversion of contact objects isn't currently supported.
- Using cross-tenant synchronization to target hybrid identities that have been converted to B2B users hasn't been tested in source of authority conflicts and isn't supported.
- Signed-in users are able to read basic attributes of a multitenant organization, and of the multitenant organization member tenants, without being assigned roles, such as [Security Reader](../role-based-access-control/permissions-reference#security-reader) or [Global Reader](../role-based-access-control/permissions-reference#global-reader).

## Cross-tenant synchronization deprovisioning

- By default, when provisioning scope is reduced while a synchronization job is running, users fall out of scope and are soft deleted, unless [Target Object Actions for Delete](cross-tenant-synchronization-configure#step-8-optional-define-who-is-in-scope-for-provisioning-with-scoping-filters) is disabled. For more information, see [Deprovisioning](cross-tenant-synchronization-overview#deprovisioning) and [Define who is in scope for provisioning](cross-tenant-synchronization-configure#step-8-optional-define-who-is-in-scope-for-provisioning-with-scoping-filters).
- Currently, [SkipOutOfScopeDeletions](../app-provisioning/skip-out-of-scope-deletions?toc=/entra/identity/multi-tenant-organizations/toc.json&amp;pivots=cross-tenant-synchronization) works for application provisioning jobs, but not for cross-tenant synchronization. To avoid soft deletion of users taken out of scope of cross-tenant synchronization, set [Target Object Actions for Delete](cross-tenant-synchronization-configure#step-8-optional-define-who-is-in-scope-for-provisioning-with-scoping-filters) to disabled.