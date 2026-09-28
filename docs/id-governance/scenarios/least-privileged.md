---
layout: Conceptual
title: Understanding least privilege with Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/least-privileged
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes the concept of least privilege and how it relates with Microsoft Entra ID Governance.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
locale: en-us
document_id: c4e54df5-026a-b80a-ca87-7dab82bc1991
document_version_independent_id: c4e54df5-026a-b80a-ca87-7dab82bc1991
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/least-privileged.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/least-privileged
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/least-privileged.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5c0a9426-e9f9-1018-77be-9033521f4b24
---

# Understanding least privilege with Microsoft Entra ID Governance | Microsoft Learn

One concept that needs to be addressed before under taking an identity governance strategy is the principle of least privilege (POLP). Least privilege is a principle in identity governance that involves assigning users and groups only the minimum level of access and permissions necessary to perform their duties. The idea is to restrict access rights so that a user or group can complete their work, but also minimizing unnecessary privileges that could potentially be exploited by attackers or lead to security breaches.

In regards to Microsoft Entra ID Governance, applying the principle of least privilege helps enhance security and mitigate risks. This approach ensures that users and groups are granted access only to the resources, data, and actions that are relevant to their roles and responsibilities, and nothing beyond that.

## Key concepts of the principle of least privilege

- **Access to only required resources:** Users are given access to information and resources only if they have a genuine need for them to perform their tasks. This prevents unauthorized access to sensitive data and minimizes the potential impact of a security breach. Automating user provisioning helps reduce unnecessary granting of access rights. [Lifecycle workflows](../what-are-lifecycle-workflows) is an identity governance feature that enables organizations to manage Microsoft Entra users by automating basic lifecycle processes.
- **Role-Based Access Control (RBAC):** Access rights are determined based on the specific roles or job functions of users. Each role is assigned the minimum permissions necessary to fulfill its responsibilities. [Microsoft Entra role-based access control](../../identity/role-based-access-control/custom-overview) manages access to Microsoft Entra resources.
- **Just-In-Time Privilege:** Access rights are granted only for the duration of time that they're needed and are revoked when they're no longer required. This reduces the window of opportunity for attackers to exploit excessive privileges. [Privileged Identity Management (PIM)](../privileged-identity-management/pim-configure) is a service in Microsoft Entra ID that enables you to manage, control, and monitor access to important resources in your organization and can provide just-in-time access.
- **Regular Auditing and Review:** Periodic reviews of user access and permissions are conducted to ensure that users still require the access they have been granted. This helps to identify and rectify any deviations from the least privilege principle. [Access reviews in Microsoft Entra ID](../access-reviews-overview), part of Microsoft Entra, enable organizations to efficiently manage group memberships, access to enterprise applications, and role assignments. User's access can be reviewed regularly to make sure only the right people have continued access.
- **Default Deny:** The default stance is to deny access, and access is explicitly granted only for approved purposes. This contrasts with a "default allow" approach, which can result in granting unnecessary privileges. [Entitlement management](../entitlement-management-overview) is an identity governance feature that enables organizations to manage identity and access lifecycle at scale, by automating access request workflows, access assignments, reviews, and expiration.

By following the principle of least privilege, your organization can reduce the risk of security issues, and ensure that access controls are aligned with business needs.

## Least privileged roles for managing in Identity Governance features

It's a best practice to use the least privileged role to perform administrative tasks in Identity Governance. We recommend that you use Microsoft Entra PIM to activate a role as needed to perform these tasks. The following are the least privileged [directory roles](../../identity/role-based-access-control/permissions-reference) to configure Identity Governance features:

| Feature | Least privileged role |
| --- | --- |
| Entitlement management | Identity Governance Administrator |
| Access reviews | User Administrator (with the exception of access reviews of Azure or Microsoft Entra roles, which require Privileged Role Administrator) |
| Lifecycle Workflows | Lifecycle Workflows Administrator |
| Privileged Identity Management | Privileged Role Administrator |
| Terms of use | Security Administrator or Conditional Access Administrator |

Note

The least privileged role for Entitlement management has changed from the User Administrator role to the Identity Governance Administrator role.