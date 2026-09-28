---
layout: Conceptual
title: User provisioning logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-provisioning-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the details included in the user provisioning logs in Microsoft Entra ID when a non-Microsoft service provisions users.
ms.topic: troubleshooting-general
ms.date: 2025-03-17T00:00:00.0000000Z
ms.reviewer: arvinh
ms.custom: sfi-image-nochange
locale: en-us
document_id: 684c1153-f8bc-0c5c-9004-4ae150c4dc37
document_version_independent_id: 33863c64-ad39-dd57-06e5-a0fc7ac4993c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-provisioning-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-provisioning-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-provisioning-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c268b81e-9f8b-fc5c-2e34-355302719aed
---

# User provisioning logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID integrates with several non-Microsoft services to provision users into your tenant. If you need to troubleshoot an issue with a provisioned user, you can use the information captured in the Microsoft Entra provisioning logs to help find a solution.

Two other activity logs are also available to help monitor the health of your tenant:

- **[Sign-ins](concept-sign-ins)** – Information about sign-ins and how your resources are used by your users.
- **[Audit](concept-audit-logs)** – Information about changes applied to your tenant such as users and group management or updates applied to your tenant’s resources.

This article gives you an overview of the logs that capture user provisioning through non-Microsoft services.

## What can you do with the provisioning logs?

You can use the provisioning logs to find answers to questions like:

- What groups were successfully created in ServiceNow?
- What users were successfully removed from Adobe?
- What users from Workday were successfully created in Active Directory?

Note

Entries in the provisioning logs are system generated and can't be changed or deleted.

## What do the logs show?

The logs display the identity, action taken, source system, target system, and the status of the provisioning event. Other columns can be added for further troubleshooting, but the following details are standard.

[![Screenshot of the provisioning logs showing a variety of details.](media/concept-provisioning-logs/provisioning-logs.png)](media/concept-provisioning-logs/provisioning-logs-expanded.png#lightbox)

- **Identity**: The display name and source ID of the identity being provisioned appear in this column.
- **Action**: Possible values include Create, Update, Delete, Disable, StagedDelete, and Other.
    - Examples of Other include if the source and target system details already match, so no change was made.
- **Source System** and **Target System**: Paired together, these details show which system the identity is coming from and where it's being provisioned.
- **Status**: Possible values include Success, Failure, Skipped, and Warning.
    - There are several scenarios that could trigger the Skipped status. For details on these scenarios, see [No users are being provisioned](../app-provisioning/application-provisioning-config-problem-no-users-provisioned)

Select an item from the provisioning logs to see more details about this item, such as the steps taken to provision the user and tips for troubleshooting issues. The details are grouped into four tabs.

- **Steps**: This tab outlines the steps taken to provision an object. Provisioning an object can include the following steps, but not all steps are applicable to all provisioning events.

    - Import the object.
    - Match the object between source and target.
    - Determine if the object is in scope.
    - Evaluate the object before synchronization.
    - Provision the object (create, update, delete, or disable).

    ![Screenshot shows the provisioning steps on the Steps tab.](media/concept-provisioning-logs/steps.png)
- **Troubleshooting & Recommendations**: If there was an error, this tab provides the error code and reason. In many cases, a detailed description of the error is provided. Review this information to understand the issue and follow the guidance provided to resolve it. Review the following troubleshooting articles:

    - [Troubleshoot HR user creation issues](../app-provisioning/hr-user-creation-issues)
    - [Troubleshoot HR user update issues](../app-provisioning/hr-user-update-issues)
    - [Troubleshoot insufficient access rights error](../app-provisioning/insufficient-access-rights-error-troubleshooting)
- **Modified Properties**: If there were changes, this tab shows the old value and the new value.
- **Summary**: Provides an overview of what happened and identifiers for the object in the source and target systems.

## Using provisioning logs workbooks and Log Analytics

With the querying and alerting capabilities of Log Analytics and workbooks, you can create custom reports and alerts. To get started, you need to [create a Log Analytics workspace](tutorial-configure-log-analytics-workspace#create-a-log-analytics-workspace). Once you have a workspace, you can stream your logs to that workspace, which allows you to query and analyze the data in Log Analytics and workbooks.

For more information, see [Integrating provisioning logs with Azure Monitor logs](../app-provisioning/application-provisioning-log-analytics).

There are two workbook templates available for provisioning logs:

- **Provisioning Analysis** provides a high-level overview of the provisioning events in your tenant.
- **Provisioning Insights** provides details on events related to syncing users from other sources so you can see analyze these events in one place. For more information, see [Provisioning insights workbook](../app-provisioning/provisioning-workbook).