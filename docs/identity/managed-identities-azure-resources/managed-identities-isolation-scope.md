---
layout: Conceptual
title: Isolation Scope For User Assigned Managed Identities - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/managed-identities-isolation-scope
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn about isolation scope for user-assigned managed identities and how it improves security and resilience.
ms.reviewer: arluca
ms.topic: concept-article
ms.date: 2025-07-16T00:00:00.0000000Z
locale: en-us
document_id: ab5e6447-d46a-98c4-0b3a-977eb2b5d192
document_version_independent_id: ab5e6447-d46a-98c4-0b3a-977eb2b5d192
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/managed-identities-isolation-scope.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/managed-identities-isolation-scope
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/managed-identities-isolation-scope.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3f88ba1c-25df-c52b-1845-76578f3842c7
---

# Isolation Scope For User Assigned Managed Identities - Managed identities for Azure resources | Microsoft Learn

You can set your managed identity's isolation scope value to either `None` or `Regional`:

- *None* (default): The identity can be used across all regions
- *Regional*: The identity can only be used by source resources in the same region as the managed identity

Setting the isolation scope to `Regional` ensures that the managed identity usage is tightly scoped and aligned with your security and operational boundaries. Regional isolation for user-assigned managed identities helps improve security and resilience by restricting where managed identities can be used.

## Understand regional isolation

When you're working with managed identities, there are two types of resources:

- **Source resource**: The resource that has the managed identity assigned to it
- **Target resource**: The resource that the source resource accesses using the managed identity

For example, if an App Service needs to access a Storage Account using a managed identity, the App Service is the source resource and the Storage Account is the target resource.

Regional isolation applies to the relationship between the managed identity and the source resource. When you enable regional isolation scope:

- The managed identity can only be assigned to source resources in the same region.
- Source resources can still access target resources in other regions (with proper role permissions). For example, a managed identity assigned to a source resource in West US can be used to access target resources in Spain Central or UAE North.

## Benefits of regional isolation

Regional isolation provides several key benefits:

### Minimizes security exposure

By scoping a managed identity to a single region, you prevent it from being used across regions, reducing the blast radius if the identity is ever compromised. Without isolation, a token issued in one region could be used to access resources in another, increasing the potential impact of credential theft or misuse.

### Enforces least privilege by design

Regional isolation ensures that identities are only granted access to resources in their own region and prevent services from retaining unnecessary privileges by unassigning identities. This helps teams avoid unintentionally granting access to services or data in other regions.

### Contains failures to a single region

If a managed identity is misconfigured or compromised, regional scoping ensures that incidents and outages are contained. Without isolation, a single identity could disrupt services across multiple regions, undermining fault isolation strategies.

### Improves service resilience

Regional scoping limits the reach of outages caused by identity misconfigurations. For example, if a role assignment or token issuance fails in one region, it won't cascade across your global footprint.

### Supports robust disaster recovery

With region-specific identities, you can design independent recovery strategies per region. This avoids scenarios where a global identity becomes a bottleneck or single point of failure during regional failover or recovery.

## Risks of setting isolation scope to none

If the isolation scope property on a user-assigned managed identity isn't set or set to `None` (the default), the identity can be used across all regions. This introduces several risks:

- Cross-region token usage: A token issued in one region could be used to access resources in another, violating data residency or compliance boundaries.
- Unintended access: You might unknowingly assign the identity to resources in multiple regions, leading to broader-than-intended access.
- Harder to audit and troubleshoot: Without isolation, it becomes difficult to trace which resources are using the identity and where, complicating incident response.
- Increased blast radius: A compromised identity could be used to access resources across your entire deployment, not just in one region.

To avoid these risks, set isolation scope to `Regional` when creating a user-assigned managed identity.

## Best practices

To maximize the benefits of regional isolation:

- Use one managed identity per region: Create separate managed identities for each Azure region where your services are deployed
- Match managed identity region to compute resources: Ensure managed identities reside in the same region as their source resources
- Plan for dependencies: Ensure all compute resources sharing a managed identity have access to the same dependencies. These dependencies are the downstream services, resources, or systems that a compute resource (like a VM, Function App, or App Service) needs to access using its managed identity.