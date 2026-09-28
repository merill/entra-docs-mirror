---
layout: Conceptual
title: Learn about the audit logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-audit-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the types of activities and events that are captured in Microsoft Entra audit logs and how you can use the logs for troubleshooting.
ms.topic: concept-article
ms.date: 2026-06-05T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange,agent-id-ignite
locale: en-us
document_id: 378b87c1-ae6d-6b16-57b9-5f312583b8bd
document_version_independent_id: bdf6b43b-ac28-f1ac-e53b-d99f22d0754c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-audit-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-audit-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-audit-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 7bdb73bb-30ad-9797-acab-4b26c0cba84c
---

# Learn about the audit logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Microsoft Entra activity logs include audit logs, which is a comprehensive report on every logged event in Microsoft Entra ID. Changes to applications, groups, users, and licenses are all captured in the Microsoft Entra audit logs.

Three other activity logs are also available to help monitor the health of your tenant:

- **[Sign-ins](concept-sign-ins)** – Information about sign-ins and how your resources are used by your users.
- **[Sign-ups (preview)](concept-sign-ups)** - For [external tenants](../../external-id/tenant-configurations) only, information about all self-service sign-up attempts, including successful sign-ups and failed attempts.
- **[Provisioning](concept-provisioning-logs)** – Activities performed by the provisioning service, such as the creation of a group in ServiceNow or a user imported from Workday.

This article gives you an overview of the audit logs, such as the information they provide and what kinds of questions they can answer.

## What can you do with audit logs?

Audit logs in Microsoft Entra ID provide access to system activity records, often needed for compliance. You can get answers to questions related to users, groups, and applications.

**Users:**

- What types of changes were recently applied to users?
- How many users were changed?
- How many passwords were changed?

**Groups:**

- What groups were recently added?
- Have the owners of group been changed?
- What licenses are to a group or a user?

**Applications:**

- What applications were, updated, or removed?
- Has a service principal for an application changed?
- Who or what created a service principal, and why was it created?
- Have the names of applications been changed?

**Custom security attributes:**

- What changes were made to [custom security attribute](../../fundamentals/custom-security-attributes-overview) definitions or assignments?
- What updates were made to attribute sets?
- What custom attribute values were assigned to a user?

**Agents:**

- What operations were performed by a specific agent?
- What changes were made to an agent service principal?
- What details of an agent ID were changed?

Note

Entries in the audit logs are system generated and can't be changed or deleted.

## What do the logs show?

Audit logs display several valuable details on the activities in your tenant. Key details are visible at-a-glance in the table, with more details available by selecting a specific log entry. The Microsoft Entra admin center defaults to the **Directory** tab, which displays the following information:

- Date and time of the occurrence
- Service that logged the occurrence
- Category and name of the activity
- Status of the activity

By selecting a specific log entry, you get even more details, such as:

- Correlation ID for troubleshooting
- Details about the actor or target resource associated with the activity
- Where applicable, old and new values for the changed properties

Note

In the audit log details, the IP address reflects the OAuth client's IP address. The IP address is the TCP peer of the service's endpoint.

A second tab for **Custom Security** displays audit logs for custom security attributes. To view data on this tab, you must have the [Attribute Log Administrator](../role-based-access-control/permissions-reference#attribute-log-administrator) or [Attribute Log Reader](../role-based-access-control/permissions-reference#attribute-log-reader) role. This audit log shows all activities related to custom security attributes. For more information, see [What are custom security attributes](../../fundamentals/custom-security-attributes-overview).

![Screenshot of the audit logs, with the Directory and Custom Security tabs highlighted.](media/concept-audit-logs/audit-log-tabs.png)

For a full list of the available audit activities, see [Audit activity reference](reference-audit-activities).

## Microsoft 365 activity logs

You can view Microsoft 365 activity logs from the [Microsoft 365 admin center](/en-us/microsoft-365/admin/admin-overview/admin-center-overview). Even though Microsoft 365 activity and Microsoft Entra activity logs share many directory resources, only the Microsoft 365 admin center provides a full view of the Microsoft 365 activity logs.

You can also access the Microsoft 365 activity logs programmatically by using the [Office 365 Management APIs](/en-us/office/office-365-management-api/office-365-management-apis-overview).

Most standalone or bundled Microsoft 365 subscriptions have back-end dependencies on some subsystems within the Microsoft 365 datacenter boundary. The dependencies require some information write-back to keep directories in sync and essentially to help enable hassle-free onboarding in a subscription opt-in for Exchange Online. For these write-backs, audit log entries show actions taken by "Microsoft Substrate Management." These audit log entries refer to create/update/delete operations executed by Exchange Online to Microsoft Entra ID. The entries are informational and don't require any action.