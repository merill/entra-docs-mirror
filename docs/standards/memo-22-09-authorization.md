---
layout: Conceptual
title: Meet authorization requirements of memorandum 22-09 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/memo-22-09-authorization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn how to meet authorization requirements outlined in OMB memorandum 22-09.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2025-02-10T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: e9ce4f34-1387-4d33-2aa5-46130621d606
document_version_independent_id: 9752f9a1-88d8-fa80-0c3c-f1aef7598a52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/memo-22-09-authorization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/memo-22-09-authorization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/memo-22-09-authorization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 7a264ceb-74ad-bb39-2f1e-f980f18acdc6
---

# Meet authorization requirements of memorandum 22-09 - Microsoft Entra | Microsoft Learn

This article series has guidance to employ Microsoft Entra ID as a centralized identity management system when implementing Zero Trust principles. Instructions and guidance are based on US Office of Management and Budget (OMB) [M-22-09 Memorandum for the Heads of Executive Departments and Agencies](https://bidenwhitehouse.archives.gov/wp-content/uploads/2022/01/M-22-09.pdf).

The memo requirements are enforcement types in multifactor authentication policies, and controls for devices, roles, attributes, and privileged access management.

## Device-based controls

A memorandum 22-09 requirement is at least one device-based signal for authorization decisions to access a system or application. Enforce the requirement by using Conditional Access. Apply several device signals during the authorization. See the following table for the signal and the requirement to retrieve the signal.

| Signal | Signal retrieval |
| --- | --- |
| Device is managed | Integration with Intune or another mobile device management (MDM) solution supporting integration. |
| Microsoft Entra hybrid joined | Active Directory manages the device, and it qualifies. |
| Device is compliant | Integration with Intune or another MDM solution supporting the integration. See, [Create a compliance policy in Microsoft Intune](/en-us/mem/intune/protect/device-compliance-get-started). |
| Threat signals | Microsoft Defender for Endpoint and other endpoint detection and response (EDR) tools have Microsoft Entra ID and Intune integrations that send threat signals to deny access. Threat signals support the compliant status signal. |
| Cross-tenant access policies (public preview) | Trust device signals from devices in other organizations. |

## Role-based controls

Use role-based access control (RBAC) to enforce authorizations through role assignments in a particular scope. For example, assign access by using entitlement management features, including access packages and access reviews. Manage authorizations with self-service requests and use automation to manage lifecycle. For example, automatically end access based on criteria.

Learn more:

- [What is entitlement management?](../id-governance/entitlement-management-overview)
- [Create a new access package in entitlement management](../id-governance/entitlement-management-access-package-create)
- [What are access reviews?](../id-governance/access-reviews-overview)

## Attribute-based controls

Attribute-based access control (ABAC) uses metadata assigned to a user or resource to permit or deny access during authentication. See the following sections to create authorizations by using ABAC enforcements for data and resources through authentication.

### Attributes assigned to users

Use attributes assigned to users, stored in Microsoft Entra ID, to create user authorizations. Users are automatically assigned to dynamic membership groups based on a rule set you define during group creation. Rules add or remove a user from the group based on rule evaluation against the user and their attributes. We recommend you maintain attributes and don't set static attributes on creation day.

Learn more: [Create or update a dynamic group in Microsoft Entra ID](../identity/users/groups-create-rule)

### Attributes assigned to data

With Microsoft Entra ID, you can integrate authorization to the data. See the following sections to integrate authorization. You can configure authentication in Conditional Access policies: restrict actions users take in an application or on data. These authentication policies are then mapped in the data source.

Data sources can be Microsoft Office files like Word, Excel, or SharePoint sites mapped to authentication. Use authentication assigned to data in applications. This approach requires integration with the application code and for developers to adopt the capability. Use authentication integration with Microsoft Defender for Cloud Apps to control actions taken on data through session controls.

Combine dynamic membership groups with authentication context to control user access mappings between the data and the user attributes.

Learn more:

- [Conditional Access: Cloud apps, actions, and authentication context](../identity/conditional-access/concept-conditional-access-cloud-apps)
- [Developer guide to Conditional Access authentication context](../identity-platform/developer-guide-conditional-access-authentication-context)
- [Session policies](/en-us/defender-cloud-apps/session-policy-aad)

### Attributes assigned to resources

Azure includes attribute-based access control (Azure ABAC) for storage. Assign metadata tags on data stored in an Azure Blob Storage account. Assign the metadata to users by using role assignments to grant access.

Learn more: [What is Azure attribute-based access control?](/en-us/azure/role-based-access-control/conditions-overview)

## Privileged access management

The memo cites the inefficiency of using of privileged access management tools with single-factor ephemeral credentials to access systems. These technologies include password vaults that accept multifactor authentication sign-in for an admin. These tools generate a password for an alternate account to access the system. System access occurs with a single factor.

Microsoft tools implement Privileged Identity Management (PIM) for privileged systems with Microsoft Entra ID as the central identity management system. Enforce multifactor authentication for most privileged systems that are applications, infrastructure elements, or devices.

Use PIM for a privileged role, when it's implemented with Microsoft Entra identities. Identify privileged systems that require protections to prevent lateral movement.

Learn more:

- [What is Microsoft Entra Privileged Identity Management?](../id-governance/privileged-identity-management/pim-configure)
- [Plan a Privileged Identity Management deployment](../id-governance/privileged-identity-management/pim-deployment-plan)