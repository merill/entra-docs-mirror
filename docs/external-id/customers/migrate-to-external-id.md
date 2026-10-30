---
layout: Conceptual
title: Transition to Microsoft Entra External ID for CIAM - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/migrate-to-external-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: 'Transition to Microsoft Entra External ID for CIAM: Learn how to migrate your legacy customer identity solutions to enhance security, compliance, and scalability.'
ms.date: 2025-07-30T00:00:00.0000000Z
ms.topic: concept-article
ms.collection:
- migration
- aws-to-azure
ms.custom:
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:07/07/2025
- ai-gen-description
locale: en-us
document_id: 5c1347a1-23f7-098c-bd6a-6eea4fe690cc
document_version_independent_id: 5c1347a1-23f7-098c-bd6a-6eea4fe690cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/migrate-to-external-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/migrate-to-external-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/migrate-to-external-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: dad78ca2-9299-e4ee-9670-8a879e39a92d
---

# Transition to Microsoft Entra External ID for CIAM - Microsoft Entra External ID | Microsoft Learn

Developers building applications often control authentication and authorization for customers accessing their applications. They use customer identity access management (CIAM) solutions to avoid building and maintaining a full identity and access management (IAM) solution. Microsoft Entra External ID lets developers connect their applications to a customer-focused version of Microsoft Entra ID, a standard IAM solution. This guide gives a migration path and resources for developers and identity teams.

## What is Microsoft Entra External ID?

For organizations and businesses that want to make their apps available to consumers and business customers, [Microsoft Entra External ID](overview-customers-ciam) lets you add CIAM features such as self-service registration, personalized sign-in experiences, and customer account management. Because these CIAM capabilities are built into Microsoft Entra ID, you benefit from platform features like enhanced security, compliance, and scalability.

## Why migrate from other CIAM solutions?

Organizations might migrate to Microsoft Entra External ID from another tool based on strategic goals such as:

- Consolidate cloud identity providers
- Align with an existing enterprise identity solution
- Enhance security and compliance
- Access to [strong developer guidance and an active community](https://developer.microsoft.com/identity/external-id)
- [Feature availability](concept-supported-features-customers#general-feature-comparison)
- [Reduce costs](https://azure.microsoft.com/pricing/details/microsoft-entra-external-id)

## Plan your migration

The [Microsoft Entra External ID deployment guide](/en-us/entra/architecture/deployment-external-intro) helps organizations get started with their deployment if they're new to the concept of a CIAM solution. Following that along with the steps outlined in this article help organizations with existing CIAM deployments complete their migration to Microsoft Entra External ID. Organizations start by [evaluating the availability of critical features in Microsoft Entra External ID](concept-supported-features-customers#general-feature-comparison) to confirm readiness for migration.

If you plan to migrate a workload from AWS to Azure, we suggest you have a methodical approach to that initiative. Component selection and Azure fundamentals are important parts of that larger process. To fine tune your migration plan using Microsoft's guidance, see [Migrate security services from Amazon Web Services](/en-us/azure/migration/migrate-security-from-aws).

### Migration steps

This guide helps you migrate legacy customer identity access management (CIAM) solutions to Microsoft Entra External ID. Follow this series of articles to navigate the steps in the migration process.

| Stage | Steps |
| --- | --- |
| Premigration planning | • Map legacy CIAM features to [Microsoft Entra External ID capabilities](overview-customers-ciam). • Complete an inventory of the existing CIAM solution. |
| Microsoft Entra External ID setup | • [Create an external tenant](how-to-create-external-tenant-portal). • [Add and manage admin accounts](how-to-manage-admin-accounts). • [Enable other identity providers](concept-authentication-methods-customers). • [Register all customer-facing applications](/en-us/entra/identity-platform/quickstart-register-app). • [Add an application to the user flow](how-to-user-flow-add-application). • [Test the user flow](how-to-test-user-flows). |
| Identity flows and branding | • [Add a sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers)• [Add an application to the user flow](how-to-user-flow-add-application)• [Manage access](how-to-use-app-roles-customers)• [Test the user flow](how-to-test-user-flows)• [Customize branding](how-to-customize-branding-customers) |
| Security and monitoring | • [Configure MFA](how-to-multifactor-authentication-customers)• [Create dashboards](how-to-user-insights) (retiring August 31, 2026; see [migration guidance](how-to-user-insights#migrate-from-user-insights)) • [Set up Azure Monitor](how-to-azure-monitor) |
| Test and rollout | • Define your rollout strategy. • Import the final batch of users if needed using the [Microsoft Graph API](/en-us/graph/api/user-post-users). • Cut over live traffic to Microsoft Entra External ID. • Monitor live authentication logs and error rates. • Collect feedback. • Decommission legacy solution. |

### Inventory

Take inventory of the existing configuration and architecture, including:

- Users
- Access and security groups
- Connected applications
- Sign-up and sign-in user flows
- Multifactor authentication mechanisms
- Social identity providers
- Any specific compliance or regulatory requirements

At this phase, determine if user data transformation is required, then complete [transformation and mapping](concept-user-attributes).