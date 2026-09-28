---
layout: Conceptual
title: Govern access for applications in your environment - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/identity-governance-applications-prepare
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Microsoft Entra ID Governance allows you to balance your organization's need for security and employee productivity with the right processes and visibility. These features can be used for your existing business critical third party on-premises and cloud-based applications.
editor: markwahl-msft
ms.topic: how-to
ms.date: 2024-11-21T00:00:00.0000000Z
ms.reviewer: markwahl-msft
ms.custom: sfi-ga-nochange
locale: en-us
document_id: d47b6dbe-58df-a8f7-fbed-c3fc037c92ab
document_version_independent_id: ea1cad7a-fec7-2c4b-7522-4dc96f07a25c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/identity-governance-applications-prepare.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/identity-governance-applications-prepare
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/identity-governance-applications-prepare.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5b985797-8491-d774-64b5-f4991c0e9ebe
---

# Govern access for applications in your environment - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra ID Governance allows you to balance your organization's need for security and employee productivity with the right processes and visibility. Its features ensure that users and agent IDs have the right access to the right resources in your organization at the right time.

Organizations with compliance requirements or risk management plans have sensitive or business-critical applications. The application sensitivity may be based on its purpose or the data it contains, such as financial information or personal information of the organization's customers. For those applications, only a subset of all the users and agent IDs in the organization will typically be authorized to have access, and access should only be permitted based on documented business requirements.

As part of your organization's controls for managing access, you can use Microsoft Entra features to:

- set up appropriate access
- provision users to applications
- enforce access checks
- produce reports to demonstrate how those controls are being used to meet your compliance and risk management objectives.

In addition to the application access governance scenario, you can also use Microsoft Entra ID Governance features and the other Microsoft Entra features for other scenarios, such as [reviewing and removing users from other organizations](access-reviews-external-users) or [managing users who are excluded from Conditional Access policies](conditional-access-exclusion). If your organization has multiple administrators in Microsoft Entra ID or Azure, uses B2B or self-service group management, then you should [plan an access reviews deployment](deploy-access-reviews) for those scenarios.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Getting started with governing access to applications

Microsoft Entra ID Governance can be integrated with many applications, using [standards](../architecture/auth-sync-overview) such as OpenID Connect, SAML, SCIM, SQL, and LDAP. Through these standards, you can use Microsoft Entra ID with many popular SaaS applications, on-premises applications, and applications that your organization has developed.

Once you've prepared your Microsoft Entra environment, as described in the section below, the three step plan covers how to connect an application to Microsoft Entra ID and enable identity governance features to be used for that application.

1. [Define your organization's policies for governing access to the application](identity-governance-applications-define)
2. [Integrate the application with Microsoft Entra ID](identity-governance-applications-integrate) to ensure only authorized users can access the application, and review user's existing access to the application to set a baseline of all users having been reviewed. This allows authentication and user provisioning
3. [Deploy those policies](identity-governance-applications-deploy) for controlling single sign-on (SSO) and automating access assignments for that application

## Prerequisites before configuring Microsoft Entra ID and Microsoft Entra ID Governance for identity governance

Before you begin the process of governing application access from Microsoft Entra ID Governance, you should check your Microsoft Entra environment is appropriately configured.

- **Select the appropriate tenant deployment architecture.** If you'll be providing business partners as well as workforce users access to an application, then select a tenant to integrate the application and deploy identity governance capabilities, that will be configured for any collaboration or isolation requirements for the business partner scenario. For more information, see [Microsoft Entra External ID deployment architectures with Microsoft Entra](../architecture/external-identity-deployment-architectures).
- **Ensure your Microsoft Entra ID and Microsoft Online Services environment is ready for the [compliance requirements](../standards/standards-overview) for the applications to be integrated and properly licensed**. Compliance is a shared responsibility among Microsoft, cloud service providers (CSPs), and organizations. To use Microsoft Entra ID to govern access to applications, you must have one of the following [license combinations](licensing-fundamentals) in your tenant:

    - **Microsoft Entra ID Governance** and its prerequisite, Microsoft Entra ID P1
    - **Microsoft Entra ID Governance Step Up for Microsoft Entra ID P2** and its prerequisite, either Microsoft Entra ID P2 or Enterprise Mobility + Security (EMS) E5
    - **Microsoft Entra Suite**

    Your tenant needs to have at least as many licenses as the number of member (non-guest) users who are governed, including those users that have or can request access to the applications, approve, or review access to the applications. With an appropriate license for those users, you can then govern access to up to 1500 applications per user. For more information, see [example license scenarios](licensing-fundamentals#example-license-scenarios).
- **If you will be governing guest's access to the application, link your Microsoft Entra tenant to a subscription for MAU billing**. This step is necessary prior to having a guest request or review their access. For more information, see [billing model for Microsoft Entra External ID](../external-id/external-identities-pricing).
- **Check that Microsoft Entra ID is already sending its audit log, and optionally other logs, to Azure Monitor.** Azure Monitor is optional, but useful for governing access to apps, as Microsoft Entra only stores audit events for up to 30 days in its audit log. You can keep the audit data for longer than the default retention period, outlined in [How long does Microsoft Entra ID store reporting data?](../identity/monitoring-health/reference-reports-data-retention), and use Azure Monitor workbooks and custom queries and reports on historical audit data. You can check the Microsoft Entra configuration to see if it's using Azure Monitor, in **Microsoft Entra ID** in the Microsoft Entra admin center, by clicking on **Workbooks**. If this integration isn't configured, and you have an Azure subscription and are in the `Global Administrator` or `Security Administrator` roles, you can [configure Microsoft Entra ID to use Azure Monitor](entitlement-management-logs-and-reporting).
- **Select an object retention approach.** If your organization requires being able to report on historical Microsoft Entra objects, such as reports that list users and agent IDs who had access to an application in a past year including those who were subsequently deleted from Microsoft Entra, then you should plan to archive objects from Microsoft Entra to a separate repository for retention and reporting purposes. For more information, see [Customized reports in Azure Data Explorer (ADX) using data from Microsoft Entra ID](custom-entitlement-report-with-adx-and-entra-id).
- **Make sure only authorized users are in the highly privileged administrative roles in your Microsoft Entra tenant.** Administrators in the *Global Administrator*, *Identity Governance Administrator*, *User Administrator*, *Application Administrator*, *Cloud Application Administrator*, and *Privileged Role Administrator* can make changes to users and their application role assignments. If the memberships of those roles haven't yet been recently reviewed, you need a user who is in the *Global Administrator* or *Privileged Role Administrator* to ensure that [access review of these directory roles](privileged-identity-management/pim-create-roles-and-resource-roles-review) are started. You should also ensure that users in Azure roles in subscriptions that hold the Azure Monitor, Logic Apps, and other resources needed for the operation of your Microsoft Entra configuration have been reviewed.
- **Check your tenant has appropriate isolation.** If your organization is using Active Directory on-premises, and these AD domains are connected to Microsoft Entra ID, then you need to ensure that highly privileged administrative operations for cloud-hosted services are isolated from on-premises accounts. Check that you've [configured your systems to protect your Microsoft 365 cloud environment from on-premises compromise](../architecture/protect-m365-from-on-premises-attacks).

Once you have checked your Microsoft Entra environment is ready, then proceed to [define the governance policies](identity-governance-applications-define) for your applications.