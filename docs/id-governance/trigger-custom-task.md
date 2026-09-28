---
layout: Conceptual
title: Trigger Logic Apps based on custom task extensions - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/trigger-custom-task
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Trigger Logic Apps based on custom task extensions
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2024-12-10T00:00:00.0000000Z
ms.custom: template-howto
locale: en-us
document_id: 9924b154-a523-1fed-e4fc-3709412df8ab
document_version_independent_id: 69fa3c4b-aecb-c8d3-3231-acca0480ed03
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/trigger-custom-task.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/trigger-custom-task
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/trigger-custom-task.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: f2cb37bd-248b-4537-c511-17d490c0e0bc
---

# Trigger Logic Apps based on custom task extensions - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows can be used to trigger custom tasks via an extension to Azure Logic Apps. This can be used to extend the capabilities of Lifecycle Workflow beyond the built-in tasks. The steps for triggering a Logic App based on a custom task extension are as follows:

- Create a custom task extension.
- Select which behavior you want the custom task extension to take.
- Link your custom task extension to a new or existing Azure Logic App.
- Add the custom task to a workflow.

For more information about Lifecycle Workflows extensibility, see: [Workflow Extensibility](lifecycle-workflow-extensibility).

## Create a custom task extension using the Microsoft Entra admin center

To use a custom task extension in your workflow, first a custom task extension must be created to be linked with an Azure Logic App. You're able to create a Logic App at the same time you're creating a custom task extension. To do this, you complete these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the Lifecycle workflows screen, select **Custom task extension**.
4. On the custom task extensions page, select **Create custom task extension**. ![Screenshot for creating a custom task extension selection.](media/trigger-custom-task/create-custom-task-extension.png)
5. On the basics page you, enter a unique display name and description for the custom task extension and select **Next**. ![Screenshot of the basics section for creating a custom task extension.](media/trigger-custom-task/custom-task-extension-basics.png)
6. On the **Task behavior** page, you specify how the custom task extension will behave after executing the Azure Logic App. If you choose **Launch and continue** you can immediately select **Next: Details**. ![Screenshot for choose task behavior for custom task extension.](media/trigger-custom-task/custom-task-extension-behavior.png)
7. If you select **Launch and wait**, you're given an option of how long to wait for a response from the logic app before the task is considered a failure, and also options to set **Response authorization**. After choosing these options, you would be able to select **Next: Details**. [![Screenshot of launch and wait option for custom task extension.](media/trigger-custom-task/custom-task-extension-launch-wait.png)](media/trigger-custom-task/custom-task-extension-launch-wait.png#lightbox)

    Note

    For more information about custom task extension behavior, see: [Lifecycle Workflow extensibility](lifecycle-workflow-extensibility)
8. On the **Logic App details** page, you select **Create new Logic App**, and specify the subscription and resource group where it will be located. You'll also give the new Azure Logic App a name. ![screen showing to create new logic app for custom task extension.](media/trigger-custom-task/custom-task-extension-new-logic-app.png)

    Important

    A Logic App must be configured to be compatible with the custom task extension. For more information, see [Configure a Logic App for Lifecycle Workflow use](configure-logic-app-lifecycle-workflows)
9. If deployed successfully, you get confirmation on the **Logic App details** page immediately, and then you can select **Next**.
10. On the **Review** page, you can review the details of the custom task extension and the Azure Logic App you've created. Select **Create** if the details match what you desire for the custom task extension.

## Add your custom task extension to a workflow

After you've created your custom task extension, you can now add it to a workflow. Unlike some tasks, which can only be added to workflow templates that match its category, a custom task extension can be added to any template you choose to make a custom workflow from.

To Add a custom task extension to a workflow, you'd do the following steps:

1. In the left menu, select **Lifecycle workflows**.
2. In the left menu, select **Workflows**.
3. Select the workflow that you want to add the custom task extension to.
4. On the workflow screen, select **Tasks**.
5. On the tasks screen, select **Add task**.
6. In the **Select tasks** side menu, select **Run a Custom Task Extension**, and select **Add**.
7. On the custom task extension page, you can give the task a name and description. You also choose from a list of configured custom task extensions to use. ![Screenshot showing to add a custom task extension to workflow.](media/trigger-custom-task/add-custom-task-extension.png)
8. When finished, select **Save**.