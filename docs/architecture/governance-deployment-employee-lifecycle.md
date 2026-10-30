---
layout: Conceptual
title: Microsoft Entra ID Governance deployment guide for employee lifecycle automation - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/governance-deployment-employee-lifecycle
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-governance
manager: martinco
description: Learn how to deploy employee lifecycle automation in Microsoft Entra ID Governance.
ms.topic: concept-article
ms.date: 2025-04-17T00:00:00.0000000Z
ms.reviewer: gasinh
locale: en-us
document_id: 02aa6a99-09c9-a04d-428f-af2dad6c4317
document_version_independent_id: 02aa6a99-09c9-a04d-428f-af2dad6c4317
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/governance-deployment-employee-lifecycle.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/governance-deployment-employee-lifecycle
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/governance-deployment-employee-lifecycle.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 191e4bd9-ff25-44cb-4490-a944695afaed
---

# Microsoft Entra ID Governance deployment guide for employee lifecycle automation - Microsoft Entra | Microsoft Learn

Deployment scenarios are guidance on how to combine and test Microsoft Security products and services. You can discover how capabilities work together to improve productivity, strengthen security, and more easily meet compliance and regulatory requirements.

The following products and services appear in this guide:

- [Microsoft Entra ID Governance](../id-governance/identity-governance-overview)
- [Lifecycle workflows](../id-governance/what-are-lifecycle-workflows)
- [Microsoft Entra](../fundamentals/what-is-entra)
- [Microsoft Entra Connect](../identity/hybrid/connect/whatis-azure-ad-connect)
- [Microsoft Entra Cloud Sync](../identity/hybrid/cloud-sync/what-is-cloud-sync)
- [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview)
- [Microsoft Graph](/en-us/graph/overview)

Use this scenario to help determine the need for Microsoft Entra ID Governance to create and grant access for your organization. Learn how you can provision your users effectively, securely, and consistently with employee lifecycle automation.

## Timelines

Timelines show approximate delivery stage duration and are based on scenario complexity. Times are estimations and vary depending on the environment.

1. HR provisioning - 3 hours
2. Software-as-a-Service (SaaS) app provisioning - 1 hour
3. Lifecycle workflows - 3 hours

## Employee lifecycle automation

To streamline employee identity management, organizations are adopting modern solutions and automation. With identity management systems and technologies, IT staff can overcome limited manual procedures and instead enhance efficiency.

### Microsoft Entra ID Governance

With the Microsoft Entra ID Governance solution, organizations improve productivity, strengthen security, and meet compliance and regulatory requirements. Use Microsoft Entra ID Governance to ensure the right people have the right access to the right resources at the right time. Learn more about Microsoft Entra ID Governance [use cases](../id-governance/scenarios/identity-governance-use-cases) and [documentation](../id-governance/identity-governance-overview).

## HR-driven provisioning

HR-driven provisioning creates digital identities based on a human resources (HR) system, which becomes the source of authority. This juncture is the starting point for numerous provisioning processes.

Learn more in the video about [HR-driven provisioning with Microsoft Entra ID](https://youtu.be/HsdBt40xEHs).

### Cloud HR to Microsoft Entra ID

Users are created in Microsoft Entra ID, and other SaaS apps that support user provisioning. When employee records are updated in cloud HR, the user account is updated in Microsoft Entra ID and supporting SaaS apps.

## Deploy Workday to Microsoft Entra ID

1. [Select cloud HR provisioning connector apps](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
2. [Design provisioning topology](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
3. [Configure integration system user in Workday](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
4. [Enable Workday provisioning connector](/en-us/azure/active-directory/saas-apps/workday-inbound-cloud-only-tutorial).
5. [Start Workday and Microsoft Entra ID attribute mapping](/en-us/azure/active-directory/saas-apps/workday-inbound-cloud-only-tutorial).
6. [(**Optional**) Configure Workday writeback in Azure AD](/en-us/azure/active-directory/saas-apps/workday-writeback-tutorial).
7. [Enable and launch provisioning](/en-us/azure/active-directory/saas-apps/workday-writeback-tutorial).

Learn more in the video about [HR-driven user provisioning with Workday](https://youtu.be/TfndXBlhlII).

## Deploy SuccessFactors to Microsoft Entra ID

1. [Select cloud HR provisioning connector apps](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
2. [Design provisioning topology](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
3. [Create API user account in SuccessFactors](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial).
4. [Create API permissions in SuccessFactors](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial).
5. [Add SuccessFactors inbound connector app](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial).
6. [Configure SuccessFactors attribute mappings](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial).
7. [(**Optional**) Configure attribute write-back from Entra ID to SAP SuccessFactors](/en-us/azure/active-directory/saas-apps/sap-successfactors-writeback-tutorial).
8. [Enable and Launch provisioning](/en-us/azure/active-directory/saas-apps/sap-successfactors-writeback-tutorial).

Learn more in the video about [HR-driven user provisioning with SuccessFactors](https://www.youtube.com/watch?v=66v2FR2-QrY).

## Cloud HR to Active Directory

Use the following video to learn about API-driven inbound provisioning for on-premises Active Directory.

## Deploy Workday to Active Directory

1. [Select cloud HR provisioning connector apps](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
2. [Design provisioning topology](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
3. [Configure integration system user in Workday](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
4. [Provisioning connector app and Provisioning Agent](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
5. [Install and configure on-premises agents](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
6. [Configure connectivity to Workday and Active Directory](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
7. [Configure attribute mappings](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
8. [Enable and launch user provisioning](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).

## Deploy SuccessFactors to Active Directory

1. [Select cloud HR provisioning connector apps](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
2. [Design provisioning topology](/en-us/azure/active-directory/app-provisioning/plan-cloud-hr-provision).
3. [Configure integration system user in Workday](/en-us/azure/active-directory/saas-apps/workday-inbound-tutorial).
4. [SuccessFactors inbound provisioning app and agent](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-tutorial).
5. [Install on-premises agents](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-tutorial).
6. [Configure app connectivity to AD](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-tutorial).
7. [Configure attribute mappings](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-tutorial).
8. [Enable and launch user provisioning](/en-us/azure/active-directory/saas-apps/sap-successfactors-inbound-provisioning-tutorial).

## API-driven provisioning

Identity data in Microsoft Entra ID is kept in sync with workforce data managed in systems of record: an HR app, a payroll app, a spreadsheet, SQL tables in a database on-premises, or in the cloud. With application programming interface [(API)-driven inbound provisioning](../identity/app-provisioning/inbound-provisioning-api-concepts), the Microsoft Entra provisioning service supports integration with systems of record.

Learn more:

- [FAQ: API-driven inbound provisioning](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-faqs)
- [Grant access to the inbound provisioning API](https://youtu.be/RnY9T7k1BL0)
- [Learn to test provisioning API with Graph Explorer](https://youtu.be/GvEdWPgQJps)

### API-driven provisioning scenarios

IT teams import data extracts with automation. Independent software vendors (ISVs) integrate with Microsoft Entra ID. System integrators build connectors to systems of record. This process is commonly used for sources like flat files, CSV files, SQL staging tables. Integrate automation tools: [PowerShell](/en-us/windows-server/administration/windows-commands/powershell) scripts, [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview), and workflows using HTTP calls.

## Configure API-driven provisioning

You can learn to configure [API-driven inbound provisioning](../identity/app-provisioning/inbound-provisioning-api-concepts). 

## Comparison: Inbound provisioning /bulkUpload API and Microsoft Graph Users API

We recommend noting the differences between the provisioning **/bulkUpload** API and the Microsoft Graph Users API endpoint: Payload format, operation result, and IT administrators retain control.

In an FAQ, learn how [the new inbound provisioning API differs from Graph Users API](../identity/app-provisioning/inbound-provisioning-api-faqs).

## Deploy API-driven inbound provisioning

1. [Create an API-driven provisioning app](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-configure-app).
2. For **Active Directory**, [configure API-driven inbound provisioning app](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-configure-app). For **Microsoft Entra ID**, [configure API-driven inbound provisioning app](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-configure-app).
3. [Grant access to inbound provisioning API](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-grant-access)
4. [Customize user provisioning attribute mappings](/en-us/azure/active-directory/app-provisioning/customize-application-attributes)
5. [Sync custom attributes](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-custom-attributes)

To learn more, see the following Quickstart guides about API-driven inbound provisioning with:

- [cURL](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-curl-tutorial)
- [Postman](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-postman)
- [Graph Explorer](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-graph-explorer)
- [PowerShell](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-powershell)
- [Azure Logic Apps](/en-us/azure/active-directory/app-provisioning/inbound-provisioning-api-logic-apps)

### Outbound app provisioning

You can provision to Software-as-a-Service (SaaS) apps, using a System for Cross-Domain Identity Management (SCIM).

Discover more about [SCIM synchronization with Microsoft Entra ID](sync-scim).

### Configure provisioning with a SCIM endpoint

SCIM 2.0 is a standardized definition of two endpoints **/Users** and **/Groups**.

See more details in the tutorial, [develop, and plan provisioning for a SCIM endpoint in Microsoft Entra ID](../identity/app-provisioning/use-scim-to-provision-users-and-groups).

## Deploy SaaS sample-app provisioning

The [Microsoft Entra ID application gallery](../identity/saas-apps/tutorial-list) displays available apps for user provisioning. Select up to four apps for your environment, or choose from these popular apps to enable automatic user provisioning:

- [ServiceNow](/en-us/azure/active-directory/saas-apps/servicenow-provisioning-tutorial)
- [Salesforce](/en-us/azure/active-directory/saas-apps/salesforce-provisioning-tutorial)
- [Box](/en-us/azure/active-directory/saas-apps/box-userprovisioning-tutorial)
- [Cisco Webex](/en-us/azure/active-directory/saas-apps/cisco-webex-provisioning-tutorial)
- [Zoom](/en-us/azure/active-directory/saas-apps/zoom-provisioning-tutorial)

### (Optional) Provision to on-premises apps

Users and schema defined in the cloud support provisioning from custom schema extensions to app-specific properties.

To learn more, go to [app provisioning samples for SCIM-enabled apps](/en-us/azure/active-directory/app-provisioning/on-premises-scim-provisioning).

## Lifecycle workflows

Lifecycle workflows are an identity governance feature to manage Microsoft Entra users by automating Joiner, Mover, and Leaver events for employees. Use the feature to schedule tasks for before, during, or after an event. Workflows can run on demand. With built-in tasks, you can generate temporary credentials, send emails, update user attributes, and memberships, and remove licenses.

Learn more in the [overview of lifecycle workflow APIs](/en-us/graph/api/resources/identitygovernance-lifecycleworkflows-overview?view=graph-rest-1.0&amp;preserve-view=true).

### Joiner

A Joiner is an individual who needs access. When you onboard new employees, use templates and workflows to make processes more efficient and faster.

### Mover

A Mover is an individual moving between boundaries in an organization, for instance, the employee goes from a role in Sales to one in Marketing. The movement might require more, or different, access, and authorization.

### Leaver

The Leaver no longer needs access, such as terminated or retiring employees. Effective Leaver workflows reduce the risk of unauthorized data access, after termination. Therefore, handle Leaver personal information in compliance with regulations and policies. Use customizable workflow templates for timely, reliable, and graceful resource-access removal.

**Remove application access**

Microsoft Entra ID provisioning service keeps source and target systems in sync. Deprovision an account when user access must end.

1. Unassign the user from one or more applications.
2. Delete the account from Microsoft Entra ID.
3. Set the **AccountEnabled** property to **False**.

    Note

    If an application supports the process, you can soft-delete users by default.

### Lifecycle workflows custom extensions

Use custom extensions to create workflows using tools like Azure Logic Apps. For workflows, you can enable custom task extensions to call out to external systems. For example, a Joiner workflow with a custom task extension assigns a Microsoft Teams number. Or, when a user becomes a Leaver, a separate workflow grants access to an email account for their manager. You can learn to [trigger Logic Apps based on custom task extensions](../id-governance/trigger-custom-task).

Note

To create a logic app resource for hosting, select **Consumption**. A consumption logic app has one workflow that runs in multitenant Azure Logic Apps.

To learn more, see the [App Service Environment overview](/en-us/azure/app-service/environment/overview) and [Azure Logic Apps documentation](/en-us/azure/logic-apps/logic-apps-overview).

## Deploy lifecycle workflows

1. [Synchronize attributes](/en-us/azure/active-directory/governance/how-to-lifecycle-workflow-sync-attributes)
2. [Prepare user accounts](/en-us/azure/active-directory/governance/tutorial-prepare-user-accounts)
3. [Automate prehire tasks for employees](/en-us/azure/active-directory/governance/tutorial-onboard-custom-workflow-portal)
4. [Automate onboarding new employees](/en-us/azure/active-directory/governance/lifecycle-workflow-templates)
5. [Automate post-onboarding](/en-us/azure/active-directory/governance/lifecycle-workflow-templates)
6. [Real-time employee change](/en-us/azure/active-directory/governance/lifecycle-workflow-templates)
7. [Real-time employee termination](/en-us/azure/active-directory/governance/tutorial-offboard-custom-workflow-portal)
8. [Employee group membership changes](../id-governance/lifecycle-workflow-templates)
9. [Employee job profile change](../id-governance/lifecycle-workflow-templates)
10. [Automate preoffboarding](/en-us/azure/active-directory/governance/lifecycle-workflow-templates)
11. [Automate offboarding](/en-us/azure/active-directory/governance/tutorial-scheduled-leaver-portal)
12. [Automate post-affboarding](/en-us/azure/active-directory/governance/lifecycle-workflow-templates)
13. [Trigger Logic Apps with custom extensions](/en-us/azure/active-directory/governance/trigger-custom-task)

### Supported tasks and workflows

The table lists tasks and workflow according to Joiner, Mover, Leaver status.

| Category | Tasks and workflows |
| --- | --- |
| Joiner | [Send welcome email to new-hire](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner | [Send onboarding reminder email](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner | [Generate temporary access pass (TAP) and send it by email to the new-hire's manager](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Mover | [Send notification email to manager about a user move](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner, Mover | [Request user access package assignment](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner, Mover, Leaver | [Add user to groups](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner, Mover, Leaver | [Add user to teams](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner, Leaver | [Enable user account](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner, Mover, Leaver | [Run a custom task extension](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Disable user account](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Joiner, Mover, Leaver | [Remove user from groups](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Remove user from all groups](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Remove user from teams](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Remove user from all teams](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver, Mover | [Remove user access package assignments](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Remove all user access package assignments](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Cancel all pending user access package assignment requests](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Remove all user license assignments](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Delete user](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Send email to user's manager before before last day](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Send email to user's manager on last day](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |
| Leaver | [Send email to user's manager after last day](/en-us/azure/active-directory/governance/lifecycle-workflow-tasks) |