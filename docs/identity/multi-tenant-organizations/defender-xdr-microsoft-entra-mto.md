---
layout: Conceptual
title: Secure and govern security operations center (SOC) access in a multitenant organization with Microsoft Defender for Cloud XDR and Microsoft Entra ID Governance - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/defender-xdr-microsoft-entra-mto
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.reviewer: hafowler
ms.service: entra-id
ms.subservice: multitenant-organizations
manager: dougeby
description: Learn how to provide security operations analysts access to resources across tenants.
ms.topic: overview
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 69c7c3a8-ee91-33da-7753-aa62b09218a7
document_version_independent_id: 69c7c3a8-ee91-33da-7753-aa62b09218a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/defender-xdr-microsoft-entra-mto.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/defender-xdr-microsoft-entra-mto
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/defender-xdr-microsoft-entra-mto.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 9d1c459f-1fd3-115e-6304-41acb868157e
---

# Secure and govern security operations center (SOC) access in a multitenant organization with Microsoft Defender for Cloud XDR and Microsoft Entra ID Governance - Microsoft Entra ID | Microsoft Learn

## Overview

Managing multitenant environments can add another layer of complexity when it comes to keeping up with the ever-evolving security threats facing your enterprise. Navigating across multiple tenants can be time consuming and reduce the overall efficiency of security operations center (SOC) teams. Multitenant management in [Microsoft Defender XDR](/en-us/microsoft-365/security/defender/mto-overview) provides security operation teams with a single, unified view of all the tenants they manage. This view enables teams to quickly investigate incidents and perform advanced hunting across data from multiple tenants, improving their security operations.

[Microsoft Entra ID Governance](../../id-governance/identity-governance-overview) enables you to govern the access and lifecycle of the users who are members of the SOC teams and threat hunter teams. This document explores:

- The controls you can put in place for SOC teams to securely access resources across tenants.
- Example topologies for how you can implement your lifecycle and access controls.
- Deployment considerations (roles, monitoring, APIs).

## Manage the lifecycle and access of a SOC user

Microsoft Entra provides the controls needed to govern the lifecycle of a SOC user and to securely provide access to the resources they need. In this document, the term source tenant refers to where the SOC users originate and authenticate against. Target tenant refers to the tenant that they're investigating when there's an incident. Organizations have multiple target tenants due to mergers and acquisitions, aligning tenants with business units, and aligning tenants with geos.

### Lifecycle control

**Entitlement management, through access packages and connected organizations** allows the target tenant administrator to define collections of resources (ex: app roles, directory roles, and groups) that users from the source tenant can request access to. If the user is approved for the resources they need, but don't yet have a B2B account, entitlement management will automatically create a B2B account for the user in the target tenant. When they don't have any remaining entitlements in the target tenant, their B2B account will automatically be removed. Entitlement management can be used both within an organization and across organizations.

For more information, see [entitlement management and connected organizations](../../id-governance/entitlement-management-organization).

**Cross-tenant synchronization** allows the source tenant to automate creating, updating, and deleting B2B users across tenants in an organization.

For more information, see [cross-tenant synchronization](cross-tenant-synchronization-overview).

**Comparing entitlement management and cross-tenant synchronization**

| Capability | Entitlement management | Cross-tenant synchronization |
| --- | --- | --- |
| Create users in the target tenant | - | - |
| Update users in the target tenant when their attributes change in the source tenant |  | - |
| Delete users | - | - |
| Assign users to groups, directory roles, app roles | - |  |
| Attributes of the user in the target tenant | Minimal, supplied by user themselves at request time | Synchronized from the source tenant |

### Access control

You can use entitlement management and cross-tenant access policies to control access to resources across tenants. Entitlement management will assign the right users to the right resources, while cross-tenant access policies and Conditional Access together perform the necessary run-time checks to ensure the right users are accessing the right resources.

**Entitlement management**

Assigning Microsoft Entra roles through entitlement management access packages helps to efficiently manage role assignments at scale and improves the role assignment lifecycle. It provides a flexible request and approval process for gaining access to directory roles, app roles, and groups while also enabling automatic assignment to resources based on user attributes.

For more information, see [entitlement management overview](../../id-governance/entitlement-management-overview).

**Cross-tenant access policies**

External identities cross-tenant access settings manage how you collaborate with other Microsoft Entra organizations through B2B collaboration. These settings determine both the level of inbound access users in external Microsoft Entra organizations have to your resources, and the level of outbound access your users have to external organizations.

For more information, see [cross-tenant access overview](../../external-id/cross-tenant-access-overview).

## Deployment topologies

This section describes how you can use tools such as cross-tenant synchronization, entitlement management, cross-tenant access policies, and Conditional Access together. In both topologies, the target tenant admin has full control over access to resources in the target tenant. They differ in who initiates provisioning and deprovisioning.

### Topology 1

In topology 1, the source tenant configures entitlement management and cross-tenant synchronization to provision users into the target tenant. Then, the administrator of the target tenant configures access packages to provide access to the necessary directory roles, group, and app roles in the target tenant.

[![Diagram that shows topology 1. Cross-tenant synchronization pushes users across tenants and entitlement management gives access to roles.](media/defender-xdr-entra-mto/mto-defender-topology-1.png)](media/defender-xdr-entra-mto/mto-defender-topology-1.png#lightbox)

**Steps to configure topology 1**

1. In the source tenant, configure [cross-tenant synchronization](cross-tenant-synchronization-overview) to provision internal accounts in the source tenant as external accounts in the target tenant.

    As users are assigned to the cross-tenant synchronization service principal, they'll automatically be provisioned into the target tenant. As they're removed from the configuration, they'll automatically be deprovisioned. As part of your attribute mappings, you can add a new mapping of type constant to provision a [directory extension](cross-tenant-synchronization-directory-extensions) attribute on the user to indicate that they're a SOC administrator. Alternatively, if you have an attribute such as department that you can rely on for this step, you can skip creating the extension. This attribute will be used in the target tenant to provide them with access to the necessary roles.
2. In the source tenant, create an access package that includes the cross-tenant synchronization service principal as a resource.

    As users are granted access to the package, they'll be assigned to the cross-tenant synchronization service principal. Ensure that you set up periodic access reviews of the access package or time-limit the assignments to ensure that only the users that need access to the target tenant continue to have access.
3. In the target tenant, [create access packages](../../id-governance/entitlement-management-access-package-create) to provide the necessary roles for investigating an incident.

    We recommend one [autoassigned](../../id-governance/entitlement-management-access-package-auto-assignment-policy) access package to provide the Security Reader role and one request-based package for the Security Operator and Security Administrator roles.

After you've completed the setup, SOC users can navigate to myaccess.microsoft.com to request time-limited access to the necessary access packages in the source tenant. After approval, they'll automatically be provisioned into the target tenants with the Security Reader role. They can then request additional access in any tenants where they need the Security Operator or Security Administrator roles. When their access period is over or they're removed as part of an access review, they'll be deprovisioned from all the target tenants they don't need access to anymore.

### Topology 2

In topology 2 the target tenant administrator defines the access packages and resources that the source users can request access to. If the source tenant administrator would like to restrict which of their users can access the target tenant, you can use a cross-tenant access policy coupled with an access package to block all access to the target tenant, except for users that are part of a group that is included in an access package in the home tenant.

[![Diagram that shows topology 2. Entitlement connected organizations enable users to request access to the target tenant and get provisioned to the necessary roles in the target tenant.](media/defender-xdr-entra-mto/mto-defender-topology-2.png)](media/defender-xdr-entra-mto/mto-defender-topology-2.png#lightbox)

**Steps to configure topology 2**

1. In the target tenant, add the source tenant as a [connected organization](../../id-governance/entitlement-management-organization).

    This setting allows the target tenant administrator to make access packages available to the source tenant.
2. In the target tenant, create an access package that provides the Security Reader, Security Administrator, and Security Operator roles.
3. Users from the source tenant can now request access packages in the target tenant.

After you've completed the setup, SOC users can navigate to myaccess.microsoft.com to request time-limited access to the necessary roles in each tenant.

**Topologies compared**

In both topologies, the target tenant can control what resources users have access to. This can be accomplished using a mix of cross-tenant access policies, Conditional Access, and assignment of apps and roles to users. They differ in who configures and initiates provisioning. In topology 1, the source tenant configures provisioning and pushes users into the target tenants. In topology 2, the target tenant defines which users are eligible to access their tenant.

If a user needs access to several tenants at one time, topology 1 makes it easy for them to request access to an access package in one tenant and automatically get provisioned into several tenants. If the target tenant wants to ensure full control over who is provisioned into their tenant and perform the necessary approvals in their tenant, topology 2 will best meet their needs.

## Deployment considerations

**Monitoring**

Actions performed by a SOC analyst in Microsoft Entra are audited in the Microsoft Entra tenant that they're working in. Organizations can maintain an audit trail of actions performed, generate alerts when specific actions are performed, and analyze actions performed by pushing audit logs into Azure Monitor.

For more information, see [integrate activity logs with Azure Monitor logs](../monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).

Actions performed by a SOC analyst in Microsoft Defender for Cloud are also audited.

For more information, see [audit log activities](/en-us/purview/audit-log-activities).

**Scaling deployment with PowerShell / APIs**

Every step that is configured through the user interface in Microsoft Entra has accompanying Microsoft Graph APIs and PowerShell cmdlets, enabling you to deploy your desired policies and configuration across the tenants in your organization.

| Capability | Microsoft Graph API | PowerShell |
| --- | --- | --- |
| Cross-tenant synchronization | [Link](cross-tenant-synchronization-configure-graph?tabs=ms-graph) | [Link](cross-tenant-synchronization-configure-graph?tabs=ms-powershell) |
| Entitlement management | [Link](/en-us/graph/tutorial-access-package-api) | [Link](/en-us/powershell/microsoftgraph/tutorial-entitlement-management) |
| Cross-tenant access policies | [Link](/en-us/graph/api/resources/crosstenantaccesspolicy-overview) | [Link](/en-us/powershell/module/microsoft.graph.identity.signins/new-mgpolicycrosstenantaccesspolicypartner) |

**Role-based access control**

Configuring the capabilities described in topology 1 and topology 2 require the following roles:

- Configuring cross-tenant access settings - Security Administrator
- Configuring cross-tenant synchronization - Hybrid Identity Administrator
- Configuring entitlement management - Identity Governance Administrator
- [Microsoft Defender](/en-us/microsoft-365/security/defender/m365d-permissions) supports both built-in roles such as Security Reader, Security Administrator, and Security Operator and custom roles.