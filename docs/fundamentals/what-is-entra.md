---
layout: Conceptual
title: What is Microsoft Entra? - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/what-is-entra
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Introduction to the Microsoft Entra product family including links to get started.
ai-usage: ai-assisted
ms.topic: overview
ms.date: 2026-06-18T00:00:00.0000000Z
locale: en-us
document_id: 8637c6b4-c7b7-1a50-cbc4-011f867e9208
document_version_independent_id: 3f9a020a-6aef-2100-19c7-d2ba59756469
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/what-is-entra.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/what-is-entra
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/what-is-entra.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4ad4fa29-faac-20d3-656e-60a07d9e41f4
---

# What is Microsoft Entra? - Microsoft Entra | Microsoft Learn

Microsoft Entra is a family of identity and network access products that helps organizations implement a [Zero Trust](/en-us/security/zero-trust/zero-trust-overview) security strategy. Use Microsoft Entra to verify identities, validate access conditions, check permissions, encrypt connection channels, and monitor for compromise across your environment. Microsoft Entra also integrates with [Security Copilot](../security-copilot/security-copilot-in-entra) to help investigate identity risks and troubleshoot access issues using AI.

## Microsoft Entra product family

The Microsoft Entra product family spans identity, access, governance, and security. It covers secure end-to-end access for employees, customers, partners, workloads, and AI agents across any cloud environment.

### Establish Zero Trust access controls

#### Microsoft Entra ID

[Microsoft Entra ID](what-is-entra) is the foundational product of Microsoft Entra. It's a cloud-based identity and access management service that provides authentication, policy enforcement, and protection for users, devices, apps, and resources. Every new Microsoft Entra directory includes an initial domain name, like `contoso.onmicrosoft.com`. You can also add your organization's custom domain names.

If you're a **Microsoft 365, Azure, or Dynamics CRM Online subscriber**, you're already using Microsoft Entra ID — every tenant is automatically a Microsoft Entra tenant. You can start managing access to your integrated cloud apps right away.

#### Microsoft Entra Domain Services

[Microsoft Entra Domain Services](../identity/domain-services/overview) provides managed domain services like group policy, LDAP, and Kerberos/NTLM authentication. It's designed for legacy applications in the cloud that can't use modern authentication methods.

> 
> **Scenario:** An organization with services that need Kerberos authentication can create a managed domain where Microsoft deploys and maintains the core service components.

### Secure access for employees

#### Microsoft Entra Private Access

[Microsoft Entra Private Access](../global-secure-access/overview-what-is-global-secure-access#microsoft-entra-private-access) secures access to all private apps and resources, including corporate networks and multicloud environments. Remote users can connect to internal resources from any device and network without a VPN.

**For example**, an employee can securely access a corporate network printer while working from home or a cafe.

#### Microsoft Entra Internet Access

[Microsoft Entra Internet Access](../global-secure-access/overview-what-is-global-secure-access#microsoft-entra-internet-access) secures access to all internet resources, including SaaS apps and Microsoft 365 apps and resources.

> 
> **Scenario:** Enable web content filtering to regulate access to websites based on content categories and domain names.

#### Microsoft Entra ID Governance

[Microsoft Entra ID Governance](../id-governance/identity-governance-overview) simplifies identity and permissions management by automating access requests, assignments, and reviews. It also helps protect critical assets through identity lifecycle management.

**For example**, administrators can automatically assign user accounts, groups, and licenses to new employees and remove those assignments when employees leave the company.

#### Microsoft Entra ID Protection

[Microsoft Entra ID Protection](../id-protection/overview-identity-protection) detects and reports identity-based risks. Administrators can investigate and automatically remediate risks using tools like [risk-based Conditional Access policies](../id-protection/concept-identity-protection-policies).

> 
> **Scenario:** Create risk-based Conditional Access policies that require multifactor authentication when the sign-in risk level is medium or high.

#### Microsoft Entra Verified ID

[Microsoft Entra Verified ID](../verified-id/decentralized-identifier-overview) is a credential verification service based on open [decentralized identity (DID) standards](../verified-id/verifiable-credentials-standards). Organizations can issue verifiable credentials — digital signatures that prove the validity of information — to users, who store the credentials on their personal devices and present them when needed.

**For example**, a recent college graduate can ask the university to issue a digital diploma to their DID, then present it to a potential employer who can independently verify the issuer, issuance time, and status.

### Secure access for customers and partners

#### Microsoft Entra External ID

[Microsoft Entra External ID](../external-id/external-identities-overview) lets external identities safely access business resources and consumer apps. It provides secure methods for collaborating with business partners and guests on internal apps, and for managing customer identity and access management (CIAM) in consumer-facing applications.

> 
> **Scenario:** Set up self-service registration for customers to sign in to a web application using one-time passcodes or social accounts from Google or Facebook.

### Secure access in any cloud

#### Microsoft Entra Workload ID

[Microsoft Entra Workload ID](../workload-id/workload-identities-overview) is the identity and access management solution for workload identities — applications, services, and containers that require authentication and authorization policies. It lets organizations secure access to resources using adaptive policies and custom security attributes.

**For example**, GitHub Actions needs a workload identity to access Azure subscriptions to automate, customize, and execute software development workflows.

### Secure access for AI agents

#### Microsoft Entra Agent ID

[Microsoft Entra Agent ID](../agent-id/what-is-microsoft-entra-agent-id) is an identity and security framework that extends Microsoft Entra capabilities to AI agents. As organizations deploy assistive, autonomous, and user-like agents, Entra Agent ID provides purpose-built identity constructs to authenticate, authorize, govern, and protect these nonhuman identities at enterprise scale.

> 
> **Scenario:** An organization deploys AI agents that access corporate data on behalf of users. Entra Agent ID provides each agent with a governed identity, enforces least-privilege access, and maintains an audit trail of the agent's actions.

## Prepare your environment

Before deploying Microsoft Entra, configure your infrastructure and processes according to security best practices and standards. The following articles provide architectural, deployment, and operational guidance:

- [Architecture](../architecture/architecture)
- [Deployment plans](../architecture/deployment-plans)
- [Operations reference](../architecture/ops-guide-intro)
- [Operations guide](../architecture/security-operations-introduction)
- [Recommended security configurations](configure-security)

### License Microsoft Entra features

The features of Microsoft Entra are licensed in multiple ways. These licenses include Microsoft Entra ID Free, Microsoft Entra ID P1, Microsoft Entra ID P2, Microsoft Entra Suite, Microsoft Entra External ID, Microsoft Entra Workload ID, Microsoft Entra ID Governance, and other standalone products. Microsoft Entra is also part of licenses like [Microsoft 365](https://www.microsoft.com/microsoft-365/enterprise/microsoft365-plans-and-pricing) and [Enterprise Mobility + Security](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing). For more information about licensing and available options, see the article [Microsoft Entra licensing](licensing) or the [Microsoft Entra pricing page](https://www.microsoft.com/security/business/microsoft-entra-pricing).

## Manage and develop with Microsoft Entra

Administrators can use the Microsoft Entra admin center and Microsoft Graph API to manage identity and network access resources. Developers can use the Microsoft identity platform to build identity-aware applications.

### Microsoft Entra admin center

The [Microsoft Entra admin center](https://entra.microsoft.com/) is a web-based portal for configuring and managing Microsoft Entra products from a single interface.

To learn more, see [Overview of Microsoft Entra admin center](entra-admin-center).

### Microsoft Graph API

The [Microsoft Graph API](/en-us/graph/api/overview) automates administrative tasks like license deployments and user lifecycle management.

To learn more, see [Manage Microsoft Entra using Microsoft Graph](/en-us/graph/api/resources/identity-network-access-overview).

### Microsoft identity platform

The [Microsoft identity platform](../identity-platform/v2-overview) enables developers to build authentication experiences for web, desktop, and mobile applications using open-source libraries and standard-compliant authentication services.

To start developing, see [Getting started](../identity-platform/v2-overview#getting-started).