---
layout: Conceptual
title: Microsoft Global Secure Access built-in roles - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-role-based-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about the built-in administrator roles you can assign to manage Global Secure Access permissions.
ms.topic: reference
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 43024a0e-0c44-e5a6-b8b9-8680ab649563
document_version_independent_id: 43024a0e-0c44-e5a6-b8b9-8680ab649563
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-role-based-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-role-based-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-role-based-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: a690bc3d-7eee-6eab-9ce3-52806c703953
---

# Microsoft Global Secure Access built-in roles - Global Secure Access | Microsoft Learn

## Overview

Global Secure Access uses Role-Based Access Control (RBAC) to effectively manage administrative access. By default, Microsoft Entra ID requires specific administrator roles for accessing Global Secure Access.

This article details the built-in Microsoft Entra roles you can assign for managing Global Secure Access.

Important

It's highly recommended to use the least privileged role required to administer the service. For more information about least privileged, see [Least privileged roles by task in Microsoft Entra ID](../identity/role-based-access-control/delegate-by-task). For more information about least privilege in Microsoft Entra ID Governance, see [The principle of least privilege with Microsoft Entra ID Governance](../id-governance/scenarios/least-privileged).

### Security Administrator

**Limited access**: This role grants permissions to perform specific tasks, such as configuring remote networks, setting up security profiles, managing traffic forwarding profiles, and viewing traffic logs and alerts. However, security admins can't configure Private Access.

### Global Secure Access Administrator

**Limited access**: This role grants permissions to perform specific tasks, such as configuring remote networks, setting up security profiles, managing traffic forwarding profiles, and viewing traffic logs and alerts. However, Global Secure Access admins can't configure Private Access, create or manage Conditional Access policies, or manage user and group assignments.

Note

To perform additional Microsoft Entra tasks, such as editing Conditional Access policies, you need to be both a Global Secure Access Administrator and have at least one other administrator role assigned to you. Consult the Role-based permissions table above.

### Conditional Access Administrator

**Conditional Access management**: This role can create and manage Conditional Access policies for Global Secure Access, such as managing all compliant network locations and utilizing Global Secure Access security profiles.

### Application Administrator

**Private Access configuration**: This role can configure Private Access, including Quick Access, private network connectors, application segments, and enterprise applications.

### Global Secure Access Log Reader

**Read-only access**: This role is primarily intended for security and network personnel who need read-only visibility into traffic logs and related insights to effectively monitor and analyze network activity without the ability to make changes to the environment. Users with this role can view detailed Global Secure Access traffic logs, including session, connection, and transaction data, as well as access and review alerts and reports in the Global Secure Access area of the Microsoft Entra admin center.

### Security Reader and Global Reader

**Read-only access**: These roles have full read-only access to all aspects of Global Secure Access, except traffic logs. They can't change any settings or perform any actions.

## Role-based permissions

The following Microsoft Entra ID admin roles have access to Global Secure Access:

| Permissions | Global Admin | Security Admin | Global Secure Access Admin | CA Admin | Apps Admin | Global Reader | Security Reader | Global Secure Access Log Reader |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Configure Private Access (Quick Access, private network connectors, application segments, and enterprise apps) | ✅ |  |  |  | ✅ |  |  |  |
| Create and interact with Conditional Access policies | ✅ | ✅ |  | ✅ |  |  |  |  |
| Manage traffic forwarding profiles | ✅ | ✅ | ✅ |  |  |  |  |  |
| User and group assignments | ✅ |  |  |  | ✅ |  |  |  |
| Configure remote networks | ✅ | ✅ | ✅ |  |  |  |  |  |
| Security profiles | ✅ | ✅ | ✅ |  |  |  |  |  |
| View traffic logs and alerts | ✅ | ✅ | ✅ |  |  |  |  | ✅ |
| View all other logs and dashboards | ✅ | ✅ | ✅ |  |  | ✅ | ✅ | ✅ |
| Configure universal tenant restrictions and Global Secure Access signaling for Conditional Access | ✅ | ✅ | ✅ |  |  |  |  |  |
| Read-only access to product settings | ✅ | ✅ | ✅ |  |  | ✅ | ✅ | ✅ |