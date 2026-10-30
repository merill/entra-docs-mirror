---
layout: Conceptual
title: What is Microsoft Entra Tenant Governance? - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about Microsoft Entra Tenant Governance and how it helps organizations discover, manage, and govern tenants across their environment
ms.topic: overview
ms.date: 2026-03-05T00:00:00.0000000Z
locale: en-us
document_id: ea1f3bcd-625d-ab16-3a78-919d00827025
document_version_independent_id: ea1f3bcd-625d-ab16-3a78-919d00827025
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 3cf185d4-b005-18b0-e5d0-3b7c15e5fb79
---

# What is Microsoft Entra Tenant Governance? - Microsoft Entra ID Governance | Microsoft Learn

Most large organizations operate Microsoft services in multiple tenants because of mergers and acquisitions, requirements for partitioning security or privacy-sensitive workloads, test environments, and other reasons. Most organizations also have user-created "shadow IT" tenants that central IT doesn't administer and often doesn't know about. In many environments, it's not easy to verify that each of these tenants is configured properly, especially if you don't know that some tenants even exist. This creates risk for your organization's security and compliance objectives.

Microsoft Entra Tenant Governance enables you to get visibility across all your tenants and ensure they are configured to meet your security and compliance requirements. This includes the tenants you administer today, "shadow IT" tenants that you don't administer but that create risks for your organization, and new tenants that your users create.

## Related tenants

Related tenants capabilities help you identify tenants that you need to govern, or that have security or privacy exposure to tenants that you administer.

Key features:

- Automatically detect tenants that are related to your tenant based on one or more discovery signals.
- The B2B discovery signal identifies and measures inbound and outbound B2B access, B2B registration, and B2B administrative access between your tenant and other tenants.
- The multitenant application discovery signal identifies tenants with registered multitenant applications that have permissions in your tenant, or tenants to which your registered multitenant applications have access.
- The billing discovery signal identifies tenants that share billing accounts with you, where either your tenant or the related tenant is an associated billing tenant for the billing account.
- View initial and recent metrics about the volume of relationships between your tenant and related tenants.
- Filter and sort the list of related tenants based on discovery signal findings to focus on tenants with particular types of risk that your organization prioritizes.

Learn more about [related tenants](related-tenants).

## Governance relationships

Governance relationship capabilities help you set up and manage cross-tenant administrative access across the tenants that you need to govern.

Key features:

- Invitation, request, and approval workflows to define a governance relationship and set up cross-tenant administrative access between existing tenants.
- Integration with the billing discovery signal to streamline the workflow for setting up relationships between tenants that share a billing account.
- Least-privilege cross-tenant administrative access that enables users in your governing tenant to perform administrative tasks in governed tenants, including configuration management tasks.
- Streamlined app injection experience to provision and maintain permissions for your custom application in a governed tenant.
- Governance policy templates to easily request the same permissions in different tenants where you need the same administrative permissions.

Learn more about [governance relationships](governance-relationships).

## Configuration management

Configuration management capabilities help you monitor the configuration of tenant resources in any tenant that you govern. Over 200 types of resources are supported across six Microsoft services: Entra, Intune, Exchange Online, Teams, Purview, and Defender.

Key features:

- Author a configuration baseline that expresses the desired state of tenant resources by using a standard JSON format.
- Create a configuration snapshot to document the current state of tenant resources. You can use a snapshot from a "known good" tenant to jumpstart the authoring of a configuration baseline. Snapshots can also help satisfy certain audit requirements.
- Create a monitor that automatically compares the actual state of tenant resources to the desired state defined in your JSON configuration baseline.
- View monitor results that show summary statistics each time the monitor runs. Currently, each monitor runs at six-hour intervals.
- View a list of configuration drifts in one monitor or across all monitors running in the tenant. Each configuration drift shows which properties of the resource differ from what the configuration baseline defines.

Learn more about [configuration management](configuration-management).

## Secure tenant creation

Secure tenant creation capabilities help you control which users can create new add-on tenants, automatically set up governance relationships with those tenants, and ensure that your organization can recover administrative access to those tenants if necessary.

Key features:

- Define a governance policy template to automatically create a governance relationship between your tenant and new tenants created by your users.
- Control which users can create new add-on tenants by assigning or limiting access to commerce billing accounts in your tenant.
- Use the Microsoft Entra asset in your commerce billing account to streamline recovery of administrative access to an add-on tenant, such as when the last administrator of that tenant leaves your organization, or when a threat actor compromises the add-on tenant.
- Use the commerce API or the Microsoft Entra admin center to create a new add-on tenant.

Learn more about [creating a governed tenant](how-to-create-tenant).

## Getting started

To begin using Tenant Governance features, sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an administrator whose roles have permission to perform Tenant Governance tasks. Navigate to the **Tenant governance** page.

## Licensing and support

Tenant Governance is available at two service levels: Tenant Governance Basic and Tenant Governance Premium. To see which Tenant Governance features are available at each service level, see [Microsoft Entra licensing](../../fundamentals/licensing).