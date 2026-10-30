---
layout: FAQ
title: Frequently asked questions for Microsoft Entra Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/faq
summary: >
  <p>This article answers frequently asked questions about Microsoft Entra Tenant Governance.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Find answers to common questions about Microsoft Entra Tenant Governance, including discovery, governance relationships, and monitoring
ms.topic: faq
ms.date: 2026-03-17T00:00:00.0000000Z
locale: en-us
document_id: 8eff4261-c85c-c3b8-da19-fc93a9083094
document_version_independent_id: 8eff4261-c85c-c3b8-da19-fc93a9083094
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 8b343e83-7a7b-5816-933b-48fd9c565a3c
---

# Frequently asked questions for Microsoft Entra Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn

This article answers frequently asked questions about Microsoft Entra Tenant Governance.

## General

### Can I manage Tenant Governance with Microsoft Graph APIs?

Yes, a set of Microsoft Graph APIs is available to manage Tenant Governance. For more information, see the [Microsoft Graph API documentation](https://aka.ms/TenantGovernance/MSGraphAPI).

### Are licenses required to use Tenant Governance?

Tenant Governance offers free, basic, and premium capabilities. For a comprehensive list of license requirements per capability, see [Microsoft Entra licensing](../../fundamentals/licensing#microsoft-entra-tenant-governance).

### How does Microsoft Entra Tenant Governance compare to the multitenant organization feature?

Microsoft Entra Tenant Governance and the multitenant organization feature are complementary. Tenant Governance enables tenant discovery, administrative access across tenants, and configuration monitoring within a tenant. The multitenant organization feature enables end-user collaboration across Microsoft Entra tenants within Microsoft 365 services. Within an organization, the list of tenants related by governance relationships remains independent of the list of tenants within a multitenant organization.

## Related tenants

### Do I own all my related tenants?

No. Related tenants don't imply ownership of a discovered tenant. Related tenants represent tenants that have historical or active relationships with your tenant based on discovery signals. The feature provides situational awareness by surfacing tenant connections based on evidence already present across identity, application, and billing systems. This awareness enables organizations to make informed governance decisions.

### What do I do if Tenant Governance shows me a related tenant that I don't recognize?

Start by checking whether the tenant shares your Commerce billing account. A shared billing account often indicates a tenant you might need to govern. Users in that tenant might have permissions to access or modify the billing account, or might have subscriptions paid for under your billing account.

You can also review B2B collaboration signals and multitenant application usage between your tenant and the related tenant. B2B registration and sign-in patterns might reveal interactions you recognize. You might also use email scanning capabilities to detect administration emails about those other tenants. When needed, reach out to the users involved using your organization's communication tools, such as Exchange Online or Teams, to understand why the relationship exists.

### How can I protect my organization if an administrator of another tenant doesn't approve my governance request?

If administrators of another tenant reject or don't respond to your governance request, run a quarantine workflow to protect your organization from actions of the related tenant. Follow the steps in [Quarantine unsanctioned tenants](/en-us/entra/fundamentals/quarantine-unsanctioned-tenants) to block users or applications in the other tenant from accessing your resources. This approach protects the security and privacy of data in your tenant.

Consider cutting off outbound B2B user access or Commerce service provisioning as a test. This action could prompt the other tenant to reconsider your request.

### How does Tenant Governance relate to B2B capabilities?

Some customers use B2B accounts for multitenant administration. This approach requires roles to be assigned per B2B user in every tenant. Granular delegated admin privileges (GDAP) don't replace B2B collaboration features. However, for multitenant administration needs, assigning and maintaining least-privileged permissions is often easier with GDAP accounts in governance relationships.

## Governance relationships

### I'm a Cloud Service Provider (CSP), Managed Service Provider (MSP), or Managed Security Service Provider (MSSP). Can I use these capabilities to manage customer tenants?

Yes. Cloud Solution Providers (CSPs), Managed Service Providers (MSPs), and Managed Security Service Providers (MSSPs) can use Tenant Governance relationships to manage customer tenants.

However, Tenant Governance relationships can't coexist with [GDAP relationships that are configured through Partner Center](/en-us/partner-center/customers/gdap-introduction) between the same two tenants. If you already have a Partner Center GDAP relationship with a customer tenant, you must first remove that Partner Center relationship before creating a Tenant Governance relationship with the same tenant.

### Can governed tenants independently terminate the relationship?

Yes. A governed tenant can always terminate the governance relationship. Administrators in the governing tenant see that the governed tenant terminated the relationship and receive an email notification.

### Does Tenant Governance support multi-tier relationships?

No. Multi-tier relationships aren't currently supported. For example, you can't set up a governance relationship where Tenant A governs Tenant B and Tenant B governs Tenant C. A tenant can't be both a governing and a governed tenant. If the system detects that a relationship setup would break this rule, API calls fail.

### Do governance relationships support PIM?

Yes. Use [PIM for Groups](/en-us/entra/id-governance/privileged-identity-management/concept-pim-for-groups) so that admins activate group membership in the governing tenant before using GDAP access configured in the relationship to manage other tenants. PIM policies configured in the governed tenant and applied to a governing tenant administrator aren't supported.

## Configuration management

### What Microsoft services and resources can I monitor?

Monitor any of over 200 resource types supported by Microsoft tenant configuration APIs. These resources span Microsoft Entra, Intune, Exchange Online, Teams, and Security & Compliance (Defender and Purview). For the full list of supported resource types, see the tenant configuration management documentation: [Entra](/en-us/graph/utcm-entra-resources), [Exchange](/en-us/graph/utcm-exchange-resources), [Intune](/en-us/graph/utcm-intune-resources), [Security and Compliance](/en-us/graph/utcm-securityandcompliance-resources), and [Teams](/en-us/graph/utcm-teams-resources).

### What does a configuration baseline look like, and how do you create one?

A configuration baseline is a declarative JSON representation of the desired tenant configuration state. Author it manually, or generate a starting baseline by using Snapshot APIs to extract the tenant's current configuration and then editing it into the desired state.

### How often do monitors run, and can you control the monitoring frequency?

After you create a monitor, it runs automatically on a periodic basis. The default run interval is every six hours.

### Are there any limits on how large a configuration baseline can be?

A monitor baseline can include up to 200 resource instances. The overall daily limit is 800 resource instances across all monitors in a tenant.

### What happens if I try to monitor or snapshot more resources than allowed?

The new monitor or snapshot job fails during creation. For example, if an existing monitor already uses the full daily quota of 800 resource instances, any attempt to create another monitor fails because it would exceed the limit.

### If the monitoring service detects a configuration drift, how do I fix it?

Use the tool of your choice to update the resource configuration, such as the admin center, PowerShell, or Graph API. The next time the monitor runs, it detects that the resource matches the configuration baseline and automatically marks the drift as no longer active.

### Can I monitor configuration across multiple tenants using the same baseline?

Reuse the same configuration baseline file to create monitors in different tenants. To create a monitor in multiple tenants, or to detect configuration drifts in multiple tenants, sign in to each tenant individually and perform the task in that tenant.

### What happens if multiple monitors define different required states for the same resource?

Both monitors run successfully, but each independently evaluates drift against its own baseline. For example, if monitor 1 expects property A to be `true` and monitor 2 expects property A to be `false`, the monitors report different results. If the actual state is `true`, only monitor 2 reports a drift. Define a single desired state per resource to avoid conflicting baselines.

## Secure tenant creation

### Why do I need to choose a subscription when creating a tenant?

To use the secure add-on tenant creation feature, you need owner or contributor permissions on a Microsoft Customer Agreement (MCA) subscription. The subscription you select is where the system stores the Microsoft Entra ID Free billing asset for the new tenant.

### What is the Microsoft Entra ID Free billing asset?

Microsoft Entra ID Free is a free billing asset that represents your Microsoft Entra tenants within your billing account. This asset demonstrates commercial and legal ownership of the tenant. The Microsoft support team can use it to restore access or securely process sensitive requests. Each billing asset is tied directly to one Microsoft Entra tenant and doesn't expire or get removed unless the tenant is deleted by a Global Administrator. For more information, see [Microsoft Entra ID Free](/en-us/azure/cost-management-billing/manage/microsoft-entra-id-free).

### How are add-on tenants governed?

When a user in your organization creates a new tenant through the secure add-on tenant creation flow in the Microsoft Entra admin center (or through APIs), the system automatically creates a governance relationship. This relationship connects the home (governing) tenant and the add-on (governed) tenant using the default governance policy template. If no default template is defined, no relationship is established.

### Can add-on tenants be created from governed tenants?

Yes. Although multi-tier governance relationships aren't supported, an exception exists for new tenant creation. If your tenant is governed by another tenant, you can still create add-on tenants. Those add-on tenants are then governed by your tenant.