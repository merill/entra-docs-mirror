---
layout: Conceptual
title: Understand Microsoft Entra role concepts - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/concept-understand-roles
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Learn how to understand Microsoft Entra built-in and custom roles with resource scope in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2024-07-30T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange
locale: en-us
document_id: 32f33bd6-2487-d3fa-6d83-bbbe8bf4959e
document_version_independent_id: dc6ceeab-09e0-4a51-d36b-a9a8e0527492
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/concept-understand-roles.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/concept-understand-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/concept-understand-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: cb90d5c6-f962-cdde-0547-941f180da4b4
---

# Understand Microsoft Entra role concepts - Microsoft Entra ID | Microsoft Learn

There are about 60 Microsoft Entra built-in roles, which are roles with a fixed set of role permissions. To supplement the built-in roles, Microsoft Entra ID also supports custom roles. Use custom roles to select the role permissions that you want. For example, you could create one to manage particular Microsoft Entra resources such as applications or service principals.

This article explains what Microsoft Entra roles are and how they can be used.

## How Microsoft Entra roles are different from other Microsoft 365 roles

There are many different services in Microsoft 365, such as Microsoft Entra ID and Intune. Some of these services have their own role-based access control systems, specifically:

- Microsoft Entra ID
- Microsoft Exchange
- Microsoft Intune
- Microsoft Defender for Cloud Apps
- Microsoft 365 Defender portal
- Compliance portal
- Cost Management + Billing

Other services such as Teams, SharePoint, and Managed Desktop don’t have separate role-based access control systems. They use Microsoft Entra roles for their administrative access. Azure has its own role-based access control system for Azure resources such as virtual machines, and this system is not the same as Microsoft Entra roles.

![Azure RBAC versus Microsoft Entra roles](media/concept-understand-roles/azure-roles-azure-ad-roles.png)

When we say separate role-based access control system, it means there is a different data store where role definitions and role assignments are stored. Similarly, there is a different policy decision point where access checks happen. For more information, see [Roles across Microsoft services](m365-workload-docs) and [Azure roles, Microsoft Entra roles, and classic subscription administrator roles](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles).

## Why some Microsoft Entra roles are for other services

Microsoft 365 has a number of role-based access control systems that developed independently over time, each with its own service portal. To make it convenient for you to manage identity across Microsoft 365 from the Microsoft Entra admin center, we have added some service-specific built-in roles, each of which grants administrative access to a Microsoft 365 service. An example of this addition is the Exchange Administrator role in Microsoft Entra ID. This role is equivalent to the [Organization Management role group](/en-us/exchange/organization-management-exchange-2013-help) in the Exchange role-based access control system, and can manage all aspects of Exchange. Similarly, we added the Intune Administrator role, Teams Administrator, SharePoint Administrator, and so on. Service-specific roles is one category of Microsoft Entra built-in roles in the following section.

## Categories of Microsoft Entra roles

Microsoft Entra built-in roles differ in where they can be used, which fall into the following three broad categories.

- **Microsoft Entra ID-specific roles**: These roles grant permissions to manage resources within Microsoft Entra-only. For example, User Administrator, Application Administrator, Groups Administrator all grant permissions to manage resources that live in Microsoft Entra ID.
- **Service-specific roles in Microsoft Entra ID**: Microsoft services such as Microsoft 365 that define roles in Microsoft Entra ID for service-specific privileges to manage all features within the service. For example, Exchange Administrator, Intune Administrator, SharePoint Administrator, and Teams Administrator roles can manage features with their respective services. Exchange Administrator can manage mailboxes, Intune Administrator can manage device policies, SharePoint Administrator can manage site collections, Teams Administrator can manage call qualities and so on.
- **Cross-service roles in Microsoft Entra ID**: There are some roles that span services. We have two global roles - Global Administrator and Global Reader. All Microsoft 365 services honor these two roles. Also, there are some security-related roles like Security Administrator and Security Reader that grant access across multiple security services within Microsoft 365. For example, using Security Administrator roles in Microsoft Entra ID, you can manage Microsoft 365 Defender portal, Microsoft Defender Advanced Threat Protection, and Microsoft Defender for Cloud Apps. Similarly, in the Compliance Administrator role you can manage Compliance-related settings in Compliance portal, Exchange, and so on.

![The three categories of Microsoft Entra built-in roles](media/concept-understand-roles/role-overlap-diagram.png)

The following table is offered as an aid to understanding these role categories. The categories are named arbitrarily, and aren't intended to imply any other capabilities beyond the [documented Microsoft Entra role permissions](permissions-reference).

| Category | Role |
| --- | --- |
| Microsoft Entra ID-specific roles | Application AdministratorApplication DeveloperAuthentication AdministratorB2C IEF Keyset AdministratorB2C IEF Policy AdministratorCloud Application AdministratorCloud Device AdministratorConditional Access AdministratorDevice AdministratorsDirectory ReadersDirectory Synchronization AccountsDirectory WritersExternal ID User Flow AdministratorExternal ID User Flow Attribute AdministratorExternal Identity Provider AdministratorGroups AdministratorGuest InviterHelpdesk AdministratorHybrid Identity AdministratorLicense AdministratorPartner Tier1 SupportPartner Tier2 SupportPassword AdministratorPrivileged Authentication AdministratorPrivileged Role AdministratorReports ReaderUser Administrator |
| Service-specific roles in Microsoft Entra ID | Azure DevOps AdministratorAzure Information Protection AdministratorBilling AdministratorCRM Service AdministratorCustomer Lockbox Access ApproverDesktop Analytics AdministratorExchange Service AdministratorInsights AdministratorInsights Business LeaderIntune Service AdministratorKaizala AdministratorLync Service AdministratorMessage Center Privacy ReaderMessage Center ReaderModern Commerce AdministratorNetwork AdministratorOffice Apps AdministratorPower BI Service AdministratorPower Platform AdministratorPrinter AdministratorPrinter TechnicianSearch AdministratorSearch EditorSharePoint Service AdministratorTeams Communications AdministratorTeams Communications Support EngineerTeams Communications Support SpecialistTeams Devices AdministratorTeams Administrator |
| Cross-service roles in Microsoft Entra ID | Compliance AdministratorCompliance Data AdministratorGlobal ReaderGlobal AdministratorSecurity AdministratorSecurity OperatorSecurity ReaderService Support Administrator |