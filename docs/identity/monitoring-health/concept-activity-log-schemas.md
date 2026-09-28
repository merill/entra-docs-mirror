---
layout: Conceptual
title: Learn about the monitoring and health activity log schemas - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-activity-log-schemas
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to interpret the details found in the Microsoft Entra audit and sign-in and logs schema.
ms.topic: concept-article
ms.date: 2025-05-27T00:00:00.0000000Z
ms.reviewer: egreenberg
locale: en-us
document_id: 10773330-19b0-66be-1f98-5901e7c5dbb4
document_version_independent_id: 10773330-19b0-66be-1f98-5901e7c5dbb4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-activity-log-schemas.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-activity-log-schemas
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-activity-log-schemas.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 58fad80f-fe06-343d-a912-a0b5f3772f20
---

# Learn about the monitoring and health activity log schemas - Microsoft Entra ID | Microsoft Learn

This article describes the information contained in the Microsoft Entra activity logs and how that schema is used by other services. This article covers the schemas from the Microsoft Entra admin center and Microsoft Graph. Descriptions of some key fields are provided.

## Prerequisites

- For license and role requirements, see [Microsoft Entra monitoring and health licensing](../../fundamentals/licensing#microsoft-entra-monitoring-and-health).
- The option to download logs is available in all editions of Microsoft Entra ID.
- Downloading logs programmatically with Microsoft Graph requires a [premium license](../../fundamentals/licensing#microsoft-entra-monitoring-and-health).
- **Reports Reader** is the least privileged role required to view Microsoft Entra activity logs.
- Audit logs are available for features that you've licensed.
- The results of a downloaded log might show `hidden` for some properties if you don't have the required license.

## What is a log schema?

Microsoft Entra monitoring and health offer logs, reports, and monitoring tools that can be integrated with Azure Monitor, Microsoft Sentinel, and other services. These services need to map the properties of the logs to their service's configurations. The schema is the map of the properties, the possible values, and how they're used by the service. Understanding the log schema is helpful for effective troubleshooting and data interpretation.

Microsoft Graph is the primary way to access Microsoft Entra logs programmatically. The response for a Microsoft Graph call is in JSON format and includes the properties and values of the log. The schema of the logs is defined in the [Microsoft Graph documentation](/en-us/graph/api/overview?view=graph-rest-1.0&amp;preserve-view=true).

There are two endpoints for the Microsoft Graph API. The V1.0 endpoint is the most stable and is commonly used for production environments. The beta version often contains more properties, but they're subject to change. For this reason, we don't recommend using the beta version of the schema in production environments.

Microsoft Entra customers can configure activity log streams to be sent to a Log Analytics workspace. This integration enables Security Information and Event Management (SIEM) connectivity, long-term storage, and improved querying capabilities with Log Analytics. The log schemas for Azure Monitor might differ from the Microsoft Graph schemas.

For full details on these schemas, see the following articles:

- [Azure Monitor audit logs](/en-us/azure/azure-monitor/reference/tables/auditlogs)
- [Azure Monitor sign-in logs](/en-us/azure/azure-monitor/reference/tables/signinlogs)
- [Azure Monitor provisioning logs](/en-us/azure/azure-monitor/reference/tables/aadprovisioninglogs)
- [Microsoft Graph audit logs](/en-us/graph/api/resources/directoryaudit?view=graph-rest-1.0&amp;preserve-view=true)
- [Microsoft Graph sign-in logs](/en-us/graph/api/resources/signin?view=graph-rest-1.0&amp;preserve-view=true)
- [Microsoft Graph provisioning logs](/en-us/graph/api/resources/provisioningobjectsummary?view=graph-rest-1.0&amp;preserve-view=true)

## How to interpret the schema

When looking up the definitions of a value, pay attention to the version you're using. There might be differences between the V1.0 and beta versions of the schema.

### Values found in all log schemas

Some values are common across all log schemas.

- `correlationId`: This unique ID helps correlate activities that span across various services and is used for troubleshooting. This value's presence in multiple logs doesn't indicate the ability to join logs across services.
- `status` or `result`: This important value indicates the result of the activity. Possible values are: `success`, `failure`, `timeout`, `unknownFutureValue`.
- Date and time: The date and time when the activity occurred is in Coordinated Universal Time (UTC).
- Some reporting features require a Microsoft Entra ID P2 license. If you don't have the correct licenses, the value `hidden` is returned.

### Audit logs

- `activityDisplayName`: Indicates the activity name or the operation name (examples: "Create User" and "Add member to group"). For more information, see [Audit log activities](reference-audit-activities).
- `category`: Indicates which resource category that's targeted by the activity. For example: `UserManagement`, `GroupManagement`, `ApplicationManagement`, `RoleManagement`. For more information, see [Audit log activities](reference-audit-activities).
- `initiatedBy`: Indicates information about the user or app that initiated the activity.
- `targetResources`: Provides information on which resource was changed. Possible values include `User`, `Device`, `Directory`, `App`, `Role`, `Group`, `Policy` or `Other`.
- `ipAddress`: Found in the `initiatedBy` section, this is the OAuth client's IP address. The IP address is the peer (directly connected client) of the service's endpoint.

### Sign-in logs

- ID values: There are unique identifiers for users, tenants, applications, and resources. Examples include:
    - `resourceId`: The *resource* that the user signed into.
    - `resourceTenantId`: The tenant that owns the *resource* being accessed. Might be the same as the `homeTenantId`.
    - `homeTenantId`: The tenant that owns the user *account* that is signing in.
- Risk details: Provides the reason behind a specific state of a risky user, sign-in, or risk detection.
    - `riskState`: Reports status of the risky user, sign-in, or a risk event.
    - `riskDetail`: Provides the reason behind a specific state of a risky user, sign-in, or risk detection. The value `none` means that no action has been performed on the user or sign-in so far.
    - `riskEventTypes_v2`: Risk detection types associated with the sign-in.
    - `riskLevelAggregated`: Aggregated risk level. The value `hidden` means the user or sign-in wasn't enabled for Microsoft Entra ID Protection.
- `crossTenantAccessType`: Describes the type of cross-tenant access used to access the resource. For example, B2B, Microsoft Support, and passthrough sign-ins are captured here.
- `status`: The sign-in status that includes the error code and description of the error (if a sign-in failure occurs).

### Applied Conditional Access policies

The `appliedConditionalAccessPolicies` subsection lists the Conditional Access policies related to that sign-in event. The section is called *applied* Conditional Access policies; however, policies that were *not* applied also appear in this section. A separate entry is created for each policy. For more information, see [conditionalAccessPolicy resource type](/en-us/graph/api/resources/conditionalaccesspolicy?view=graph-rest-1.0&amp;preserve-view=true).