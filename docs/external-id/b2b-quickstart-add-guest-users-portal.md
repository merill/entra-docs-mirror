---
layout: Conceptual
title: 'Quickstart: Add a guest user and send an invitation - Microsoft Entra External ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/b2b-quickstart-add-guest-users-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Use this quickstart to learn how Microsoft Entra admins can add B2B guest users in the Microsoft Entra admin center and walk through the B2B invitation workflow.
ms.date: 2026-04-24T00:00:00.0000000Z
ms.topic: quickstart
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: it-pro, mode-ui, sfi-image-nochange
locale: en-us
document_id: 9b3c7993-0036-507f-f3eb-40845fa312c8
document_version_independent_id: 59f8fd79-2104-fed4-0b47-250a61b0138b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/b2b-quickstart-add-guest-users-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/b2b-quickstart-add-guest-users-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/b2b-quickstart-add-guest-users-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: cdb5a677-9fbe-d3d1-4660-0ab057a729b8
---

# Quickstart: Add a guest user and send an invitation - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

With Microsoft Entra [B2B collaboration](what-is-b2b), you can invite anyone to collaborate with your organization using their own work, school, or social account.

In this quickstart, you'll learn how to add a new guest user to your Microsoft Entra directory in the Microsoft Entra admin center. You'll also send an invitation and see what the guest user's invitation redemption process looks like.

This guide provides the basic steps to invite an external user. To learn about all of the properties and settings that you can include when you invite an external user, see [How to create and delete a user](../fundamentals/how-to-create-delete-users).

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

B2B invitation emails that originate from onmicrosoft default domains are subject to Exchange Online sending limits. See [Limiting onmicrosoft domain usage for sending emails](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits) for more information. Consider updating to a custom domain if you need higher limits. For more information, see [Add your custom domain name to your tenant](../fundamentals/add-custom-domain).

## Prerequisites

To complete the scenario in this quickstart, you need:

- A role that allows you to create users in your tenant directory, such as at least a [Guest Inviter role](../identity/role-based-access-control/permissions-reference#guest-inviter) or a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
- Access to a valid email address outside of your Microsoft Entra tenant, such as a separate work, school, or social email address. You'll use this email to create the guest account in your tenant directory and access the invitation.

## Invite an external guest user

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.

    ![Screenshot of the All users page.](media/quickstart-add-users-portal/all-users-page.png)
3. Select **Invite external user** from the menu.

    ![Screenshot of the invite external user menu option.](media/quickstart-add-users-portal/invite-external-user-menu.png)

### Basics for external users

In this section, you're inviting the guest to your tenant using *their email address*. For this quickstart, enter an email address that you can access.

- **Email**: Enter the email address for the guest user you're inviting.
- **Display name**: Provide the display name.
- **Invitation message**: Select the **Send invite message** checkbox to send an invitation message. When you enable this checkbox, you can also set up a customized short message and another CC recipient.

![Screenshot of the invite external user Basics tab.](media/quickstart-add-users-portal/invite-external-user-basics-tab.png)

Select the **Review and invite** button to finalize the process.

### Review and invite

The final tab captures several key details from the user creation process. Review the details and select the **Invite** button if everything looks good.

An email invitation is sent automatically.

1. After you send the invitation, the user account is automatically added to the directory as a guest.

    ![Screenshot showing the new guest user in the directory.](media/quickstart-add-users-portal/new-guest-user-directory.png)

## Accept the invitation

Now sign in as the guest user to see the invitation.

1. Sign in to your test guest user's email account.
2. In your inbox, open the email from "Microsoft Invitations on behalf of Contoso."

    ![Screenshot showing the B2B invitation email.](media/quickstart-add-users-portal/quickstart-users-portal-email-small.png)
3. In the email body, select **Accept invitation**. A **Permission requested by:** page opens in the browser.

    ![Screenshot showing the Review permissions page.](media/quickstart-add-users-portal/consent-screen.png)
4. Select **Accept**.
5. The **My Apps** page opens. Because we haven't assigned any apps to this guest user, you'll see the message "There are no apps to show." In a real-life scenario, you would [add the guest user to an app](add-users-administrator#add-guest-users-to-an-application) so the app would appear here.

## Clean up resources

When no longer needed, delete the test guest user.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users** &gt; **User settings**.
3. Select the test user, and then select **Delete user**.