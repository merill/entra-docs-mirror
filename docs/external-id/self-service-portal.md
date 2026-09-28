---
layout: Conceptual
title: Self-service sign-up portal for B2B collaboration - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/self-service-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to customize the onboarding workflow for Microsoft Entra B2B users to fit your organization’s needs.
ms.topic: concept-article
ms.date: 2025-04-15T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 8e8716f7-edc3-5715-cd43-149fe6a7e318
document_version_independent_id: e6797ee1-0b48-5b83-ff32-a41acd74e0a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/self-service-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/self-service-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/self-service-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 0d0c78b8-2351-2dc0-a565-bca6babc1e70
---

# Self-service sign-up portal for B2B collaboration - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Customers can do a lot with the built-in features that are exposed through the [Azure portal](https://portal.azure.com) and the [Application Access Panel](https://myapps.microsoft.com) for end users. However, you might need to customize the onboarding workflow for B2B users to fit your organization’s needs.

## Microsoft Entra entitlement management for B2B guest user sign-up

As an inviting organization, you might not know ahead of time who the individual external collaborators are who need access to your resources. You need a way for users from partner companies to sign themselves up with policies that you control. You can use [Microsoft Entra entitlement management](../id-governance/entitlement-management-overview) to configure policies, which [manage access for external users](../id-governance/entitlement-management-external-users#how-access-works-for-external-users). Then users from other organizations can request access, and upon approval be provisioned with guest accounts and assigned to groups, apps, and SharePoint Online sites.

## Microsoft Entra B2B invitation API

Organizations can use the [Microsoft Graph invitation manager API](/en-us/graph/api/resources/invitation) to build their own onboarding experiences for B2B guest users. When you want to offer self-service B2B guest user sign-up, we recommend that you use [Microsoft Entra entitlement management](../id-governance/entitlement-management-overview). But if you want to build your own experience, you can use the [invitation API](/en-us/graph/api/invitation-post?tabs=http) to automatically send your customized invitation email directly to the B2B user, for example. Or your app can use the inviteRedeemUrl returned in the creation response to craft your own invitation (through your communication mechanism of choice) to the invited user.