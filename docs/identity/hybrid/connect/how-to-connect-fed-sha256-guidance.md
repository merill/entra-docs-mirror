---
layout: Conceptual
title: Change signature hash algorithm for Microsoft 365 relying party trust - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-fed-sha256-guidance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This page provides guidelines for changing SHA algorithm for federation trust with Microsoft 365.
keywords: SHA1,SHA256,M365,federation,aadconnect,adfs,ad fs,change sha,federation trust,relying party trust
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
locale: en-us
document_id: ff349cdd-7faa-fa4c-e9af-d12b30180a35
document_version_independent_id: fdc9ee32-01ea-ca37-7bf5-500f7f8aa05d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-fed-sha256-guidance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-fed-sha256-guidance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-fed-sha256-guidance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9908e60b-5f2a-88f6-6c35-fabf57271330
---

# Change signature hash algorithm for Microsoft 365 relying party trust - Microsoft Entra ID | Microsoft Learn

## Overview

Active Directory Federation Services (AD FS) signs its tokens to Microsoft Entra ID to ensure that they cannot be tampered with. This signature can be based on SHA1 or SHA256. Microsoft Entra ID now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security. This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.

Note

Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.

## Change the token-signing algorithm

After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Microsoft 365 relying party trust with SHA256. You don't need to make any extra configuration changes, and this change has no impact on your ability to access Microsoft 365 or other Microsoft Entra applications.

### AD FS management console

1. Open the AD FS management console on the primary AD FS server.
2. Expand the AD FS node and click **Relying Party Trusts**.
3. Right-click your Microsoft 365/Azure relying party trust and select **Properties**.
4. Select the **Advanced** tab and select the secure hash algorithm SHA256.
5. Click **OK**.

![SHA256 signing algorithm--MMC](media/how-to-connect-fed-sha256-guidance/mmc.png)

### AD FS PowerShell cmdlets

1. On any AD FS server, open PowerShell under administrator privileges.
2. Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.

    `Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'https://www.w3.org/2001/04/xmldsig-more#rsa-sha256'`

## Also read

- [Repair Microsoft 365 trust with Microsoft Entra Connect](how-to-connect-fed-management#repairthetrust)