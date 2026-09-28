---
layout: Conceptual
title: Add sponsors to a guest user in the Microsoft Entra admin center - External ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/b2b-sponsors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Shows how an admin can add sponsors to guest users in Microsoft Entra B2B collaboration.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: d1db2d9f-3434-7f7a-e4fe-623ee34f7e36
document_version_independent_id: a7fcc12e-978b-c8a1-a571-a511123f83f2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/b2b-sponsors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/b2b-sponsors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/b2b-sponsors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 6a92caa9-b97d-49be-55e8-d89c7d74b073
---

# Add sponsors to a guest user in the Microsoft Entra admin center - External ID - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

The sponsor feature helps you manage B2B users in your directory. It allows tracking of who is responsible for each guest user. While [entitlement management](/en-us/entra/id-governance/entitlement-management-overview) can track guests in certain domains, it doesn't include guests outside these areas. By using the sponsor feature, you can assign a person or group to each guest user. This helps track who invited them and supports accountability.

This article provides an overview of the sponsor feature and explains how to use it in B2B scenarios.

## Sponsors field on the user object

The **Sponsors** field on the user object refers to the person or group who manages and monitors the lifecycle of the user, ensuring they have access to the right resources. Being a sponsor doesn't grant administrative powers for the sponsor user or the group, but it can be used for approval processes in entitlement management. You can also use it for custom solutions, but it doesn't offer any other built-in directory powers.

![Screenshot of a guest user profile showing one sponsor listed in the Sponsors field.](media/b2b-sponsors/single-sponsor.png)

## Who can be a sponsor?

If you invite a guest user, you automatically become their sponsor unless you specify someone else during the invitation process. Your name will be added to the **Sponsors** field on the user object automatically. You can also specify a different sponsor, a person, or a group when inviting a guest user. If a sponsor leaves the organization, the tenant administrator can change the **Sponsors** field to a different person or group during offboarding. This transition ensures the guest user's account remains properly tracked.

## Other scenarios using the B2B sponsors feature

The Microsoft Entra B2B collaboration sponsor feature serves as a foundation for other scenarios that aim to provide a full governance lifecycle for external partners. These scenarios aren't part of the sponsor feature but rely on it for managing guest users:

- Administrators can transfer sponsorship to another user or group, if the guest user starts working on a different project.
- When requesting new access packages, sponsors can be added as approvers in entitlement management to help reduce reviewers' workload.

## Add sponsors when inviting a new guest user

You can add up to five sponsors when inviting a new guest user. If you don’t specify a sponsor, the inviter will be added as a sponsor. To invite a guest user, you need to have at least the [Guest Inviter](/en-us/entra/identity/role-based-access-control/permissions-reference#guest-inviter) or [User Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator) role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Invite external user** from the menu.
4. Enter the details on the **Basics** tab, and then select **Next: Properties**.
5. You can add sponsors under **Job information** on the **Properties** tab.

    ![Screenshot of the invite external user flow showing where to add sponsors under Job information on the Properties tab.](media/b2b-sponsors/add-sponsors.png)
6. Select the **Review and invite** button to finalize the process.

You can also add sponsors with the Microsoft Graph API, using invitation manager for any new guest users, by including them in the payload. If there are no sponsors in the payload, the inviter will be marked as the sponsor. To learn more, see [Assign sponsors](/en-us/graph/api/user-post-sponsors).

Note

Currently, if an external user is invited through SharePoint (for example, when sharing a file with a non-existing external user), sponsors will not be added to that external user. This is a known issue. For now, you can manually add sponsors by following the steps above.

## Edit the Sponsors field in the Microsoft Entra admin center

When you invite a guest user, you become their sponsor by default. If you need to manually change the guest user's sponsor, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. In the list, select the user's name to open their user profile.
4. Under **Properties** &gt; **Job information** check the **Sponsors** field. If the guest user already has a sponsor, you can select **View** to see the sponsor's name.

    ![Screenshot of the sponsors field under the job information.](media/b2b-sponsors/sponsors-under-properties.png)
5. Close the window with the sponsor name list, if you want to edit the **Sponsors** field.
6. There are two ways to edit the **Sponsors** field. Either select the pencil icon next to the **Job Information**, or select **Edit properties** from the top of the page and go to the **Job Information** tab.
7. If the user has only one sponsor, you can see the sponsor's name. If the user has multiple sponsors, you can't see the individual names:

    ![Screenshot of multiple sponsors option.](media/b2b-sponsors/multiple-sponsors.png)
8. To add or remove sponsors, select **Edit**, select or remove the users or groups, and select **Save** on the **Job Information** tab.
9. If the guest user doesn't have a sponsor, select **Add sponsors**.

    ![Screenshot of adding a sponsor to an existing user.](media/b2b-sponsors/add-sponsors-existing-user.png)
10. Once you select sponsor users or groups, save the changes on the **Job Information** tab.

## Edit the Sponsors field with PowerShell

You can manage the **Sponsors** field for all existing users using the [Update-MsIdInvitedUserSponsorsFromInvitedBy](https://azuread.github.io/MSIdentityTools/commands/Update-MsIdInvitedUserSponsorsFromInvitedBy) PowerShell script in the [Microsoft Identity Tools module](https://azuread.github.io/MSIdentityTools). The script updates the sponsors attribute to include the user who initially invited them to the tenant using the `InvitedBy` property.