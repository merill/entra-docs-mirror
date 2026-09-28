---
layout: HowTo
title: Add B2B collaboration users - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/add-users-administrator
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add B2B collaboration users in the Microsoft Entra admin center. Invite guest users to the directory, groups, or applications, and manage their access to resources.
ms.date: 2026-03-20T00:00:00.0000000Z
ms.topic: how-to
ms.collection: M365-identity-device-management
ms.custom:
- ge-structured-content-pilot
- sfi-image-nochange
locale: en-us
document_id: 751889da-f001-117f-d525-3b27d467edf2
document_version_independent_id: ce46adec-de86-7c34-45ba-d735cba76d2d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/add-users-administrator.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/add-users-administrator
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/add-users-administrator.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 95ecd834-12c3-3582-7019-cb59425df8e3
---

# Add B2B collaboration users - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

As a user who is assigned any of the limited administrator directory roles, you can use the Microsoft Entra admin center to invite B2B collaboration users. You can invite guest users to the directory, to a group, or to an application. After you invite a user through any of these methods, the invited user's account is added to Microsoft Entra ID, with a user type of *Guest*. The guest user must then redeem their invitation to access resources. An invitation of a user doesn't expire.

After you add a guest user to the directory, you can either send the guest user a direct link to a shared app, or the guest user can select the redemption URL in the invitation email. For more information about the redemption process, see [B2B collaboration invitation redemption](redemption-experience).

Important

You should follow the steps in [How-to: Add your organization's privacy info in Microsoft Entra ID](../fundamentals/properties-area) to add the URL of your organization's privacy statement. As part of the first time invitation redemption process, an invited user must consent to your privacy terms to continue.

Instructions in this topic provide the basic steps to invite an external user. To learn about all of the properties and settings that you can include when you invite an external user, see [How to create and delete a user](../fundamentals/how-to-create-delete-users).

## Prerequisites

Make sure your organization's external collaboration settings are configured such that you're allowed to invite guests. By default, all users and admins can invite guests. But your organization's external collaboration policies might be configured to prevent certain types of users or admins from inviting guests. To find out how to view and set these policies, see [Enable B2B external collaboration and manage who can invite guests](external-collaboration-settings-configure).

## Add guest users to the directory

To add B2B collaboration users to the directory, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Microsoft Entra ID** &gt; **Users**.

![Screenshot of the All users page.](media/add-users-administrator/all-users-page.png)

1. Select **New user** &gt; **Invite external user** from the menu.

![Screenshot of the invite external user menu option.](media/add-users-administrator/invite-external-user-menu.png)

### Basics

In this section, you're inviting the guest to your tenant using *their email address*. If you need to create a guest user with a domain account, use the [create new user process](../fundamentals/how-to-create-delete-users#create-a-new-user) but change the **User type** to **Guest**.

- **Email**: Enter the email address for the guest user you're inviting.
- **Display name**: Provide the display name.
- **Invitation message**: Select the **Send invite message** checkbox to customize a brief message to the guest. Provide a Cc recipient, if necessary.

![Screenshot of the invite external user Basics tab.](media/add-users-administrator/invite-external-user-basics-tab.png)

Either select the **Review + invite** button to create the new user or **Next: Properties** to complete the next section.

### Properties

There are six categories of user properties you can provide. These properties can be added or updated after the user is created. To manage these details, go to **Microsoft Entra ID** &gt; **Users** and select a user to update.

- **Identity:** Enter the user's first and family name. Set the User type as either Member or Guest. For more information about the difference between external guests and members, see [B2B collaboration user properties](user-properties).
- **Job information:** Add any job-related information, such as the user's job title, department, or manager.
- **Contact information:** Add any relevant contact information for the user.
- **Parental controls:** For organizations like K-12 school districts, the user's age group may need to be provided. *Minors* are 12 and under, *Not adult* are 13-18 years old, and *Adults* are 18 and over. The combination of age group and consent provided by parent options determine the Legal age group classification. The Legal age group classification may limit the user's access and authority.
- **Settings:** Specify the user's global location.

Either select the **Review + invite** button to create the new user or **Next: Assignments** to complete the next section.

### Assignments

You can assign external users to a group, or Microsoft Entra role when the account is created. You can assign the user to up to 20 groups or roles. Group and role assignments can be added after the user is created. The **Privileged Role Administrator** role is required to assign Microsoft Entra roles.

**To assign a group to the new user**:

1. Select **+ Add group**.
2. From the menu that appears, choose up to 20 groups from the list and select the **Select** button.
3. Select the **Review + create** button.

![Screenshot of the add group assignment process.](media/add-users-administrator/invite-external-user-assignments-tab.png)

**To assign a role to the new user**:

1. Select **+ Add role**.
2. From the menu that appears, choose up to 20 roles from the list and select the **Select** button.
3. Select the **Review + invite** button.

### Review and create

The final tab captures several key details from the user creation process. Review the details and select the **Invite** button if everything looks good. An email invitation is automatically sent to the user. After you send the invitation, the user account is automatically added to the directory as a guest.

![Screenshot showing the user list including the new Guest user.](media/add-users-administrator/guest-user-type.png)

### External user invitations

When you invite an external guest user by sending an email invitation, you can check the status of the invitation from the user's details. If they haven't redeemed their invitation, you can resend the invitation email.

1. Go to **Microsoft Entra ID** &gt; **Users** and select the invited guest user.
2. In the **My Feed** section, locate the **B2B collaboration** tile.

    - If the invitation state is **Pending acceptance**, select the **Resend invitation** link to send another email and follow the prompts.
    - You can also select the **Properties** for the user and view the **Invitation state**.

    ![Screenshot of the My Feed section of the user overview page.](media/add-users-administrator/external-user-invitation-state.png)

    Note

    Group email addresses aren’t supported; enter the email address for an individual. Also, some email providers allow users to add a plus symbol (+) and additional text to their email addresses to help with things like inbox filtering. However, Microsoft Entra doesn’t currently support plus symbols in email addresses. To avoid delivery issues, omit the plus symbol and any characters following it up to the @ symbol.

    The user is added to your directory with a user principal name (UPN) in the format *emailaddress*#EXT#@*domain*. For example: *john\_contoso.com#EXT#@fabrikam.onmicrosoft.com*, where fabrikam.onmicrosoft.com is the organization from which you sent the invitations. ([Learn more about B2B collaboration user properties](user-properties).)

## Add guest users to a group

If you need to manually add B2B collaboration users to a group after the user was invited, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Microsoft Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select a group (or select **New group** to create a new one). It's a good idea to include in the group description that the group contains B2B guest users.
4. Under **Manage**, select **Members**.
5. Select **Add members**.
6. Complete the following set of steps:

    - *If the guest user is already in the directory:*

        a. On the **Add members** page, start typing the name or email address of the guest user.

        b. In the search results, choose the user, and then choose **Select**.

    You can also use dynamic membership groups with Microsoft Entra B2B collaboration. For more information, see [Dynamic groups and Microsoft Entra B2B collaboration](use-dynamic-groups).

## Add guest users to an application

To add B2B collaboration users to an application, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Microsoft Entra ID** &gt; **Enterprise apps**.
3. On the **All applications** page, select the application to which you want to add guest users.
4. Under **Manage**, select **Users and groups**.
5. Select **Add user/group**.
6. On the **Add Assignment** page, select the link under **Users**.
7. Complete the following set of steps:

    - *If the guest user is already in the directory:*

        a. On the **Users** page, start typing the name or email address of the guest user.

        b. In the search results, choose the user, and then choose **Select**.

        c. On the **Add Assignment** page, choose **Assign** to add the user to the app.
8. The guest user appears in the application's **Users and groups** list with the assigned role of **Default Access**. If the application provides different roles and you want to change the user's role, do the following:

    a. Select the check box next to the guest user, and then select the **Edit** button.

    b. On the **Edit Assignment** page, choose the link under **Select a role**, and select the role you want to assign to the user.

    c. Choose **Select**.

    d. Select **Assign**.