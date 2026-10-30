---
layout: Conceptual
title: Assignment restriction for managed identities (preview) - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/managed-identities-assignment-restriction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: mmacy-msft
ms.author: marshmacy
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn how assignment restrictions scope a user-assigned managed identity to one or more resource providers to improve security and resilience.
ms.topic: concept-article
ms.custom: msecd-doc-authoring-10012
ms.date: 2026-07-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9d30dcef-2ce5-292f-f486-3d09a952bb7b
document_version_independent_id: 9d30dcef-2ce5-292f-f486-3d09a952bb7b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/managed-identities-assignment-restriction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/managed-identities-assignment-restriction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/managed-identities-assignment-restriction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 83f60fb3-dceb-303f-02ca-fd6be4ee4951
---

# Assignment restriction for managed identities (preview) - Managed identities for Azure resources | Microsoft Learn

Assignment restrictions, also known as resource restrictions, are a security feature for user-assigned managed identities that limit the resource providers an identity can be assigned to. Assignment restrictions are currently in preview. They let you isolate a managed identity to one or more resource providers so that it can't be reused across unrelated services.

When you configure assignment restriction, managed identity usage stays tightly scoped. This scoping reduces the blast radius of a compromised or misconfigured identity and helps improve both security and resilience.

## Understand resource restriction

When you work with user-assigned managed identities, two resource roles are involved:

- **Source resource**: The resource that the managed identity is assigned to.
- **Target resource**: The resource that the source resource accesses by using the managed identity.

For example, if an App Service accesses a Storage Account by using a managed identity, the App Service is the source resource and the Storage Account is the target resource.

Assignment restriction applies to the relationship between the managed identity and the *source resource*. It doesn't apply to the target resource.

If you want a managed identity to be restricted to source resources across multiple resource providers (for example, both `Microsoft.Web` and `Microsoft.ContainerRegistry`), [set resource restrictions](configure-managed-identities-assignment-restriction) that include each allowed resource provider.

## Assignment restriction scope

When assignment restriction is configured for a user-assigned managed identity:

- The identity can only be assigned to source resources that match the allowed resource providers.
- Source resources can still access target resources outside that scope, as long as the appropriate role assignments exist.

This behavior lets services maintain their downstream dependencies while keeping identity assignment tightly controlled.

## Benefits of assignment restriction

Assignment restriction provides the following security and operational benefits.

### Reduced security exposure

Restricting where a managed identity can be assigned prevents the identity from being reused across unrelated resource providers. This restriction limits the blast radius if credentials are misused or compromised.

### Least privilege by design

Assignment restriction prevents accidental or unnecessary identity reuse. Services don't retain permissions beyond their intended scope.

### Failure containment

If a managed identity is misconfigured, disabled, or compromised, the impact is contained to a limited set of resources instead of cascading across multiple resource providers or services.

### Improved service resilience

Scoping identity assignment limits the reach of outages caused by identity or role assignment issues, which helps prevent service-wide failures.

### Operational clarity

Restricting assignment scope simplifies auditing, troubleshooting, and incident response by making identity usage more predictable and traceable.

## Risks of not setting assignment restriction

Note

By default, the assignment restrictions value is blank, which represents an empty array.

If the assignment restriction value is unset or configured as an empty array:

- Managed identities can be assigned across multiple resource providers.
- Identity usage becomes difficult to audit.
- A single identity misconfiguration can result in multi-service or service-wide outages.
- A compromised identity can enable broad, unintended access beyond the original design intent.

## Best practices

Consider the following best practices when you plan assignment restriction for user-assigned managed identities:

- Create separate managed identities per resource provider.
- Match managed identity scope to the intended source resources only.
- Avoid reusing managed identities across unrelated workloads for convenience.

## Supported resource providers and resource types in the Azure portal

Note

Selecting **None** for resource assignment restrictions leaves the identity unrestricted, allowing it to be assigned to resources from any resource provider that supports managed identities.

Configure resource assignment restrictions only when you want to limit identity assignment to specific resource providers. The **Select Resource Types** list in the Azure portal might not include all supported resource providers and resource types.

If the resource provider or resource type you want to configure isn't listed in the **Select Resource Types** pane, use the Azure CLI. For configuration steps and command examples, see [Configure assignment restriction for user-assigned managed identities](configure-managed-identities-assignment-restriction).

Warning

In Azure CLI commands and infrastructure-as-code (IaC) templates, specify the resource provider namespace on its own, for example `Microsoft.Storage`. Don't use `Microsoft.Storage/*`.

The **Select Resource Types** pane in the Azure portal displays a provider-wide selection as `Microsoft.Storage/*`. The `/*` suffix is a portal display convention and isn't part of the value that the API accepts. Even when the portal shows `Microsoft.Storage/*`, use `Microsoft.Storage` in Azure CLI commands and IaC templates. To restrict the identity to a single resource type instead of the whole provider, specify the full resource type, for example `Microsoft.Storage/storageAccounts`.