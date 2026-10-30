---
layout: Conceptual
title: Automate identity lifecycle management with Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/automate-identity-lifecycle
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Describes overview of identity lifecycle management for Microsoft Entra ID Governance.
ms.workload: identity
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
locale: en-us
document_id: edd8cf7f-f71f-8615-0966-ede39ea11dc9
document_version_independent_id: edd8cf7f-f71f-8615-0966-ede39ea11dc9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/automate-identity-lifecycle.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/automate-identity-lifecycle
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/automate-identity-lifecycle.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: d13a4fd6-ec1e-3ce5-ec15-20f9e5a6e35e
---

# Automate identity lifecycle management with Microsoft Entra ID Governance | Microsoft Learn

The following document provides an overview of how you can [automate identity lifecycle processes](https://youtu.be/NxSu3JEsxmY?si=PELWAnpdI4iAMfki) using Microsoft Entra ID Governance.

## Automatic inbound provisioning from Active Directory

Provisioning from active directory to Microsoft Entra ID can be accomplished in several different ways using any of the following:

- [Microsoft Entra Cloud Sync](../../identity/hybrid/cloud-sync/what-is-cloud-sync)
- [Microsoft Entra Connect Sync](../../identity/hybrid/connect/whatis-azure-ad-connect-v2)
- [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) to trigger provisioning when a new identity is created in these HR systems.

## Automatic inbound provisioning from your organization's HR sources

HR driven provisioning is the process of creating digital identities based on a human resources system. The HR systems, become the start-of-authority for these newly created digital identities and is often the starting point for numerous provisioning processes. These HR systems can be either on-premises or cloud based.

To manage the identity lifecycles of employees, vendors, or contingent workers, [Microsoft Entra user provisioning service](../../identity/app-provisioning/user-provisioning) offers integration with cloud-based human resources (HR) applications.

Microsoft on-premises HR provisioning solutions use [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) to trigger provisioning when a new identity is created in these HR systems. Using MIM, you can provision users from your on-premises HR systems to Active Directory or Microsoft Entra ID. Users already present in Active Directory can be automatically created and maintained in Microsoft Entra ID using [inter-directory provisioning](../../identity/hybrid/what-is-inter-directory-provisioning).

### Enabled HR scenarios

The Microsoft Entra user provisioning service enables automation of the following HR-based identity lifecycle management scenarios:

- **New employee hiring:** Adding an employee to the cloud HR app automatically creates a user in Active Directory and Microsoft Entra ID. Adding a user account includes the option to write back the email address and username attributes to the cloud HR app.
- **Employee attribute and profile updates:** When an employee record such as name, title, or manager is updated in the cloud HR app, their user account is automatically updated in Active Directory and Microsoft Entra ID.
- **Employee terminations:** When an employee is terminated in the cloud HR app, their user account is automatically disabled in Active Directory and Microsoft Entra ID.
- **Employee rehires:** When an employee is rehired in the cloud HR app, their old account can be automatically reactivated or reprovisioned to Active Directory and Microsoft Entra ID.

For more information see [What is HR driven provisioning?](../../identity/app-provisioning/plan-cloud-hr-provision) and [Plan cloud HR application to Microsoft Entra user provisioning](../../identity/app-provisioning/plan-cloud-hr-provision)

## Automatic workflow tasks with Lifecycle Workflows

- [Lifecycle workflows](../what-are-lifecycle-workflows) automate workflow tasks that run at certain key events, such before a new employee is scheduled to start work at the organization, as they change status during their time in the organization, and as they leave the organization. For example, a workflow can be configured to send an email with a temporary access pass to a new user's manager, or a welcome email to the user, on their first day.

## Automatic assignment policies in entitlement management

- [Automatic assignment policies in entitlement management](../entitlement-management-access-package-auto-assignment-policy) add and remove a user's group memberships, application roles, and SharePoint site roles, based on changes to the user's attributes. Users can also upon request, be assigned to groups, Teams, Microsoft Entra roles, Azure resource roles, and SharePoint Online sites, using [entitlement management](../entitlement-management-scenarios) and [Privileged Identity Management](../privileged-identity-management/pim-configure).

## Automatic provisioning to on-premises apps and other directories

- Once the users are in Microsoft Entra ID with the correct group memberships and app role assignments, [user provisioning](../what-is-provisioning) can create, update and remove user accounts in other applications, with connectors to hundreds of cloud and on-premises applications via SCIM, LDAP and SQL.

## Automatic guest user lifecycle rights assignment

- For guest lifecycle, you can specify in [entitlement management](../entitlement-management-overview) the other organizations whose users are allowed to request access to your organization's resources. When one of those users's request is approved, they are automatically added by entitlement management as a [B2B](../../external-id/what-is-b2b) guest to your organization's directory, and assigned appropriate access. And entitlement management automatically removes the B2B guest user from your organization's directory when their access rights expire or are revoked.

## Automatic reoccurring reviews of users and guests

- [Access reviews](../access-reviews-overview) automates recurring reviews of existing guests already in your organization's directory, and removes those users from your organization's directory when they no longer need access.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals).