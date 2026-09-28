---
layout: Conceptual
title: What are Microsoft Entra recommendations? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/overview-recommendations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Provides a general overview of Microsoft Entra recommendations so you can keep your tenant secure and healthy.
ms.topic: overview
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: jadedsouza
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 602a1bca-28f6-3bce-de1d-b2d391fc1204
document_version_independent_id: b119896f-ef42-2f19-6456-0904e8068c13
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/overview-recommendations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/overview-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/overview-recommendations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 43f64ab3-0e5e-4a73-fdae-1bbcc4fb3f6f
---

# What are Microsoft Entra recommendations? - Microsoft Entra ID | Microsoft Learn

Keeping track of all the settings and resources in your tenant can be overwhelming. The Microsoft Entra recommendations feature helps monitor the status of your tenant so you don't have to. These recommendations help ensure your tenant is in a secure and healthy state while also helping you maximize the value of the features available in Microsoft Entra ID.

Microsoft Entra recommendations now include *Identity Secure Score* recommendations. These recommendations provide similar insights into the security of your tenant. For more information, see [What is Identity Secure Score](concept-identity-secure-score).

All these Microsoft Entra recommendations provide you with personalized insights with actionable guidance to:

- Help you identify opportunities to implement identity best practices.
- Improve the state of your Microsoft Entra tenant.
- Optimize the configurations for your scenarios.

This article gives you an overview of how you can use Microsoft Entra recommendations.

## How does it work?

On a daily basis, Microsoft Entra ID analyzes the configuration of your tenant. During this analysis, Microsoft Entra ID compares the configuration of your tenant with security best practices and recommendation data. If a recommendation is flagged as applicable to your tenant, the recommendation appears in the **Recommendations** section of the Microsoft Entra identity overview area.

![Screenshot of the Overview page of the tenant with the Recommendations option highlighted.](media/overview-recommendations/recommendations-overview.png)

Each recommendation contains a description, a summary of the value of addressing the recommendation, and a step-by-step action plan. If applicable, impacted resources associated with the recommendation are listed, so you can resolve each affected area. If a recommendation doesn't have any associated resources, the impacted resource type is *Tenant level*, so your step-by-step action plan impacts the entire tenant and not just a specific resource. The system processes recommendation data daily, reflecting activity from the preceding 24-hour window. Occasionally, data synchronization may extend up to 72 hours.

## Roles and licenses

The following roles and Microsoft Graph permissions provide access to Microsoft Entra recommendations. License requirements depend on the specific recommendation; see the Recommendations overview table for per-recommendation details.

There are different role requirements for viewing or updating a recommendation. Use the least-privileged role for the type of access needed. For a full list of roles, see [Least privileged roles by task](../role-based-access-control/delegate-by-task#monitoring-and-health---recommendations-least-privileged-roles).

| Microsoft Entra role | Access type |
| --- | --- |
| Reports Reader | Read-only |
| Security Reader | Read-only |
| Global Reader | Read-only |
| Authentication Policy Administrator | Update and read |
| Exchange Administrator | Update and read |
| Security Administrator | Update and read |
| `DirectoryRecommendations.Read.All` | Read-only in Microsoft Graph |
| `DirectoryRecommendations.ReadWrite.All` | Update and read in Microsoft Graph |

Some recommendations might require a P2 or other license. For more information, see the [Recommendations overview table](overview-recommendations#recommendations-overview-table).

## Recommendations overview table

The recommendations listed in the following table are currently available in public preview or general availability the types of resources addressed by the recommendation, and more. The license requirements for recommendations in public preview are subject to change. The table provides links to available documentation for those recommendations that required separate guidance.

| Recommendation | Impacted resources | Availability | Identity Secure Score | Target roles for email notifications |
| --- | --- | --- | --- | --- |
| AAD Connect Deprecated | Tenant | Preview | No | Hybrid Identity Administrator |
| Configure VPN integration | Users | Preview | Yes | N/A |
| [Convert per-user MFA to Conditional Access MFA](recommendation-turn-off-per-user-mfa) | Users | Generally available | No | Security Administrator |
| Designate more than one Global Administrator | Users | Generally available | Yes | Global Administrator |
| Disable Print spooler service on domain controllers | Tenant | Preview | Yes | N/A |
| Do not allow users to grant consent to unreliable applications | Tenant | Generally available | Yes | Global Administrator |
| Do not expire passwords | Tenant | Generally available | Yes | Global Administrator |
| Edit misconfigured Certificate Authority ACL | Applications | Preview | Yes | N/A |
| Edit misconfigured certificate templates access control lists | Applications | Preview | Yes | N/A |
| Edit misconfigured certificate templates owner | Applications | Preview | Yes | N/A |
| Edit misconfigured enrollment agent certificate template | Applications | Preview | Yes | N/A |
| Edit overly permissive Certificate Template with privileged EKU | Applications | Preview | Yes | N/A |
| Edit vulnerable Certificate Authority setting | Applications | Preview | Yes | N/A |
| Enable password hash sync if hybrid | Tenant | Generally available | Yes | Hybrid Identity Administrator |
| Enable policy to block legacy authentication | Users | Generally available | Yes | Conditional Access Administrator, Security Administrator |
| Enable self-service password reset | Users | Generally available | Yes | Authentication Policy Administrator |
| Ensure all users can complete multifactor authentication | Users | Generally available | Yes | Conditional Access Administrator, Security Administrator |
| Ensure privileged accounts are not delegated | Users | Preview | Yes | N/A |
| Group Policy Object (GPO) assigns unprivileged identities to local groups with elevated privileges | Users | Preview | Yes | N/A |
| [Migrate applications from AD FS to Microsoft Entra ID](recommendation-migrate-apps-from-adfs-to-azure-ad) | Applications | Generally available | No | Application Administrator, Authentication Administrator Hybrid Identity Administrator |
| [Migrate applications from the retiring Azure AD Graph APIs to Microsoft Graph](recommendation-migrate-to-microsoft-graph-api) | Applications | Preview | No | Application Administrator |
| [Migrate from MFA server to Microsoft Entra MFA](recommendation-migrate-to-microsoft-entra-mfa) | Tenant | Generally Available | No | Global Administrator |
| [Migrate service principals from the retiring Azure AD Graph APIs to Microsoft Graph](recommendation-migrate-to-microsoft-graph-api) | Applications | Preview | No | Application Administrator |
| [Migrate to Microsoft Authenticator](recommendation-migrate-to-authenticator) | Users | Preview | No | Global Administrator |
| [Minimize MFA prompts from known devices](recommendation-mfa-from-known-devices) | Users | Generally available | No | Global Administrator |
| Modify unsecure Kerberos delegations to prevent impersonation | Applications | Preview | Yes | N/A |
| Prevent Certificate Enrollment with arbitrary application policies | Applications | Preview | Yes | N/A |
| Protect all users with a sign-in risk policy | Users | Generally available | Yes | Conditional Access Administrator, Security Administrator |
| Protect all users with a user risk policy | Users | Generally available | Yes | Conditional Access Administrator, Security Administrator |
| Protect and manage local admin passwords with Microsoft LAPS | Users | Preview | Yes | N/A |
| [Protect your tenant with Insider Risk Conditional Access policy](recommendation-insider-risk-condition) | Users | Generally available | Yes | Conditional Access Administrator, Security Administrator |
| Reduce lateral movement path risk to sensitive entities | Users | Preview | Yes | N/A |
| Remove access rights on suspicious accounts with the Admin SDHolder permission | Users | Preview | Yes | N/A |
| Remove dormant accounts from sensitive groups | Users | Preview | Yes | N/A |
| Remove non-admin accounts with DCsync permissions | Users | Preview | Yes | N/A |
| Remove unsafe permissions on sensitive Microsoft Entra Connect accounts | Users | Preview | Yes | N/A |
| [Remove unused applications](recommendation-remove-unused-apps) | Applications | Preview | No | Application Administrator |
| [Remove unused credentials from applications](recommendation-remove-unused-credential-from-apps) | Applications | Preview | No | Application Administrator |
| [Renew expiring application credentials](recommendation-renew-expiring-application-credential) | Applications | Preview | No | Application Administrator |
| [Renew expiring service principal credentials](recommendation-renew-expiring-service-principal-credential) | Applications | Preview | No | Application Administrator |
| Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector | Users | Preview | Yes | N/A |
| Require MFA for administrative roles | Users | Generally available | Yes | Conditional Access Administrator, Security Administrator |
| Resolve Unsecure Account Attributes | Users | Preview | Yes | N/A |
| Reversible passwords found in GPOs | Users | Preview | Yes | N/A |
| Review inactive users with Access Reviews | Users | Preview | No | Identity Governance Administrator |
| Rotate password for Microsoft Entra Connect AD DS Connector account | Users | Preview | Yes | N/A |
| Secure and govern your apps with automatic user and group provisioning | Applications | Preview | No | Application Administrator, IT Governance Administrator |
| Stop clear text credentials exposure | Users | Preview | Yes | N/A |
| Stop weak cipher usage | Tenant | Preview | Yes | N/A |
| Use least privileged administrative roles | Users | Generally available | Yes | Privileged Role Administrator |
| Verify App Publisher | Applications | Preview | No | Global Administrator |

Microsoft Entra only displays the recommendations that apply to your tenant, so you might not see all supported recommendations listed.

## Identity Secure Score

Your Identity Secure Score, which appears at the top of the page, is a numerical representation of the health of your tenant. Recommendations that apply to the Identity Secure Score are given individual scores in the table at the bottom of the page. You can filter the list of recommendations to only the Identity Secure Score recommendations using the **Security** filter card. Identity Secure Score recommendations include *secure score points*, which are calculated as an overall score based on several security factors.

These scores add up to generate your Identity Secure Score. For more information, see [What is Identity Secure Score](concept-identity-secure-score).

![Screenshot of the Identity Secure Score.](media/overview-recommendations/identity-secure-score.png)

## Are Microsoft Entra recommendations related to Azure Advisor?

The Microsoft Entra recommendations feature is the Microsoft Entra specific implementation of [Azure Advisor](/en-us/azure/advisor/advisor-overview), which is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments. Azure Advisor analyzes your resource configuration and usage data to recommend solutions that can help you improve the cost effectiveness, performance, reliability, and security of your Azure resources.

Microsoft Entra recommendations use similar data to support you with the roll-out and management of Microsoft's best practices for Microsoft Entra tenants to keep your tenant in a secure and healthy state. The Microsoft Entra recommendations feature provides a holistic view into your tenant's security, health, and usage.

## Email notifications (preview)

Microsoft Entra recommendations now generate email notifications when a new recommendation is generated. This new preview feature sends emails to a predetermined set of roles for each recommendation. For example, recommendations that are associated with the health of your tenant's applications are sent to users who have the Application Administrator role.

If your organization is using Privileged Identity Management (PIM), the recipients must be elevated to the role indicated in order to receive the email notification. If no one is actively assigned to the role, no emails are sent. For this reason, we recommend checking the recommendations regularly to ensure that you're aware of any new recommendations.