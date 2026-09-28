---
layout: Conceptual
title: What is password hash synchronization with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-phs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Describes password hash synchronization.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: e19175c5-1af9-a7be-71b4-adbe2faa1438
document_version_independent_id: 438ce820-a2c7-a1f2-08d4-29e1b980e4d0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/whatis-phs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/whatis-phs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/whatis-phs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: e577f518-7740-2cf1-474a-b615a4bbc496
---

# What is password hash synchronization with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

Password hash synchronization is one of the sign-in methods used to accomplish hybrid identity. Microsoft Entra Connect synchronizes a hash of a user's password from an on-premises Active Directory instance to a cloud-based Microsoft Entra instance.

Password hash synchronization is an extension to the directory synchronization feature implemented by Microsoft Entra Connect Sync. You can use this feature to sign in to Microsoft Entra services like Microsoft 365. You sign in to the service by using the same password you use to sign in to your on-premises Active Directory instance.

![What is Microsoft Entra Connect](media/how-to-connect-password-hash-synchronization/arch1.png)

Password hash synchronization helps by reducing the number of passwords, your users need to maintain to just one. Password hash synchronization can:

- Improve the productivity of your users.
- Reduce your helpdesk costs.

Password Hash Sync also enables [leaked credential detection](../../../id-protection/concept-identity-protection-risks#leaked-credentials) for your hybrid accounts. Microsoft works alongside dark web researchers and law enforcement agencies to find publicly available username/password pairs. If any of these pairs match those of our users, the associated account is moved to high risk.

Note

Only new leaked credentials found after you enable PHS will be processed against your tenant. Verifying against previously found credential pairs is not performed.

Optionally, you can set up password hash synchronization as a backup if you decide to use [Federation with Active Directory Federation Services (AD FS)](how-to-connect-fed-whatis) as your sign-in method.

To use password hash synchronization in your environment, you need to:

- Install the Microsoft Entra Cloud Sync agent.
- Configure directory synchronization between your on-premises Active Directory instance and your Microsoft Entra instance.
- Enable password hash synchronization.

For more information, see [What is hybrid identity?](../whatis-hybrid-identity).