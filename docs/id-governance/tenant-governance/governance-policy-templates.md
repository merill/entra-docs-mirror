---
layout: Conceptual
title: Governance policy templates - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/governance-policy-templates
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about governance policy templates and how to use them to enforce consistent governance across tenants in Microsoft Entra
ms.topic: concept-article
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b5f28d83-6869-c2bc-a131-ae63a1b2cc4d
document_version_independent_id: b5f28d83-6869-c2bc-a131-ae63a1b2cc4d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/governance-policy-templates.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/governance-policy-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/governance-policy-templates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 5ce1d584-17de-399c-4de1-0a43a9c3af56
---

# Governance policy templates - Microsoft Entra ID Governance | Microsoft Learn

Governance policy templates are a foundational component of the Tenant Governance service, which helps organizations secure Microsoft Entra tenants at scale. Before establishing a governance relationship between tenants, create a governance policy template that defines the relationship behavior. These templates are reusable across distinct governance relationships, enabling consistent and scalable management of cross-tenant access.

## How governance policy templates work

A governance policy template serves as a blueprint for governance relationships. When you create a template, you define two key areas of access:

- Cross-tenant delegated administration roles - Specify which Microsoft Entra built-in roles users from the governing tenant have in the governed tenant.
- Multitenant applications - Select custom applications to create and manage across tenants.

After you create a template, you can use it to establish multiple governance relationships with different governed tenants, ensuring consistent access policies across your organization.

When you create a governance relationship, Tenant Governance captures and stores a policy snapshot with the relationship. This snapshot represents the roles and permissions that applied at the time you established or last updated the relationship.

Updating a governance policy template doesn't automatically update relationships that you created using that template. This design ensures that the governed tenant always has the opportunity to review desired permission changes for the relationship. To apply permission updates to an active relationship, you must repeat the request and approval process.

## Cross-tenant delegated administration configuration

By selecting Microsoft Entra built-in roles and assigning them to a group in the governing tenant, you define which roles (and level of access) users in that group have in the governed tenant. With these roles, users can:

- Sign in to the governed tenant using their governing tenant credentials.
- Manage the governed tenant without needing a local or business-to-business (B2B) account in that tenant.

Each group can have multiple role assignments, and each policy template can have multiple groups defined. When you create the governance relationship, Tenant Governance creates [granular delegated admin privileges (GDAP)](cross-tenant-delegated-administration) role assignments in the governed tenant.

## Multitenant application configuration

By selecting custom, multitenant applications in the policy template, you enable centralized application management. When you create the governance relationship, Tenant Governance creates a service principal with the same permissions in the governed tenant.

This capability allows you to manage your custom, multitenant applications at scale from the central governing tenant. You don't need to go into every tenant individually to monitor and maintain least privileged app access.

For example, assume you've built a custom line of business app called Contoso Resource Manager, responsible for monitoring, reporting, and automating resource configuration across your tenants. Use the governance relationship to set up a service principal instance of Contoso Resource Manager across your governed tenants, with the right provisioned permissions consented. When you need to add or remove permissions, do so through the governance relationship instead of making changes and consenting to permissions on a per-tenant basis.

## Default policy template

The default policy template is a special template used for secure tenant creation scenarios. When you create a new add-on tenant, Tenant Governance automatically establishes a governance relationship between the parent tenant and the add-on tenant using the default policy template. This setup ensures that new tenants immediately come under centralized tenant administration from the start.

The default policy template has these characteristics:

- **Unique identifier**: Instead of a GUID, the default policy template has an ID of "default."
- **Configuration required**: You must configure the default policy template before you can use it.

## Limitations

The following limitations apply to governance policy templates:

| Limit | Value |
| --- | --- |
| Maximum number of multitenant applications per template | 10 |
| Maximum number of permissions per multitenant application | 100 |
| Maximum number of role assignments per template | 10 |