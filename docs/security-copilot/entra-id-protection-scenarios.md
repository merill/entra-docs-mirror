---
layout: Conceptual
title: Microsoft Security Copilot scenarios in Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-id-protection-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Learn how to use Microsoft Security Copilot with Microsoft Entra ID Protection for identity risk scenarios.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: concept-article
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: c821a345-d0d9-1f83-dad6-3a4f16d25c09
document_version_independent_id: c821a345-d0d9-1f83-dad6-3a4f16d25c09
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-id-protection-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-id-protection-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-id-protection-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: d3b9e489-27ea-18f1-0165-aa39e0273505
---

# Microsoft Security Copilot scenarios in Microsoft Entra ID Protection | Microsoft Learn

Microsoft Security Copilot enhances Microsoft Entra ID Protection capabilities by providing AI-powered insights for identity risk investigation and remediation. This article describes how to use Microsoft Security Copilot with Microsoft Entra ID Protection to streamline identity risk management and improve your organization's security posture. Using this feature requires a tenant with Microsoft Security Copilot enabled.

## Microsoft Entra ID Protection scenarios supported by Microsoft Security Copilot

Security Copilot is integrated into the Microsoft Entra admin center and works seamlessly with Microsoft Entra ID Protection features. The following list provides an overview of the scenarios supported by Security Copilot:

| Scenario | Role(s) | License | Tenant |
| --- | --- | --- | --- |
| Risky users | [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator) | [Microsoft Entra ID P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any |
| Application risk | [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)[Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) | Workload Identity Premium or [Microsoft Entra ID P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any with Risky Service Principal prompts |

### Risky users

Microsoft Entra ID Protection applies the capabilities of Security Copilot to [summarize a user's risk level](entra-risky-user-summarization), provide insights relevant to the incident at hand, and provide recommendations for rapid mitigation. Identity risk investigation is a crucial step to defend an organization. Security Copilot helps reduce the time to resolution by providing IT admins and security operations center (SOC) analysts the right context to investigate and remediate identity risk and identity-based incidents. Risky user summarization provides admins and responders quick access to the most critical information in context to aid their investigation.

You can add your own prompts in the Copilot window for the following use cases;

- [List or Identify Users Based on Risk](entra-risky-user-summarization#list-or-identify-users-based-on-risk)
- [User-Specific Risk Information](entra-risky-user-summarization#user-specific-risk-information)
- [User Risk History](entra-risky-user-summarization#user-risk-history)

![Screenshot that shows the ID Protection risky user summarization details.](media/copilot-entra-risky-user-summarization/risky-user-details.png)

### Application risk

Identity administrators and security analysts can use Microsoft Security Copilot to quickly assess the risk level of applications from workload identities. By using natural language queries, you can easily discover the granted permissions, unused apps in your tenant, and the risk level of applications. This allows admins to take appropriate actions to mitigate risks and ensure the security of your organization's applications.

Refer to the prompts and examples in [Assess application risks using Microsoft Security Copilot in Microsoft Entra](entra-investigate-risky-apps) to learn how to use Microsoft Security Copilot to assess application risk for the following use-cases;

- [Explore Microsoft Entra risky service principals](entra-investigate-risky-apps#explore-microsoft-entra-risky-service-principals)
- [Explore Microsoft Entra service principals](entra-investigate-risky-apps#explore-microsoft-entra-service-principals)
- [Explore Microsoft Entra applications](entra-investigate-risky-apps#explore-microsoft-entra-applications)
- [View the permissions granted on a Microsoft Entra service principal](entra-investigate-risky-apps#explore-microsoft-entra-risky-service-principals)
- [Explore unused Microsoft Entra applications](entra-investigate-risky-apps#explore-unused-microsoft-entra-applications)
- [Explore Microsoft Entra Applications outside my tenant](entra-investigate-risky-apps#explore-microsoft-entra-applications-outside-my-tenant)