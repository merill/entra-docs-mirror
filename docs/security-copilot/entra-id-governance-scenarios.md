---
layout: Conceptual
title: Microsoft Security Copilot scenarios in Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-id-governance-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Learn how to use Microsoft Security Copilot with Microsoft Entra ID Governance for identity lifecycle and access management scenarios.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: concept-article
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 13b2f6d4-a851-f565-109e-52dabd9cbb01
document_version_independent_id: 13b2f6d4-a851-f565-109e-52dabd9cbb01
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-id-governance-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-id-governance-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-id-governance-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 31614740-621a-b90a-e4b8-36405de684e1
---

# Microsoft Security Copilot scenarios in Microsoft Entra ID Governance | Microsoft Learn

Identity administrators face increasing pressure to ensure proper access governance while managing complex identity lifecycles at scale. Microsoft Security Copilot transforms how you approach Microsoft Entra ID Governance by enabling natural language queries to quickly analyze access reviews, manage entitlement packages, monitor privileged access, and streamline lifecycle workflows.

In this article, learn about the Security Copilot scenarios available in Microsoft Entra ID Governance to enhance your identity lifecycle and access governance efforts.

## Microsoft Entra ID Governance scenarios supported by Microsoft Security Copilot

Security Copilot is integrated into the Microsoft Entra admin center and works seamlessly with Microsoft Entra ID Governance features. The following list provides an overview of Microsoft Entra ID Governance scenarios supported by Security Copilot:

| Scenario | Role | License | Tenant |
| --- | --- | --- | --- |
| Access reviews | [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator) | [Microsoft Entra ID P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any with access reviews configured |
| Entitlement management | [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator) | [Microsoft Entra ID P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any with entitlement management configured |
| Privileged Identity Management (PIM) | [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)[Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader)[Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader) | [Microsoft Entra ID P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any with PIM configured |
| Privileged Identity Management (PIM) write actions | None | [Microsoft Entra ID P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements), Microsoft Entra ID Governance SKUs, Entra Suite | Any with PIM configured |
| Lifecycle workflows | [Lifecycle Workflows Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator) | Microsoft Entra ID Governance license | Any with lifecycle workflows configured |

### Access reviews

Administrators can easily now extract and analyze access review data in Microsoft Entra ID Governance using Security Copilot. This integration empowers you to quickly explore, track, and gain insights from access reviews at scale—helping you make informed decisions and streamline your access governance processes.

This feature helps administrators;

- Understand who approved access
- Identify reviewers who took no decisions
- Investigate overrides of AI recommendations

Refer to the prompts and examples in [Governance and optimization with Microsoft Security Copilot](entra-governance-optimization) to learn how to use Microsoft Security Copilot with access reviews for the following use-cases;

- [Access review exploration and management](entra-governance-optimization#access-review-exploration-and-management)
- [Access review decision analysis](entra-governance-optimization#access-review-decision-analysis)

For more information about access reviews, see;

- [What are access reviews?](/en-us/entra/id-governance/access-reviews-overview)
- [Prepare for an access review of users' access to an application](/en-us/entra/id-governance/access-reviews-application-preparation)

## Entitlement management

Entitlement management in Microsoft Entra ID enables organizations to manage identity and access lifecycle at scale, by automating workflows, access assignments, reviews, and expirations. Administrators can now interact with entitlement management data using natural language queries to get quick access to information. This includes access packages, policies, connected organizations, catalog resources, and customize curated data only previously available through custom scripting.

Refer to the prompts and examples in [Governance and optimization with Microsoft Security Copilot](entra-governance-optimization) to learn how to use Microsoft Security Copilot with entitlement management for the following use-cases;

- [Catalog and access package management](entra-governance-optimization#catalog-and-access-package-management)
- [User assignments and connected organizations](entra-governance-optimization#user-assignments-and-connected-organizations)

For more information about entitlement management, see [What is entitlement management?](/en-us/entra/id-governance/entitlement-management-overview)

## Privileged Identity Management (PIM)

Using Security Copilot, privileged access can be managed and monitored more efficiently using natural language queries integrated with Microsoft Entra Privileged Identity Management (PIM). This approach provides instant insights into just-in-time role assignments, group memberships, and access to critical resources. AI-powered analysis enables quick identification of eligible or active PIM assignments, tracking of changes, and rapid response to potential risks—streamlining privileged access management and strengthening your security posture.

Refer to the prompts and examples in [Governance and optimization with Microsoft Security Copilot](entra-governance-optimization) to learn how to use Microsoft Security Copilot with PIM for the following use-case;

- [PIM role assignment queries](entra-governance-optimization#pim-role-assignment-queries)

For more information about Privileged Identity Management, see [What is Microsoft Entra Privileged Identity Management?](/en-us/entra/id-governance/privileged-identity-management/pim-configure)

## Privileged Identity Management (PIM) write actions

Users often encounter access denied errors in the Microsoft Entra admin center when attempting actions that require elevated privileges, such as viewing sign-in logs or listing admin role assignments. Identifying the correct role and ensuring it’s the least-privileged option can be complex and time-consuming. This combined with finding the right avenue to get that assignment can be overwhelming.

By using best practices from our least privileged access framework, Microsoft Security Copilot intelligently determines the least privileged role based on the desired task, checks for the eligible assignments, and enables the user through Just-in-Time (JIT) activation using PIM. This provides a seamless experience, reducing the burden for users who had to leave their Copilot chat, navigate to, and activate the role manually, and return to retry the query. This feature keeps everything in one continuous conversation, resulting in reduced friction, improved productivity, and secure access management.

Use the following prompts to get started with PIM write actions;

- *I want to perform {the desired task}, help me activate a role so that I can perform the desired action.*
- *I am done with my investigation or {desired task}, deactivate my access.*
- *I accidentally activated a role, roll back my changes.*

You can use these prompts in any of the following articles to get started with your investigations and then deactivate your access when you are done.

- [Enterprise user management with Microsoft Security Copilot](entra-enterprise-user-management)
- [Identity Governance and optimization with Microsoft Security Copilot](entra-governance-optimization)
- [Investigate security incidents using Microsoft Security Copilot](entra-investigate-incident)
- [Assess application risks using Microsoft Security Copilot in Microsoft Entra](entra-investigate-risky-apps)
- [Manage employee lifecycle using Microsoft Security Copilot](entra-lifecycle-workflows)

## Lifecycle workflows

Microsoft Entra ID Governance applies the capabilities of Security Copilot to save identity administrators time and effort when configuring custom workflows to manage the lifecycle of users across JML scenarios. It also helps you to customize workflows more efficiently using natural language to configure workflow information including custom tasks, execute workflows, and get workflow insights.

Refer to the prompts and examples in [Manage employee lifecycle using Microsoft Security Copilot](entra-lifecycle-workflows) to learn how to use Microsoft Security Copilot with lifecycle workflows for the following use-cases;

- [Create step-by-step guidance for a new lifecycle workflow](entra-lifecycle-workflows#create-step-by-step-guidance-for-a-new-lifecycle-workflow)
- [Explore available workflow configurations](entra-lifecycle-workflows#explore-available-workflow-configurations)
- [Analyze active workflow lists](entra-lifecycle-workflows#analyze-active-workflow-list)
- [Troubleshoot a Lifecycle Workflow run](entra-lifecycle-workflows#troubleshoot-a-lifecycle-workflow-run)
- [Compare versions of a lifecycle workflow](entra-lifecycle-workflows#compare-versions-of-a-lifecycle-workflow)

For more information about lifecycle workflows, see [What are lifecycle workflows?](/en-us/entra/id-governance/what-are-lifecycle-workflows)