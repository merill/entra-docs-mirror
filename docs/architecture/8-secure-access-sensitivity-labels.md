---
layout: Conceptual
title: Control external access to resources in Microsoft Entra ID with sensitivity labels - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/8-secure-access-sensitivity-labels
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Use sensitivity labels as a part of your overall security plan for external access
ms.topic: how-to
ms.date: 2023-02-23T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
ms.subservice: architecture
locale: en-us
document_id: f01f7cda-1178-f395-87f2-58ad17c02e6e
document_version_independent_id: 4ac926e1-e6da-91ec-ee57-fe99e18927ce
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/8-secure-access-sensitivity-labels.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/8-secure-access-sensitivity-labels
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/8-secure-access-sensitivity-labels.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 73fb873b-f8ee-aab0-d54f-60e7daf67062
---

# Control external access to resources in Microsoft Entra ID with sensitivity labels - Microsoft Entra | Microsoft Learn

Use sensitivity labels to help control access to your content in Office 365 applications, and in containers like Microsoft Teams, Microsoft 365 Groups, and SharePoint sites. They protect content without hindering user collaboration. Use sensitivity labels to send organization-wide content across devices, apps, and services, while protecting data. Sensitivity labels help organizations meet compliance and security policies.

See, Learn about [sensitivity labels](/en-us/purview/sensitivity-labels?preserve-view=true&amp;view=o365-worldwide)

## Before you begin

This article is number 8 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Assign classification and enforce protection settings

You can classify content without adding any protection settings. Content classification assignment stays with the content while it's used and shared. The classification generates usage reports with sensitive-content activity data.

Enforce protection settings such as encryption, watermarks, and access restrictions. For example, users apply a Confidential label to a document or email. The label can encrypt the content and add a Confidential watermark. In addition, you can apply a sensitivity label to a container like a SharePoint site, and help manage external users access.

Learn more:

- [Restrict access to content by using sensitivity labels to apply encryption](/en-us/purview/encryption-sensitivity-labels?preserve-view=true&amp;view=o365-worldwide)
- [Use sensitivity labels to protect content in Microsoft Teams, Microsoft 365 Groups, and SharePoint sites](/en-us/purview/sensitivity-labels-teams-groups-sites)

Sensitivity labels on containers can restrict access to the container, but content in the container doesn't inherit the label. For example, a user takes content from a protected site, downloads it, and then shares it without restrictions, unless the content had a sensitivity label.

Note

To apply sensitivity labels users sign in to their Microsoft work or school account.

## Permissions to create and manage sensitivity levels

Team members who need to create sensitivity labels require permissions to:

- Microsoft 365 Defender portal or
- [Microsoft Purview portal](/en-us/purview/purview-portal?view=o365-worldwide&amp;preserve-view=true)

By default, [Global Administrators](../identity/role-based-access-control/permissions-reference#global-administrator) have access to admin centers and can provide access, without granting tenant Admin permissions. For this delegated limited admin access, add users to the following role groups:

- Compliance Data Administrator,
- Compliance Administrator, or
- Security Administrator

## Sensitivity label strategy

As you plan the governance of external access to your content, consider content, containers, email, and more.

### High, Medium, or Low Business Impact

To define high business impact (HBI), medium business impact (MBI), or low business impact (LBI) for data, sites, and groups, consider the effect on your organization if the wrong content types are shared.

- Credit card, passport, national/regional ID numbers
    - [Apply a sensitivity label to content automatically](/en-us/purview/apply-sensitivity-label-automatically?preserve-view=true&amp;view=o365-worldwide)
- Content created by corporate officers: compliance, finance, executive, and so on.
- Strategic or financial data in libraries or sites.

Consider the content categories that external users can't have access to, such as containers and encrypted content. You can use sensitivity labels, enforce encryption, or use container access restrictions.

### Email and content

Sensitivity labels can be applied automatically or manually to content.

See, [Apply a sensitivity label to content automatically](/en-us/purview/apply-sensitivity-label-automatically?view=o365-worldwide&amp;preserve-view=true)

#### Sensitivity labels on email and content

A sensitivity label in a document or email is customizable, clear text, and persistent.

- **Customizable** - create labels for your organization and determine the resulting actions
- **Clear text** - is incorporated in metadata and readable by applications and services
- **Persistency** - ensures the label and associated protections stay with the content, and help enforce policies

Note

Each content item can have one sensitivity label applied.

### Containers

Determine the access criteria if Microsoft 365 Groups, Teams, or SharePoint sites are restricted with sensitivity labels. You can label content in containers or use automatic labeling for files in SharePoint, OneDrive, and so on.

Learn more: [Get started with sensitivity labels](/en-us/purview/get-started-with-sensitivity-labels?preserve-view=true&amp;view=o365-worldwide)

#### Sensitivity labels on containers

You can apply sensitivity labels to containers such as Microsoft 365 Groups, Microsoft Teams, and SharePoint sites. Sensitivity labels on a supported container apply the classification and protection settings to the connected site or group. Sensitivity labels on these containers can control:

- **Privacy** - select the users who can see the site
- **External user access** - determine whether group owners can add guests to a group
- **Access from unmanaged devices** - decide whether and how unmanaged devices access content

    ![Screenshot of options and entries under Site and group settings.](media/secure-external-access/8-edit-label.png)

Sensitivity labels applied to a container, such as a SharePoint site, aren't applied to content in the container; they control access to content in the container. Labels can be applied automatically to the content in the container. For users to manually apply labels to content, enable sensitivity labels for Office files in SharePoint and OneDrive.

Learn more:

- [Enable sensitivity labels for Office files in SharePoint and OneDrive](/en-us/purview/sensitivity-labels-sharepoint-onedrive-files?view=o365-worldwide&amp;preserve-view=true).
- [Use sensitivity labels to protect content in Microsoft Teams, Microsoft 365 Groups, and SharePoint sites](/en-us/purview/sensitivity-labels-teams-groups-sites)
- [Assign sensitivity labels to Microsoft 365 groups in Microsoft Entra ID](../identity/users/groups-assign-sensitivity-labels)

### Implement sensitivity labels

After you determine use of sensitivity labels, see the following documentation for implementation.

- [Get started with sensitivity labels](/en-us/purview/get-started-with-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)
- [Create and publish sensitivity labels](/en-us/purview/create-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)
- [Restrict access to content by using sensitivity labels to apply encryption](/en-us/purview/encryption-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)