---
layout: Conceptual
title: Security and access control with Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-security-access-control
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot in the Microsoft Entra admin center to manage roles, authentication methods, conditional access policies, and assess application risks.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 8c990f2e-4937-00fd-71f2-f8628ba4fdf8
document_version_independent_id: 8c990f2e-4937-00fd-71f2-f8628ba4fdf8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-security-access-control.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-security-access-control
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-security-access-control.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: b1d2fd00-3008-176e-70e9-41c8f80ec8da
---

# Security and access control with Microsoft Security Copilot | Microsoft Learn

Microsoft Security Copilot empowers administrators to implement and manage comprehensive security controls in Microsoft Entra using natural language queries. This capability helps you control access to resources, configure authentication methods, manage privileged roles, and assess application risks to strengthen your organization's security posture.

This article describes how to use Microsoft Security Copilot to undertake a security assessment by evaluating role-based access controls, authentication methods, conditional access policies, and device compliance across an organization. Specifically, for the following use cases in the Microsoft Entra admin center;

- Investigate and manage role assignments
- Configure authentication methods and policies
- Analyze conditional access policies
- Monitor and manage device compliance

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.
- The following roles and licenses are required for different security and access control use cases:

    | Use case | Role | License | Tenant |
    | --- | --- | --- | --- |
    | **Role management** | [Directory Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) or [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader) | Any Microsoft Entra ID license | Any tenant |
    | **Device management** | Available to any user | Free Microsoft Entra ID license | Any tenant |
    | **Authentication management** | [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator) (tenant) or [Privileged Authentication Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-authentication-administrator) (user) | Any Microsoft Entra ID license | Any tenant |
    | **Conditional Access** | [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader), or [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader) | [Microsoft Entra ID P1 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Tenant with CA policies |

## Launch Security Copilot in Microsoft Entra

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate administrative role(s) for your scenario based off the specific use cases.
2. Launch Security Copilot from the **Copilot** button in the Microsoft Entra admin center.

    ![Screenshot that shows Security Copilot in the Microsoft Entra admin center.](media/copilot-security-entra/security-copilot-entra-admin-center.png)
3. Refer to the following use cases and prompts to retrieve information or perform actions using natural language queries.

Note

If an action is blocked by insufficient permissions, a recommended role is displayed. You can use the following prompt in the Security Copilot chat to activate the required role. This is dependent on having an eligible role assignment that provides the necessary access.

- *Activate the {required role} so that I can perform {the desired task}.*

## Investigate and manage role assignments

Begin your assessment by examining role-based access control (RBAC) to ensure that privileged roles are properly assigned and that the principle of least privilege is being followed across your organization's Microsoft Entra setup.

### Role assignment queries

Start by investigating current role assignments to understand who has access to sensitive administrative functions and ensure that privileged access is appropriately controlled. Use the following prompts to get the information you need:

- *What role does user/group/app (name/email/ID) have?*
- *What are the transitive roles user/group/app (name/email/ID) has?*
- *What are the eligible roles user/group/app (name/email/ID) has?*
- *What are the scheduled roles user/group/app (name/email/ID) has?*
- *Who has the Cloud Application Administrator role assigned to them?*
- *Who has eligibility for the Global Reader role?*

### Role information and identification

You can then examine specific roles and their identifiers to understand the scope of permissions and ensure that role assignments align with business requirements and security policies. Use the following prompts to get the information you need:

- *What is the ID of role (role name)*
- *Name of the role with ID 5d6b6bb7-de71-4623-b4af-96380a352509*

## Configure authentication methods and policies

Next, you should assess and manage authentication methods across your Microsoft Entra tenant to ensure strong authentication practices are in place to protect users and resources.

### Authentication method configuration

Next, you can assess the authentication methods to ensure that strong practices are in place and that multifactor authentication (MFA) is properly configured to protect against unauthorized access. Use the following prompts to get the information you need:

- *What authentication methods are enabled in my tenant?*
- *Is Microsoft Authenticator enabled in my tenant? For who?*
- *Is registration campaign enabled in my tenant? For who?*
- *Is system preferred authentication enabled in my tenant? For who?*
- *Is report suspicious activity enabled in my tenant? For who?*

### User authentication status

You can then review individual user authentication configurations and registration status to ensure compliance with security policies and identify any users who may need assistance with their authentication setup. Use the following prompts to get the information you need:

- *What authentication methods does karita@woodgrovebank.com have registered?*
- *Is user karita@woodgrovebank.com enabled for per-user MFA?*
- *How many users have the FIDO2 Security keys method registered?*

## Monitor and manage device compliance

You can continue your assessment by monitoring and investigating device compliance across your organization. Device compliance is crucial for many organizations to ensure that only secure and compliant devices can access sensitive information and corporate resources.

### Device identification and status

By examining device details and compliance status, you can ensure that devices accessing your organization's resources meet security standards and policies. Use the following prompts to get the information you need:

- *Show me the device for with an ID of {ID}*
- *Show me all compliant devices/Show me all non-compliant devices.*
- *List devices that are not under management.*
- *How many devices are there?*

### Device join types and configuration

You can also investigate device join types and configurations to ensure that devices are properly registered and managed within your Microsoft Entra setup. Use the following prompts to get the information you need:

- *List all devices that are Entra ID registered/Entra ID joined/Entra ID hybrid joined.*
- *How many devices exist for each device trust type?*

### Device activity and operating systems

Next, you should look into device activity and operating systems to ensure that devices are actively managed and running supported, secure operating systems. Use the following prompts to get the information you need:

- *Show me when device {ID} was last active.*
- *List the devices with specific {operating system name}.*
- *Show me how many devices are running Windows (8,10,11).*
- *Show the count of Windows devices categorized by release.*

## Analyze Conditional Access policies

Finally, you should evaluate your organization's Conditional Access policies to ensure that proper access controls are in place and that your organization's security requirements are being enforced consistently across all users and devices.

### Policy identification and status

You can examine the current state of Conditional Access policies to understand which policies are active and ensure that critical security controls are properly enforced. Use the following prompts to get the information you need:

- *Authentication strength policies.*
- *Conditional Access policy by name.*
- *Active Multifactor Authentication Conditional Access Policies.*
- *Enforced MFA policies.*
- *Enabled Conditional Access Policies.*
- *CA Policies currently enforced.*
- *Actively enforced CA Policies.*

### Policy configuration and management

Finally, you can investigate specific policy configurations to identify any gaps in coverage and ensure that policies align with your organization's security posture and compliance requirements.

- *Conditional Access Policies to enable.*
- *What CA Policies are not currently enabled?*
- *What policies can I enable?*
- *List inactive Conditional Access Policies/*
- *Conditional Access Policies.*
- *List CA policies.*
- *What CA Policies not applicable to trusted locations?*
- *Conditional Access Policies excluding all trusted locations.*
- *Get all conditional access policies for user considering the groups.*