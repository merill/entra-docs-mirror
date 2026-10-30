---
layout: Conceptual
title: How to use Microsoft Entra workbooks - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-use-workbooks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to use Azure Monitor workbooks for Microsoft Entra ID, for analyzing identity related activity, trends, and gaps.
ms.topic: how-to
ms.date: 2024-10-02T00:00:00.0000000Z
ms.reviewer: sarbar
locale: en-us
document_id: eb2155a4-d8b2-a542-1aba-387183c3f2e3
document_version_independent_id: 11565414-4093-d4cf-2665-1343b45a732a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-use-workbooks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-use-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-use-workbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3d1688d7-3397-781e-a11d-38b9a4379b5c
---

# How to use Microsoft Entra workbooks - Microsoft Entra ID | Microsoft Learn

Workbooks are found in Microsoft Entra ID and in Azure Monitor. The concepts, processes, and best practices are the same for both types of workbooks, however, workbooks for Microsoft Entra ID cover only those identity management scenarios that are associated with Microsoft Entra ID.

When using workbooks, you can either start with an empty workbook, or use an existing template. Workbook templates enable you to quickly get started using workbooks without needing to build from scratch.

- **Public templates** published to a [gallery](/en-us/azure/azure-monitor/visualize/workbooks-overview#the-gallery) are a good starting point when you're just getting started with workbooks.
- **Private templates** are helpful when you start building your own workbooks and want to save one as a template to serve as the foundation for multiple workbooks in your tenant.

## Prerequisites

To use Azure Workbooks for Microsoft Entra ID, you need:

- A Microsoft Entra tenant with a [Premium P1 license](../../fundamentals/get-started-premium)
- A Log Analytics workspace *and* access to that workspace
- The appropriate roles for Azure Monitor *and* Microsoft Entra ID

### Log Analytics workspace

You must create a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace)*before* you can use Microsoft Entra Workbooks. several factors determine access to Log Analytics workspaces. You need the right roles for the workspace *and* the resources sending the data.

For more information, see [Manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access).

### Azure Monitor roles

Azure Monitor provides [two built-in roles](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) for viewing monitoring data and editing monitoring settings. Azure role-based access control (RBAC) also provides two Log Analytics built-in roles that grant similar access.

- **View**:

    - Monitoring Reader
    - Log Analytics Reader
- **View and modify settings**:

    - Monitoring Contributor
    - Log Analytics Contributor

### Microsoft Entra roles

Read only access allows you to view Microsoft Entra ID log data inside a workbook, query data from Log Analytics, or read logs in the Microsoft Entra admin center. Update access adds the ability to create and edit diagnostic settings to send Microsoft Entra data to a Log Analytics workspace.

- **Read**:

    - Reports Reader
    - Security Reader
    - Global Reader
- **Update**:

    - Security Administrator

For more information on Microsoft Entra built-in roles, see [Microsoft Entra built-in roles](../role-based-access-control/permissions-reference).

For more information on the Log Analytics RBAC roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor).

## Access Microsoft Entra workbooks

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.

    - **Workbooks**: All workbooks created in your tenant
    - **Public Templates**: Prebuilt workbooks for common or high priority scenarios
    - **My Templates**: Templates you created
3. Select a report or template from the list. Workbooks might take a few moments to populate.

    - Search for a template by name.
    - Select the **Browse across galleries** to view templates that aren't specific to Microsoft Entra ID.

    ![Screenshot of the Microsoft Entra workbooks with navigation steps highlighted.](media/howto-use-workbooks/workbooks-gallery.png)

## Create a new workbook

Workbooks can be created from scratch or from a template. When creating a new workbook, you can add elements as you go or use the **Advanced Editor** option to paste in the JSON representation of a workbook, copied from the [workbooks GitHub repository](https://github.com/Microsoft/Application-Insights-Workbooks/blob/master/schema/workbook.json).

To create a new workbook from scratch:

1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
2. Select **+ New**.
3. Select an element from the **+ Add** menu.

    For more information on the available elements, see [Creating an Azure Workbook](/en-us/azure/azure-monitor/visualize/workbooks-create-workbook).

    ![Screenshot of the options available in the workbook editing area.](media/howto-use-workbooks/add-new-workbooks-elements.png)

To create a new workbook from a template:

1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
2. Select a workbook template from the Gallery.
3. Select **Edit** from the top of the page.

    - Each element of the workbook has its own **Edit** button.
    - For more information on editing workbook elements, see [Azure Workbooks Templates](/en-us/azure/azure-monitor/visualize/workbooks-templates)

    ![Screenshot of a workbook template with the edit button highlighted.](media/howto-use-workbooks/workbooks-edit-button.png)
4. Select the **Edit** button for any element. Make your changes and select **Done editing**.

    ![Screenshot of a workbook in edit mode, with the edit element and done editing buttons highlighted.](media/howto-use-workbooks/workbooks-edit-elements.png)
5. When you're done editing the workbook, select the **Save** button. The **Save as** window opens.
6. Provide a **Title**, **Subscription**, **Resource Group**\* and **Location**

    - You must have the ability to save a workbook for the selected Resource Group.
    - Optionally choose to save your workbook content to an [Azure Storage Account](/en-us/azure/azure-monitor/visualize/workbooks-bring-your-own-storage).
7. Select the **Apply** button.