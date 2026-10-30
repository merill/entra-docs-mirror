---
layout: Conceptual
title: Microsoft Entra B2B in government and national clouds - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/b2b-government-national-clouds
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn what features are available in Microsoft Entra B2B collaboration in US Government and national clouds
ms.topic: concept-article
ms.date: 2025-07-07T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 04526d45-3fb4-ebd6-108f-0a21c53b2e21
document_version_independent_id: 3fbc1e93-9119-a925-c687-ed51d80cbeb2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/b2b-government-national-clouds.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/b2b-government-national-clouds
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/b2b-government-national-clouds.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/653971be-c25b-47ce-b561-80221556af0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f998336e-f087-4bda-99f7-4001451d0bd2
platformId: 284860b5-580c-a805-310a-0a6d79c459f3
---

# Microsoft Entra B2B in government and national clouds - Microsoft Entra External ID | Microsoft Learn

Microsoft Azure [national clouds](../identity-platform/authentication-national-cloud) are physically isolated instances of Azure. B2B collaboration isn't enabled by default across national cloud boundaries, but you can use Microsoft cloud settings to establish mutual B2B collaboration between the following Microsoft Azure clouds:

- Microsoft Azure global cloud and Microsoft Azure Government
- Microsoft Azure global cloud and Microsoft Azure operated by 21Vianet

Organizations with multiple tenants across Microsoft clouds can use [cross-cloud synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview) to automate creating, updating, and deleting B2B users.

## B2B collaboration across Microsoft clouds

To set up B2B collaboration between tenants in different clouds, both tenants need to configure their Microsoft cloud settings to enable collaboration with the other cloud. Then each tenant must configure inbound and outbound cross-tenant access with the tenant in the other cloud. For details, see [Microsoft cloud settings](cross-cloud-settings).

## B2B collaboration within the Microsoft Azure Government cloud

Within the Azure US Government cloud, B2B collaboration is enabled between tenants where:

- Both tenants are within Azure US Government cloud, *and*
- Both tenants support B2B collaboration.

Azure US Government tenants that support B2B collaboration can also collaborate with social users using:

- Microsoft accounts
- Google accounts
- Email one-time passcode accounts

If you invite a user outside of these groups (for example, if the user is in a tenant that isn't part of the Azure US Government cloud or doesn't yet support B2B collaboration), the invitation fails or the user can't redeem the invitation.

For Microsoft accounts, there are known limitations with accessing the Microsoft Entra admin center:

- Newly invited MSA guests are unable to redeem direct link invitations to the Microsoft Entra admin center
- Existing MSA guests are unable to sign in to the Microsoft Entra admin center.

For details about other limitations, see [Microsoft Entra ID P1 and P2 Variations](/en-us/azure/azure-government/compare-azure-government-global-azure#azure-active-directory-premium-p1-and-p2).

### How can I tell if B2B collaboration is available in my Azure US Government tenant?

To find out if your Azure US Government cloud tenant supports B2B collaboration, take the following steps:

1. In a browser, go to the following URL, substituting your tenant name for *&lt;tenantname&gt;*:

    `https://login.microsoftonline.com/<tenantname>/v2.0/.well-known/openid-configuration`
2. Find `"tenant_region_scope"` in the JSON response:

    - If `"tenant_region_scope":"USGOV”` appears, B2B is supported.
    - If `"tenant_region_scope":"USG"` appears, B2B isn't supported.

## B2B collaboration in Microsoft Azure operated by 21Vianet

Microsoft Azure operated by 21Vianet supports the following identity providers for B2B collaboration:

- Microsoft Entra ID
- SAML/WS-Fed

For more information about Microsoft Azure operated by 21Vianet, see [Service availability and roadmaps](/en-us/azure/china/concepts-service-availability).