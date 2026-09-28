---
layout: Conceptual
title: Define organizational policies for governing access to applications in your environment - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/identity-governance-applications-define
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Microsoft Entra ID Governance allows you to balance your organization's need for security and employee productivity with the right processes and visibility. You can define policies for how users should obtain access to your business critical applications integrated with Microsoft Entra ID Governance.
editor: markwahl-msft
ms.topic: how-to
ms.date: 2024-12-10T00:00:00.0000000Z
ms.reviewer: markwahl-msft
locale: en-us
document_id: b0ff1f12-204c-0e8e-046a-b4349e573154
document_version_independent_id: acb7adac-7ab2-4c6b-11d0-c7af2ea5a2c6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/identity-governance-applications-define.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/identity-governance-applications-define
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/identity-governance-applications-define.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 91605c02-13c8-ae95-ee6f-1312d8229e15
---

# Define organizational policies for governing access to applications in your environment - Microsoft Entra ID Governance | Microsoft Learn

Once you've identified one or more applications that you want to use Microsoft Entra ID to [govern access](identity-governance-applications-prepare), write down the organization's policies for determining which users should have access, and any other constraints that the system should provide.

## Select applications and their roles in scope

Organizations with compliance requirements or risk management plans have sensitive or business-critical applications. If this application is an existing application in your environment, you may already have documented the access policies for who 'should have access' to this application. If not, you may need to consult with various stakeholders, such as compliance and risk management teams, to ensure that the policies being used to automate access decisions are appropriate for your scenario.

1. **Collect the roles and permissions that each application provides.** Some applications may have only a single role, for example, an application that only has the role "User". More complex applications may surface multiple roles to be managed through Microsoft Entra ID. These application roles typically make broad constraints on the access a user with that role would have within the app. For example, an application that has an administrator persona might have two roles, "User" and "Administrator". Other applications may also rely upon group memberships or claims for finer-grained role checks, which can be provided to the application from Microsoft Entra ID in provisioning or claims issued using federation SSO protocols, or written to AD as a security group membership. Finally, there may be application-specific roles that don't surface in Microsoft Entra ID - perhaps the application doesn't permit defining the administrators in Microsoft Entra ID, instead relying upon its own authorization rules to identify administrators. SAP Cloud Identity Services only has one role, **User**, available for assignment.

    Note

    If you're using an application from the Microsoft Entra application gallery that supports provisioning, then Microsoft Entra ID may import defined roles in the application and automatically update the application manifest with the application's roles automatically, once provisioning is configured.
2. **Select which roles and groups have membership that are to be governed in Microsoft Entra ID.** Based on compliance and risk management requirements, organizations often prioritize those application roles or groups that give privileged access or access to sensitive information.

## Define the organization's policy with prerequisites and other constraints for access to the application

In this section, you'll write down the organizational policies you plan to use to determine access to the application. You can record this as a table in a spreadsheet, for example

| App Role | Prerequisite for access | Approvers | Default duration of access | Separation of duties constraints | Conditional Access policies |
| --- | --- | --- | --- | --- | --- |
| *Western Sales* | Member of sales team | user's manager | Yearly review | Cannot have *Eastern Sales* access | Multifactor authentication (MFA) and registered device required for access |
| *Western Sales* | Any employee outside of sales | head of Sales department | 90 days | N/A | MFA and registered device required for access |
| *Western Sales* | Non-employee sales rep | head of Sales department | 30 days | N/A | MFA required for access |
| *Eastern Sales* | Member of sales team | user's manager | Yearly review | Cannot have *Western Sales* access | MFA and registered device required for access |
| *Eastern Sales* | Any employee outside of sales | head of Sales department | 90 days | N/A | MFA and registered device required for access |
| *Eastern Sales* | Non-employee sales rep | head of Sales department | 30 days | N/A | MFA required for access |

If you already have an organization role definition, then see [how to migrate an organizational role](identity-governance-organizational-roles) for more information.

1. **Identify if there are prerequisite requirements, standards that a user must meet before to they're given access to an application.** For example, under normal circumstances, only full time employees, or those in a particular department or cost center, should be allowed to have access to a particular department's application. Also, you may require the entitlement management policy for a user from some other department requesting access to have one or more additional approvers. While having multiple stages of approval may slow the overall process of a user gaining access, these extra stages ensure access requests are appropriate and decisions are accountable. For example, requests for access by an employee could have two stages of approval, first by the requesting user's manager, and second by one of the resource owners responsible for data held in the application.
2. **Determine how long a user who has been approved for access, should have access, and when that access should go away.** For many applications, a user might retain access indefinitely, until they're no longer affiliated with the organization. In some situations, access may be tied to particular projects or milestones, so that when the project ends, access is removed automatically. Or, if only a few users are using an application through a policy, you may configure quarterly or yearly reviews of everyone's access through that policy, so that there's regular oversight.
3. **If your organization is governing access already with an organizational role model, plan to bring that organizational role model into Microsoft Entra ID.** You may have an [organizational role](identity-governance-organizational-roles) defined which assigns access based on a user's property, such as their position or department. These processes can ensure users lose access eventually when access is no longer needed, even if there isn't a pre-determined project end date.
4. **Inquire if there are separation of duties constraints.** For example, you may have an application with two app roles, *Western Sales* and *Eastern Sales*, and you want to ensure that a user can only have one sales territory at a time. Include a list of any pairs of app roles that are incompatible for your application, so that if a user has one role, they aren't allowed to request the second role.
5. **Select the appropriate Conditional Access policy for access to the application.** We recommend that you analyze your applications and group them into applications that have the same resource requirements for the same users. If this is the first federated SSO application you're integrating with Microsoft Entra ID Governance for identity governance, you may need to create a new Conditional Access policy to express constraints, such as requirements for Multifactor authentication (MFA) or location-based access. You can configure users to be required to agree to [a terms of use](../identity/conditional-access/policy-all-users-require-terms-of-use). See [plan a Conditional Access deployment](../identity/conditional-access/plan-conditional-access) for more considerations on how to define a Conditional Access policy.
6. **Determine how exceptions to your criteria should be handled.** For example, an application may typically only be available for designated employees, but an auditor or vendor may need temporary access for a specific project. Or, an employee who is traveling may require access from a location that is normally blocked as your organization has no presence in that location. In these situations, you may choose to also have an entitlement management policy for approval that may have different stages, or a different time limit, or a different approver. A vendor who is signed in as a guest user in your Microsoft Entra tenant may not have a manager, so instead their access requests could be approved by a sponsor for their organization, or by a resource owner, or a security officer.

As the organizational policy for who should have access is being reviewed by the stakeholders, then you can begin [integrating the application](identity-governance-applications-integrate) with Microsoft Entra ID. That way at a later step you are ready to [deploy the organization-approved policies](identity-governance-applications-deploy) for access in Microsoft Entra ID Governance.