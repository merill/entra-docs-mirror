---
layout: Conceptual
title: Create a security plan for external access to resources - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/3-secure-access-plan
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Plan the security for external access to your organization's resources.
ms.topic: how-to
ms.date: 2023-02-23T00:00:00.0000000Z
ms.reviewer: gasinh
ms.subservice: architecture
locale: en-us
document_id: ca33aefd-ea4d-f62b-091f-05d04ccac343
document_version_independent_id: 1c95c089-02cd-3934-7e4d-b0cb8fb7462f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/3-secure-access-plan.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/3-secure-access-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/3-secure-access-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: d71a107b-02cf-a945-462c-7547cc5249e0
---

# Create a security plan for external access to resources - Microsoft Entra | Microsoft Learn

Before you create an external-access security plan, review the following two articles, which add context and information for the security plan.

- [Determine your security posture for external access with Microsoft Entra ID](1-secure-access-posture)
- [Discover the current state of external collaboration in your organization](2-secure-access-current-state)

## Before you begin

This article is number 3 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Security plan documentation

For your security plan, document the following information:

- Applications and resources grouped for access
- Sign-in conditions for external users
    - Device state, sign-in location, client application requirements, user risk, and so on.
- Policies to determine timing for reviews and access removal
- User populations grouped for similar experiences

To implement the security plan, you can use Microsoft identity and access management policies, or another identity provider (IdP).

Learn more: [Identity and access management overview](/en-us/compliance/assurance/assurance-identity-and-access-management)

## Use groups for access

See the following links to articles about resource grouping strategies:

- Microsoft Teams groups files, conversation threads, and other resources
    - Formulate an external access strategy for Teams
    - See, [Secure external access to Microsoft Teams, SharePoint, and OneDrive for Business with Microsoft Entra ID](9-secure-access-teams-sharepoint)
- Use entitlement management access packages to create and delegate package management of applications, groups, teams, SharePoint sites, and so on.
    - [Create a new access package in entitlement management](../id-governance/entitlement-management-access-package-create)
- Apply Conditional Access policies to up to 250 applications, with the same access requirements
    - [What is Conditional Access?](../identity/conditional-access/overview)
- Define access for external user application groups
    - [Overview: Cross-tenant access with Microsoft Entra External ID](../external-id/cross-tenant-access-overview)

Document the grouped applications. Considerations include:

- **Risk profile**- assess the risk if a bad actor gains access to an application
    - Identify application as High, Medium, or Low risk. We recommend you don't group High-risk with Low-risk.
    - Document applications that can't be shared with external users
- **Compliance frameworks**- determine compliance frameworks for apps
    - Identify access and review requirements
- **Applications for roles or departments** - assess applications grouped for role, or department, access
- **Collaboration applications**- identify collaboration applications external users can access, such as Teams or SharePoint
    - For productivity applications, external users might have licenses, or you might provide access

Document the following information for application and resource group access by external users.

- Descriptive group name, for example High\_Risk\_External\_Access\_Finance
- Applications and resources in the group
- Application and resource owners and their contact information
- The IT team controls access, or control is delegated to a business owner
- Prerequisites for access: background check, training, and so on.
- Compliance requirements to access resources
- Challenges, for example multifactor authentication for some resources
- Cadence for reviews, by whom, and where results are documented

Tip

Use this type of governance plan for internal access.

## Document sign-in conditions for external users

Determine the sign-in requirements for external users who request access. Base requirements on the resource risk profile, and the user's risk assessment during sign-in. Configure sign-in conditions using Conditional Access: a condition and an outcome. For example, you can require multifactor authentication.

Learn more: [What is Conditional Access?](../identity/conditional-access/overview)

**Resource risk-profile sign-in conditions**

Consider the following risk-based policies to trigger multifactor authentication.

- **Low** - multifactor authentication for some application sets
- **Medium** - multifactor authentication when other risks are present
- **High** - external users always use multifactor authentication

Learn more:

- [Tutorial: Enforce multifactor authentication for B2B guest users](../external-id/b2b-tutorial-require-mfa)
- Trust multifactor authentication from external tenants
    - See, [Configure cross-tenant access settings for B2B collaboration, Modify inbound access settings](../external-id/cross-tenant-access-settings-b2b-collaboration#modify-inbound-access-settings)

### User and device sign-in conditions

Use the following table to help assess policy to address risk.

| User or sign-in risk | Proposed policy |
| --- | --- |
| Device | Require compliant devices |
| Mobile apps | Require approved apps |
| Microsoft Entra ID Protection user risk is high | Require user to change password |
| Network location | To access confidential projects, require sign-in from an IP address range |

To use device state as policy input, register, or join the device to your tenant. To trust the device claims from the home tenant, configure cross-tenant access settings. See, [Modify inbound access settings](../external-id/cross-tenant-access-settings-b2b-collaboration#modify-inbound-access-settings).

You can use identity-protection risk policies. However, mitigate issues in the user home tenant. See, [Common Conditional Access policy: Sign-in risk-based multifactor authentication](../identity/conditional-access/policy-risk-based-sign-in).

For network locations, you can restrict access to IP addresses ranges that you own. Use this method if external partners access applications while at your location. See, [Conditional Access: Block access by location](../identity/conditional-access/policy-block-by-location)

## Document access review policies

Document policies that dictate when to review resource access, and remove account access for external users. Inputs might include:

- Compliance frameworks requirements
- Internal business policies and processes
- User behavior

Generally, organizations customize policy, however consider the following parameters:

- **Entitlement management access reviews**:
    - [Change lifecycle settings for an access package in entitlement management](../id-governance/entitlement-management-access-package-lifecycle-policy)
    - [Create an access review of an access package in entitlement management](../id-governance/entitlement-management-access-reviews-create)
    - [Add a connected organization in entitlement management](../id-governance/entitlement-management-organization): Group users from a partner and schedule reviews
- **Microsoft 365 groups**
    - [Microsoft 365 group expiration policy](/en-us/microsoft-365/solutions/microsoft-365-groups-expiration-policy?view=o365-worldwide&amp;preserve-view=true)
- **Options**:
    - If external users don't use access packages or Microsoft 365 groups, determine when accounts become inactive or deleted
    - Remove sign-in for accounts that don't sign in for 90 days
    - Regularly assess access for external users

## Access control methods

Some features, for example entitlement management, are available with a Microsoft Entra ID P1 or P2 license. Microsoft 365 E5 and Office 365 E5 licenses include Microsoft Entra ID P2 licenses. Learn more in the following entitlement management section.

Note

Licenses are for one user. Therefore users, administrators, and business owners can have delegated access control. This scenario can occur with Microsoft Entra ID P2 or Microsoft 365 E5, and you don't have to enable licenses for all users. The first 50,000 external users are free. If you don't enable P2 licenses for other internal users, they can't use entitlement management.

Other combinations of Microsoft 365, Office 365, and Microsoft Entra ID have functionality to manage external users. See, [Microsoft 365 guidance for security and compliance](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance).

## Govern access with Microsoft Entra ID P2 and Microsoft 365 or Office 365 E5

Microsoft Entra ID P2, included in Microsoft 365 E5, has additional security and governance capabilities.

### Provision, sign-in, review access, and deprovision access

Entries in bold are recommended actions.

| Feature | Provision external users | Enforce sign-in requirements | Review access | Deprovision access |
| --- | --- | --- | --- | --- |
| Microsoft Entra B2B collaboration | Invite via email, one-time password (OTP), self-service | N/A | **Periodic partner review** | Remove accountRestrict sign-in |
| Entitlement management | **Add user by assignment or self-service access** | N/A | Access reviews | **Expiration of, or removal from, access package** |
| Office 365 groups | N/A | N/A | Review group memberships | Group expiration or deletion Removal from group |
| Microsoft Entra security groups | N/A | **Conditional Access policies**: Add external users to security groups as needed | N/A | N/A |

### Resource access

Entries in bold are recommended actions.

| Feature | App and resource access | SharePoint and OneDrive access | Teams access | Email and document security |
| --- | --- | --- | --- | --- |
| Entitlement management | **Add user by assignment or self-service access** | **Access packages** | **Access packages** | N/A |
| Office 365 Group | N/A | Access to sites and group content | Access to teams and group content | N/A |
| Sensitivity labels | N/A | **Manually and automatically classify and restrict access** | **Manually and automatically classify and restrict access** | **Manually and automatically classify and restrict access** |
| Microsoft Entra security groups | **Conditional Access policies for access not included in access packages** | N/A | N/A | N/A |

### Entitlement management

Use entitlement management to provision and deprovision access to groups and teams, applications, and SharePoint sites. Define the connected organizations granted access, self-service requests, and approval workflows. To ensure access ends correctly, define expiration policies and access reviews for packages.

Learn more: [Create a new access package in entitlement management](../id-governance/entitlement-management-access-package-create)

## Manage access with Microsoft Entra ID P1, Microsoft 365, Office 365 E3

### Provision, sign-in, review access, and deprovision access

Items in bold are recommended actions.

| Feature | Provision external users | Enforce sign-in requirements | Review access | Deprovision access |
| --- | --- | --- | --- | --- |
| Microsoft Entra B2B collaboration | **Invite by email, OTP, self-service** | Direct B2B federation | **Periodic partner review** | Remove accountRestrict sign-in |
| Microsoft 365 or Office 365 groups | N/A | N/A | N/A | Group expiration or deletionRemoval from group |
| Security groups | N/A | **Add external users to security groups (org, team, project, and so on)** | N/A | N/A |
| Conditional Access policies | N/A | **Sign-in Conditional Access policies for external users** | N/A | N/A |

### Resource access

| Feature | App and resource access | SharePoint and OneDrive access | Teams access | Email and document security |
| --- | --- | --- | --- | --- |
| Microsoft 365 or Office 365 groups | N/A | **Access to group sites and associated content** | **Access to Microsoft 365 group teams and associated content** | N/A |
| Sensitivity labels | N/A | Manually classify and restrict access | Manually classify and restrict access | Manually classify to restrict and encrypt |
| Conditional Access policies | Conditional Access policies for access control | N/A | N/A | N/A |
| Other methods | N/A | Restrict SharePoint site access with security groupsDisallow direct sharing | **Restrict external invitations from a team** | N/A |