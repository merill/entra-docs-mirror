---
layout: Conceptual
title: Discover the current state of external collaboration in your organization - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/2-secure-access-current-state
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Discover the current state of an organization's collaboration with audit logs, reporting, allowlist, blocklist, and more.
ms.reviewer: gasinh
ms.topic: how-to
ms.date: 2023-02-23T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 1d4bcc71-9d63-caf6-8c8e-542062669f0e
document_version_independent_id: d010c541-87c5-2643-790d-dc89985a29af
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/2-secure-access-current-state.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/2-secure-access-current-state
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/2-secure-access-current-state.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ffc9e65b-b0d2-74cc-1966-c2996b29046f
---

# Discover the current state of external collaboration in your organization - Microsoft Entra | Microsoft Learn

Before you learn about the current state of your external collaboration, determine a security posture. Consider centralized vs. delegated control, also governance, regulatory, and compliance targets.

Learn more: [Determine your security posture for external access with Microsoft Entra ID](1-secure-access-posture)

Users in your organization likely collaborate with users from other organizations. Collaboration occurs with productivity applications like Microsoft 365, by email, or sharing resources with external users. These scenarios include users:

- Initiating external collaboration
- Collaborating with external users and organizations
- Granting access to external users

## Before you begin

This article is number 2 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Determine who initiates external collaboration

Generally, users seeking external collaboration know the applications to use, and when access ends. Therefore, determine users with delegated permissions to invite external users, create access packages, and complete access reviews.

To find collaborating users:

- Microsoft 365 [Audit log activities](/en-us/purview/audit-log-activities?view=o365-worldwide&amp;preserve-view=true) - search for events and discover activities audited in Microsoft 365
- [Auditing and reporting a B2B collaboration user](../external-id/auditing-and-reporting) - verify Guest User access, and see records of system and user activities

## Enumerate guest users and organizations

External users might be Microsoft Entra B2B users with partner-managed credentials, or external users with locally provisioned credentials. Typically, these users are the Guest UserType. To learn about inviting guests users and sharing resources, see [B2B collaboration overview](../external-id/what-is-b2b).

You can enumerate guest users with:

- [Microsoft Graph API](/en-us/graph/api/user-list?tabs=http)
- [PowerShell](/en-us/graph/api/user-list?tabs=http)
- [Azure portal](../identity/users/users-bulk-download)

Use the following tools to identify Microsoft Entra B2B collaboration, external Microsoft Entra tenants, and users accessing applications:

- PowerShell module, [Get MsIdCrossTenantAccessActivity](https://github.com/AzureAD/MSIdentityTools/wiki/Get-MSIDCrossTenantAccessActivity)
- [Cross-tenant access activity workbook](../identity/monitoring-health/workbook-cross-tenant-access-activity)

### Discover email domains and companyName property

You can determine external organizations with the domain names of external user email addresses. This discovery might not be possible with consumer identity providers. We recommend you write the companyName attribute to identify external organizations.

### Use allowlist, blocklist, and entitlement management

Use the allowlist or blocklist to enable your organization to collaborate with, or block, organizations at the tenant level. Control B2B invitations and redemptions regardless of source (such as Microsoft Teams, SharePoint, or the Azure portal).

See, [Allow or block invitations to B2B users from specific organizations](../external-id/allow-deny-list)

If you use entitlement management, you can confine access packages to a subset of partners with the **Specific connected organizations** option, under New access packages, in Identity Governance.

![Screenshot of settings and options under Identity Governance, New access package.](media/secure-external-access/2-new-access-package.png)

## Determine external user access

With an inventory of external users and organizations, determine the access to grant to the users. You can use the Microsoft Graph API to determine Microsoft Entra group membership or application assignment.

- [Working with groups in Microsoft Graph](/en-us/graph/api/resources/groups-overview?context=graph/context&amp;view=graph-rest-1.0&amp;preserve-view=true)
- [Applications API overview](/en-us/graph/applications-concept-overview?view=graph-rest-1.0&amp;preserve-view=true)

### Enumerate application permissions

Investigate access to your sensitive apps for awareness about external access. See, [Grant or revoke API permissions programmatically](/en-us/graph/permissions-grant-via-msgraph?view=graph-rest-1.0&amp;tabs=http&amp;pivots=grant-application-permissions&amp;preserve-view=true).

### Detect informal sharing

If your email and network plans are enabled, you can investigate content sharing through email or unauthorized software as a service (SaaS) apps.

- Identify, prevent, and monitor accidental sharing
    - Learn about [data loss prevention (DLP)](/en-us/purview/dlp-learn-about-dlp?view=o365-worldwide&amp;preserve-view=true)
- Identify unauthorized apps
    - [Microsoft Defender for Cloud Apps overview](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)