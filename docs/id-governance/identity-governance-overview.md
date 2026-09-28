---
layout: Conceptual
title: Microsoft Entra ID Governance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/identity-governance-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Microsoft Entra ID Governance enables you to balance your organization's need for security and end user productivity with the right processes and visibility.
editor: markwahl-msft
ms.topic: overview
ms.date: 2026-05-08T00:00:00.0000000Z
ms.reviewer: markwahl-msft
locale: en-us
document_id: a68d2671-8e5e-63b2-b5d2-5f58c5b9aa2f
document_version_independent_id: 7dd0b7fd-042a-c68f-8979-d5828f1ce2e8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/identity-governance-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/identity-governance-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/identity-governance-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 15544a7b-d4cf-d668-7acc-118a439141fa
---

# Microsoft Entra ID Governance - Microsoft Entra ID Governance | Microsoft Learn

[Microsoft Entra ID Governance](https://www.microsoft.com/security/business/identity-access/microsoft-entra-id-governance) is an identity governance solution that enables organizations to improve productivity, strengthen security and more easily meet compliance and regulatory requirements. Microsoft Entra ID Governance leverages AI-driven insights to help organizations automatically ensure that the right people have the right access to the right resources. This is achieved through identity and access process automation, delegation to business groups, and increased visibility. With features in Microsoft Entra ID Governance and related Microsoft products, you can mitigate identity and access risks by protecting, monitoring, and auditing access to critical assets.

Specifically, Microsoft Entra ID Governance helps organizations address these four key questions, for access across services and applications both on-premises and in clouds:

- Which identities should have access to which resources?
- What are those identities doing with that access?
- Are there organizational controls in place for managing access?
- Can auditors verify that the controls are working effectively?

With Microsoft Entra ID Governance you can implement the following scenarios for employees, business partners and vendors:

- Govern the identity lifecycle
- Govern the access lifecycle
- Secure privileged access for administration

## Identity lifecycle

Identity Governance helps organizations achieve a balance between *productivity* - How quickly can a person have access to the resources they need, such as when they join my organization? And *security* - How should their access change over time, such as due to changes to that person's employment status? Identity lifecycle management is the foundation for Identity Governance, and effective governance at scale requires modernizing the identity lifecycle management infrastructure for applications.

![Identity lifecycle](media/identity-governance-overview/identity-lifecycle.png)

For many organizations, identity lifecycle for employees and other workers is tied to the representation of that person in an HCM (human capital management) or HR system. Organizations need to automate the process of creating an identity for a new employee that is based on a signal from that system so that the employee can be productive on day 1. And organizations need to ensure those identities and access are removed when the employee leaves the organization.

In Microsoft Entra ID Governance, you can [automate the identity lifecycle](https://youtu.be/NxSu3JEsxmY?si=fuY8nV4Fg5DbMArd) for these individuals using:

- [inbound provisioning from your organization's HR sources](../identity/app-provisioning/plan-cloud-hr-provision), including retrieving from Workday and SuccessFactors, to automatically maintain user identities in both Active Directory and Microsoft Entra ID.
- [lifecycle workflows](what-are-lifecycle-workflows) to automate workflow tasks that run at certain key events, such before a new employee is scheduled to start work at the organization, as they change status during their time in the organization, and as they leave the organization. For example, a workflow can be configured to send an email with a temporary access pass to a new user's manager, or a welcome email to the user, on their first day.
- [automatic assignment policies in entitlement management](entitlement-management-access-package-auto-assignment-policy) to add and remove a user's group memberships, application roles, and SharePoint site roles, based on changes to the user's attributes.
- [user provisioning](what-is-provisioning) to create, update, and remove user accounts in other applications, with connectors to [hundreds of cloud and on-premises applications](apps) via SCIM, LDAP and SQL.

Organizations also need additional identities, for partners, suppliers and other guests, to enable them to collaborate or have access to resources.

In Microsoft Entra ID Governance, you can enable business groups to determine which of these guests should have access, and for how long, using:

- [entitlement management](entitlement-management-overview) in which you can specify the other organizations whose identities are allowed to request access to your organization's resources. When one of the identities request is approved, they're automatically added by entitlement management as a [B2B](../external-id/what-is-b2b) guest to your organization's directory. Then, they're assigned appropriate access. Entitlement management automatically removes the B2B guest user from your organization's directory when their access rights expire or are revoked.
- [access reviews](access-reviews-overview) that automates recurring reviews of existing guests already in your organization's directory, and removes those identities from your organization's directory when they no longer need access. AI-powered suggestions help reviewers make better informed decisions.

For more information, see [Govern the employee and guest lifecycle](scenarios/govern-the-employee-lifecycle).

## Access lifecycle

Organizations need a process to manage access beyond what was initially provisioned for a user when that user's identity was created. Furthermore, enterprise organizations need to be able to scale efficiently to be able to develop and enforce access policy and controls on an ongoing basis.

![Access lifecycle](media/identity-governance-overview/access-lifecycle.png)

With Microsoft Entra ID Governance, IT departments can establish which access rights identities should have across various resources. They can also determine necessary enforcement checks, such as separation of duties or access removal on job change are necessary. Microsoft Entra ID has connectors to [hundreds of cloud and on-premises applications](apps). You can integrate your organization's other apps that rely upon [AD groups](entitlement-management-group-writeback), [other on-premises directories](../identity/app-provisioning/on-premises-ldap-connector-configure) or [databases](../identity/app-provisioning/on-premises-sql-connector-configure), that have a [SOAP or REST API](../identity/app-provisioning/on-premises-web-services-connector) including [SAP](sap), or that implement standards such as [SCIM](../identity/app-provisioning/use-scim-to-provision-users-and-groups), SAML or OpenID Connect. When a user attempts to sign into to one of those applications, Microsoft Entra ID enforces [Conditional Access](../identity/conditional-access/) policies. For example, Conditional Access policies can include displaying a [terms of use](../identity/conditional-access/terms-of-use) and [ensuring the user has agreed to those terms](../identity/conditional-access/policy-all-users-require-terms-of-use) prior to being able to access an application. For more information, see [govern access to applications in your environment](identity-governance-applications-prepare), including how to [define organizational policies for governing access to applications](identity-governance-applications-define), [integrate applications](identity-governance-applications-integrate), and [deploy policies](identity-governance-applications-deploy).

Access changes across apps and groups can be automated based on attribute changes. [Microsoft Entra lifecycle workflows](create-lifecycle-workflow) and [Microsoft Entra entitlement management](entitlement-management-overview) automatically adds and removes identities into groups or access packages, so that access to applications and resources is updated. Identities can also be moved when their condition within the organization changes to different groups, and can even be removed entirely from all groups or access packages.

Organizations that previously had been using an on-premises identity governance product can [migrate their organizational role model](identity-governance-organizational-roles) to Microsoft Entra ID Governance.

Furthermore, IT can delegate access management decisions to business decision makers. For example, employees that wish to access confidential customer data in a company's marketing application in Europe could need approval from their manager, a department lead or resource owner, and a security risk officer. [Entitlement management](entitlement-management-overview) enables you to define how identities request access across packages of group and team memberships, app roles, and SharePoint Online roles, and enforce separation of duties checks on access requests. Access packages can require regular access reviews, and other access rights, such as group memberships, can also be regularly reviewed using recurring [Microsoft Entra access reviews](access-reviews-overview) for access recertification, including AI-identified peer outliers which may require higher scrutiny.

Organizations can also control which guest identities have access, including to [on-premises applications](../external-id/hybrid-cloud-to-on-premises).

## Privileged access lifecycle

Governing privileged access is a key part of modern Identity Governance especially given the potential for misuse associated with administrator rights can cause to an organization. The employees, vendors, and contractors that take on administrative rights need to have their accounts and privileged access rights governed.

![Privileged access lifecycle](media/identity-governance-overview/privileged-access-lifecycle.png)

[Microsoft Entra Privileged Identity Management (PIM)](privileged-identity-management/pim-configure) provides additional controls tailored to securing access rights for resources, across Microsoft Entra, Azure, other Microsoft Online Services and other applications. The just-in-time access, and role change alerting capabilities provided by Microsoft Entra PIM, in addition to multifactor authentication and Conditional Access, provide a comprehensive set of governance controls to help secure your organization's resources (directory roles, Microsoft 365 roles, Azure resource roles and group memberships). As with other forms of access, organizations can use access reviews to configure recurring access re-certification for all identities in privileged administrator roles.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Getting started

Check out the [Prerequisites before configuring Microsoft Entra ID for identity governance](identity-governance-applications-prepare). Then, visit the [Governance dashboard](https://entra.microsoft.com/#view/Microsoft_Azure_IdentityGovernance/Dashboard.ReactView) in the Microsoft Entra admin center to start using entitlement management, access reviews, lifecycle workflows and Privileged Identity Management.

There are also tutorials for [managing access to resources in entitlement management](entitlement-management-access-package-first), [onboarding external users to Microsoft Entra ID through an approval process](entitlement-management-onboard-external-user), [governing access to your applications](identity-governance-applications-prepare) and the [application's existing users](identity-governance-applications-existing-users).

While each organization may have its own unique requirements, the following configuration guides also provide the baseline policies Microsoft recommends you follow to ensure a more secure and productive workforce.

- [Plan an access reviews deployment to manage resource access lifecycle](deploy-access-reviews)
- [Zero Trust identity and device access configurations](/en-us/microsoft-365/enterprise/microsoft-365-policies-configurations)
- [Securing privileged access](../identity/role-based-access-control/security-planning)

You may also wish to engage with one of Microsoft's [services and integration partners](services-and-integration-partners) to plan your deployment or integrate with the applications and other systems in your environment.

If you have any feedback about Identity Governance features, select **Got feedback?** in the Microsoft Entra admin center to submit your feedback. The team regularly reviews your feedback.

## Simplifying identity governance tasks with automation

Once you've started using these identity governance features, you can easily automate common identity governance scenarios. The following table shows how to get started with automation for each scenario:

| Scenario to automate | Automation guide |
| --- | --- |
| Creating, updating and deleting AD and Microsoft Entra user accounts automatically for employees | [Plan cloud HR to Microsoft Entra user provisioning](../identity/app-provisioning/plan-cloud-hr-provision) |
| Updating the membership of a group, based on changes to the member user's attributes | [Create a dynamic group](../identity/users/groups-create-rule) |
| Assigning licenses | [group-based licensing](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true) |
| Adding and removing a user's group memberships, application roles, and SharePoint site roles, based on changes to the user's attributes | [Configure an automatic assignment policy for an access package in entitlement management](entitlement-management-access-package-auto-assignment-policy) |
| Adding and removing a user's group memberships, application roles, and SharePoint site roles, on a specific date | [Configure lifecycle settings for an access package in entitlement management](entitlement-management-access-package-lifecycle-policy) |
| Running custom workflows when a user requests or receives access, or access is removed | [Trigger Logic Apps in entitlement management](entitlement-management-logic-apps-integration) |
| Regularly having memberships of guests in Microsoft groups and Teams reviewed, and removing guest memberships that are denied | [Create an access review](create-access-review) |
| Removing guest accounts that were denied by a reviewer | [Review and remove external users who no longer have resource access](access-reviews-external-users) |
| Removing guest accounts that have no access package assignments | [Manage the lifecycle of external users](entitlement-management-external-users#manage-the-lifecycle-of-external-users) |
| Provisioning users into on-premises and cloud applications that have their own directories or databases | [Configure automatic user provisioning](../identity/app-provisioning/user-provisioning) with user assignments or [scoping filters](../identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts) |
| Other scheduled tasks | [Automate identity governance tasks with Azure Automation](identity-governance-automation) and Microsoft Graph via the [Microsoft.Graph.Identity.Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) PowerShell module |
| Discover orphan or local accounts in your applications | [Discover existing](../identity/app-provisioning/how-to-account-discovery) users in your applications. |

## Identity governance for agents (preview)

With the addition of the Microsoft agent identity platform, managing an agent's identity and access in the same way as people is just as important in the governance lifecycle of your organization. Microsoft Entra Agent ID introduces [agent identities](../agent-id/what-is-microsoft-entra-agent-id) — purpose-built identity constructs for AI agents — with governance controls that address the unique challenges of autonomous and semi-autonomous agents operating at enterprise scale.

Every agent identity requires a human [sponsor](../agent-id/agent-owners-sponsors-managers) accountable for the agent's purpose, lifecycle decisions, and access reviews. If a sponsor leaves the organization, sponsorship automatically transfers to their manager, ensuring continuous human oversight. [Agent identity blueprints](../agent-id/identity-platform/agent-blueprint) serve as centralized templates that enable organizations to apply Conditional Access rules, permissions, and governance controls once and have all current and future agent instances inherit them automatically. This blueprint model allows administrators to govern, disable, or revoke permissions for an entire class of agents in a single operation.

Agent identities are governed through the same [entitlement management](entitlement-management-overview) access packages available for human identities, providing time-bound, auditable access with approval workflows. Sponsors receive expiration notifications and can request extensions or let access expire. [Lifecycle Workflows](agent-sponsor-tasks) automate sponsor transition notifications when sponsorship changes occur. All agent identities are discoverable, searchable, and queryable through the Microsoft Entra admin center and Microsoft Graph, giving organizations centralized visibility to prevent agent sprawl and shadow AI.

For more information, see [Governing agent identities (preview)](agent-id-governance-overview).