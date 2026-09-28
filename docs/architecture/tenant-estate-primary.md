---
layout: Conceptual
title: Microsoft Entra primary production tenant guidance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/tenant-estate-primary
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: bathawes
ms.author: beathawe
ms.service: entra
manager: martinco
description: Learn about Microsoft Entra tenant architecture for primary production tenants so that you can identify your needs and compare architectural options.
ms.reviewer: ramical
ms.subservice: architecture
ms.topic: concept-article
ms.date: 2026-06-22T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f2bada35-4b23-bb36-06ad-160270cc9b3c
document_version_independent_id: f2bada35-4b23-bb36-06ad-160270cc9b3c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/tenant-estate-primary.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/tenant-estate-primary
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/tenant-estate-primary.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cd620a06-97e7-45ee-6bf7-2a94fd1521c6
---

# Microsoft Entra primary production tenant guidance - Microsoft Entra | Microsoft Learn

Designing your Microsoft Entra **tenant estate** — the set of tenants your organization operates — means balancing security, compliance, administrative complexity, and user experience. While a single production tenant is ideal for simplicity and user experience, your specific business and technical requirements might necessitate multiple production tenants.

This article series describes the following common tenant architecture patterns that Microsoft has observed across real-world deployments.

- [Microsoft Entra tenant estate guidance introduction](tenant-estate-guide)
- [Collaborating production tenants](tenant-estate-collaborating)
- [Nonproduction environments](tenant-estate-nonproduction)
- [Isolated tenants for critical production systems](tenant-estate-critical-production)
- [Isolated tenants for business partner access](tenant-estate-business-partner)
- [Hybrid identity and isolation](tenant-estate-hybrid-identity)

Primary production tenants host workforce identities and production workloads, and optionally external collaboration. Most organizations begin with a single such tenant. Requirements can grow from there — a large organization might operate multiple production tenants, along with numerous tenants aligned to one or more of the patterns listed above. Working within a single tenant provides the most seamless collaboration experience and the highest level of functionality across Microsoft services.

This article is the baseline for the [Microsoft Entra tenant estate guidance](tenant-estate-guide) series: it covers the seven [architecture evaluation areas](tenant-estate-guide#tenant-architecture-evaluation-areas) in detail. Each other pattern article describes only the incremental differences for its role, in the context of those same evaluation areas. If you plan to host workloads, identities, or external collaboration in a separate tenant, see the corresponding pattern article.

For the tradeoffs that determine whether to keep a workload here versus splitting it into another tenant, see [When to integrate an app or workload with an existing tenant](tenant-estate-guide#when-to-integrate-an-app-or-workload-with-an-existing-tenant).

## Example scenario

Contoso operates a single primary production tenant for their workforce. This tenant hosts their workforce identities, production applications and resources, and the external guests and business partners they invite through B2B collaboration. Contoso meets its security, compliance, and operational requirements within this one tenant, which keeps administration simple and the collaboration experience seamless. The following example scenario diagram shows Contoso's primary production tenant architecture.

![Example scenario diagram shows single production tenant architecture.](media/multi-tenant-architecture-guide/single-production-tenant.png)

## Administration

Tenant-wide privileged roles include *Global Administrator* and *Privileged Role Administrator*. You can use the following capabilities to implement administration delegation. These capabilities apply to specific scenarios in specific workloads.

- **[Microsoft Entra built-in roles](../identity/role-based-access-control/permissions-reference)** grant a narrower set of permissions required for a user to perform their assigned tasks. For example, the Exchange Administrator role can only manage all aspects of Exchange Online.
- **[Microsoft Entra custom roles](../identity/role-based-access-control/custom-overview)** allow you to create specific permissions and assign them at the single application scope as a limited owner or at the directory scope (all applications) as a limited administrator.
- **[Azure role-based access control](/en-us/azure/role-based-access-control/overview)** (RBAC) provides a hierarchical scope to configure Azure resources with management groups, subscriptions, resource groups, and resource-level administration delegation.
- **[Service-specific roles](../identity/role-based-access-control/m365-workload-docs)** provide roles specific to Microsoft services such as SharePoint, Intune, and Purview.
- **[Administrative units](../identity/role-based-access-control/administrative-units)** restrict permissions to specific Microsoft Entra roles to portions of your organization that you define. For example, you can use administrative units to delegate the [Helpdesk Administrator](../identity/role-based-access-control/permissions-reference#helpdesk-administrator) role to regional support specialists so that they can manage users only in the region that they support.
- **[Restricted management administrative units](../identity/role-based-access-control/admin-units-restricted-management)** allow you to protect specific objects such as executive user accounts or sensitive groups in your tenant from modification by anyone other than a specific set of people that you designate. This approach allows you to meet security or compliance requirements without needing to remove tenant-level role assignments from your administrators.
- **Delegate ownership** of Microsoft Entra objects such as applications and groups and Microsoft 365 data such as SharePoint Site Collections and Microsoft Teams.

In addition to delegating administration controls, carefully govern privileged roles because misuse or compromise of these roles can have organization‑wide impact. [Microsoft Entra Privileged Identity Management](../id-governance/privileged-identity-management/pim-configure) (PIM) helps reduce this risk by limiting standing administrative access and introducing governance over high‑impact operations that you can't isolate to smaller scopes. When you require explicit, time‑bound activation of privileged roles, PIM supports least‑privilege principles in environments where administrative actions inherently apply across the tenant.

[Configuration management](../id-governance/tenant-governance/configuration-management) in Microsoft Entra Tenant Governance allows you to define configuration baselines, monitor tenants for drift, and generate snapshots of current settings. These definitions can apply across workloads such as Microsoft Entra, Exchange Online, Intune, Defender, Purview, and Teams. You can express your desired state of tenant resources, continuously monitor security configurations against that baseline, and document the current state. This approach helps you to satisfy audit and recoverability requirements.

## Change control

Change control in production tenants is high stakes, particularly because some settings are tenant-wide and can't be piloted through gradual rollout mechanisms such as security groups. Applied directly in the primary production tenant, these changes can require a carefully planned "big bang" rollout. This amplified risk demands thorough testing, rollback planning, and clear communication. Examples include cross-tenant access settings, tenant restrictions, network locations, and branding changes. In Exchange Online, global settings apply instantly across all mailboxes. Settings include accepted domains, remote domains, disabling POP/IMAP or basic auth, external email tagging, and organization-wide transport rules. For Intune, tenant-wide configurations such as compliance policy defaults, device cleanup rules, and enrollment restrictions affect all enrolled devices at once. These controls lack scoping mechanisms for gradual rollout. Therefore, validate dependencies, document pre-change configuration state, and prepare rollback strategies before implementation. Align stakeholders across your entire organization. To validate tenant-wide changes before applying them in production, organizations can use a separate [Non-production tenant](tenant-estate-nonproduction). Differences in data and scale mean this reduces, but doesn't fully remove, the need for careful production rollout.

Some organizations opt to host and test nonproduction or prerelease applications within the primary production tenant. This can enable business users to validate application behavior or user experience changes against real production data and workflows. While this approach can simplify testing and reduce duplication of environments, it introduces other change‑control and risk considerations. It can be well suited to applications that request minimal Microsoft Graph permissions. For applications that request high‑impact permissions (such as directory‑wide read or write access), consider testing in an isolated [nonproduction tenant](tenant-estate-nonproduction) where possible.

## Account lifecycle

Microsoft Entra [provisions workforce user identities from HR systems](../identity/app-provisioning/what-is-hr-driven-provisioning) and [provisions to applications](../identity/app-provisioning/toc.json) such as software-as-a-service (SaaS) applications based on access assignment. [Lifecycle workflows](../id-governance/what-are-lifecycle-workflows) automate identity management across the joiner, mover, and leaver phases of a user's lifecycle.

You can onboard external users to the tenant when they accept Business-to-Business (B2B) collaboration invitations from a tenant user. To onboard external users, you can use [entitlement management](../id-governance/entitlement-management-overview) access packages with built-in controls such as approval workflows. You can automatically remove external user accounts that you onboard with entitlement management from the directory after they lose access to packages. To secure and govern external access, review [Plan a Microsoft Entra B2B collaboration deployment](https://docs.azure.cn/entra/architecture/secure-external-access-resources) and [Govern access for external users in entitlement management](../id-governance/entitlement-management-external-users).

## Credential management

Manage authentication methods available to workforce users through tenant-wide policies in Microsoft Entra. Adopt [phishing-resistant passwordless authentication](../identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication) such as Windows Hello for Business, Authenticator App passkeys, FIDO2 security keys, or certificate-based authentication.

Enforce multifactor authentication for external users. [Authentication and Conditional Access for B2B users](../external-id/authentication-conditional-access) describes how to create Conditional Access policies that target guests. [Cross-tenant access settings](../external-id/cross-tenant-access-settings-b2b-collaboration) allow you to trust multifactor authentication (MFA) method claims from specific business partner organizations. Otherwise, enforce these user accounts to register for other MFA methods in Microsoft Entra ID.

## Collaboration

Workforce users get the most streamlined Microsoft 365 collaboration experience with one another when they're homed in the same tenant. When you also host external users in that tenant, they join as guests in the same directory. When administrators enable Microsoft cloud services such as Microsoft Teams and Power BI for external users, workforce and external users can be added to the same teams, shared channels, SharePoint sites, and applications, and can collaborate with each other ad-hoc without switching tenants.

## Role-based resource assignment

Grant access to users with entitlement management access packages that have built-in controls. Controls include time-limited application role assignment, separation of duties, and ability to scope to specific organizations for external collaboration.

## Risk management

### Blast radius

Compromise of a high-privileged user or application or a misconfigured tenant-level policy can affect every user, resource, or application tied to that tenant. Even non-privileged users or applications, when compromised, can have a wide impact if broad access permissions exist (for example, SharePoint sites with *Everyone access* settings).

Microsoft Cloud Security solutions provide a broad set of technical controls to help mitigate this risk within a single tenant by following [Zero Trust](/en-us/security/zero-trust/) principles to protect endpoints, data, applications, infrastructure, networks, and security operations. Specific recommendations include the following.

- Implement all controls in the [Configure Microsoft Entra for increased security](../fundamentals/configure-security) article.
- Use the controls in the [Secure resource isolation in a single tenant in Microsoft Entra ID](secure-single-tenant) article.
- Implement policies to protect, detect, and respond with [Microsoft Defender](/en-us/defender/).
- Address oversharing with [Microsoft Purview Information Protection](/en-us/purview/information-protection).
- Implement data security and governance controls such as [Microsoft Purview Insider Risk Management](/en-us/purview/insider-risk-management) and data classification. This mitigation is especially critical when external users have access to the tenant.

### Regulatory requirements

Microsoft Entra provides technical controls to help customers meet regulatory requirements within a single tenant. A common consideration across regulations is data residency at rest. Microsoft Entra determines [directory data residency](../fundamentals/data-residency) at tenant creation. [Microsoft 365 Multi-Geo](/en-us/microsoft-365/enterprise/microsoft-365-multi-geo) enables management and storage of in-scope data at a user level for core services such as Exchange Online, SharePoint/OneDrive, Microsoft Teams, and Microsoft Copilot.

Regulations often call out Identity and Access Management (IAM) controls such as authentication methods, access lifecycle management, and reporting. [Implement identity standards with Microsoft Entra ID](../standards/) provides detailed guidance on specific standards.