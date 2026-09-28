---
layout: Conceptual
title: What's new - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/whats-new-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Overview of the What's new experience in the Microsoft Entra admin center.
ms.topic: overview
ms.date: 2024-11-13T00:00:00.0000000Z
locale: en-us
document_id: 4cb4e141-0458-cf08-d4ac-0a45fc983a0f
document_version_independent_id: 4cb4e141-0458-cf08-d4ac-0a45fc983a0f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/whats-new-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/whats-new-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/whats-new-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 80ebb103-4c55-b98e-cea8-2a4928241424
---

# What's new - Microsoft Entra | Microsoft Learn

## Overview

Microsoft Entra is updated regularly to deliver new features, enhance existing functionality, fix defects, and address customer feedback. The best way to stay current with these developments is to visit **What's new** in the [Microsoft Entra admin center](entra-admin-center).

**What's new** is an information hub that provides a consolidated view of the Microsoft Entra roadmap and change announcements. It gives administrators a centralized location to track, learn, and plan for the releases and changes across the Microsoft Entra family of products.

The remaining sections describe the features and functionality of the **What's new** experience.

## Explore What's new

### Highlights

The **Highlights** tab summarizes important product releases and impactful changes. From the Highlights tab, you can select an announcement or release to view its details and access links to documentation for more information.

![Screenshot of the Microsoft Entra What's new Highlights experience in the Microsoft Entra admin center.](media/whats-new/entra-whats-new-highlights.png)

### Roadmap

The **Roadmap** tab lists the details of public preview and recent general availability releases in a sortable table. From the table, you can select a release to view the release **Details**, which includes an overview and a link to learn more.

![Screenshot of the Microsoft Entra What's new Roadmap experience in the Microsoft Entra admin center.](media/whats-new/entra-whats-new-roadmap.png)

To find a release, you can customize the table view using the following controls:

- **Search**: Enter keywords to find a specific release.
- **Add filter**: Filter by **Release Type** or by **State**.
- **Category**: Filter by product and/or feature category (for example, *User Authentication*, *Identity Governance*)
- **Release Date**: Filter by date range.
- **Manage view**: Remove or add columns.

#### Roadmap column descriptions

The following are the descriptions for the sortable columns in the roadmap table:

| Column | Description |
| --- | --- |
| **Title** | Brief description of the product or feature. |
| **Category** | The identity and network access category of the product or feature (for example, *Identity Governance*, *Identity Security & Protection*). |
| **Service** | The Microsoft Entra service of the product or feature (for example, *Entitlement Management*, *Conditional Access*). |
| **Release Type** | The [lifecycle phase](licensing-preview-info) of the release: <br>- *Public Preview*: Available to all customers with the required license. The release might include limited customer support, and standard service level agreements don't apply.<br>- *GA* (general availability): Available to all licensed customers. The release is supported via all Microsoft support channels. |
| **Release Date** | Date the release is made available. |
| **State** | Indicates whether the release is *Available* or *Coming Soon*. |

### Change announcements

The **Change announcements** tab lists the upcoming changes to existing products and features in a sortable table. From the table, you can select a change announcement to view the change **Details**, which includes an overview of what's changing and a link to learn more.

![Screenshot of the Microsoft Entra What's new Change announcements experience in the Microsoft Entra admin center.](media/whats-new/entra-whats-new-change-announcements.png)

To find a change announcement, you can customize the table view using the following controls:

- **Search**: Enter keywords to find a specific release.
- **Add filter**: Filter by **Action Required** or by **Change Type**.
- **Service**: Filter by the product or feature service (for example, *Entitlement Management*, *Conditional Access*)
- **Release Date**: Filter by date range.
- **Manage view**: Remove or add columns.

#### Roadmap column descriptions

The following are the descriptions for the sortable columns in the roadmap table:

| Column | Description |
| --- | --- |
| **Title** | Brief description of the product or feature. |
| **Service** | The Microsoft Entra service of the product or feature (for example, *Entitlement Management*, *Conditional Access*). |
| **Change Type** | The scope of the change: <br>- *UX Change*: A user experience change that doesn't require action.<br>- *Feature Change*: A change to existing functionality that might require action.<br>- *Breaking Change* A change that is expected to break the user experience if no action is taken.<br>- *Deprecation*: The product or feature is no longer available to new customers and is scheduled for retirement. Deprecated products or features are still available and supported for existing customers.<br>- *Retirement*: The product or feature is no longer available or supported.<br>- End of Support: The product or feature is no longer supported for existing customers. |
| **Announcement Date** | Date of the announcement. |
| **Target Date** | The release date of the change. |
| **Action Required** | Indicates whether the change requires a user to take action. |

## What's new FAQ

### Why is a What's new feature needed when the Microsoft 365 and Azure roadmaps already exist?

Not all Microsoft Entra products are part of Microsoft 365 and Azure (for example, Microsoft Entra External ID). The What's new feature ensures transparency about new features and changes across all Microsoft Entra products in a centralized location.

### Is What's new publicly accessible like the Microsoft 365 roadmap?

No, to access What's new you must sign in to the Microsoft Entra admin center. The sign-in requirement enables a more personalized experience, tailored specifically to each tenant in future versions of What's new.

### Can I consume Microsoft Entra updates programmatically and automate processes?

Yes, in the future you can use [Microsoft Graph](/en-us/graph/identity-network-access-overview) to retrieve updates (currently in beta) and automate processes. For example, you can automate responses to feature lifecycle events or integrate them with a product lifecycle management system.

### Can I still use the existing RSS feeds and view the public release notes for What's new information?

Yes, the existing RSS feeds and [release notes](whats-new) are still available.

### Can I access What's new in the Microsoft 365 or Azure portal?

No, What's new is available only in the Microsoft Entra admin center.

### How can I provide feedback about this feature?

To share feedback, go to the **Roadmap** tab or the **Change announcements** tab and select **Got feedback?**.

### Do I need a specific Microsoft Entra role to access What's new?

No, all Microsoft Entra ID roles can access the What's new feature.

### Are there any licensing requirements to access What's new?

No, What's new is available to all Microsoft Entra customers, including Microsoft Entra ID Free.

### Can guest users in my tenant access What's new?

Yes, What's new is accessible to your business guests.

### Is What’s new available to government cloud customers?

Currently, What's new is only available to public cloud customers. But there are plans to deliver the What's new experience to government clouds in the future.

### Does What's new include all Microsoft Entra products?

Yes, What's new provides a consolidated view of the releases and change announcements across the Microsoft Entra product family.