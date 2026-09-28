---
layout: Conceptual
title: Workflow Extensibility - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-extensibility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Conceptual article discussing workflow extensibility with Lifecycle Workflows
ms.subservice: lifecycle-workflows
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-concept
locale: en-us
document_id: 6672413f-9630-67be-cb4c-2a6f532e4143
document_version_independent_id: 1b999e35-7ef9-c2bc-95af-b963f8d96f4b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-extensibility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-extensibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-extensibility.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: c82bcb7d-399d-a9dd-a285-8070931344a1
---

# Workflow Extensibility - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows allow you to create workflows that can be triggered based on joiner, mover, or leaver scenarios. While Lifecycle Workflows provide several built-in tasks to automate common scenarios throughout the lifecycle of users, eventually you may reach the limits of these built-in tasks. With the extensibility feature, you're able to utilize the concept of custom task extensions to call out to external systems as part of a workflow. For example, when a user joins your organization you can have a workflow with a custom task extension that assigns a Teams number, or have a separate workflow that grants access to an email account for a manager when a user leaves. With the extensibility feature, Lifecycle Workflows currently support creating custom task extensions to call out to [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview).

## Logic Apps prerequisites

To link an Azure Logic App with a custom task extension, the following prerequisites must be available:

- An Azure subscription
- A resource group
- Permissions to create a new consumption-based Logic App or access to an existing consumption-based Logic App

One of the following Azure role assignments is required either on the Logic App itself or on a higher scope such as the resource group, subscription or management group:

- **Logic App contributor**
- **Contributor**
- **Owner**

Note

The **Logic App Operator** role is not sufficient.

## Custom task extension deployment scenarios

When creating custom task extensions, the scenarios for how they interact with Lifecycle Workflows can be one of two ways:

![Screenshot of custom task deployment scenarios.](media/lifecycle-workflow-extensibility/task-extension-deployment-scenarios.png)

- **Launch and continue** - The Azure Logic App is started, and the following task's execution immediately continues with no response expected from the Azure Logic App. This scenario is best suited if the Lifecycle workflow doesn't require any feedback (including status) from the Azure Logic App. If the Logic App is started successfully, the Lifecycle Workflow task is considered a success.
- **Launch and wait** - The Azure Logic App is started, and the following task's execution waits on the response from the Logic App. You enter a time duration for how long the custom task extension should wait for a response from the Azure Logic App. If no response is received within the defined duration window, the task is considered failed. [![Screenshot of custom task launch and wait task choice.](media/lifecycle-workflow-extensibility/custom-task-launch-wait.png)](media/lifecycle-workflow-extensibility/custom-task-launch-wait.png#lightbox)

Note

The response does not necessarily have to be provided by the Logic App, a third party system is able to respond if the Logic App only acts as an intermediary. To learn more about this, see: [taskProcessingResult: resume](/en-us/graph/api/identitygovernance-taskprocessingresult-resume).

## Response authorization

When you create a custom task extension that waits for a response from the Logic App, you're able to define which applications can send a response.

![Screenshot of custom task extension launch and wait options.](media/lifecycle-workflow-extensibility/launch-wait-options.png)

The response can be authorized in one of the following ways:

- **System-assigned managed identity (Default)** - With this choice you enable and utilize the Logic Apps system-assigned managed identity. For more information, see: [Authenticate access to Azure resources with managed identities in Azure Logic Apps](/en-us/azure/logic-apps/create-managed-service-identity)
- **No authorization** - With this choice no authorization is granted, and you must separately assign an application permission (LifecycleWorkflows.ReadWrite.All), or role assignment (Lifecycle Workflows Administrator). If an application is responding, this option isn't recommended, as it doesn't follow the principle of least privilege. This option may also be used if responses are only provided on behalf of a user (LifecycleWorkflows.ReadWrite.All delegated permission AND Lifecycle Workflows Administrator role assignment).
- **Existing application** - With this choice you're able to choose an existing application to respond. This can be a regular application and a system or user-assigned managed identity. For more information on managed identity types, see: [Managed identity types](../identity/managed-identities-azure-resources/overview#managed-identity-types).

## Custom task extension integration with Azure Logic Apps high-level steps

The high-level steps for the Azure Logic Apps integration are as follows:

Note

Creating a custom task extension and logic app through the Microsoft Entra admin center will automate most of these steps. For a guide on creating a custom task extension this way, see: [Trigger Logic Apps based on custom task extensions](trigger-custom-task).

- **Create a consumption-based Azure Logic App**: A consumption-based Azure Logic App to be called from the custom task extension.
- **Configure the Azure Logic App so it's compatible with Lifecycle workflows**: Configuring the consumption-based Azure Logic App so that it can be used with the custom task extension. For more information, see: [Configure a Logic App for Lifecycle Workflow use](configure-logic-app-lifecycle-workflows)
- **Build your custom business logic within your Azure Logic App**: Set up your business logic within the Azure Logic App using Logic App designer.
- **Create a lifecycle workflow customTaskExtension which holds necessary information about the Azure Logic App**: Creating a custom task extension that references the configured Azure Logic App.
- **Update or create a Lifecycle workflow with the “Run a custom task extension” task, referencing your created customTaskExtension**: Adding the newly created custom task extension to a new workflow, or updating the information to an existing workflow.