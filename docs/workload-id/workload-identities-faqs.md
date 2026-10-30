---
layout: Conceptual
title: Frequently asked questions about Microsoft Entra Workload ID - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-faqs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: martinco
description: Learn about Microsoft Entra Workload ID license plans, features, and capabilities.
ms.topic: faq
ms.date: 2025-03-18T00:00:00.0000000Z
ms.reviewer: gasinh
ms.custom: aaddev
locale: en-us
document_id: 0b2ed8dd-72be-b9b1-5a72-509a3c224758
document_version_independent_id: e53694fc-553a-d95b-3aae-e37280dd7263
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identities-faqs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identities-faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identities-faqs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f233afb4-f511-4877-ab18-c53e36c47c54
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aa758f63-7086-440d-afba-dcb5819f0b6f
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 73f129e6-4d16-fa71-45a0-850724701fab
---

# Frequently asked questions about Microsoft Entra Workload ID - Microsoft Entra Workload ID | Microsoft Learn

[Microsoft Entra Workload ID](workload-identities-overview) is available in two editions: **Free** and **Microsoft Entra Workload ID Premium**. The free edition of workload identities is included with a subscription of a commercial online service such as [Azure](https://azure.microsoft.com/) and [Power Platform](https://powerplatform.microsoft.com/). The Workload ID Premium offering is available through a Microsoft representative, the [Open Volume License Program](https://www.microsoft.com/licensing/how-to-buy/how-to-buy), and the [Cloud Solution Providers program](/en-us/azure/lighthouse/concepts/cloud-solution-provider). Azure and Microsoft 365 subscribers can purchase Workload ID Premium online.

For more information, see [what are workload identities?](workload-identities-overview)

Note

Workload ID Premium is a standalone product and isn't included in other premium product plans. All subscribers require a license to use Workload ID Premium features.

Learn more about [Workload ID pricing](https://www.microsoft.com/security/business/identity-access/microsoft-entra-workload-identities#office-StandaloneSKU-k3hubfz).

This document addresses Microsoft Entra Workload ID most frequent customer questions.

[Microsoft Entra Workload ID](workload-identities-overview) (Workload ID Premium) is generally available through a Microsoft representative, the Open Volume License Program, and the Cloud Solution Providers program. Azure and Office 365 subscribers can buy it online. Workload ID Premium is a standalone stock-keeping unit (SKU), $3 per workload identity per month, and not part of another SKU.

The free features come with a subscription for a commercial online service such as Azure, Power Platform, and others. Examples are managed identities and workload identity federation.

## What are Workload ID Premium features, and which are free?

| Capabilities | Description | Free | Premium |
| --- | --- | --- | --- |
| **Authentication and authorization** |  |  |  |
| Create, read, update, and delete workload identities | Create and update identities to secure service to service access | Yes | Yes |
| Access resources by authenticating workload identities and tokens | Use Microsoft Entra ID to protect resource access | Yes | Yes |
| Workload identities sign-in activity and audit trail | Monitor and track workload identity behavior | Yes | Yes |
| **Managed identities** | Use Microsoft Entra identities in Azure without handling credentials | Yes | Yes |
| Workload identity federation | To access Microsoft Entra protected resources, use workloads tested by external identity providers (IdPs) | Yes | Yes |
| **Lifecycle management** |  |  |  |
| Application management policies | IT admins can enforce best practices for how apps are configured | Yes | Yes |
| Access reviews for service provider-assigned privileged roles | Closely monitor workload identities with impactful permissions |  | Yes |
| App Health Recommendations | Identify unused or inactive workload identities and their risk levels. Get remediation guidelines. |  | Yes |
| **Microsoft Entra Conditional Access** |  |  |  |
| Conditional Access policies for workload identities | Define the condition for a workload to access a resource, such as an IP range. Doesn't cover managed identities. |  | Yes |
| **Microsoft Entra ID Protection** |  |  |  |
| ID Protection for workload identities | Detect and remediate compromised workload identities |  | Yes |

## How much is the Workload ID Premium plan?

The [Microsoft Entra Workload ID Premium](https://www.microsoft.com/security/business/identity-access/microsoft-entra-workload-identities#office-StandaloneSKU-k3hubfz) is $3/workload identity/month.

Note

Learn about [Conditional Access for workload identities](../identity/conditional-access/workload-identity).

## How many licenses do I need? Do I need to license all workload identities, including Microsoft applications and managed identities?

Only workload identities eligible for premium features require licensing. License enterprise apps and service principals listed appear in the first category, on the Workload ID landing page, in the Microsoft Entra admin center. To use premium features for a subset of enterprise apps and service principals, procure needed licenses tailored to your requirements. An exception appears if you use [access reviews](../id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review) for managed identities. Obtain licenses based on the number of managed identities in the graph.

You can use Conditional Access for workload identities for single-tenant applications. [ID Protection](../id-protection/concept-workload-identity-risk) protects single and multitenant applications under Enterprise apps/Service Principals. Microsoft apps and managed identities aren't eligible for Conditional Access and ID Protection. Access reviews are applicable for Service Principals assigned to privileged roles, including managed identities. This feature requires Microsoft Entra ID P2 licenses for reviewers, and Workload ID Premium licenses for access review Service Principles.

## How do I purchase a Workload ID Premium plan?

You need a current or new Azure or Microsoft 365 subscription. Sign in to the [Microsoft Microsoft Entra admin center](https://entra.microsoft.com/) with your credentials, then buy Workload ID licenses.

## Do the licenses require individual workload identities assignment?

No, license assignment isn't required. One license in the tenant unlocks all features for all workload identities.

## How can I track licenses assigned to workload identities?

Unfortunately, we don’t provide a dashboard to track that information. You can track enabled Conditional Access policies targeting workload identities in the **Insights and reporting** area.

![Screenshot of the impact summary under Service Principal sign-ins.](media/workload-identities-faqs/insights-and-reportin.png)

## Can I get a free trial of Workload ID Premium?

Yes. You can get a [90-day free trial](https://entra.microsoft.com/#view/Microsoft_Azure_ManagedServiceIdentity/WorkloadIdentitiesBlade). In the Modern channel, a 30-day trial is available. Free trial is unavailable in [Microsoft Azure Government](https://azure.microsoft.com/global-infrastructure/government/) clouds.

## Is the Workload ID Premium plan available on Azure Government clouds?

Yes. For Azure Government cloud customers, contact your account manager.

## Can I have Microsoft Entra ID P1, P2, and Workload ID Premium licenses in one tenant?

Yes, customers can have a mix of licenses in one tenant.