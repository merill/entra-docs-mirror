---
layout: Conceptual
title: Enterprise user management with Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-enterprise-user-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot in the Microsoft Entra admin center to manage users, tenants, groups, using natural language queries.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 10280295-39b4-9998-21a8-a0ada4f80707
document_version_independent_id: 10280295-39b4-9998-21a8-a0ada4f80707
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-enterprise-user-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-enterprise-user-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-enterprise-user-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 7fb6f8c3-05b9-0412-150b-7771f80d563b
---

# Enterprise user management with Microsoft Security Copilot | Microsoft Learn

Microsoft Security Copilot streamlines enterprise user management in Microsoft Entra by enabling IT administrators to quickly manage users, tenants, groups, and licenses using natural language queries. This capability helps streamline administrative tasks, helping users keep identities secure and up to date, reduce time spent navigating portals and improving response times for identity-related requests.

This article describes how an IT administrator can prepare for a quarterly identity governance review, and how to use Microsoft Security Copilot for the following core identity management use cases in the Microsoft Entra admin center.

- Understand tenant configuration
- Manage domain information
- Investigate and manage users
- Organize and manage groups
- Analyze license usage and optimization

Use the prompts and examples in this article to compile your findings into actionable insights and reports for reviews and audits by your team or management.

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.
- The following roles and licenses are required for different governance and optimization use cases:

    | Use Case | Role(s) | License | Tenant |
    | --- | --- | --- | --- |
    | Tenant information | [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader) | Any Microsoft Entra ID license | Any tenant |
    | User management | [User Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator) | Any Microsoft Entra ID license | Any tenant |
    | Group management | [Directory Writer](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-writer), [Groups Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#groups-administrator), or [User Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator) | Free Microsoft Entra license | Any public cloud tenant with groups |
    | Domain management | [Domain Name Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#domain-name-administrator) | Any Microsoft Entra ID license | Any tenant |
    | License usage | [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader) | [Microsoft Entra ID Governance license](/en-us/entra/id-governance/licensing-fundamentals) | Any tenant |

## Launch Security Copilot in Microsoft Entra

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate administrative role(s) for your scenario based off the specific use cases.
2. Launch Security Copilot from the **Copilot** button in the Microsoft Entra admin center.

    ![Screenshot that shows Security Copilot in the Microsoft Entra admin center.](media/copilot-security-entra/security-copilot-entra-admin-center.png)
3. Refer to the following use cases and prompts to retrieve information or perform actions using natural language queries.

Note

If an action is blocked by insufficient permissions, a recommended role is displayed. You can use the following prompt in the Security Copilot chat to activate the required role. This is dependent on having an eligible role assignment that provides the necessary access.

- *Activate the {required role} so that I can perform {the desired task}.*

## Understand tenant configuration

Begin your assessment by gathering essential tenant information to understand your overall Microsoft Entra configuration. This foundational knowledge helps you establish context for further analysis.

### Tenant identity and basic information

Start by retrieving key tenant details such as display name, tenant ID, and creation date to establish the scope of your review. Use the following prompts to get the information you need:

- *What is my tenant's display name?*
- *What is my tenant ID?*
- *Can users in my tenant create new tenants?*

### Tenant licensing and contacts

You can gather information about your tenant's licensing and assigned contacts for technical and security compliance matters, which can be useful for audits and executive reporting. Use these prompts to retrieve relevant details:

- *What are all the active licenses assigned to my tenant?*
- *Who is the technical contact for my tenant?*
- *Who is the security compliance contact for my tenant?*

## Manage domain information

As part of your tenant review, you can also verify domain configurations and DNS records to ensure that your domains are properly set up and secure. This helps prevent issues related to domain verification and or setup.

### Domain details and verification

Examine your domain configurations and DNS verification status to ensure that your domains are correctly set up, secured, and compliant with your organizational policies. Use the following prompts to get the information you need:

- *List details of contoso.com.*
- *Show me DNS verification records of contoso.com.*
- *What is my initial domain name?*

## Investigate and manage users

Next, focus on understanding the user landscape in your Microsoft Entra setup. You can analyze user accounts, organizational structure, authentication methods, and identify any inconsistencies that may require attention.

### User information and details

Begin by examining user details and organizational relationships to understand how employees are structured within the company and identify any anomalies. Use the following prompts to gather the information you need:

- *Show recently deleted users.*
- *Tell me about myself.*
- *Are there guest users in the Human Resources department?*
- *Show transitive reports of Brandon Artois.*
- *Give the member count of each department.*
- *Who is Asha Brunelle's manager?*
- *Is Blake Martin's account cloud managed?*
- *Show users by mail nickname.*

### User authentication and permissions

You can then review user authentication methods and permissions to ensure security compliance and identify users who may need extra authentication requirements. Use these prompts get the information you need:

- *What are Abbi Atin's authentication methods?*
- *Look up Abadi Bod's permissions.*
- *How many users are reporting to Brandon Artois?*

### User filtering and organization

To identify potential compliance issues, you can filter users based on specific criteria such as licensing status, departments, and account configurations. Use the following prompts to get the information you need:

- *List users without assigned licenses.*
- *List users in Finance or Marketing department.*
- *Show users not in {Company Name}.*
- *Show users with account disabled.*
- *Are there any users with {Specific license}?*

## Organize and manage groups

Continue your assessment by examining group management across your organization. Groups are essential for organizing users and managing access to resources, so understanding their configuration is crucial to ensure proper governance. It also helps identify any potential security risks associated with group memberships.

### Group membership and composition

Start by analyzing group membership patterns and identify potential issues such as ownerless groups or unusual membership types that could pose security risks. Use the following prompts to get the information you need:

- *Count the total ownerless groups in my tenant.*
- *Count the total user memberships for a group.*
- *Provide separate counts for users, groups, devices, and service principals in a group.*
- *How many different object types does a group have in total?*
- *Show me all user members of a group.*
- *Which users are included in a group?*

### Group configuration and roles

Continue by reviewing group configurations, role assignments, and dynamic membership rules to understand how your groups are structured and managed. Use the following prompts to get the information you need:

- *What directory roles are assigned to a group?*
- *Does this group have any built-in roles?*
- *Show me the membership rules for a group.*
- *Is the dynamic membership rule currently processing for a group?*
- *Give me the details of a group.*

### Group organization and governance

To maintain proper organization and governance, you can categorize and analyze groups by type and identify any inconsistencies or opportunities for optimization. Use the following prompts to get the information you need:

- *Show the count of groups categorized by group type.*
- *List the number of groups under each of the group types.*
- *How many groups exist for each group type?*

## Analyze license usage and optimization

Finally, you can review license usage and optimization opportunities to ensure that your organization is making the most of its Microsoft Entra investment. This helps identify underutilized licenses and optimize costs.

### License analysis and utilization

Use the following prompts to analyze your license allocation, usage patterns, and feature utilization for cost optimization and better license management for upcoming budget planning:

- *How many Microsoft Entra P1/P2 licenses do I have?*
- *Count of P1/P2 Microsoft Entra licenses.*
- *Number of Microsoft Entra ID P1/P2 licenses.*
- *What is the usage of Microsoft Entra P1/P2 license?*
- *Show me P1/P2 feature utilization.*
- *Provide Microsoft Entra P1/P2 license usage details.*

## Deactivate your role

After completing your tasks with Microsoft Security Copilot, ensure that you deactivate any elevated roles you activated during your session to maintain security best practices. Use the following prompt to deactivate your role:

- *I am done with my investigation or {desired task}, deactivate my access.*