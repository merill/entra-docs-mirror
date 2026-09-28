---
layout: Conceptual
title: Microsoft Security Copilot scenarios in Microsoft Entra overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-security-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Learn about the Microsoft Security Copilot scenarios across Microsoft Entra products and services.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: concept-article
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: fd0030a5-c652-2949-ed67-829c7d2964d9
document_version_independent_id: fd0030a5-c652-2949-ed67-829c7d2964d9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-security-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-security-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-security-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 022b9557-a9a9-27f9-f0d3-862ecf395084
---

# Microsoft Security Copilot scenarios in Microsoft Entra overview | Microsoft Learn

Microsoft Security Copilot is a powerful tool that can help you manage and secure your Microsoft Entra identity environment. This article outlines the different capabilities in Microsoft Entra that you can investigate using natural language queries. These capabilities are available across different Microsoft Entra products to enhance your identity protection efforts. To use Security Copilot in Microsoft Entra, ensure that you have a tenant with Security Copilot enabled.

## Microsoft Security Copilot integration with Microsoft Entra

Security Copilot is a part of the Microsoft Entra admin center, and you can use it to create your own prompts. Security Copilot is launched from a globally available button in the menu bar. Choose from a set of starter prompts that appear at the top of the Security Copilot window or enter your own in the prompt bar to get started. Suggested prompts can appear after a response, which are predefined prompts that Security Copilot selects based on the prior response.

![Screenshot that shows Security Copilot in the Microsoft Entra admin center.](media/copilot-security-entra/security-copilot-entra-admin-center.png)

### Data exploration using Microsoft Security Copilot (preview)

Microsoft Security Copilot supports data exploration when prompts return datasets with more than 10 items. This feature is in preview and available for select Microsoft Entra scenarios. From the Copilot chat response, select **Open list** to access a comprehensive data grid. This allows you to explore large datasets with complete and accurate results, enabling more efficient decision-making. Each data grid displays the underlying Microsoft Graph URL, helping you verify query accuracy and build confidence in the results.

Note

This functionality is currently in preview and limited to simple, single-step prompts (for example *"Provide a list of users in the Sales department"*). Tasks that require multi-step prompting and cross scenario functionality (for example *"Which risky apps have high privileged permissions?"*) are not currently supported by this feature. Copilot will still provide chat-based summaries for all prompts.

[![Screenshot that shows Data Exploration in Security Copilot for Microsoft Entra.](media/copilot-security-entra/data-explorer.png)](media/copilot-security-entra/data-explorer.png#lightbox)

## Security Copilot scenarios in Microsoft Entra

There's a large selection of Security Copilot scenarios available in Microsoft Entra. Use the following table to learn more about each scenario by product area, their use cases, license and role requirements.

| Microsoft Entra product | Security Copilot scenarios | Data Exploration Enabled |
| --- | --- | --- |
| **Microsoft Entra ID** | [Tenants](entra-id-scenarios#tenants)[Users](entra-id-scenarios#users)[Groups](entra-id-scenarios#groups)[Domains](entra-id-scenarios#domains)[Licenses](entra-id-scenarios#licenses)[Sign-in logs](entra-id-scenarios#sign-in-logs)[Audit logs](entra-id-scenarios#audit-logs)[Provisioning logs](entra-id-scenarios#provisioning-logs)[Recommendations](entra-id-scenarios#recommendations)[Health monitoring alerts](entra-id-scenarios#health-monitoring-alerts)[Service Level Agreement](entra-id-scenarios#service-level-agreement)[Roles and administrators](entra-id-scenarios#roles-and-administrators)[Devices](entra-id-scenarios#devices)[Conditional Access](entra-id-scenarios#conditional-access)[Authentication](entra-id-scenarios#authentication) | ![Tenants data exploration enabled](../media/common/applies-to-yes.png)![Users data exploration enabled](../media/common/applies-to-yes.png)![Groups data exploration enabled](../media/common/applies-to-yes.png)![Domains data exploration enabled](../media/common/applies-to-yes.png)![Licenses data exploration enabled](../media/common/applies-to-no.png)![Sign in logs data exploration enabled](../media/common/applies-to-yes.png)![Audit logs data exploration enabled](../media/common/applies-to-yes.png)![Provisioning logs data exploration enabled](../media/common/applies-to-no.png)![Recommendations data exploration enabled](../media/common/applies-to-yes.png)![Health monitoring alerts data exploration enabled](../media/common/applies-to-yes.png)![Service Level Agreement data exploration enabled](../media/common/applies-to-yes.png)![Role and administrators data exploration enabled](../media/common/applies-to-yes.png)![Devices data exploration enabled](../media/common/applies-to-yes.png)![Conditional access data exploration enabled](../media/common/applies-to-yes.png)![Authentication data exploration enabled](../media/common/applies-to-yes.png) |
| **Microsoft Entra ID Protection** | [Risky users](entra-id-protection-scenarios#risky-users)[Application risk](entra-id-protection-scenarios#application-risk) | ![Risky users data exploration enabled](../media/common/applies-to-yes.png)![Application risk data exploration enabled](../media/common/applies-to-yes.png) |
| **Microsoft Entra ID Governance** | [Access reviews](entra-id-governance-scenarios#access-reviews)[Entitlement management](entra-id-governance-scenarios#entitlement-management)[Privileged Identity Management (PIM)](entra-id-governance-scenarios#privileged-identity-management-pim)[PIM write actions](entra-id-governance-scenarios#privileged-identity-management-pim-write-actions)[Lifecycle workflows](entra-id-governance-scenarios#lifecycle-workflows) | ![Access reviews data exploration enabled](../media/common/applies-to-yes.png)![Entitlement management data exploration enabled](../media/common/applies-to-yes.png)![Privileged Identity Management (PIM) data exploration enabled](../media/common/applies-to-yes.png)![Privileged Identity Management (PIM) write actions data exploration enabled](../media/common/applies-to-no.png)![Lifecycle workflows data exploration enabled](../media/common/applies-to-yes.png) |
| **Microsoft Entra Internet Access** **Microsoft Entra Private Access** | [Global Secure Access](entra-internet-access-private-access-scenarios#global-secure-access) | ![Global Secure Access data exploration enabled](../media/common/applies-to-yes.png) |

## Microsoft Entra ID scenarios

Microsoft Entra ID is the foundational production of Microsoft Entra, and provides the essential identity, authentication, policy, and protection to secure users, devices, apps, and resources. Security Copilot enhances these capabilities across multiple areas:

- **Enterprise user management**: Quickly retrieve user, group, domain and license information
- **Authentication**: Discover enabled authentication methods, registration status, and overall authentication strategy
- **Role based access control (RBAC)**: Investigate role assignments within a directory
- **Conditional Access**: Understand and evaluate conditional access policies
- **Device identity**: Explore device details and compliance status

## Microsoft Entra ID Protection scenarios

Microsoft Entra ID Protection focuses on identity risk detection and remediation. Security Copilot provides AI-powered insights for:

- **Risky user investigation**: Summarize user risk levels and provide remediation recommendations
- **Application risk assessment**: Analyze workload identities and application permissions

## Microsoft Entra ID Governance scenarios

Microsoft Entra ID Governance helps you manage identity lifecycle and access governance at scale. Security Copilot enhances these capabilities for:

- **Access reviews**: Analyze access review data and decision patterns
- **Entitlement management**: Manage access packages and connected organizations
- **Privileged Identity Management**: Monitor privileged access and role assignments
- **Lifecycle workflows**: Configure and troubleshoot employee lifecycle automation