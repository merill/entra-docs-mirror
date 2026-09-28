---
layout: Conceptual
title: How to investigate why a service principal was created in your tenant - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-view-service-principal-creation-with-audit-log-properties
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Use new audit log properties to understand why a new service principal was added to your tenant.
ms.topic: how-to
ms.date: 2026-06-05T00:00:00.0000000Z
ms.reviewer: arielsc
ai-usage: ai-assisted
locale: en-us
document_id: 69b20978-43f3-5f26-f8cb-5a6682fdce04
document_version_independent_id: 69b20978-43f3-5f26-f8cb-5a6682fdce04
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-view-service-principal-creation-with-audit-log-properties.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-view-service-principal-creation-with-audit-log-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-view-service-principal-creation-with-audit-log-properties.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 6ed9836e-783e-7bc3-0d0e-ca62e1c3a1cb
---

# How to investigate why a service principal was created in your tenant - Microsoft Entra ID | Microsoft Learn

When a new service principal appears in your tenant, you might want to understand why it was created and who or what initiated the process. The [new audit log properties](understand-service-principal-creation-with-new-audit-log-properties)`ServicePrincipalProvisioningType`, `SubscribedSkus`, and `AppOwnerOrganizationId` help you quickly determine whether the service principal was provisioned by Microsoft, created by a user, or added by an external application. The following steps show you how to access these properties in the Microsoft Entra admin center to use them in your investigations. You can also leverage Microsoft Graph API and Log Analytics to access these new properties.

## Prerequisites

To view and use these properties in Microsoft Entra audit logs, you need:

- Access to the Microsoft Entra admin center.
- One of the following roles (or a role with equivalent permissions): [Security Administrator](../role-based-access-control/permissions-reference#security-administrator), [Security Reader](../role-based-access-control/permissions-reference#security-reader), or [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
- Audit logging enabled for your tenant. For more information, see the [Microsoft Entra audit logs overview](concept-audit-logs).

## View audit log properties to understand service principal details

To view audit log properties in the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Browse to **Monitoring & health** &gt; **Audit logs**.
3. Set **Category** to **ApplicationManagement** and apply the filter.
4. Filter **Activity** to **Add service principal** and apply the filter.
5. Select an event and expand **Additional details**. Look for these properties `ServicePrincipalProvisioningType`, `SubscribedSkus`, and `AppOwnerOrganizationId`.

If you send audit logs to Log Analytics, Microsoft Sentinel, or another destination, the same properties are available in the **AuditLogs** table under the **AdditionalDetails** JSON. You can parse these fields in your queries to group events by provisioning type, SKU, or owning tenant.

## Investigate the new service principal

Once the new properties are available in your tenant, you can use them to streamline investigations into new service principals in Log Analytics and Microsoft Sentinel:

1. Start with `ServicePrincipalProvisioningType` to distinguish Microsoft-driven provisioning from direct user or app activity in your tenant.
2. When the value is subscription, review `SubscribedSkus` to see which subscriptions or service plans in your tenant made the Microsoft service principal eligible for just-in-time provisioning.
3. Use `AppOwnerOrganizationId` to understand whether the app is homed in your tenant, in a Microsoft services tenant, or in another external tenant.
4. Combine these fields with existing audit log properties such as `initiatedBy` and `targetResources` to get a full picture of who or what created the service principal, without relying on additional API calls.

Note

The `AppOwnerOrganizationId` property will only show for events where there is a backing application object. The `SubscribedSkus` property will only show for events when `ServicePrincipalProvisioningType` = `Subscription`.

These enhancements are designed to make it easier for you to interpret service principal creation events, quickly understand the meaning of different values, and plug that information into your own alerting and governance workflows. These alerts can categorize service principal creation events as "expected" versus "unexpected" based on your tenant security preferences.

## Use Microsoft Graph

To retrieve these events programmatically, query the [List directoryAudits](/en-us/graph/api/directoryaudit-list?view=graph-rest-1.0&amp;preserve-view=true) operation and filter on the activity name. The new properties are returned in the `additionalDetails` collection of each event.

```http
GET https://graph.microsoft.com/v1.0/auditLogs/directoryAudits?$filter=activityDisplayName eq 'Add service principal'
```