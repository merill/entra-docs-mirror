---
layout: Conceptual
title: Govern the employee lifecycle with Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/govern-the-employee-lifecycle
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Describes overview of identity lifecycle management and what is meant by governing the employee lifecycle.
ms.subservice: entitlement-management
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
locale: en-us
document_id: 00d9b2c3-356d-0d2d-fa18-fbee2c309b87
document_version_independent_id: 00d9b2c3-356d-0d2d-fa18-fbee2c309b87
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/govern-the-employee-lifecycle.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/govern-the-employee-lifecycle
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/govern-the-employee-lifecycle.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 593722e0-bb39-bd6e-f86e-336051ece1d5
---

# Govern the employee lifecycle with Microsoft Entra ID Governance | Microsoft Learn

Identity Governance helps organizations achieve a balance between *productivity* - How quickly can a person have access to the resources they need, such as when they join my organization? And *security* - How should their access change over time, such as due to changes to that person's employment status?

## Identity lifecycle management

**Identity lifecycle management** is the foundation for Identity Governance, and effective governance at scale requires modernizing the identity lifecycle management infrastructure for applications. Identity Lifecycle Management aims to automate and manage the entire digital identity lifecycle process for individuals affiliated with an organization.

![Diagram of the Microsoft Entra relationship in provisioning with other sources and targets.](media/what-is-identity-lifecycle-management/cloud-1-id-governance.png)

## What is a digital identity?

A digital identity is information on an entity used by one or more computing resources, such as operating systems or applications. These entities may represent people, organizations, applications, or devices. The identity is usually described by the attributes that are associated with it, such as the name, identifiers, and properties such as roles used for access management. These attributes help systems make determinations such who has access to what, and who is allowed to use that resource.

## Managing the lifecycle of digital identities

Managing digital identities is a complex task, especially as it relates correlating real-world objects, such as a person and their relationship with an organization as an employee of that organization, with a digital representation. In small organizations, keeping the digital representation of individuals who require an identity can be a manual process. For example, when someone is hired, or a contractor arrives, an IT specialist can create an account for them in a directory, and assign them the access they need. However, in mid-size and large organizations, automation can enable the organization to scale more effectively and keep the identities accurate.

The typical process for establishing identity lifecycle management in an organization follows these steps:

1. Determine whether there are already systems of record - data sources, which the organization treats as authoritative. For example, the organization may have an HR system such as Workday or SuccessFactors, and that system is authoritative for providing the current list of employees, and some of their properties such as the employee's name or department. In addition, an email system such as Exchange Online may be authoritative for an additional attributes, employee's email address.
2. Connect those systems of record with Microsoft Entra ID, and resolve any inconsistencies between existing users in Microsoft Entra ID and the systems of record. For example, Microsoft Entra ID may have been populated with now-obsolete data, such as a user account for a former employee that is no longer affiliated with the organization.
3. Once Microsoft Entra ID has the correct users, connect Microsoft Entra ID with one or more directories and databases used by applications, and resolve any inconsistencies between those directories and the copy of the system of record data in Microsoft Entra ID. For example, a directory for an application that was previously disconnected may have obsolete data, such as an account for a former employee.
4. Determine what processes can be used to supply authoritative information in the absence of a system of record. For example, if there are digital identities for visitors, but the organization has no database for visitors, then it may be necessary to find an alternate way to determine when a digital identity for a visitor is no longer needed.
5. Ensure that changes from the system of record or other processes are replicated through Microsoft Entra ID to each of the directories or databases that require an update.

## Identity lifecycle management for representing employees and other individuals with an organizational relationship

When planning identity lifecycle management for employees, or other individuals with an organizational relationship such as a contractor or student, many organizations model the "join, move, and leave" as following process:

- Join - when an individual comes into scope of needing access, an identity is needed by those applications, so a new digital identity may need to be created if one isn't already available
- Move - when an individual moves between boundaries that require additional access authorizations to be added or removed to their digital identity
- Leave - when an individual leaves the scope of needing access, access may need to be removed, and subsequently the identity may no longer be required by applications other than for audit or forensics purposes

So for example, if a new employee joins your organization and that employee has never been affiliated with your organization before, that employee requires a new digital identity, represented as a user account in Microsoft Entra ID. The creation of this account would fall into a "Joiner" process, which could be automated if there was a system of record such as Workday that could indicate when the new employee starts work. Later, if your organization has an employee move from say, Sales to Marketing, they would fall into a "Mover" process. This move would require removing the access rights they had in the Sales organization, which they no longer require, and granting them rights in the Marketing organization that they new require.

## Identity lifecycle management for guests

Similar processes are also needed for additional identities, for partners, suppliers and other guests, to enable them to collaborate or have access to resources. Microsoft Entra entitlement management utilizes Microsoft Entra External ID business-to-business (B2B) to provide the lifecycle controls needed to collaborate with people outside your organization who require access to your organization's resources. With Microsoft Entra B2B, external users authenticate to their home directory or identity provider, but have a representation in your organization's directory. The representation in your organization's directory enables the user to be assigned access to your resources. Entitlement management enables individuals outside your organization to request access, creating a digital identity for them as needed. These digital identities are automatically removed when the user loses access.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals).