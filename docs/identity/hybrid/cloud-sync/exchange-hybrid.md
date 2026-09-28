---
layout: Conceptual
title: Exchange hybrid writeback with cloud sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/exchange-hybrid
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to enable exchange hybrid writeback scenarios.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2026-08-25T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 56a864a4-0822-243d-17b3-a2c58b1eac7d
document_version_independent_id: d6fcd9de-3fab-d451-a3be-5316c6621e27
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/exchange-hybrid.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/exchange-hybrid
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/exchange-hybrid.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e69f8d33-e977-8ea9-351f-bfaec72799ae
---

# Exchange hybrid writeback with cloud sync - Microsoft Entra ID | Microsoft Learn

An Exchange hybrid deployment offers organizations the ability to extend the feature-rich experience and administrative control they have with their existing on-premises Microsoft Exchange organization to the cloud. A hybrid deployment provides the seamless look and feel of a single Exchange organization between an on-premises Exchange organization and Exchange Online.

[![Conceptual image of exchange hybrid scenario.](media/exchange-hybrid/exchange-hybrid.png)](media/exchange-hybrid/exchange-hybrid.png#lightbox)

This scenario is now supported in cloud sync. Cloud sync detects the Exchange on-premises schema attributes and then "writes back" the exchange on-line attributes to your on-premises AD environment.

For more information on Exchange Hybrid deployments, see [Exchange Hybrid](/en-us/exchange/exchange-hybrid).

## Prerequisites

Before deploying Exchange Hybrid with cloud sync, you must meet the following prerequisites.

- The [provisioning agent](what-is-provisioning-agent) must be version 1.1.1107.0 or later.
- Your on-premises Active Directory must be extended to contain the Exchange schema.
    - To extend your schema for Exchange see [Prepare Active Directory and domains for Exchange Server](/en-us/exchange/plan-and-deploy/prepare-ad-and-domains?view=exchserver-2019&amp;preserve-view=true)

    Note

    If your schema has been extended after you have installed the provisioning agent, you will need to restart it in order to pick up the schema changes.

## How to enable

Exchange Hybrid Writeback is disabled by default.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Select on an existing configuration.
2. At the top, select **Properties**. You should see Exchange hybrid writeback disabled.
3. Select the pencil next to **Basic**. [![Screenshot of the basic properties.](media/exchange-hybrid/exchange-hybrid-1.png)](media/exchange-hybrid/exchange-hybrid-1.png#lightbox)
4. On the right, place a check in **Exchange hybrid writeback** and select **Apply**. [![Screenshot of enabling Exchange writeback.](media/exchange-hybrid/exchange-hybrid-2.png)](media/exchange-hybrid/exchange-hybrid-2.png#lightbox)

Note

If the checkbox for **Exchange hybrid writeback** is disabled, it means that the schema has not been detected. Verify that the prerequisites are met and that you have re-started the provisioning agent.

## Attributes synchronized

Cloud sync writes Exchange Online attributes back to users in order to enable Exchange hybrid scenarios.

### Entra2ADExchangeOnlineAttributeWriteback (LES Writeback)

For the Exchange Online-authoritative attribute writeback (LES Writeback) scenario, see [Cloud-based management of Exchange attributes for Remote Mailboxes in hybrid environments](/en-us/exchange/hybrid-deployment/enable-exchange-attributes-cloud-management).

In this scenario, Exchange Online is the source of truth for specific Exchange-related user attributes, and cloud sync writes those cloud-managed attributes back to your on-premises Active Directory.

This differs from **Exchange hybrid writeback** (AAD2ADExchangeHybridWriteback), which follows the hybrid writeback template used in preview scenarios.

The following table lists the supported attributes and the mappings for LES Writeback.

| Microsoft Entra attribute | AD attribute | Object Class | Mapping Type |
| --- | --- | --- | --- |
| cloudAnchor | msDS-ExternalDirectoryObjectId | User, InetOrgPerson | Direct |
| cloudLegacyExchangeDN | proxyAddresses | User, Contact, InetOrgPerson | Expression |
| cloudMSExchArchiveStatus | msExchArchiveStatus | User, InetOrgPerson | Direct |
| cloudMSExchBlockedSendersHash | msExchBlockedSendersHash | User, InetOrgPerson | Expression |
| cloudMSExchSafeRecipientsHash | msExchSafeRecipientsHash | User, InetOrgPerson | Expression |
| cloudMSExchSafeSendersHash | msExchSafeSendersHash | User, InetOrgPerson | Expression |
| cloudMSExchUCVoiceMailSettings | msExchUCVoiceMailSettings | User, InetOrgPerson | Expression |
| cloudMSExchUserHoldPolicies | msExchUserHoldPolicies | User, InetOrgPerson | Expression |

## Provisioning on-demand

Provisioning on-demand with Exchange hybrid writeback requires two steps. You need to first provision or create the user. Exchange online then populates the necessary attributes on the user. Then cloud sync can then "write back" these attributes to the user. The steps are:

- Provision and sync the initial user - this brings the user into the cloud and allows them to be populated with Exchange online attributes.
- Write back exchange attributes to Active Directory - this writes the Exchange online attributes to the user on-premises.

Provisioning on-demand with Exchange hybrid use the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Enter the distinguished name of a user and select the **Provision** button.
4. A success screen appears with four green check marks.
5. Select **Next**. On the **Writeback exchange attributes to Active Directory** tab, the synchronization starts.
6. You should see the success details. [![Screenshot of Exchange attributes being written back.](media/exchange-hybrid/exchange-hybrid-4.png)](media/exchange-hybrid/exchange-hybrid-4.png#lightbox)

    Note

    This final step may take up to 2 minutes to complete.

## Exchange hybrid writeback using MS Graph

You can use MS Graph API to enable Exchange hybrid writeback. For more information, see [Exchange hybrid writeback with MS Graph](how-to-inbound-synch-ms-graph#exchange-hybrid-writeback-public-preview).