---
layout: Conceptual
title: Users aren't being provisioned in my application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/application-provisioning-config-problem-no-users-provisioned
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Troubleshoot common issues faced when a user isn't appearing in a Microsoft Entra Gallery Application configured for user provisioning with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-04-15T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
locale: en-us
document_id: 4362f184-ede0-a014-654b-c02fdb431150
document_version_independent_id: 3a85b79c-395b-bb6b-5c93-375eea1d5359
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/application-provisioning-config-problem-no-users-provisioned.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/application-provisioning-config-problem-no-users-provisioned
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/application-provisioning-config-problem-no-users-provisioned.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 86e14d8a-ef56-d69f-1555-06a36475bca5
---

# Users aren't being provisioned in my application - Microsoft Entra ID | Microsoft Learn

After automatic provisioning is configured for an application (including verifying that the app credentials provided to Microsoft Entra ID to connect to the app are valid), then users and/or groups are provisioned to the app. Provisioning is determined by the following things:

- Which users and groups have been **assigned** to the application. Provisioning nested groups isn't supported. For more information on assignment, see [Assign a user or group to an enterprise app in Microsoft Entra ID](../enterprise-apps/assign-user-or-group-access-portal).
- Whether or not **attribute mappings** are enabled, and configured to sync valid attributes from Microsoft Entra ID to the app. For more information on attribute mappings, see [Customizing User Provisioning Attribute Mappings for SaaS Applications in Microsoft Entra ID](customize-application-attributes).
- Whether or not there's a **scoping filter** present that is filtering users based on specific attribute values. For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](define-conditional-rules-for-provisioning-user-accounts).

If you observe that users aren't being provisioned, consult the [Provisioning logs](../monitoring-health/concept-provisioning-logs?context=azure/active-directory/manage-apps/context/manage-apps-context) in Microsoft Entra ID. Search for log entries for a specific user.

You can access the provisioning logs in the Microsoft Entra admin center by browsing to **Entra ID** &gt; **Enterprise apps** &gt; **Provisioning logs**. You can also select a specific application and then select **Provisioning logs** in the **Activity** section. You can search the provisioning data based on the name of the user or the identifier in either the source system or the target system. For details, see [Provisioning logs](../monitoring-health/concept-provisioning-logs?context=azure/active-directory/manage-apps/context/manage-apps-context).

The provisioning logs record all the operations performed by the provisioning service, including querying Microsoft Entra ID for assigned users that are in scope for provisioning, querying the target app for the existence of those users, comparing the user objects between the system. Then add, update, or disable the user account in the target system based on the comparison.

## Provisioning service doesn't appear to start

If you set the **Provisioning Status** to be **On** in the **Enterprise applications &gt; [Application Name] &gt;Provisioning** section of the Microsoft Entra admin center. However no other status details are shown on that page after subsequent reloads, it's likely that the service is running but hasn't completed an initial cycle yet. Check the **Provisioning logs** to determine what operations the service is performing, and if there are any errors.

Note

An initial cycle can take anywhere from 20 minutes to several hours, depending on the size of the Microsoft Entra directory and the number of users in scope for provisioning. Subsequent syncs after the initial cycle are faster, as the provisioning service stores watermarks that represent the state of both systems after the initial cycle. The initial cycle improves performance of subsequent syncs.

## Provisioning logs say users are skipped and not provisioned even though they're assigned

When a user shows up as “skipped” in the provisioning logs, it's important to review the **Steps** tab of the log to determine the reason. Common reasons and resolutions:

- **A scoping filter has been configured** **that is filtering the user out based on an attribute value**. For more information on scoping filters, see [scoping filters](define-conditional-rules-for-provisioning-user-accounts).
- **The user is “not effectively entitled”.** If you see this specific error message, it's because there's a problem with the user assignment record stored in Microsoft Entra ID. To fix this issue, unassign the user (or group) from the app, and reassign it again. For more information on assignment, see [Assign user or group access](../enterprise-apps/assign-user-or-group-access-portal).
- **A required attribute is missing or not populated for a user.** An important thing to consider when setting up provisioning is to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Microsoft Entra ID to the application. This configuration includes setting the “matching property” that is used to uniquely identify and match users/groups between the two systems. For more information on this important process, see [Customizing User Provisioning Attribute Mappings for SaaS Applications in Microsoft Entra ID](customize-application-attributes).
- **Attribute mappings for groups:** Provisioning of the group name and group details, in addition to the members, if supported for some applications. You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab. If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”. The matching ID can be the display name or email alias. The group and its members aren't provisioned if the matching property is empty or not populated for a group in Microsoft Entra ID.

## Provisioning users assigned to the default access role

The default role on an application from the gallery is called the "default access" role. Historically, users assigned to this role aren't provisioned and are marked as skipped in the [provisioning logs](../monitoring-health/concept-provisioning-logs) due to being "not effectively entitled."