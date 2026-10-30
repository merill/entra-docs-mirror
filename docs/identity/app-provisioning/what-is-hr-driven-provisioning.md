---
layout: Conceptual
title: What is HR-driven provisioning with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/what-is-hr-driven-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Describes overview of HR driven provisioning.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 15027d3b-49bd-adc5-7c48-328e60f4cac5
document_version_independent_id: 22795283-551d-3b08-7aee-636b0e543574
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/what-is-hr-driven-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/what-is-hr-driven-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/what-is-hr-driven-provisioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 2014e112-2abb-cf0c-9fba-f592c0435feb
---

# What is HR-driven provisioning with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

![HR provisioning](media/what-is-hr-driven-provisioning/cloud2a.png)

HR-driven provisioning is the process of creating digital identities based on a human resources system. The HR systems become the source of authority for these newly created digital identities and are often the starting point for numerous provisioning processes. For example, if a new employee joins your company, they're created in the human resource system. The creation triggers the provisioning of a user account into Active Directory, and then Microsoft Entra Connect provisions this account to Microsoft Entra ID.

Organizations may have either on-premises HR systems such as SAP HCM, cloud-based HR systems such as SAP SuccessFactors or Workday, or a mix of both. Historically, integration with on-premises HR systems for HR driven provisioning leveraged on-premises HR tools such as SAP Identity Management (SAP IDM) or Microsoft Identity Manager (MIM) to create users in Active Directory. Microsoft Entra can also be used with on-premises HR systems, to either create and update users in Active Directory, or for those environments that don't have Active Directory, create and update users in Microsoft Entra ID.

## On-premises-based HR provisioning

On-premises-based HR provisioning is accomplished by using a local HR system and a means of provisioning new digital identities.

HR systems come in various packages, software bundles and may use SQL servers or files to exchange data with other systems.

Customers who use SAP Human Capital Management (HCM) and have SAP SuccessFactors can bring identities into Microsoft Entra ID by using SAP Integration Suite to synchronize lists of workers between SAP HCM and SAP SuccessFactors. From there, you can bring identities directly into Microsoft Entra ID or provision them into Active Directory Domain Services.

![Diagram of SAP HR integrations.](../../id-governance/media/sap/sap-hr-no-mim.png)

Microsoft Entra [API-driven inbound provisioning](inbound-provisioning-api-concepts) also allows you to integrate with on-premises HR systems. Flat files, CSV files, and SQL staging tables are commonly used in enterprise integration scenarios. Employee, contractor, and vendor information are periodically exported into one of these formats and an automation tool is used to sync this data with enterprise identity directories. Partners can build custom HR connectors to meet different integration requirements around data flow from systems of record to Microsoft Entra ID. With API-driven inbound provisioning, integration is simplified as the Microsoft Entra provisioning service takes over the responsibility of performing identity profile comparison, restricting the data sync to scoping logic configured by the IT admin, and executing rule-based attribute flow and transformation managed in the Microsoft Entra admin center.

[![Diagram showing API workflow scenarios.](media/inbound-provisioning-api-concepts/api-workflow-scenarios.png)](media/inbound-provisioning-api-concepts/api-workflow-scenarios.png#lightbox)

You can also use Microsoft Identity Manager to trigger provisioning when a new identity is created in an on-premises HR system. Using MIM, you can provision users from your on-premises HR systems to Active Directory or Microsoft Entra ID. For information on Microsoft Identity Manager and the systems it supports, see the [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) documentation.

![Diagram of SAP HR integrations with MIM.](../../id-governance/media/sap/sap-hr.png)

## Cloud HR application to Microsoft Entra user provisioning

Historically, IT staff have relied on manual methods to create, update, and delete employees. They've used methods such as uploading CSV files or custom scripts to sync employee data. These provisioning processes are error prone, insecure, and hard to manage.

To manage the identity lifecycles of employees, vendors, or contingent workers, [Microsoft Entra user provisioning service](user-provisioning) offers integration with cloud-based human resources (HR) applications. Examples of applications include Workday or SuccessFactors.

Microsoft Entra ID uses this integration to enable the following cloud HR application (app) workflows:

- **Provision users to Active Directory:** Provision selected sets of users from a cloud HR app into one or more Active Directory domains.
- **Provision cloud-only users to Microsoft Entra ID:** In scenarios where Active Directory isn't used, provision users directly from the cloud HR app to Microsoft Entra ID.
- **Write back to the cloud HR app:** Write the email addresses and username attributes from Microsoft Entra back to the cloud HR app.

## Enabled HR scenarios

The Microsoft Entra user provisioning service enables automation of the following HR-based identity lifecycle management scenarios:

- **New employee hiring:** When a new employee is added to the cloud HR app, a user account is automatically created in Active Directory and Microsoft Entra ID with the option to write back the email address and username attributes to the cloud HR app.
- **Employee attribute and profile updates:** When an employee record such as name, title, or manager is updated in the cloud HR app, their user account is automatically updated in Active Directory and Microsoft Entra ID.
- **Employee terminations:** When an employee is terminated in the cloud HR app, their user account is automatically disabled in Active Directory and Microsoft Entra ID.
- **Employee rehires:** When an employee is rehired in the cloud HR app, their old account can be automatically reactivated or reprovisioned to Active Directory and Microsoft Entra ID.

## Who is this integration best suited for?

The cloud HR app integration with Microsoft Entra user provisioning is ideally suited for organizations that:

- Want a prebuilt, cloud-based solution for cloud HR user provisioning.
- Require direct user provisioning from the cloud HR app to Active Directory or Microsoft Entra ID.
- Require users to be provisioned by using data obtained from the cloud HR app.
- Require joining, moving, and leaving users to be synced to one or more Active Directory forests, domains, and OUs based only on change information detected in the cloud HR app.
- Use Office 365 for email.

### Key benefits

This capability of HR-driven IT provisioning offers the following significant business benefits:

- **Increase productivity:** You can now automate the assignment of user accounts and Office 365 licenses and provide access to key groups. Automating assignments gives new hires immediate access to their job tools and increases productivity.
- **Manage risk:** You can increase security by automating changes based on employee status or group memberships with data flowing in from the cloud HR app. Automating changes ensures that user identities and access to key apps update automatically when users transition or leave the organization.
- **Address compliance and governance:** Microsoft Entra ID supports native audit logs for user provisioning requests performed by apps of both source and target systems. With auditing, you can track who has access to the apps from a single screen.
- **Manage cost:** Automatic provisioning reduces costs by avoiding inefficiencies and human error associated with manual provisioning. It reduces the need for custom-developed user provisioning solutions built over time by using legacy and outdated platforms.

## Manage Joiner-Mover-Leaver lifecycle workflows

You can extend your HR-driven provisioning process to further automate business processes and security controls associated with new hires, employment changes, and termination. With [Microsoft Entra ID Governance Lifecycle Workflows](../../id-governance/what-are-lifecycle-workflows), you can configure Joiner-Mover-Leaver workflows such as:

- “X” days before the new hire joins, send email to manager, add user to groups, and generate a temporary access pass for first time login.
- When there's a change in user’s department or job title or group membership, launch a custom task.
- On the last day of work, send email to manager, and remove user from groups and license assignments.
- “X” days after termination, delete user from Microsoft Entra ID.