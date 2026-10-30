---
layout: Conceptual
title: Create an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-create
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to create an access package of resources that you want to share in Microsoft Entra entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-08-25T00:00:00.0000000Z
locale: en-us
document_id: 066dbfa5-08ba-8b7a-845b-854c873362b6
document_version_independent_id: 97d7f2b3-904a-574f-3732-9f6851291890
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-create.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-create
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-create.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 4418da3b-0479-5a67-7637-7b0c77aa6d8b
---

# Create an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

An access package enables you to do a one-time setup of resources and policies that automatically administers access for the life of the access package. This article describes how to create an access package.

## Overview

All access packages must be in a container called a catalog. A catalog defines what resources you can add to your access package. If you don't specify a catalog, your access package goes in the general catalog. Currently, you can't move an existing access package to a different catalog.

An access package can be used to assign access to roles of multiple resources that are in the catalog. If you're an administrator or catalog owner, you can add resources to the catalog while you're creating an access package. You can also add resources after the access package is created, and identities assigned to the access package will also receive the extra resources.

If you're an access package manager, you can't add resources that you own to a catalog. You're restricted to using the resources available in the catalog. If you need to add resources to a catalog, you can ask the catalog owner.

All access packages must have at least one policy for identities to be assigned to them. Policies specify who can request the access package, along with approval and lifecycle settings, or how access is automatically assigned. When you create an access package, you can create an initial policy for identities in your directory, for identities not in your directory, or for administrator direct assignments only.

![Diagram of an example marketing catalog, including its resources and its access package.](media/entitlement-management-access-package-create/access-package-create.png)

Here are the high-level steps to create an access package with an initial policy:

1. In Identity Governance, start the process to create an access package.
2. Select the catalog where you want to put the access package and ensure that it has the necessary resources.
3. Add resource roles from resources in the catalog to your access package.
4. Specify an initial policy for identities who can request access for themselves or [on-behalf-of other identities](entitlement-management-request-behalf).
5. Specify approval settings and lifecycle settings in that policy.

Then once the access package is created, you can [change the hidden setting](entitlement-management-access-package-edit#change-the-hidden-setting), [add or remove resource roles](entitlement-management-access-package-resources), and [add additional policies](entitlement-management-access-package-request-policy).

## Start the creation process

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner or Access Package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Select **New access package**.

    ![Screenshot that shows the button for creating a new access package in the Microsoft Entra admin center.](media/entitlement-management-shared/access-packages-list.png)

## Configure basics

On the **Basics** tab, you give the access package a name and specify which catalog to create the access package in.

1. Enter a display name and description for the access package. Users see this information when they submit a request for the access package.
2. In the **Catalog** dropdown list, select the catalog where you want to put the access package. For example, you might have a catalog owner who manages all the marketing resources that can be requested. In this case, you could select the marketing catalog.

    You see only catalogs that you have permission to create access packages in. To create an access package in an existing catalog, you must be at least an Identity Governance Administrator. Or you must be a catalog owner or access package manager in that catalog.

    ![Screenshot that shows basic information for a new access package.](media/entitlement-management-access-package-create/basics.png)

    If you're at least an Identity Governance Administrator, or catalog creator, and you want to create your access package in a new catalog that's not listed, select **Create new catalog**. Enter the catalog name and description, and then select **Create**.

    The access package that you're creating, and any resources included in it, are added to the new catalog. Later, you can add more catalog owners or add attributes to the resources that you put in the catalog. To learn more about how to edit the attributes list for a specific catalog resource and the prerequisite roles, read [Add resource attributes in the catalog](entitlement-management-catalog-create#add-resource-attributes-in-the-catalog).
3. Select **Next: Resource roles**.

## Select resource roles

On the **Resource roles** tab, you select the resources to include in the access package. Identities who request and receive the access package receive all the resource roles, such as group membership in the access package.

If you're not sure which resource roles to include, you can skip adding them while creating the access package, and then [add them](entitlement-management-access-package-resources) later.

1. Select the resource type that you want to add (**Groups and Teams**, **Applications**, **SharePoint sites**, **Microsoft Entra role (Preview)**, or **API Permissions (Preview)**.
2. In the **Select applications** panel that appears, select one or more resources from the list.

    ![Screenshot that shows the panel for selecting applications for resource roles in a new access package.](media/entitlement-management-access-package-create/resource-roles.png)

    If you're creating the access package in the general catalog or a new catalog, you can choose any resource from the directory that you own. You must be at least an Identity Governance Administrator, or catalog creator.

    Note

    You can add dynamic membership groups to a catalog and to an access package. However, you can select only the owner role when you're managing a dynamic group resource in an access package.

    If you're creating the access package in an existing catalog, you can select any resource that's already in the catalog without needing to be an owner of that resource.

    If you're at least an Identity Governance Administrator, or catalog owner, you have the additional option of selecting resources that you own or administer but that aren't yet in the catalog. If you select resources in the directory but not currently in the selected catalog, these resources are also added to the catalog for other catalog administrators to build access packages with. To see all the resources in the directory that can be added to the catalog, select the **See all** checkbox at the top of the panel. If you want to select only resources that are currently in the selected catalog, leave the **See all** checkbox cleared (the default state).
3. In the **Role** list, select the role that you want identities to be assigned for the resource. For more information on selecting the appropriate roles for a resource, see [how to determine which resource roles to include in an access package](entitlement-management-access-package-resources#determine-which-resource-roles-to-include-in-an-access-package).

    ![Screenshot that shows resource role selection for a new access package.](media/entitlement-management-access-package-create/resource-roles-role.png)

    For SharePoint Online sites with a large number of roles, use the search box to find the role you want to add to the access package. Search returns matching SharePoint roles even when all available roles aren't initially displayed in the list.
4. For [groups managed by Privileged Identity Management](privileged-identity-management/groups-discover-groups), both active and eligible roles are available as options. ![Screenshot of available roles to be assigned to PIM for groups resource in an access package.](media/entitlement-management-access-package-create/pim-for-groups-roles.png)
5. For [assigning Microsoft Entra roles](entitlement-management-roles), both active and eligible member assignments are available as options.
6. For [including API permissions](entitlement-management-access-package-resources#add-an-api-permission) as a resource role of an access package for service principals or agent IDs, select one or more API permissions from the list. API permissions can be either delegated or application permissions, depending on whether the agent is working alongside the user or operating autonomously on its own. ![Screenshot of adding API permissions as resource roles to an access package.](media/entitlement-management-access-package-create/api-permissions-roles.png)
7. Select **Next: Requests**.

## Create the initial policy

On the **Requests** tab, you create the first policy to specify who can request the access package. You also configure approval settings for that policy. Later, after creating the access package with this initial policy, you can [add more policies](entitlement-management-access-package-request-policy) to allow additional groups of identities to request the access package with their own approval settings, or to assign access automatically.

![Screenshot that shows the Requests tab for a new access package.](media/entitlement-management-access-package-create/requests.png)

Depending on which identities you want to be able to request this access package, perform the steps in one of the following sections Allow users, service principals, and agent identities in your directory to request the access package, Allow identities not in your directory to request the access package or Allow administrator direct assignments only. If you're not sure which request or approval settings you'll need, you plan to create assignments for identities who already have access to the underlying resources, or you plan to use access package automatic assignment polices to automate access, then select the direct assignment policy as the initial policy.

## Allow users, service principals, and agent identities in your directory to request the access package

Use the following steps if you want to allow identities in your directory to be able to request this access package. When you're defining the request policy, you can specify individual identities or (more commonly) groups of identities. For example, your organization might already have a group such as **All employees**. If that group is added in the policy for identities who can request access, any member of that group can then request access.

1. In the **Who can get access** section, select **For users, service principals, and agent identities in your directory**.

    When you select this option, new options appear so you can refine who in your directory can request this access package.

    ![Screenshot that shows the option for allowing users and groups in the directory to request an access package.](../includes/media/entitlement-management-request-policy/for-users-in-your-directory.png)
2. Select one of the following options:

    | Option | Description |
    | --- | --- |
    | **Specific users and groups** | Choose this option if you want only the users and groups in your directory that you specify to be able to request this access package. |
    | **All members (excluding guests)** | Choose this option if you want all member users in your directory to be able to request this access package. This option doesn't include any guest users you might have invited into your directory. |
    | **All users (including guests)** | Choose this option if you want all member users and guest users in your directory to be able to request this access package. |
    | **All Service principals** | Choose this option if you want all service principals in your directory to be able to request this access package. |
    | **All agents** | Choose this option if you want all agents in your directory to be able to have access assigned to them. |

    Guest users are external identities who have been invited into your directory via [Microsoft Entra B2B](../external-id/what-is-b2b). For more information about the differences between member users and guest users, see [What are the default user permissions in Microsoft Entra ID?](../fundamentals/users-default-permissions).

    The **All Service principals** and **All agents** options require Microsoft Entra Agent ID. For more information, see [Governing agent identities](agent-id-governance-overview).
3. If you selected **Specific users and groups**, select **Add users and groups**.
4. On the **Select users and groups** pane, select the users and groups that you want to add.

    ![Screenshot that shows the pane for selecting users and groups for an access package.](../includes/media/entitlement-management-request-policy/select-users-groups.png)
5. Choose **Select** to add the users and groups.
6. Skip down to the Specify approval settings section.

## Allow identities not in your directory to request the access package

Identities who are in another Microsoft Entra directory or domain might not have been invited into your directory yet. Microsoft Entra directories must be configured to allow invitations in **Collaboration restrictions**. For more information, see [Configure external collaboration settings](../external-id/external-collaboration-settings-configure).

A guest identity account will be created for an identity not yet in your directory whose request is approved or does not need approval. The guest will be invited but won't receive an invite email. Instead, they'll receive an email when their access package assignment is delivered. Later, when that guest user no longer has any access package assignments because the last assignment expired or was canceled, the account will be blocked from sign-in and subsequently deleted. The blocking and deletion happen by default.

If you want guest users to remain in your directory indefinitely, even if they have no access package assignments, you can change the settings for your entitlement management configuration. For more information about the guest user object, see [Properties of a Microsoft Entra B2B collaboration user](../external-id/user-properties).

Follow these steps if you want to allow identities not in your directory to request the access package:

1. In the **Who can get access** section, select **For users not in your directory**.

    When you select this option, new options appear.

    ![Screenshot that shows the option for allowing users and groups not in the directory to request an access package.](../includes/media/entitlement-management-request-policy/for-users-not-in-your-directory.png)
2. Select one of the following options:

    | Option | Description |
    | --- | --- |
    | **Specific connected organizations** | Choose this option if you want to select from a list of organizations that your administrator previously added. All users from the selected organizations can request this access package. |
    | **All connected organizations** | Choose this option if all users from all your configured connected organizations can request this access package. |
    | **All users (All connected organizations + any new external users)** | Choose this option if any users can request this access package and the B2B allow list or block list settings should take precedence for any new external user. |

    A connected organization is an external Microsoft Entra directory or domain that you have a relationship with.
3. If you selected **Specific connected organizations**, select **Add directories** to select from a list of connected organizations that your administrator previously added.
4. Enter the name or domain name to search for a previously connected organization.

    ![Screenshot that shows the search box for selecting a directory for requests to an access package.](../includes/media/entitlement-management-request-policy/select-directories.png)

    If the organization that you want to collaborate with isn't in the list, you can ask your administrator to add it as a connected organization. For more information, see [Add a connected organization](entitlement-management-organization).
5. If you selected **All connected organizations**, then you should confirm the list of connected organizations that are currently configured and planned to be in scope.
6. If you selected **All users**, then you will need to configure approvals in the approvals section, as this scope would allow any identity on the Internet to request access.
7. After you select all your connected organizations, choose **Select**.

    All users from the selected connected organizations will be able to request this access package. This includes users in Microsoft Entra ID from all subdomains associated with the organization, unless the Azure B2B allow list or block list blocks those domains. If you specify a social identity provider domain, such as **live.com**, then any user from the social identity provider will be able to request this access package. For more information, see [Allow or block invitations to B2B users from specific organizations](../external-id/allow-deny-list).
8. Skip down to the Specify approval settings section.

## Allow administrator direct assignments only

Follow these steps if you want to bypass access requests and allow administrators to directly assign specific users and agents to this access package. Users won't have to request the access package. You can still set lifecycle settings, but there are no request settings.

1. In the **Who can get access** section, select **None (administrator direct assignments only)**.

    ![Screenshot that shows the option for allowing only administrator direct assignments for an access package.](../includes/media/entitlement-management-request-policy/none-admin-direct-assignments-only.png)

    After you create the access package, you can directly assign specific internal and external users to it. If you specify an external user, a guest user account is created in your directory. For information about directly assigning a user, see [View, add, and remove assignments for an access package](entitlement-management-access-package-assignments).
2. Skip down to the Who can request access section.

## Specify approval settings

In the **Approval** section, you specify whether an approval is required when identities request this access package. The approval settings work in the following way:

- Only one of the selected approvers or fallback approvers needs to approve a request for single-stage approval.
- Only one of the selected approvers from each stage needs to approve a request for two-stage approval.
- An approver can be a manager, a sponsor of a user, an internal sponsor, or an external sponsor, depending on access governance for the policy.
- Approval from every selected approver isn't required for single-stage or two-stage approval.
- The approval decision is based on whichever approver reviews the request first.

For a demonstration of how to add approvers to a request policy, watch the following video:

For a demonstration of how to add a multiple-stage approval to a request policy, watch the following video:

Follow these steps to specify the approval settings for requests for the access package:

1. To require approval for requests from the selected identities, set the **Require approval** toggle to **Yes**. Or, to have requests automatically approved, set the toggle to **No**. If the policy allows external identities from outside your organization to request access, you should require approval, so there is oversight on who is being added to your organization's directory.
2. To require identities to provide a justification to request the access package, set the **Require requestor justification** toggle to **Yes**.
3. Determine if requests require single-stage or two-stage approval. Set the **How many stages** toggle to **1** for single-stage approval, **2** for two-stage approval, or **3** for three-stage approval.

    ![Screenshot that shows approval settings for requests to an access package.](../includes/media/entitlement-management-request-policy/approval.png)

Use the following steps to add approvers after you select the number of stages.

### Single-stage approval

1. Add the **First Approver** information:

    - If the policy is set to **For users in your directory**, you can select either **Manager as approver** or **Sponsors as approvers**. Or, you can add a specific user by selecting **Choose specific approvers**, and then selecting **Add approvers**.

        To use **Sponsors as approvers** for **Approval**, you must have a Microsoft Entra ID Governance license. For more information, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access/microsoft-entra-id-governance?rtc=1).

        ![Screenshot that shows options for a first approver if the policy is set to users in your directory.](../includes/media/entitlement-management-request-policy/approval-single-stage-first-approver-manager.png)
    - If the policy is set to **For users not in your directory**, you can select either **External sponsor** or **Internal sponsor**. Or, you can add a specific user by selecting **Choose specific approvers**, and then selecting **Add approvers**.

        ![Screenshot that shows options for a first approver if the policy is set to users not in your directory.](../includes/media/entitlement-management-request-policy/out-directory-first-approver.png)
2. If you selected **Manager** as the first approver, select **Add fallback** to select one or more users or groups in your directory to be a fallback approver. Fallback approvers receive the request if entitlement management can't find the manager for the user who's requesting access.

    Entitlement management finds the manager by using the **Manager** attribute. The attribute is in the user's profile in Microsoft Entra ID. For more information, see [Add or update a user's profile information and settings](../fundamentals/how-to-manage-user-profile-info).
3. If you selected **Sponsors** as the first approver, select **Add fallback** to select one or more users or groups in your directory to be a fallback approver. Fallback approvers receive the request if entitlement management can't find the sponsor for the user who's requesting access.

    Entitlement management finds sponsors by using the **Sponsors** attribute. The attribute is in the user's profile in Microsoft Entra ID. For more information, see [Add or update a user's profile information and settings](../fundamentals/how-to-manage-user-profile-info).
4. If you selected **Choose specific approvers**, select **Add approvers** to select one or more users or groups in your directory to be approvers.
5. In **Decision must be made in how many days?** box, specify the number of days that an approver has to review a request for this access package.

    If a request isn't approved within this time period, it's automatically denied. The user must then submit another request for the access package.
6. To require approvers to provide a justification for their decision, set **Require approver justification** to **Yes**.

    The justification is visible to other approvers and the requestor.

### Two-stage approval

If you selected a two-stage approval, you need to add a second approver:

1. Add the **Second Approver** information:

    - If the users are in your directory, you can select **Sponsors as approvers**. Or, add a specific user by selecting **Choose specific approvers** from the dropdown menu, and then selecting **Add approvers**.

        ![Screenshot that shows options for a second approver if the policy is set to users in your directory.](../includes/media/entitlement-management-request-policy/in-directory-second-approver.png)
    - If the users aren't in your directory, select **Internal sponsor** or **External sponsor** as the second approver. After you select the approver, add the fallback approvers.

        ![Screenshot that shows options for a second approver if the policy is set to users not in your directory.](../includes/media/entitlement-management-request-policy/out-directory-second-approver.png)
2. In the **Decision must be made in how many days?** box, specify the number of days the second approver has to approve the request.
3. Set the **Require approver justification** toggle to **Yes** or **No**.

### Three-stage approval

If you selected a three-stage approval, you need to add a third approver:

1. Add the **Third Approver** information:

    If the users are in your directory, add a specific user as the third approver by selecting **Choose specific approvers** &gt; **Add approvers**.

    ![Screenshot that shows options for a third approver if the policy is set to users in your directory.](../includes/media/entitlement-management-request-policy/in-directory-third-approver.png)
2. In the **Decision must be made in how many days?** box, specify the number of days the second approver has to approve the request.
3. Set the **Require approver justification** toggle to **Yes** or **No**.

### Alternate approvers

You can specify alternate approvers, similar to specifying the first and second approvers who can approve requests. Having alternate approvers helps ensure that the requests are approved or denied before they expire (time out). You can list alternate approvers for the first approver and the second approver for two-stage approval.

When you specify alternate approvers, if the first or second approvers can't approve or deny the request, the pending request is forwarded to the alternate approvers. The request is sent according to the forwarding schedule that you specified during policy setup. The approvers receive an email to approve or deny the pending request.

After the request is forwarded to the alternate approvers, the first or second approvers can still approve or deny the request. Alternate approvers use the same **My Access** site to approve or deny the pending request.

You can list people or groups of people to be approvers and alternate approvers. Ensure that you list different sets of people to be the first, second, and alternate approvers. For example, if you listed Alice and Bob as the first approvers, list Carol and Dave as the alternate approvers.

Use the following steps to add alternate approvers to an access package:

1. Under **First Approver**, **Second Approver**, or both, select **Show advanced request settings**.

    ![Screenshot of the selection for showing advanced request settings.](../includes/media/entitlement-management-request-policy/alternate-approvers-click-advanced-request.png)
2. Set the **If no action taken, forward to alternate approvers?** toggle to **Yes**.
3. Select **Add alternate approvers**, and then select the alternate approvers from the list.

    ![Screenshot that shows advanced request settings, including the link for adding alternate approvers.](../includes/media/entitlement-management-request-policy/alternate-approvers-add.png)

    If you select **Manager** as the first approver, an extra option appears in the **Alternate Approver** box: **Second level manager as alternate approver**. If you select this option, you need to add a fallback approver to forward the request to, in case the system can't find the second-level manager.
4. In the **Forward to alternate approver(s) after how many days** box, enter the number of days the approvers have to approve or deny a request. If no approvers approve or deny the request before the request duration, the request expires (times out). The user must then submit another request for the access package.

Requests can only be forwarded to alternate approvers a day after the request duration reaches half-life. The decision of the main approvers must time out after at least four days. If the request time-out is less or equal than three days, there isn't enough time to forward the request to alternate approvers.

In this example, the duration of the request is 14 days. The request duration reaches half-life at day 7. So, the request can't be forwarded earlier than day 8.

Also, requests can't be forwarded on the last day of the request duration. So in the example, the latest the request can be forwarded is day 13.

## Email Notifications

1. You're able to disable assignment emails notifying you of assignment requests that are delivered, expired, or near expiration. ![Screenshot of the email notifications selection in creating an access package.](../includes/media/entitlement-management-request-policy/email-notifications.png)

You can always either enable, or disable, email notifications in the future after you finish creating the access package.

## Who can request access

Note

Previously, a setting called "*Enable new requests and assignments*" controlled self-service access requests. This capability is now more accurately reflected by the "*Self*" option.

1. After deciding who the access package is for you can designate who can request access for the access package. You can choose Self, Admin, or Manager as those who can request access.

You can always enable it in the future, after you finish creating the access package.

If you selected **None (administrator direct assignments only)** and you set enable to **No**, then administrators can't directly assign this access package.

![Screenshot that shows the option for enabling new requests and assignments.](../includes/media/entitlement-management-request-policy/enable-requests.png)

1. Go to the next section to learn how to add a verified ID requirement to your access package. Otherwise, select **Next**.

## Add a verified ID requirement

Use the following steps if you want to add a verified ID requirement to your access package policy. Users who want access to the access package need to present the required verified IDs before successfully submitting their request. To learn how to configure your tenant with the Microsoft Entra Verified ID service, see [Introduction to Microsoft Entra Verified ID](../verified-id/decentralized-identifier-overview).

You need a Global Administrator role to add verified ID requirements to an access package in a request policy. An Identity Governance administrator, user administrator, catalog owner, or access package manager can't yet add verified ID requirements.

1. Select **+ Add issuer**, and then select an issuer from the Microsoft Entra Verified ID network. If you want to issue your own credentials to users, you can find instructions in [Issue Microsoft Entra Verified ID credentials from an application](../verified-id/verifiable-credentials-configure-issuer).

    ![Screenshot that shows the pane for selecting an issuer for an access package.](../includes/media/entitlement-management-request-policy/access-package-select-issuer.png)
2. Select the credential types that you want users to present during the request process.

    ![Screenshot that shows the area for selecting credential types for an access package.](../includes/media/entitlement-management-request-policy/access-package-select-credential.png)

    If you select multiple credential types from one issuer, users will be required to present credentials of all selected types. Similarly, if you include multiple issuers, users will be required to present credentials from each of the issuers that you include in the policy. To give users the option of presenting different credentials from various issuers, configure separate policies for each issuer or credential type you'll accept.
3. Select **Add** to add the verified ID requirement to the access package policy.

## Add requestor information to an access package

1. Go to the **Requestor information** tab, and then select the **Questions** tab.
2. In the **Question** box, enter a question that you want to ask the requestor. This question is also known as the display string.
3. If you want to add your own localization options, select **add localization**.

    ![Screenshot that shows the box for entering a question for a requestor.](../includes/media/entitlement-management-request-policy/add-requestor-info-question.png)

    On the **Add localizations for question** pane:

    1. For **Language code**, select the language code for the language in which you're localizing the question.
    2. In the **Localized Text** box, enter the question in the language that you configured.
    3. When you finish adding all the localizations that you need, select **Save**.

    ![Screenshot that shows localization selections for a question.](../includes/media/entitlement-management-request-policy/add-localization-question.png)
4. For **Answer format**, select the format in which you want requestors to answer. Answer formats include **Short text**, **Multiple choice**, and **Long text**.
5. If you selected multiple choice, select the **Edit and localize** button to configure the answer options.

    ![Screenshot that shows multiple choice selected as an answer format, along with the button for editing and localizing answer options.](../includes/media/entitlement-management-request-policy/answer-format-view-edit.png)

    On the **View/edit question** pane:

    1. In the **Answer values** boxes, enter the response options that you want to give when the requestor is answering the question.
    2. In the **Language** boxes, select the language for the response options. You can localize response options if you choose extra languages.
    3. Select **Save**.

    ![Screenshot that shows options for editing and localizing multiple-choice answers.](../includes/media/entitlement-management-request-policy/answer-multiple-choice.png)
6. To require requestors to answer this question when they're requesting access to an access package, select the **Required** checkbox.
7. Select the **Attributes** tab to view attributes associated with resources that you added to the access package.

    Note

    To add or update attributes for an access package's resources, go to **Catalogs** and find the catalog associated with the access package. To learn more about how to edit the attributes list for a specific catalog resource and the prerequisite roles, read [Add resource attributes in the catalog](entitlement-management-catalog-create#add-resource-attributes-in-the-catalog).
8. Select **Next**.

## Specify a lifecycle

On the **Lifecycle** tab, you specify when an identity's assignment to the access package expires. You can also specify whether identities can extend their assignments.

1. In the **Expiration** section, set **Access package assignments expire** to **On date**, **Number of days**, **Number of hours**, or **Never**.

    - For **On date**, select an expiration date in the future.
    - For **Number of days**, specify a number from 0 to 3660 days.
    - For **Number of hours**, specify how many hours.

    Based on your selection, a user's assignment to the access package expires on a certain date, some days after they're approved, or never.
2. If you want the user to request a specific start and end date for their access, select **Yes** for the **Users can request specific timeline** toggle.
3. Select **Show advanced expiration settings** to show more settings.

    ![Screenshot that shows lifecycle expiration settings for an access package.](../includes/media/entitlement-management-lifecycle-policy/expiration.png)
4. To allow the user to extend their assignments, set **Allow users to extend access** to **Yes**.

    If extensions are allowed in the policy, the user receives an email 14 days before, and then one day before, their access package assignment is set to expire. The email prompts the user to extend the assignment. The user must still be in the scope of the policy at the time that they request an extension.

    Also, if the policy has an explicit end date for assignments, and a user submits a request to extend access, the extension date in the request must be at or before when assignments expire. The policy that you used to grant the user access to the access package defines whether the extension date is at or before the assignment expiration. For example, if the policy indicates that assignments are set to expire on June 30, the maximum extension that a user can request is June 30.

    If a user's access is extended, they won't be able to request the access package after the specified extension date (the date set in the time zone of the user who created the policy).
5. To require approval to grant an extension, set **Require approval to grant extension** to **Yes**.

    This approval will use the same approval settings that you specified on the **Requests** tab.
6. If you want to **Require an access review** for this access package, move the toggle to **Yes**. Refer to the [detailed article on configuring the access review](/en-us/entra/id-governance/entitlement-management-access-reviews-create) and then return back here to finish setting up the access package.
7. If you didn't require an access review, or once you have configured it, select **Next** or **Update**.

## Review and create the access package

On the **Review + create** tab, you can review your settings and check for any validation errors.

1. Review the access package's settings.

    ![Screenshot that shows a summary of access package configuration.](media/entitlement-management-access-package-create/review-create.png)
2. Select **Create** to create the access package and its initial policy.

    The new access package appears in the list of access packages.
3. If the access package is intended to be visible to everyone in scope of the policies, then leave the **Hidden** setting of the access package at **No**. Optionally, if you intend to only allow identities with the direct link to request the access package, [edit the access package](entitlement-management-access-package-edit#change-the-hidden-setting) to change the **Hidden** setting to **Yes**. Then [copy the link to request the access package](entitlement-management-access-package-settings#share-link-to-request-an-access-package) and share it with identities who need access.
4. You can next [add more policies](entitlement-management-access-package-request-policy) to the access package, [configure separation of duties checks](entitlement-management-access-package-incompatible), or [directly assign an identity](entitlement-management-access-package-assignments#directly-assign-an-identity).

## Create an access package programmatically

There are two ways to create an access package programmatically: through Microsoft Graph and through the PowerShell cmdlets for Microsoft Graph.

### Create an access package by using Microsoft Graph

You can create an access package by using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission can call the API to:

1. [List the resources in the catalog](/en-us/graph/api/accesspackagecatalog-list-resources?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) and [create an accessPackageResourceRequest](/en-us/graph/api/entitlementmanagement-post-resourcerequests?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) for any resources that aren't yet in the catalog.
2. [Retrieve the roles and scopes of each resource in the catalog](/en-us/graph/api/accesspackagecatalog-list-resources?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true). This list of roles will then be used to select a role, when subsequently creating a resourceRoleScope.
3. [Create an accessPackage](/en-us/graph/api/entitlementmanagement-post-accesspackages?view=graph-rest-1.0&amp;preserve-view=true).
4. [Create a resourceRoleScope](/en-us/graph/api/accesspackage-post-resourcerolescopes?view=graph-rest-1.0&amp;preserve-view=true) for each resource role needed in the access package.
5. [Create an assignmentPolicy](/en-us/graph/api/entitlementmanagement-post-assignmentpolicies?view=graph-rest-1.0&amp;preserve-view=true) for each policy needed in the access package.

### Create an access package by using Microsoft PowerShell

You can also create an access package in PowerShell by using the cmdlets from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module.

First, retrieve the ID of the catalog, and of the resource in that catalog and its scopes and roles, that you want to include in the access package. Use a script similar to the following example:

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"

$catalog = Get-MgEntitlementManagementCatalog -Filter "displayName eq 'Marketing'" -All
if ($catalog -eq $null) { throw "catalog not found" }
$rsc = Get-MgEntitlementManagementCatalogResource -AccessPackageCatalogId $catalog.id -Filter "originSystem eq 'AadApplication'" -ExpandProperty scopes
if ($rsc -eq $null) { throw "resource not found" }
$filt = "(id eq '" + $rsc.Id + "')"
$rrs = Get-MgEntitlementManagementCatalogResourceRole -AccessPackageCatalogId $catalog.id -Filter $filt -ExpandProperty roles,scopes
```

Then, create the access package:

```powershell

$params = @{
    displayName = "sales reps"
    description = "outside sales representatives"
    catalog = @{
        id = $catalog.id
    }
}
$ap = New-MgEntitlementManagementAccessPackage -BodyParameter $params

```

After you create the access package, assign the resource roles to it. For example, if you want to include the first resource role of the resource returned earlier as a resource role of the new access package, and the role has an ID, you can use a script similar to this one:

```powershell

$rparams = @{
    role = @{
        id =  $rrs.Roles[0].Id
        displayName =  $rrs.Roles[0].DisplayName
        description =  $rrs.Roles[0].Description
        originSystem =  $rrs.Roles[0].OriginSystem
        originId =  $rrs.Roles[0].OriginId
        resource = @{
            id = $rrs.Id
            originId = $rrs.OriginId
            originSystem = $rrs.OriginSystem
        }
    }
    scope = @{
        id = $rsc.Scopes[0].Id
        originId = $rsc.Scopes[0].OriginId
        originSystem = $rsc.Scopes[0].OriginSystem
    }
}

New-MgEntitlementManagementAccessPackageResourceRoleScope -AccessPackageId $ap.Id -BodyParameter $rparams
```

If the role doesn't have an ID, then don't include the `id` parameter of the `role` structure in the request payload.

Finally, create the policies. In this policy, only the administrators or access package assignment managers can assign access, and there are no access reviews. For more examples, see [Create an assignment policy through PowerShell](entitlement-management-access-package-request-policy#create-an-access-package-assignment-policy-through-powershell) and [Create an assignmentPolicy](/en-us/graph/api/entitlementmanagement-post-assignmentpolicies?tabs=http&amp;view=graph-rest-1.0&amp;preserve-view=true).

```powershell

$pparams = @{
    displayName = "New Policy"
    description = "policy for assignment"
    allowedTargetScope = "notSpecified"
    specificAllowedTargets = @(
    )
    expiration = @{
        endDateTime = $null
        duration = $null
        type = "noExpiration"
    }
    requestorSettings = @{
        enableTargetsToSelfAddAccess = $false
        enableTargetsToSelfUpdateAccess = $false
        enableTargetsToSelfRemoveAccess = $false
        allowCustomAssignmentSchedule = $true
        enableOnBehalfRequestorsToAddAccess = $false
        enableOnBehalfRequestorsToUpdateAccess = $false
        enableOnBehalfRequestorsToRemoveAccess = $false
        onBehalfRequestors = @(
        )
    }
    requestApprovalSettings = @{
        isApprovalRequiredForAdd = $false
        isApprovalRequiredForUpdate = $false
        stages = @(
        )
    }
    accessPackage = @{
        id = $ap.Id
    }
}
New-MgEntitlementManagementAssignmentPolicy -BodyParameter $pparams

```

For more information, see [Create an access package in entitlement management for an application with a single role using PowerShell](entitlement-management-access-package-create-app).