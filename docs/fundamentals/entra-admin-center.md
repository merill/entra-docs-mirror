---
layout: Conceptual
title: Microsoft Entra admin center - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/entra-admin-center
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Overview of the Microsoft Entra admin center interface for configuring and managing Microsoft Entra products.
ms.topic: overview
ms.date: 2026-06-18T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5393c8f5-159e-3b8e-1da4-a09cbc0f30ef
document_version_independent_id: 5393c8f5-159e-3b8e-1da4-a09cbc0f30ef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/entra-admin-center.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/entra-admin-center
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/entra-admin-center.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 59842cf7-bf4d-062f-4298-24120cb62137
---

# Microsoft Entra admin center - Microsoft Entra | Microsoft Learn

## Overview

The [Microsoft Entra admin center](https://entra.microsoft.com/) is a web-based portal that provides a unified administrative experience for configuring and managing Microsoft Entra products in a centralized location. From the admin center, administrators can manage users and groups, configure authentication methods, create Conditional Access policies, monitor identity security posture, and govern access across the organization.

The admin center brings together the following Microsoft Entra product areas, each accessible from the left-hand navigation menu:

- **Entra ID** — Manage users, groups, devices, applications, roles, and authentication methods.
- **ID Protection** — Monitor and respond to identity-based risks with risk policies and reports.
- **ID Governance** — Control access lifecycle with entitlement management, access reviews, and lifecycle workflows.
- **Verified ID** — Issue and manage verifiable credentials.
- **Global Secure Access** — Secure access to apps and resources with Private Access and Internet Access.

## Explore the Microsoft Entra admin center

The Microsoft Entra admin center is organized by product. Access the products through the search bar or left-hand menu. You can also use the search bar at the top of the page to find specific settings, features, or documentation.

**Home** includes at-a-glance information about your tenant, recent activities, and other helpful resources, including shortcuts and deployment guides. The home page provides quick access to:

- **Tenant overview** — View your tenant name, ID, and license information.
- **Recommended actions** — Personalized [recommendations](../identity/monitoring-health/overview-recommendations) to help improve the security and health of your tenant.
- **Deployment guides** — Step-by-step guidance for deploying Microsoft Entra features.
- **Recent activity** — Quick access to recently visited pages and recent changes.

![Screenshot of the Microsoft Entra admin center overview home page.](media/entra-admin-center/entra-admin-center-home.png)

The following sections provide a high-level overview of the product interfaces and links to learn more about the features.

### Entra ID

**Entra ID** gives administrators and developers access to [Microsoft Entra ID](what-is-entra) and [Microsoft Entra External ID](../external-id/external-identities-overview) solutions, including tenants, users, groups, devices, applications, roles, and licensing.

![Screenshot of the Microsoft Entra admin center Identity menu.](media/entra-admin-center/entra-admin-identity.png)

For more information about configuring and managing Microsoft Entra ID solutions, see the following documentation:

- [Users and groups](../identity/users/directory-overview-user-model)
- [Devices](../identity/devices/overview)
- [Agents](../agent-id/what-is-microsoft-entra-agent-id)
- [Enterprise applications](../identity/enterprise-apps/what-is-application-management)
- [App registrations](../identity-platform/application-model)
- [Roles and admins](../identity/role-based-access-control/custom-overview)
- [External identities](../external-id/external-identities-overview)
- [Conditional Access](../identity/conditional-access/overview)
- [Multifactor authentication](../identity/authentication/concept-mfa-howitworks)
- [Identity secure score](../identity/monitoring-health/concept-identity-secure-score)
- [Authentication methods](../identity/authentication/overview-authentication)
- [Password reset](../identity/authentication/concept-sspr-howitworks)
- [Custom security attributes](custom-security-attributes-overview)

### ID Protection

**ID Protection** gives administrators and developers access to [Microsoft Entra ID Protection](../id-protection/overview-identity-protection) solutions, including the protection dashboard, risk-based access policies, risky users report, multifactor authentication, and password reset.

![Screenshot of the Microsoft Entra admin center Protection menu.](media/entra-admin-center/entra-admin-protection.png)

For more information about configuring and managing Microsoft Entra ID Protection solutions, see the following documentation:

- [Identity Protection dashboard](../id-protection/id-protection-dashboard)
- [Risk-based access policies](../id-protection/concept-identity-protection-policies)
- [Risky users](../id-protection/howto-identity-protection-investigate-risk)
- [Risky workload identities](../id-protection/concept-workload-identity-risk)

### ID Governance

**ID Governance** gives administrators and developers access to [Microsoft Entra ID Governance](../id-governance/identity-governance-overview) solutions, including entitlement management, access reviews, and lifecycle workflows.

![Screenshot of the Microsoft Entra admin center Identity governance menu.](media/entra-admin-center/entra-admin-identity-governance.png)

For more information about configuring and managing Microsoft Entra ID Governance solutions, see the following documentation:

- [Identity Governance dashboard](../id-governance/governance-dashboard)
- [Entitlement management](../id-governance/entitlement-management-overview)
- [Access reviews](../id-governance/access-reviews-overview)
- [Privileged Identity Management](../id-governance/privileged-identity-management/pim-configure)
- [Lifecycle workflows](../id-governance/what-are-lifecycle-workflows)
- [Custom task extensions for Lifecycle workflows](../id-governance/lifecycle-workflow-extensibility)

### Verified ID

**Verified ID** gives administrators and developers access to [Microsoft Entra Verified ID](../verified-id/decentralized-identifier-overview) solutions, including credentials and organization settings.

![Screenshot of the Microsoft Entra admin center Verified ID menu.](media/entra-admin-center/entra-admin-verified-id.png)

For more information about configuring and managing Microsoft Entra Verified ID solutions, see the following documentation:

- [Credentials](../verified-id/verifiable-credentials-configure-tenant-quick)

### Global Secure Access

**Global Secure Access** gives administrators and developers access to [Microsoft Entra Private Access](../global-secure-access/overview-what-is-global-secure-access#microsoft-entra-private-access) and [Microsoft Entra Internet Access](../global-secure-access/overview-what-is-global-secure-access#microsoft-entra-internet-access) solutions, including the Global Secure Access dashboard, clients, connectors, and monitoring.

![Screenshot of the Microsoft Entra admin center Global Secure Access menu.](media/entra-admin-center/entra-admin-global-secure-access.png)

For more information about configuring and managing Global Secure Access solutions, see the following documentation:

- [Global Secure Access dashboard](../global-secure-access/concept-traffic-dashboard)
- [Global Secure Access client](../global-secure-access/concept-clients)
- [Traffic forwarding](../global-secure-access/concept-traffic-forwarding)
- [Remote networks](../global-secure-access/concept-remote-network-connectivity)
- [Logs and monitoring](../global-secure-access/concept-global-secure-access-logs-monitoring)

## Common admin tasks

The following table lists common administrative tasks you can perform from the Microsoft Entra admin center, with links to detailed guidance for each task.

| Task | Description | Learn more |
| --- | --- | --- |
| Create or delete users | Add new members or guests to your organization, or remove existing users. | [Create or delete users](how-to-create-delete-users) |
| Manage groups | Create and manage groups to organize users for access management and licensing. | [Manage groups and group membership](how-to-manage-groups) |
| Assign roles | Delegate administrative responsibilities using built-in or custom roles. | [Overview of role-based access control](../identity/role-based-access-control/custom-overview) |
| Manage applications | Register and configure applications for single sign-on and API access. | [What is application management?](../identity/enterprise-apps/what-is-application-management) |
| Create a Conditional Access policy | Define access controls based on conditions such as user, device, location, and risk. | [What is Conditional Access?](../identity/conditional-access/overview) |
| Review identity secure score | Check your tenant's security posture and follow recommendations to improve it. | [What is Identity Secure Score?](../identity/monitoring-health/concept-identity-secure-score) |
| Set up multifactor authentication | Require users to verify their identity with more than one authentication method. | [How it works: Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-howitworks) |
| Configure self-service password reset | Allow users to reset their own passwords without contacting an administrator. | [How it works: Microsoft Entra self-service password reset](../identity/authentication/concept-sspr-howitworks) |

## Need help?

**Diagnose & solve problems** provides troubleshooting resources to fix common problems, and the option to contact the support team by opening a **New support request**.

![Screenshot of the Microsoft Entra admin center Diagnose &amp; solve menu.](media/entra-admin-center/entra-admin-diagnose-and-solve.png)

![Screenshot of the Microsoft Entra admin center Learn &amp; support menu.](media/entra-admin-center/entra-admin-learn-and-support.png)