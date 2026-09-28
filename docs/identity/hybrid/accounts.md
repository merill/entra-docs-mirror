---
layout: Conceptual
title: Accounts for integrating with Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the required accounts for each of the synchronization tools.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 7c4dca19-ce85-d3dc-f3e2-3d0f3d52874b
document_version_independent_id: 3c660665-d507-ed79-5d63-161666cf721e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: fe18f4ba-2bab-1ac2-bf49-ff130f978583
---

# Accounts for integrating with Active Directory - Microsoft Entra ID | Microsoft Learn

The following article describes the accounts that are required for each of the two synchronization tools. Use these sections as a reference when configuring and setting up your environment.

## Accounts for installing and running cloud sync

| Requirement | Description and more requirements |
| --- | --- |
| Domain/Enterprise administrator | Required to install the agent on the server and create the gMSA service account. |
| Hybrid Identity Administrator | Required to configure cloud sync. This account cannot be a guest account. |
| gMSA service account | Required to run the agent. |

For more information, on cloud sync accounts, and how to set up a custom gMSA account, see [Cloud sync prerequisites](cloud-sync/how-to-prerequisites).

## Accounts for installing and running Microsoft Entra Connect

Microsoft Entra Connect uses three accounts to *synchronize information* from on-premises Windows Server Active Directory (Windows Server AD) to Microsoft Entra ID:

| Requirement | Description and additional requirements |
| --- | --- |
| AD DS Connector account | Used to read and write information to Windows Server AD by using Active Directory Domain Services (AD DS). |
| ADSync service account | Used to run the sync service and access the SQL Server database. |
| Microsoft Entra Connector account | Used to write information to Microsoft Entra ID. |
| Local Administrator account | The administrator who is installing Microsoft Entra Connect and who has local Administrator permissions on the computer. |
| AD DS Enterprise Administrator account | Optionally used to create the required AD DS Connector account. |
| Hybrid Identity Administrator | Used to create the Microsoft Entra Connector account and to configure Microsoft Entra ID. You can view Hybrid Identity Administrator accounts in the [Microsoft Entra admin center](https://entra.microsoft.com). See [List Microsoft Entra role assignments](../role-based-access-control/view-assignments). |
| SQL SA account (optional) | Used to create the ADSync database when you use the full version of SQL Server. The instance of SQL Server can be local or remote to the Microsoft Entra Connect installation. This account can be the same account as the Enterprise Administrator account. |

For more information, on Microsoft Entra Connect accounts, and how to configure them, see [Accounts and permissions](connect/reference-connect-accounts-permissions).