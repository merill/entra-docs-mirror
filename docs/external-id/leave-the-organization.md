---
layout: Conceptual
title: Leave an organization - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/leave-the-organization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: As a B2B collaboration user, learn how to leave an organization if you no longer need guest user access to apps. If you're an admin, see how to allow external users to leave.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
adobe-target: true
locale: en-us
document_id: b448cfd0-b673-7d04-047b-71aa62bebc27
document_version_independent_id: 75118bff-94de-c9f9-7666-d2a6f4253b11
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/leave-the-organization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/leave-the-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/leave-the-organization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: db762726-dbfa-d2eb-12f6-b029649f79c6
---

# Leave an organization - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

As a Microsoft Entra B2B collaboration or B2B direct connect user, you can leave an organization whenever you no longer need access to its apps. Leaving the organization also ends your association with it.

## Before you begin

You can usually leave an organization on your own without having to contact an administrator. However, in some cases this option won't be available and you'll need to contact your tenant admin, who can delete your account in the external organization.

This article includes guidance for users who want to leave an organization and for administrators who manage external user leave settings.

If you're a user looking for information about how to manage and leave an organization, see [Manage organizations for your work or school account in the My Account portal](https://support.microsoft.com/account-billing/manage-organizations-for-a-work-or-school-account-in-the-my-account-portal-a9b65a70-fec5-4a1a-8e00-09f99ebdea17).

## What organizations do I belong to?

1. To view the organizations you belong to, first open your **My Account** page. You either have a work or school account created by an organization or a personal account such as for Xbox, Hotmail, or Outlook.com.

    - If you're using a work or school account, go to https://myaccount.microsoft.com and sign in.
    - If you're using a personal account or email one-time passcode, you'll need to use a My Account URL that includes your tenant name or tenant ID. For example:

        `https://myaccount.microsoft.com?tenantId=contoso.onmicrosoft.com`

        -or-

        `https://myaccount.microsoft.com?tenantId=aaaabbbb-0000-cccc-1111-dddd2222eeee`

        You might need to open this URL in a private browser session.
2. Select **Organizations** from the left navigation pane or select the **Manage organizations** link from the **Organizations** block.
3. The **Organizations** page appears, where you can view and manage the organizations you belong to.

    [![Screenshot showing the list of organizations you belong to.](media/leave-the-organization/organization-list.png)](media/leave-the-organization/organization-list.png#lightbox)

    - **Home organization**: Your home organization is listed first. This organization owns your work or school account. Because your account is managed by your administrator, you're not allowed to leave your home organization. You'll see there's no link to **Leave**. If you don't have an assigned home organization, you'll just see a single heading that says **Organizations** with the list of your associated organizations.
    - **Other organizations you collaborate with**: You'll also see the other organizations that you've signed in to previously using your work or school account. You can decide to leave any of these organizations at any time.

## How to leave an organization

If your organization allows users to remove themselves from external organizations, you can follow these steps to leave an organization.

1. Open your **Organizations** page. (Follow the steps in What organizations do I belong to, above.)
2. Under **Other organizations you collaborate with** (or **Organizations** if you don't have a home organization), find the organization that you want to leave, and then select **Leave**.

    [![Screenshot showing Leave organization option in the user interface.](media/leave-the-organization/leave-org.png)](media/leave-the-organization/leave-org.png#lightbox)
3. When asked to confirm, select **Leave**.
4. If you select **Leave** for an organization but you see the following message, it means you’ll need to contact the organization's admin, or privacy contact and ask them to remove you from their organization.

    ![Screenshot showing the message when you need permission to leave an organization.](media/leave-the-organization/need-permission-leave.png)

## Why can’t I leave an organization?

In the **Home organization** section, there's no link to **Leave** your organization. Only an administrator can remove your account from your home organization.

For the external organizations listed under **Other organizations you collaborate with**, you might not be able to leave on your own, for example when:

- the organization you want to leave doesn’t allow users to leave by themselves
- your account has been disabled

In these cases, you can select **Leave**, but then you'll see a message saying you need to contact the admin or privacy contact for that organization to ask them to remove you.

## More information for administrators

Administrators can use the **External user leave settings** to control whether external users can remove themselves from their organization. If you disallow the ability for external users to remove themselves from your organization, external users will need to contact your admin, or privacy contact to be removed.

Important

You can configure **External user leave settings** only if you have [added your privacy information](../fundamentals/properties-area) to your Microsoft Entra tenant. Otherwise, this setting will be unavailable. We recommend adding your privacy information to allow external users to review your policies and email your privacy contact when necessary.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External Identity Provider Administrator](../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **External user leave** settings, choose whether to allow external users to leave your organization themselves:

    - **Yes**: Users can leave the organization themselves without approval from your admin or privacy contact.
    - **No**: Users can't leave your organization themselves. They'll see a message guiding them to contact your admin, or privacy contact to request removal from your organization.

    [![Screenshot showing External user leave settings in the portal.](media/leave-the-organization/external-user-leave-settings.png)](media/leave-the-organization/external-user-leave-settings.png#lightbox)

### Account removal

When a B2B collaboration user leaves an organization, the user's account is "soft deleted" in the directory. By default, the user object moves to the **Deleted users** area in Microsoft Entra ID, but permanent deletion doesn't start for 30 days. This soft deletion enables the administrator to restore the user account, including groups and permissions, if the user makes a request to restore the account before it's permanently deleted.

If desired, a tenant administrator can permanently delete the account at any time during the soft-deleted period with the following steps. This action is irrevocable.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External Identity Provider Administrator](../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
2. Browse to **Entra ID** &gt; **Users**
3. Select **Deleted users**.
4. Select the check box next to a deleted user, and then select **Delete permanently**.

Permanent deletion can be initiated by the admin, or it happens at the end of the soft deletion period. Permanent deletion can take up to an extra 30 days for data removal.

For B2B direct connect users, data removal begins as soon as the user selects **Leave** in the confirmation message and can take up to 30 days to complete.

## Need help?

If you need additional assistance not covered in our content, you have several options. [Learn how to get help and support](/en-us/entra/fundamentals/how-to-get-support) from the Microsoft community, or submit a support request directly to Microsoft.