---
layout: Conceptual
title: Change the Microsoft Entra Connector account password - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-azureadaccount
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic documents how to restore the Microsoft Entra Connector account.
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: has-adal-ref, sfi-ga-nochange
locale: en-us
document_id: 101c9adb-b728-e73d-369d-fc69bf9c2672
document_version_independent_id: d3380cfe-d76e-5147-9c49-0ea0c3c6bfc5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-azureadaccount.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-azureadaccount
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-azureadaccount.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ed196a4d-0bba-98b9-ed8a-9b877c290804
---

# Change the Microsoft Entra Connector account password - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra Connector account is supposed to be service free. If you need to reset its credentials, then this topic is for you.

## Reset the credentials

If the Microsoft Entra Connector account cannot contact Microsoft Entra ID due to authentication problems, the password can be reset.

1. Sign in to the Microsoft Entra Connect Sync server and open PowerShell.
2. To provide the Microsoft Entra Global Administrator credentials, run `$credential = Get-Credential`.
3. Run the cmdlet `Add-ADSyncAADServiceAccount -AADCredential $credential`.

    If the cmdlet is successful, the PowerShell command prompt appears.

The cmdlet resets the password for the service account and updates it both in Microsoft Entra ID and the sync engine.

## Known issues these steps can solve

This section is a list of errors reported by customers that were fixed by a credentials reset on the Microsoft Entra Connector account.

Event 6900 The server encountered an unexpected error while processing a password change notification: AADSTS70002: Error validating credentials. AADSTS50054: Old password is used for authentication.

Event 659 Error while retrieving password policy sync configuration. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException: AADSTS70002: Error validating credentials. AADSTS50054: Old password is used for authentication.