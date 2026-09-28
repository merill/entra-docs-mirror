---
layout: Conceptual
title: Secure external access to Microsoft Teams, SharePoint, and OneDrive with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/9-secure-access-teams-sharepoint
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Secure access to Microsoft 365 services as a part of your external access security plan
ms.topic: how-to
ms.date: 2023-02-28T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: da9be29d-f5d8-22f4-32e5-f2c76f850214
document_version_independent_id: 7053e636-ea15-da4b-475d-826a9eb7364a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/9-secure-access-teams-sharepoint.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/9-secure-access-teams-sharepoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/9-secure-access-teams-sharepoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fd866488-90c2-e5d5-8659-cdcfa978ee0d
---

# Secure external access to Microsoft Teams, SharePoint, and OneDrive with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Use this article to determine and configure your organization's external collaboration using Microsoft Teams, OneDrive for Business, and SharePoint. A common challenge is balancing security and ease of collaboration for end users and external users. If an approved collaboration method is perceived as restrictive and onerous, end users evade the approved method. End users might email unsecured content, or set up external processes and applications, such as a personal Dropbox or OneDrive.

## Before you begin

This article is number 9 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## External Identities settings and Microsoft Entra ID

Sharing in Microsoft 365 is partially governed by the **External Identities, External collaboration settings** in Microsoft Entra ID. If external sharing is disabled or restricted in Microsoft Entra ID, it overrides sharing settings configured in Microsoft 365. An exception is if Microsoft Entra B2B integration isn't enabled. You can configure SharePoint and OneDrive to support ad hoc sharing via one-time password (OTP). The following screenshot shows the External Identities, External collaboration settings dialog.

![Screenshot of options and entries under External Identities, External collaboration settings.](media/secure-external-access/9-external-collaboration-settings-new.png)

Learn more:

- [Microsoft Entra admin center](https://entra.microsoft.com)
- [External Identities in Microsoft Entra ID](../external-id/external-identities-overview)

### Guest User access

Guest users are invited to have access to resources.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Find the **Guest user access** options.
4. To prevent guest-user access to other guest-user details, and to prevent enumeration of group membership, select **Guest users have limited access to properties and memberships of directory objects**.

### Guest invite settings

Guest invite settings determine who invites guests and how guests are invited. The settings are enabled if the B2B integration is enabled. It's recommended that administrators and users, in the Guest Inviter role, can invite. This setting allows setup of controlled collaboration processes. For example:

- Team owner submits a ticket requesting assignment to the Guest Inviter role:

    - Responsible for guest invitations
    - Agrees to not add users to SharePoint
    - Performs regular access reviews
    - Revokes access as needed
- The IT team:

    - After training is complete, the IT team grants the Guest Inviter role
    - Ensures there are sufficient Microsoft Entra ID P2 licenses for the Microsoft 365 group owners who will review
    - Creates a Microsoft 365 group access review
    - Confirms access reviews occur
    - Removes users added to SharePoint

1. Select the banner for **Email one-time passcodes for guests**.
2. For **Enable guest self-service sign up via user flows**, select **Yes**.

### Collaboration restrictions

For the Collaboration restrictions option, the organization's business requirements dictate the choice of invitation.

- **Allow invitations to be sent to any domain (most inclusive)** - any user can be invited
- **Deny invitations to the specified domains** - any user outside those domains can be invited
- **Allow invitations only to the specified domains (most restrictive)** - any user outside those domains can't be invited

## External users and guest users in Teams

Teams differentiates between external users (outside your organization) and guest users (guest accounts). You can manage collaboration setting in the [Microsoft Teams admin center](https://admin.teams.microsoft.com/company-wide-settings/external-communications) under Org-wide settings. Authorized account credentials are required to sign in to the Teams Admin portal.

- **External Access**- Teams allows external access by default. The organization can communicate with all external domains
    - Use External Access setting to restrict or allow domains
- **Guest Access** - manage guest access in Teams

Learn more: [Use guest access and external access to collaborate with people outside your organization](/en-us/microsoftteams/communicate-with-users-from-other-organizations).

The External Identities collaboration feature in Microsoft Entra ID controls permissions. You can increase restrictions in Teams, but restrictions can't be lower than Microsoft Entra settings.

Learn more:

- [Manage external meetings and chat in Microsoft Teams](/en-us/microsoftteams/trusted-organizations-external-meetings-chat)
- [Step 1. Determine your cloud identity model](/en-us/microsoft-365/enterprise/deploy-identity-solution-identity-model)
- [Identity models and authentication for Microsoft Teams](/en-us/microsoftteams/identify-models-authentication)
- [Sensitivity labels for Microsoft Teams](/en-us/microsoftteams/sensitivity-labels)

## Govern access in SharePoint and OneDrive

SharePoint administrators can find organization-wide settings in the SharePoint admin center. It's recommended that your organization-wide settings are the minimum security levels. Increase security on some sites, as needed. For example, for a high-risk project, restrict users to certain domains, and disable members from inviting guests.

Learn more:

- [SharePoint admin center](https://microsoft-admin.sharepoint.com) - access permissions are required
- [Get started with the SharePoint admin center](/en-us/sharepoint/manage-sites-in-new-admin-center)
- [External sharing overview](/en-us/sharepoint/external-sharing-overview)

### Integrating SharePoint and OneDrive with Microsoft Entra B2B

As a part of your strategy to govern external collaboration, it's recommended you enable SharePoint and OneDrive integration with Microsoft Entra B2B. Microsoft Entra B2B has guest-user authentication and management. With SharePoint and OneDrive integration, use one-time passcodes for external sharing of files, folders, list items, document libraries, and sites.

Learn more:

- [Email one-time passcode authentication](../external-id/one-time-passcode)
- [SharePoint and OneDrive integration with Microsoft Entra B2B](/en-us/sharepoint/sharepoint-azureb2b-integration)
- [B2B collaboration overview](../external-id/what-is-b2b)

If you enable Microsoft Entra B2B integration, then SharePoint and OneDrive sharing is subject to the Microsoft Entra organizational relationships settings, such as **Members can invite** and **Guests can invite**.

### Sharing policies in SharePoint and OneDrive

In the Azure portal, you can use the External Sharing settings for SharePoint and OneDrive to help configure sharing policies. OneDrive restrictions can't be more permissive than SharePoint settings.

Learn more: [External sharing overview](/en-us/sharepoint/external-sharing-overview)

![Screenshot of external sharing settings for SharePoint and OneDrive.](media/secure-external-access/9-sharepoint-settings.png)

#### External sharing settings recommendations

Use the guidance in this section when configuring external sharing.

- **Anyone**- Not recommended. If enabled, regardless of integration status, no Azure policies are applied for this link type.
    - Don't enable this functionality for governed collaboration
    - Use it for restrictions on individual sites
- **New and existing guests**- Recommended, if integration is enabled
    - Microsoft Entra B2B integration enabled: new and current guests have a Microsoft Entra B2B guest account you can manage with Microsoft Entra policies
    - Microsoft Entra B2B integration not enabled: new guests don't have a Microsoft Entra B2B account, and can't be managed from Microsoft Entra ID
    - Guests have a Microsoft Entra B2B account, depending on how the guest was created
- **Existing guests**- Recommended, if you don't have integration enabled
    - With this option enabled, users can share with other users in your directory
- **Only people in your organization**- Not recommended with external user collaboration
    - Regardless of integration status, users can share with other users in your organization
- **Limit external sharing by domain**- By default, SharePoint allows external access. Sharing is allowed with external domains.
    - Use this option to restrict or allow domains for SharePoint
- **Allow only users in specific security groups to share externally** - Use this setting to restrict who shares content in SharePoint and OneDrive. The setting in Microsoft Entra ID applies to all applications. Use the restriction to direct users to training about secure sharing. Completion is the signal to add them to a sharing security group. If this setting is selected, and users can't become an approved sharer, they might find unapproved ways to share.
- **Allow guests to share items they don't own** - Not recommended. The guidance is to disable this feature.
- **People who use a verification code must reauthenticate after this many days (default is 30)** - Recommended

### Access controls

Access controls setting affect all users in your organization. Because you might not be able to control whether external users have compliant devices, the controls won't be addressed in this article.

- **Idle session sign-out**- Recommended
    - Use this option to warn and sign out users on unmanaged devices, after a period of inactivity
    - You can configure the period of inactivity and the warning
- **Network location**- Set this control to allow access from IP addresses your organization owns.
    - For external collaboration, set this control if your external partners access resources when in your network, or with your virtual private network (VPN).

### File and folder links

In the SharePoint admin center, you can set how file and folder links are shared. You can configure the setting for each site.

![Screenshot of File and folder links options.](media/secure-external-access/9-file-folder-links.png)

With Microsoft Entra B2B integration enabled, sharing files and folders with users outside the organization results in the creation of a B2B user.

1. For **Choose the type of link that's selected by default when users share files and folders in SharePoint and OneDrive**, select **Only people in your organization**.
2. For **Choose the permission that's selected by default for sharing links**, select **Edit**.

You can customize this setting for a per-site default.

### Anyone links

Enabling Anyone links isn't recommended. If you enable it, set an expiration, and restrict users to view permissions. If you select View only permissions for files or folders, users can't change Anyone links to include edit privileges.

Learn more:

- [External sharing overview](/en-us/sharepoint/external-sharing-overview)
- [SharePoint and OneDrive integration with Microsoft Entra B2B](/en-us/sharepoint/sharepoint-azureb2b-integration)