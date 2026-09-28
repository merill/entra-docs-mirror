---
layout: Conceptual
title: 'Microsoft Entra Connect: Troubleshoot Source Anchor Issues during Installation - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-connect-source-anchor
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic provides steps for how to troubleshoot issues with the source anchor during installation.
ms.topic: troubleshooting
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: ca3f3048-be85-7ae5-327b-1f1304e7a21f
document_version_independent_id: d5533fb1-802e-577f-0dc1-e057fdb1297f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-connect-source-anchor.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-connect-source-anchor
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-connect-source-anchor.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 565876c1-0da6-95c1-8e4b-a52c2fff8617
---

# Microsoft Entra Connect: Troubleshoot Source Anchor Issues during Installation - Microsoft Entra ID | Microsoft Learn

This article explains the different source anchor related issues that may occur during installation and offers ways to resolve these issues.

## Invalid Source Anchor in Microsoft Entra ID

### Custom Installation

During custom installation, Microsoft Entra Connect reads the source anchor policy from Microsoft Entra ID. If the policy exists in Microsoft Entra ID, Microsoft Entra Connect applies it unless the customer overrides it. The wizard informs you which attribute is read. Additionally, the wizard warns if you try to override the source anchor policy.

During this read operation, it's possible that the source anchor policy in Microsoft Entra ID is unexpected. In this case, Microsoft Entra Connect doesn't know what the source anchor to use and needs manual override.![Screenshot that shows where to manually override the source anchor.](media/tshoot-connect-source-anchor/source1.png)

To resolve this issue, you can manually override the source anchor by selecting a specific attribute. Proceed with this option if and only if you're certain of which attribute to select. If you're not certain, contact [Microsoft support](https://support.microsoft.com/contactus/) for guidance. If you change the source anchor policy, it can break the association between your on-premises users and their associated Azure resources.![Screenshot that shows the specified attribute that overrides the source anchor.](media/tshoot-connect-source-anchor/source2.png)

### Express Installation

During express installation, Microsoft Entra Connect reads the source anchor policy from Microsoft Entra ID. If the policy exists in Microsoft Entra ID, Microsoft Entra Connect applies the same policy. There's no option for a manual override.

During this read operation, it's possible that the source anchor policy in Microsoft Entra ID is unexpected. In this case, Microsoft Entra Connect doesn't know what the source anchor should be.![Screenshot that shows what happens when the source anchor in Microsoft Entra ID is unexpected.](media/tshoot-connect-source-anchor/source3.png)

To resolve this issue, you need to reinstall using the custom mode and manually override the source anchor by selecting a specific attribute. Proceed with this option if and only if you're certain of which attribute to select. If you're not certain, contact [Microsoft support](https://support.microsoft.com/contactus/) for guidance. If you change the source anchor policy, it can break the association between your on-premises users and their associated Azure resources.

### Invalid Source Anchor in Sync Engine

During installation, it's possible Microsoft Entra Connect attempts to configure the sync engine using an invalid source anchor. This operation is most likely a product issue and the installation of Microsoft Entra Connect fails. Contact [Microsoft support](https://support.microsoft.com/contactus/) if you run in to this issue.![unexpected](media/tshoot-connect-source-anchor/source4.png)