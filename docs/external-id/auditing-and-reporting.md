---
layout: Conceptual
title: Auditing and reporting a B2B collaboration user - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/auditing-and-reporting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Guest user properties are configurable in Microsoft Entra B2B collaboration
ms.topic: how-to
ms.date: 2024-10-21T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: e3423f0e-220b-a02c-f1b2-75221f4c8ac8
document_version_independent_id: 2f14d8c3-daff-4209-491b-3253fa4fcc6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/auditing-and-reporting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/auditing-and-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/auditing-and-reporting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6e64a7af-7f07-c95a-5444-a6a445b47fef
---

# Auditing and reporting a B2B collaboration user - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

With guest users, you have auditing capabilities similar to with member users.

## Access reviews

You can use access reviews to periodically verify whether guest users still need access to your resources. The **Access reviews** feature is available in **Microsoft Entra ID** under **ID Governance** &gt; **Access reviews**. To learn how to use access reviews, see [Manage guest access with Microsoft Entra access reviews](../id-governance/manage-guest-access-with-access-reviews).

## Audit logs

The Microsoft Entra audit logs provide records of system and user activities, including activities initiated by guest users. To access audit logs, browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**. To access audit logs of one specific user, select **Entra ID** &gt; **Users** &gt; select the user &gt; **Audit logs**.

[![Screenshot showing an example of audit log output.](media/auditing-and-reporting/audit-log.png)](media/auditing-and-reporting/audit-log-large.png#lightbox)

You can dive into each of these events to get the details. For example, let's look at the user management details.

[![Screenshot showing an example of activity details output.](media/auditing-and-reporting/activity-details.png)](media/auditing-and-reporting/activity-details-large.png#lightbox)

You can also export these logs from Microsoft Entra ID and use the reporting tool of your choice to get customized reports.

## Sponsors field for B2B users

You can also manage and track your guest users in the organization using the sponsors feature. The **Sponsors** field on the user account displays who is responsible for the guest user. A sponsor can be a user or a group. To learn more about the sponsors feature, see [Add sponsors to a guest user](b2b-sponsors).

### Related content

- [Troubleshoot B2B collaboration](troubleshoot)