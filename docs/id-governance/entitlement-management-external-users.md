---
layout: Conceptual
title: Govern access for external users in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-external-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about the settings you can specify to govern access for external users in entitlement management.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
ms.reviewer: mwahl
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7bd8b41a-26fd-936b-5773-3eb158de253a
document_version_independent_id: eac9538f-02c5-efec-77ed-1059777c294d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-external-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-external-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-external-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 25380023-2f46-99f8-b1de-e92ece952cd3
---

# Govern access for external users in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

Entitlement management uses [Microsoft Entra business-to-business (B2B)](../external-id/what-is-b2b) to share access so you can collaborate with people outside your organization. With Microsoft Entra B2B, external users authenticate to their home directory, but have a representation in your directory. The representation in your directory enables the user to be assigned access to your resources.

This article describes the settings you can specify to govern access for external users.

## How entitlement management can help

When using the [Microsoft Entra B2B](../external-id/what-is-b2b) invite experience, you must already know the email addresses of the external guest users you want to bring into your resource directory and work with. Directly inviting each user works great when you're working on a smaller or short-term project and you already know all the participants. This process is harder to manage if you have lots of users you want to work with, or if the participants change over time. For example, you might be working with another organization and have one point of contact with that organization, but over time more users from that organization will also need access.

With entitlement management, you can define a policy that allows users from organizations you specify to be able to self-request an access package. That policy includes whether approval is required, whether access reviews are required, and an expiration date for the access. In most cases, you want to require approval, in order to have appropriate oversight over which users are brought into your directory. If approval is required, then for major external organization partners, you might consider inviting one or more users from the external organization to your directory, designating them as sponsors, and configuring that sponsors are approvers - since they're likely to know which external users from their organization need access. Once you've configured the access package, obtain the access package's request link so you can send that link to your contact person (sponsor) at the external organization. That contact can share with other users in their external organization, and they can use this link to request the access package. Users from that organization who are already invited into your directory can also use that link.

You can also use entitlement management for bringing in users from organizations that don't have their own Microsoft Entra directory. You can configure a federated identity provider for their domain, or use email-based authentication. You can also bring in users from social identity providers, including those with Microsoft accounts.

Typically, when a request is approved, entitlement management provisions the user with the necessary access. If the user isn't already in your directory, entitlement management will first invite the user. When the user is invited, Microsoft Entra ID automatically creates a B2B guest account for them, but won't send the user an email. An administrator might have limited which organizations are allowed for collaboration, by setting a [B2B allow or blocklist](../external-id/allow-deny-list) to allow or block invites to other organization's domains. If the user's domain isn't allowed by those lists, then they aren't invited and can't be assigned access until the lists are updated.

Since you don't want the external user's access to last forever, you specify an expiration date in the policy, such as 180 days. After 180 days, if their access isn't extended, entitlement management will remove all access associated with that access package. By default, if the user who was invited through entitlement management has no other access package assignments, then when they lose their last assignment, their guest account is blocked from signing in for 30 days, and later removed. This prevents the proliferation of unnecessary accounts. As described in the following sections, these settings are configurable.

## How access works for external users

The following diagram and steps provide an overview of how external users are granted access to an access package.

![Diagram showing the lifecycle of external users](media/entitlement-management-external-users/external-users-lifecycle.png)

1. You [add a connected organization](entitlement-management-organization) for the Microsoft Entra directory or domain you want to collaborate with. You can also configure a connected organization for a social identity provider.
2. You check the catalog setting **Enabled for external users** in the catalog to contain the access package is **Yes**.
3. You create an access package in your directory that includes a policy [For identities not in your directory](entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package) and specifies the connected organizations that can request, the approver and lifecycle settings. If you select in the policy the option of specific connected organizations or the option of all connected organizations, then only users from those organizations that have previously been configured can request. If you select in the policy the option of all users, then any user can request, including those which aren't already part of your directory and not part of any connected organization.
4. You check [the hidden setting on the access package](entitlement-management-access-package-edit#change-the-hidden-setting) to ensure the access package is hidden. If it isn't hidden, then any user allowed by the policy settings in that access package can browse for the access package in the My Access portal for your tenant.
5. You send a [My Access portal link](entitlement-management-access-package-settings) to your contact at the external organization that they can share with their users to request the access package.
6. An external user (**Requestor A** in this example) uses the My Access portal link to [request access](entitlement-management-request-access) to the access package. The My access portal requires that the user sign in as part of their connected organization. How the user signs in depends on the authentication type of the directory or domain that's defined in the connected organization and in the external users settings.
7. An approver [approves the request](entitlement-management-request-approve) (assuming the policy requires approval).
8. The request goes into the [delivering state](entitlement-management-process).
9. Using the B2B invite process, a guest user account is created in your directory (**Requestor A (Guest)** in this example). If an [allowlist or a blocklist](../external-id/allow-deny-list) is defined, the list setting is applied.
10. The guest user is assigned access to all of the resources in the access package. It can take some time for changes to be made in Microsoft Entra ID and to other Microsoft Online Services or connected SaaS applications. For more information, see [When changes are applied](entitlement-management-access-package-resources#when-changes-are-applied).
11. The external user receives an email indicating that their access was [delivered](entitlement-management-process).
12. To access the resources, the external user can either select the link in the email or attempt to access any of the directory resources directly to complete the invitation process.
13. If the policy settings include an expiration date, then later when the access package assignment for the external user expires, the external user's access rights from that access package are removed.
14. Depending on the lifecycle of external users settings, when the external user no longer has any access package assignments, the external user is blocked from signing in, and the external user account is removed from your directory.

## Settings for external users

To ensure people outside of your organization can request access packages and get access to the resources in those access packages, there are some settings that you should verify are properly configured.

### Enable catalog for external users

- By default, when you create a [new catalog](entitlement-management-catalog-create), it's enabled to allow external users to request access packages in the catalog. Make sure **Enabled for external users** is set to **Yes**.

    ![Edit catalog settings](media/entitlement-management-shared/catalog-edit.png)

    If you're an administrator or catalog owner, you can view the list of catalogs currently enabled for external users in the Microsoft Entra admin center list of catalogs, by changing the filter setting for **Enabled for external users** to **Yes**. If any of those catalogs shown in that filtered view have a nonzero number of access packages, those access packages might have a policy [for users not in your directory](entitlement-management-access-package-request-policy#for-users-not-in-your-directory) that allow external users to request.

### Configure your Microsoft Entra B2B external collaboration settings

- Allowing guests to invite other guests to your directory means that guest invites can occur outside of entitlement management. We recommend setting **Guests can invite** to **No** to only allow for properly governed invitations.
- If you have been previously using the B2B allowlist, you must either remove that list, or make sure all the domains of all the organizations you want to partner with using entitlement management are added to the list. Alternatively, if you're using the B2B blocklist, you must make sure no domain of any organization you want to partner with is present on that list.
- If you create an entitlement management policy for **All users** (All connected organizations + any new external users), and a user doesn’t belong to a connected organization in your directory, a connected organization will automatically be created for them when they request the package. However, any B2B [allow or blocklist](../external-id/allow-deny-list) settings you have takes precedence. Therefore, you want to remove the allowlist, if you were using one, so that **All users** can request access, and exclude all authorized domains from your blocklist if you're using a blocklist.
- If you want to create an entitlement management policy that includes **All users** (All connected organizations + any new external users), you must first enable email one-time passcode authentication for your directory. For more information, see [Email one-time passcode authentication](../external-id/one-time-passcode).
- For more information about Microsoft Entra B2B external collaboration settings, see [Configure external collaboration settings](../external-id/external-collaboration-settings-configure).

    [![Microsoft Entra external collaboration settings](media/entitlement-management-external-users/collaboration-settings.png)](media/entitlement-management-external-users/collaboration-settings.png#lightbox)

### Review your cross-tenant access settings

- Ensure your cross-tenant access settings for inbound B2B collaboration allow access to be requested and assigned. You should check that the settings allow tenants that are part of your current or future connected organizations, and that the users from those tenants aren't blocked from being invited. In addition, check that those users are permitted by the cross-tenant access settings to be able to authenticate to the applications for which you want to enable collaboration scenarios. For more information, see [Configure cross-tenant access settings](../external-id/cross-tenant-access-settings-b2b-collaboration).
- If you create a connected organization for a Microsoft Entra tenant from a different Microsoft cloud, you also need to configure cross-tenant access settings appropriately. For more information, see [Configure Microsoft cloud settings](../external-id/cross-cloud-settings).

### Review your Conditional Access policies

- Make sure to exclude the Entitlement Management app from any Conditional Access policies that impact guest users. Otherwise, a Conditional Access policy could block them from accessing MyAccess or being able to sign in to your directory. For example, guests likely don't have a registered device, aren't in a known location, and don't want to re-register for multifactor authentication (MFA), so adding these requirements in a Conditional Access policy will block guests from using entitlement management. For more information, see [What are conditions in Microsoft Entra Conditional Access?](../identity/conditional-access/concept-conditional-access-conditions).
- If the Conditional Access is blocking all cloud applications, in addition to excluding the Entitlement Management App, ensure that the *Request Approvals Read Platform* is also excluded in your Conditional Access policy. Start by confirming that you have the necessary roles: Conditional Access Administrator, Application Administrator, Attribute Assignment Administrator, and Attribute Definition Administrator. Then, create a custom security attribute with a suitable name and values. Locate the service principal for *Request Approvals Read Platform* in Enterprise Applications, and assign the custom attribute with the chosen value to this application. In your Conditional Access policy, apply a filter to exclude selected applications based on the custom attribute name and value assigned to *Request Approvals Read Platform*. For more details on filtering applications in Conditional Access policies, refer to: [Conditional Access: Filter for applications](../identity/conditional-access/concept-filter-for-applications)

    ![Screenshot of exclude app options.](media/entitlement-management-external-users/exclude-app-guests.png)

    ![Screenshot of selection to exclude cloud apps.](media/entitlement-management-external-users/exclude-cloud-apps.png)

    ![Screenshot of the exclude guests app selection.](media/entitlement-management-external-users/exclude-app-guests-selection.png)

Note

The Entitlement Management app includes the entitlement management side of MyAccess, the Entitlement Management side of the Microsoft Entra admin center, and the Entitlement Management part of MS graph. The latter two require additional permissions for access, hence won't be accessed by guests unless explicit permission is provided.

### Review your SharePoint Online external sharing settings

- If you want to include SharePoint Online sites in your access packages for external users, make sure that your organization-level external sharing setting is set to **Anyone** (users don't require sign in), or **New and existing guests** (guests must sign in or provide a verification code). For more information, see [Turn external sharing on or off](/en-us/sharepoint/turn-external-sharing-on-or-off#change-the-organization-level-external-sharing-setting).
- If you want to restrict any external sharing outside of entitlement management, you can set the external sharing setting to **Existing guests**. Then, only new users that are invited through entitlement management are able to gain access to these sites. For more information, see [Turn external sharing on or off](/en-us/sharepoint/turn-external-sharing-on-or-off#change-the-organization-level-external-sharing-setting).
- Make sure that the site-level settings enable guest access (same option selections as previously listed). For more information, see [Turn external sharing on or off for a site](/en-us/sharepoint/change-external-sharing-site).

### Review your Microsoft 365 group sharing settings

- If you want to include Microsoft 365 groups in your access packages for external users, make sure the **Let users add new guests to the organization** is set to **On** to allow guest access. For more information, see [Manage guest access to Microsoft 365 Groups](/en-us/microsoft-365/admin/create-groups/manage-guest-access-in-groups#manage-groups-guest-access).
- If you want external users to be able to access the SharePoint Online site and resources associated with a Microsoft 365 group, make sure you turn on SharePoint Online external sharing. For more information, see [Turn external sharing on or off](/en-us/sharepoint/turn-external-sharing-on-or-off#change-the-organization-level-external-sharing-setting).
- For information about how to set the guest policy for Microsoft 365 groups at the directory level in PowerShell, see [Example: Configure Guest policy for groups at the directory level](../identity/users/groups-settings-cmdlets#example-configure-guest-policy-for-groups-at-the-directory-level).

### Review your Teams sharing settings

- If you want to include Teams in your access packages for external users, make sure the **Allow guest access in Microsoft Teams** is set to **On** to allow guest access. For more information, see [Configure guest access in the Microsoft Teams admin center](/en-us/microsoftteams/set-up-guests#configure-guest-access-in-the-teams-admin-center).

## Manage the lifecycle of external users

You can select what happens when an external user, who was invited to your directory through making an access package request, no longer has any access package assignments. This can happen if the user relinquishes all their access package assignments, or their last access package assignment expires. By default, when an external user no longer has any access package assignments, they're blocked from signing in to your directory. After 30 days, their guest user account is removed from your directory. You can also configure that an external user isn't blocked from sign in or deleted, or that an external user isn't blocked from sign in but is deleted.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Control Configurations**.
3. Select **View settings** on the Lifecycle of external users setting card. ![Screenshot of external settings for ID governance.](media/entitlement-management-external-users/settings-external-users.png)
4. On the settings page, you'll see a list of actions to take for external users onboarded via an access package once their last access package assignment expires. This includes options to **Remove external user**, **Block external user from signing in to directory**, and **Number of days before removing external user from directory**. ![Screenshot of the external settings options.](media/entitlement-management-external-users/external-settings-list.png)
5. Once an external user loses their last assignment to any access packages, if you want to remove their guest user account in this directory, check the **Remove external user** box.

    Note

    Entitlement management only removes external guest user accounts that were invited through entitlement management or that were added to entitlement management for lifecycle management by having their guest user account [converted to governed](entitlement-management-access-package-manage-lifecycle). A user will be removed from this directory even if that user was added to resources in this directory that weren't access package assignments. If the guest was present in this directory prior to receiving access package assignments, they'll remain. However, if the guest was invited through an access package assignment, and after being invited was also assigned to a OneDrive or SharePoint Online site, they'll still be removed. Changing the **Remove external user** setting to **No** only affects users who later lose their last access package assignment; users that were scheduled for deletion and are blocked from sign in will still be deleted on their original schedule.
6. Once an external user loses their last assignment to any access packages, if you want to block them from signing in to this directory, check the **Block external user from signing in to this directory** box.

    Note

    Entitlement management only blocks external guest user accounts from signing in that were invited through entitlement management or that were added to entitlement management for lifecycle management by having their guest user account [converted to governed](entitlement-management-access-package-manage-lifecycle). A user will be blocked from signing in even if that user was added to resources in this directory that weren't access package assignments. If a user is blocked from signing in to this directory, then the user is unable to re-request the access package or request additional access in this directory. Don't configure blocking them from signing in if they'll later need to request access to this or other access packages.
7. If you want to remove the guest user account in this directory, you can set the number of days before it's removed. While an external user is notified when their access package expires, there's no notification when their account is removed. If you want to remove the guest user account as soon as they lose their last assignment to any access packages, set **Number of days before removing external user from this directory** to **0**. Changes to this value only affect users who subsequently use their last access package assignment; users that were scheduled for deletion will still be deleted on their original schedule.
8. Select **Save**.