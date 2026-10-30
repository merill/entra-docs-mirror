---
layout: Conceptual
title: Troubleshoot provisioning to a Microsoft Entra gallery app. - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: How to troubleshoot common issues faced when configuring user provisioning to an application already listed in the Microsoft Entra application gallery.
ms.topic: troubleshooting
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: asteen, arvinh
ai-usage: ai-assisted
locale: en-us
document_id: 9114c9b5-9c13-ae02-5af9-46741fbe7cf1
document_version_independent_id: 9114c9b5-9c13-ae02-5af9-46741fbe7cf1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 332d97eb-f189-86dc-0ba9-01a5b7fdfdcc
---

# Troubleshoot provisioning to a Microsoft Entra gallery app. - Microsoft Entra ID | Microsoft Learn

Troubleshoot configuration for application provisioning. For more information, see [automatic user provisioning](user-provisioning).

Start by finding the setup tutorial for your application. Then follow the steps to configure both the app and Microsoft Entra ID to create the provisioning connection. For a list of tutorials, see [List of Tutorials on How to Integrate SaaS Apps with Microsoft Entra ID](../saas-apps/tutorial-list).

## Check if provisioning is working

Once the service is configured, most insights into the operation of the service can be drawn from two places.

- **Provisioning logs (preview)** – The [provisioning logs](../monitoring-health/concept-provisioning-logs?context=azure/active-directory/manage-apps/context/manage-apps-context) record all operations performed by the provisioning service. The logs include querying Microsoft Entra ID for assigned users that are in scope for provisioning. Query the target app for the existence of those users, comparing the user objects between the system. Then add, update, or disable the user account in the target system based on the comparison. You access the provisioning logs in the Microsoft Entra admin center by selecting **Entra ID** &gt; **Enterprise apps** &gt; **Provisioning logs** in the **Activity** section.
- **Current status –** A summary of the last provisioning run for a given app can be seen in the **Entra ID** &gt; **Enterprise apps** &gt; `[Application Name]` &gt; **Provisioning** section, at the bottom of the screen under the service settings. The Current Status section shows if a provisioning cycle starts provisioning user accounts. Watch the progress of the cycle, see how many users and groups are provisioned, and how many roles are created. If there are errors, details can be found in the [Provisioning logs] (~/identity/monitoring-health/concept-provisioning-logs.md?context=azure/active-directory/manage-apps/context/manage-apps-context).

## Provisioning service doesn't appear to start

You set the **Provisioning Status** to be **On** in the **Entra ID** &gt; **Enterprise apps** &gt; `[Application Name]` &gt; **Provisioning** section of the Microsoft Entra admin center. However, no other status details are shown on the page after subsequent reloads. It's likely that the service is running but an initial cycle didn't complete. Check the **Provisioning logs** to determine what operations the service is performing, and if there are any errors.

Note

An initial cycle takes between 20 minutes and several hours. The time depends on the size of the Microsoft Entra directory and the number of users in scope for provisioning. Subsequent syncs are faster, as the provisioning service stores watermarks that represent the state of both systems after the initial cycle. The watermarks improve performance of subsequent syncs.

## Can’t save configuration due to app credentials not working

Microsoft Entra ID requires valid credentials for provisioning. The credentials connect to a user management API provided by the app. If the credentials don’t work, or you don’t know what they are, review the tutorial for setting up the app.

## Provisioning logs say users are skipped and not provisioned even though they're assigned

Read the extended details in the log message to determine why a user shows up as skipped in the provisioning logs. Common reasons and resolutions include:

- **A scoping filter has been configured that is filtering the user out based on an attribute value**. For more information, see [Attribute-based application provisioning with scoping filters](define-conditional-rules-for-provisioning-user-accounts).
- **The user is “not effectively entitled”.** There's a problem with the user assignment record stored in Microsoft Entra ID. To fix this issue, unassign the user (or group) from the app, and reassign it again. For more information, see [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).
- **A required attribute is missing or not populated for a user.** Review and configure the attribute mappings and workflows that define which user (or group) properties flow from Microsoft Entra ID to the application. Check the setting `matching property` that is used to uniquely identify and match users/groups between the two systems. For more information, see [Customizing user provisioning attribute-mappings](customize-application-attributes).
- **Attribute mappings for groups:** Provisioning of the group name and group details, in addition to the members, if supported for some applications. You enable or disable the functionality using the **Mapping** for group objects shown in the **Provisioning** tab. If provisioning groups are enabled, review the attribute mappings to ensure an appropriate field is being used for `matching ID`. The field is the display name or email alias. The group and its members aren't provisioned if the matching property is empty or not populated for a group in Microsoft Entra ID.