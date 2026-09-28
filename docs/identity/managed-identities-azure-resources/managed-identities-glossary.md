---
layout: Conceptual
title: Managed identities glossary - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/managed-identities-glossary
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: A comprehensive glossary of terms related to managed identities for Azure resources.
ms.reviewer: arluca
ms.topic: reference
ms.date: 2025-08-19T00:00:00.0000000Z
locale: en-us
document_id: 96774ae2-f4a0-7625-7a03-a8bc2f8f5aad
document_version_independent_id: 96774ae2-f4a0-7625-7a03-a8bc2f8f5aad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/managed-identities-glossary.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/managed-identities-glossary
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/managed-identities-glossary.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: e0227ec4-9c3f-9ad8-7f03-8380dff7055c
---

# Managed identities glossary - Managed identities for Azure resources | Microsoft Learn

This glossary defines key terms and concepts related to managed identities for Azure resources and their broader ecosystem.

## A

**Application Object** : The globally unique configuration of an application in Microsoft Entra ID. Managed identities don't have application objects, only service principal objects.

**Azure Instance Metadata Service (IMDS)** : A REST endpoint available to all VMs created through Azure Resource Manager. IMDS provides access to managed identity tokens without requiring credentials.

**Azure Resource Manager** : The deployment and management service for Azure that provides a management layer for creating, updating, and deleting resources.

## C

**Conditional Access for Workload Identities** : Security policies that can be applied to service principals owned by an organization to control access based on conditions like location and risk.

**Continuous Access Evaluation (CAE)** : A feature that provides real-time enforcement of Conditional Access policies and risk signals for workload identities, offering instant revocation capabilities.

**Control Plane** : Management operations performed on Azure resources, such as creating, updating, or deleting resources. Distinct from data plane operations.

**Credential Rotation** : The process of regularly changing authentication credentials. Managed identities handle this automatically with 90-day certificate expiration and 45-day rotation cycles.

## D

**Data Plane** : Operations that interact with the data or functionality provided by a resource, such as reading from a storage account or querying a database.

**Device Identity** : A type of machine identity that represents physical or virtual devices such as desktop computers, mobile devices, or IoT sensors.

## F

**Federated Identity Credential (FIC)** : A configuration that allows a managed identity to be used as a credential on Microsoft Entra applications, enabling workload identity federation.

## H

**Human Identity** : Identities that represent people, including employees, external users, customers, consultants, vendors, and partners.

## I

**Identity** : A directory object that can be authenticated and authorized to access resources. In managed identities context, refers to both human and workload identities.

**Isolation Scope** : A property of user-assigned managed identities that determines whether the identity can be used across regions (None) or only within a single region (Regional).

## L

**Least Privilege** : A security principle that grants users and services only the minimum permissions necessary to perform their functions.

**Lifecycle Management** : The process of managing identities from creation through updates to deletion, including proper cleanup of permissions and resources.

**Long Lived Tokens (LLTs)** : Extended duration access tokens (up to 24 hours) used with Continuous Access Evaluation that are subject to continuous security checks.

## M

**Machine Identity** : Non-human identities that include both device identities and workload identities. Used to distinguish from human identities.

**Managed Identity** : An automatically managed identity in Microsoft Entra ID that provides Azure resources with an identity to authenticate when accessing other resources that support Microsoft Entra authentication.

**Managed Identity Contributor Role** : A built-in Azure role that allows creation, reading, updating, and deleting of user-assigned managed identities.

**Managed Identity Operator Role** : A built-in Azure role that allows reading and assigning user-assigned managed identities to resources.

**Microsoft Authentication Library (MSAL)** : A library that enables applications to acquire tokens from Microsoft Entra ID for accessing protected web APIs.

**Microsoft Entra ID Protection** : A service that detects, investigates, and remediates identity-based risks for both user and workload identities.

## P

**Principal ID** : The unique identifier for a managed identity's service principal in Microsoft Entra ID.

## R

**Regional Isolation** : A security feature that restricts user-assigned managed identities to be used only by resources within the same Azure region.

**Resource ID** : The unique identifier for an Azure resource, following the format `/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/{resource-provider}/{resource-type}/{resource-name}`.

**Role-Based Access Control (RBAC)** : Azure's authorization system that provides fine-grained access management for Azure resources based on role assignments.

## S

**Service Principal** : The local representation of an application object in a specific Microsoft Entra tenant. All managed identities have service principals, but not all service principals are managed identities.

**Source Resource** : In managed identity context, the Azure resource that has the managed identity assigned to it (e.g., a virtual machine or app service).

**System-Assigned Managed Identity** : A managed identity that is created as part of an Azure resource and shares the same lifecycle. When the resource is deleted, the identity is automatically deleted.

## T

**Target Resource** : In managed identity context, the resource that the source resource accesses using the managed identity (e.g., a storage account or key vault).

**Token Endpoint** : The IMDS endpoint that managed identities use to request access tokens for authentication to other Azure services.

## U

**User-Assigned Managed Identity** : A managed identity created as a standalone Azure resource that can be assigned to multiple Azure resources and has an independent lifecycle.

## W

**Workload Identity** : A category of non-human identities that includes applications, service principals, and managed identities. These identities represent software workloads rather than human users.

**Workload Identity Federation** : A feature that allows external identity providers to access Microsoft Entra ID protected resources without needing to manage secrets or certificates.