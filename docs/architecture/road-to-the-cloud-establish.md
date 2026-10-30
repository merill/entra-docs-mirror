---
layout: Conceptual
title: Road to the cloud - Establish a footprint for moving identity and access management from Active Directory to Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/road-to-the-cloud-establish
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Establish a Microsoft Entra footprint as part of planning your migration of IAM from Active Directory to Microsoft Entra ID.
documentationCenter: ''
ms.topic: how-to
ms.date: 2023-07-27T00:00:00.0000000Z
ms.custom: references_regions
ms.subservice: architecture
locale: en-us
document_id: bb73f61f-9e6f-39f9-44ae-5f11302d2a4c
document_version_independent_id: 59b1806b-6e32-0dab-becf-3134f4152a66
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/road-to-the-cloud-establish.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/road-to-the-cloud-establish
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/road-to-the-cloud-establish.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: edd5f7a0-f205-8a70-66a1-f11d65b04db2
---

# Road to the cloud - Establish a footprint for moving identity and access management from Active Directory to Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Before you migrate identity and access management (IAM) from Active Directory to Microsoft Entra ID, you need to set up Microsoft Entra ID.

## Required tasks

If you're using Microsoft Office 365, Exchange Online, or Teams, then you're already using Microsoft Entra ID. Your next step is to establish more Microsoft Entra capabilities:

- Establish hybrid identity synchronization between Active Directory and Microsoft Entra ID by using [Microsoft Entra Connect](../identity/hybrid/connect/whatis-azure-ad-connect) or [Microsoft Entra Connect cloud sync](../identity/hybrid/cloud-sync/what-is-cloud-sync).
- [Select authentication methods](../identity/hybrid/connect/choose-ad-authn). We strongly recommend password hash synchronization.
- Secure your hybrid identity infrastructure by following [Five steps to securing your identity infrastructure](/en-us/azure/security/fundamentals/steps-secure-identity).

## Optional tasks

The following functions aren't specific or mandatory to move from Active Directory to Microsoft Entra ID, but we recommend incorporating them into your environment. These items are also recommended in the [Zero Trust](/en-us/security/zero-trust/) guidance.

### Deploy passwordless authentication

In addition to the security benefits of [passwordless credentials](../identity/authentication/concept-authentication-passkeys-fido2), passwordless authentication simplifies your environment because the management and registration experience is already native to the cloud. Microsoft Entra ID provides passwordless credentials that align with various use cases. Use the information in this article to plan your deployment: [Plan a passwordless authentication deployment in Microsoft Entra ID](../identity/authentication/howto-authentication-passwordless-deployment).

After you roll out passwordless credentials to your users, consider reducing the use of password credentials. You can use the [reporting and insights dashboard](../identity/authentication/howto-authentication-methods-activity) to continue to drive the use of passwordless credentials and reduce the use of passwords in Microsoft Entra ID.

Important

During your application discovery, you might find applications that have a dependency or assumptions around passwords. Users of these applications need to have access to their passwords until those applications are updated or migrated.

### Configure Microsoft Entra hybrid join for existing Windows clients

You can configure Microsoft Entra hybrid join for existing Active Directory-joined Windows clients to benefit from cloud-based security features such as [co-management](/en-us/mem/configmgr/comanage/overview), Conditional Access, and Windows Hello for Business. New devices should be Microsoft Entra joined and not Microsoft Entra hybrid joined.

To learn more, check [Plan your Microsoft Entra hybrid join implementation](../identity/devices/hybrid-join-plan).