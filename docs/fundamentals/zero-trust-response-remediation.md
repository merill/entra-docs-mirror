---
layout: Conceptual
title: Security guidance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/zero-trust-response-remediation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Improve your security posture with the Microsoft Entra Zero Trust assessment to accelerate response and remediation.
ms.topic: concept-article
ms.date: 2025-09-12T00:00:00.0000000Z
ms.reviewer: ramical
locale: en-us
document_id: 58e13b1e-cf6e-033c-00a9-873f87a90a28
document_version_independent_id: 58e13b1e-cf6e-033c-00a9-873f87a90a28
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/zero-trust-response-remediation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/zero-trust-response-remediation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/zero-trust-response-remediation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 83220eb3-d2a5-9335-bf70-f043c5ffe721
---

# Security guidance - Microsoft Entra | Microsoft Learn

The ability to rapidly detect, respond to, and remediate security threats is critical in today's evolving threat landscape. As one of the pillars of the [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars), accelerating response and remediation encourages organizations to minimize the time between threat detection and containment.

This pillar emphasizes automated, risk-based responses that reduce manual intervention and help prevent security incidents from escalating. The following Microsoft Entra Zero Trust assessment checks ensure your organization has the necessary controls in place to quickly identify and mitigate high-risk scenarios, protecting both user identities and workload identities through proactive security policies.

## Zero Trust security recommendations

### Workload Identities are configured with risk-based policies

Set up risk-based Conditional Access policies for workload identities based on risk policy in Microsoft Entra ID to make sure only trusted and verified workloads use sensitive resources. Without these policies, threat actors can compromise workload identities with minimal detection and perform further attacks. Without conditional controls to detect anomalous activity and other risks, there's no check against malicious operations like token forgery, access to sensitive resources, and disruption of workloads. The lack of automated containment mechanisms increases dwell time and affects the confidentiality, integrity, and availability of critical services.

**Remediation action** Create a risk-based Conditional Access policy for workload identities.

- [Create a risk-based Conditional Access policy](/en-us/entra/identity/conditional-access/workload-identity#create-a-risk-based-conditional-access-policy)

### Restrict high risk sign-ins

When high-risk sign-ins are not properly restricted through Conditional Access policies, organizations expose themselves to security vulnerabilities. Threat actors can exploit these gaps for initial access through compromised credentials, credential stuffing attacks, or anomalous sign-in patterns that Microsoft Entra ID Protection identifies as risky behaviors. Without appropriate restrictions, threat actors who successfully authenticate during high-risk scenarios can perform privilege escalation by misusing the authenticated session to access sensitive resources, modify security configurations, or conduct reconnaissance activities within the environment. Once threat actors establish access through uncontrolled high-risk sign-ins, they can achieve persistence by creating additional accounts, installing backdoors, or modifying authentication policies to maintain long-term access to the organization's resources. The unrestricted access enables threat actors to conduct lateral movement across systems and applications using the authenticated session, potentially accessing sensitive data stores, administrative interfaces, or critical business applications. Finally, threat actors achieve impact through data exfiltration, or compromise business-critical systems while maintaining plausible deniability by exploiting the fact that their risky authentication was not properly challenged or blocked.

**Remediation action**

- [Deploy a Conditional Access policy to require MFA for elevated sign-in risk](/en-us/entra/identity/conditional-access/policy-risk-based-sign-in)

### Restrict access to high risk users

Assume high risk users are compromised by threat actors. Without investigation and remediation, threat actors can execute scripts, deploy malicious applications, or manipulate API calls to establish persistence, based on the potentially compromised user's permissions. Threat actors can then exploit misconfigurations or abuse OAuth tokens to move laterally across workloads like documents, SaaS applications, or Azure resources. Threat actors can gain access to sensitive files, customer records, or proprietary code and exfiltrate it to external repositories while maintaining stealth through legitimate cloud services. Finally, threat actors might disrupt operations by modifying configurations, encrypting data for ransom, or using the stolen information for further attacks, resulting in financial, reputational, and regulatory consequences.

Organizations using passwords can rely on password reset to automatically remediate risky users.

Organizations using passwordless credentials already mitigate most risk events that accrue to user risk levels, thus the volume of risky users should be considerably lower. Risky users in an organization that uses passwordless credentials must be blocked from access until the user risk is investigated and remediated.

**Remediation action**

- [Deploy a Conditional Access policy to require a secure password change for elevated user risk](/en-us/entra/identity/conditional-access/policy-risk-based-user).
- Use Microsoft Entra ID Protection to [investigate risk further](/en-us/entra/id-protection/howto-identity-protection-investigate-risk).