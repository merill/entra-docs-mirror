---
layout: Conceptual
title: 'Microsoft Entra Connect: msExchUserHoldPolicies and cloudMsExchUserHoldPolicies - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-msexchuserholdpolicies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes attribute behavior of the msExchUserHoldPolicies and cloudMsExchUserHoldPolicies attributes
ms.tgt_pltfrm: na
ms.topic: reference
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 9d37dea8-9611-d1a6-a505-596c55464f8f
document_version_independent_id: 01a47298-0196-a1b4-cea8-52740c549b24
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-msexchuserholdpolicies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-msexchuserholdpolicies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-msexchuserholdpolicies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: faa04996-4509-b3a5-e998-58b9e0da8f9e
---

# Microsoft Entra Connect: msExchUserHoldPolicies and cloudMsExchUserHoldPolicies - Microsoft Entra ID | Microsoft Learn

The following reference document describes these attributes used by Exchange and the proper way to edit the default sync rules.

## What are msExchUserHoldPolicies and cloudMsExchUserHoldPolicies?

There are two types of [holds](/en-us/exchange/policy-and-compliance/holds/holds) available for an Exchange Server: Litigation Hold and In-Place Hold. When Litigation Hold is enabled, all mailbox all items are placed on hold. An In-Place Hold is used to preserve only those items that meet the criteria of a search query that you defined by using the In-Place eDiscovery tool.

The MsExchUserHoldPolicies and cloudMsExchUserHoldPolicies attributes allow on-premises AD and Microsoft Entra ID to determine which users are under a hold depending on whether they're using on-premises Exchange or Exchange on-line.

## msExchUserHoldPolicies synchronization flow

By default MsExchUserHoldPolicies are synchronized by Microsoft Entra Connect directly to the msExchUserHoldPolicies attribute in the metaverse and then to the msExchUserHoldPolicies attribute in Microsoft Entra ID

The following tables describe the flow:

Inbound from on-premises Active Directory:

| Active Directory attribute | Attribute name | Flow type | Metaverse attribute | Sync Rule |
| --- | --- | --- | --- | --- |
| On-premises Active Directory | msExchUserHoldPolicies | Direct | msExchUserHoldPolicies | In from AD - User Exchange |

Outbound to Microsoft Entra ID:

| Metaverse attribute | Attribute name | Flow type | Microsoft Entra attribute | Sync Rule |
| --- | --- | --- | --- | --- |
| Microsoft Entra ID | msExchUserHoldPolicies | Direct | msExchUserHoldPolicies | Out to Microsoft Entra ID – UserExchangeOnline |

## cloudMsExchUserHoldPolicies synchronization flow

By default cloudMsExchUserHoldPolicies are synchronized by Microsoft Entra Connect directly to the cloudMsExchUserHoldPolicies attribute in the metaverse. Then, if msExchUserHoldPolicies isn't null in the metaverse, the attribute in flowed out to Active Directory.

The following tables describe the flow:

Inbound from Microsoft Entra ID:

| Active Directory attribute | Attribute name | Flow type | Metaverse attribute | Sync Rule |
| --- | --- | --- | --- | --- |
| On-premises Active Directory | cloudMsExchUserHoldPolicies | Direct | cloudMsExchUserHoldPolicies | In from Microsoft Entra ID - User Exchange |

Outbound to on-premises Active Directory:

| Metaverse attribute | Attribute name | Flow type | Microsoft Entra attribute | Sync Rule |
| --- | --- | --- | --- | --- |
| Microsoft Entra ID | cloudMsExchUserHoldPolicies | IF(NOT NULL) | msExchUserHoldPolicies | Out to AD – UserExchangeOnline |

## Information on the attribute behavior

The msExchangeUserHoldPolicies are a single authority attribute. A single authority attribute can be set on an object (in this case, user object) in the on-premises directory or in the cloud directory. The Start of Authority rules dictate, that if the attribute is synchronized from on-premises, then Microsoft Entra ID won't be allowed to update this attribute.

To allow users to set a hold policy on a user object in the cloud, the cloudMSExchangeUserHoldPolicies attribute is used. This attribute is used because Microsoft Entra ID can't set msExchangeUserHoldPolicies directly based on the rules explained above. This attribute will then synchronize back to the on-premises directory if, the msExchangeUserHoldPolicies isn't null and replace the current value of msExchangeUserHoldPolicies.

Under certain circumstances, for instance, if both were changed on-premises and in Azure at the same time, this could cause some issues.