---
layout: Landing
title: Microsoft Entra Workload ID documentation - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/
summary: Microsoft Entra Workload ID helps you manage and secure identities for digital workloads, such as apps and services.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Learn how to manage and help secure identities for digital workloads, such as apps and services.
ms.date: 2023-03-22T00:00:00.0000000Z
ms.topic: landing-page
locale: en-us
document_id: ff879990-3122-046d-c849-362b06f3efc1
document_version_independent_id: dec56403-0997-61f8-1166-b8f59231bfe3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: landing
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/index.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f233afb4-f511-4877-ab18-c53e36c47c54
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aa758f63-7086-440d-afba-dcb5819f0b6f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 014a9995-007a-905d-10ea-c614960aeec6
---

# Microsoft Entra Workload ID documentation

Microsoft Entra Workload ID helps you manage and secure identities for digital workloads, such as apps and services.

## About workload identities

### Overview

- [What are workload identities?](workload-identities-overview)
- [Frequently asked questions about license plans](workload-identities-faqs)

## Check app health status and mitigate risk

### How-To Guide

- [Remove unused applications](../identity/monitoring-health/recommendation-remove-unused-apps?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)
- [Remove unused credentials from apps](../identity/monitoring-health/recommendation-remove-unused-credential-from-apps?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)
- [Renew expiring application credentials](../identity/monitoring-health/recommendation-renew-expiring-application-credential?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

## Connect workloads without managing secrets

### Overview

- [What is workload identity federation?](workload-identity-federation)

### video

- [Learn why you would use workload identity federation](https://learn-video.azurefd.net/vod/player?id=4b15d772-e6de-4347-b8f6-d943c200667a)

### How-To Guide

- [Configure an app to trust an external identity provider](workload-identity-federation-create-trust)
- [Configure a managed identity to trust an external identity provider](workload-identity-federation-create-trust-user-assigned-managed-identity)

## Enforce best practice for how apps use auth methods

### Overview

- [Application authentication methods API](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

## Secure risky workload identities

### Overview

- [Secure workload identities](../id-protection/concept-workload-identity-risk?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

## Configuring applications to trust managed identities

### How-To Guide

- [Configure an application to trust a managed identity (preview)](workload-identity-federation-config-app-trust-managed-identity)

## Apply Conditional Access policies to service principals

### How-To Guide

- [Conditional Access for workload identities](../identity/conditional-access/workload-identity?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

## Enable real-time enforcement of Conditional Access location and risk policies

### How-To Guide

- [Continuous access evaluation for workload identities](../identity/conditional-access/concept-continuous-access-evaluation-workload?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

## Contain threats and reduce risk to workload identities

### How-To Guide

- [Microsoft Entra ID Protection](../id-protection/concept-workload-identity-risk?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

## Review service principals and applications privileged directory roles

### How-To Guide

- [Access reviews for service principals](../id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)