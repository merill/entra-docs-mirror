---
layout: Conceptual
title: Prerequisites for integrating with Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/prerequisites
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the prerequisites required to integrate with Active Directory.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-09-29T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 1b00cc74-b597-6e6e-743a-41258116e933
document_version_independent_id: c45d73b7-82ec-a96b-9399-9e99decce825
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/prerequisites.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/prerequisites.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: fed30ed3-0f0c-f1ba-83bf-3e476bc5d0b8
---

# Prerequisites for integrating with Active Directory - Microsoft Entra ID | Microsoft Learn

The following document provides the prerequisites for integrating with Active Directory.

## Cloud sync

### Hardware and software

| Requirement | Description and more requirements |
| --- | --- |
| Windows Server 2022, Windows Server 2019, or Windows Server 2016 | • 4-GB RAM or more• .NET 4.7.1 runtime or greater• domain-joined• PowerShell execution policy set to **Undefined** or **RemoteSigned**• TLS 1.2 enabled |
| Active Directory | • On-premises AD that has a forest functional level 2003 or higher |
| Microsoft Entra tenant | • A tenant in Azure that's used to synchronize from on-premises |

For more information on the cloud sync prerequisites, see [Cloud sync prerequisites](cloud-sync/how-to-prerequisites).

### Accounts

| Requirement | Description and more requirements |
| --- | --- |
| Domain/Enterprise administrator | Required to install the agent on the server and create the gMSA service account. |
| Hybrid Identity Administrator | Required to configure cloud sync. This account can't be a guest account. |
| gMSA service account | Required to run the agent. |

For more information on the cloud sync accounts, and how to set up a custom gMSA account, see [Cloud sync prerequisites](cloud-sync/how-to-prerequisites).

## Microsoft Entra Connect

### Hardware and software

| Requirement | Description and more requirements |
| --- | --- |
| Windows Server 2022, Windows Server 2019, and Windows Server 2016 | • 4-GB RAM or more• .NET 4.6.2 runtime or greater• domain-joined• PowerShell execution policy set to **RemoteSigned**• TLS 1.2 enabled• if federation is being used, the AD FS severs must be Windows Server 2012 R2 or higher and TLS/SSL certificates must be configured. |
| Active Directory | • On-premises AD that has a forest functional level 2003 or higher• a writeable domain controller |
| Microsoft Entra tenant | • A tenant in Azure used to synchronize from on-premises |
| SQL Server | Microsoft Entra Connect requires a SQL Server database to store identity data. By default, a SQL Server 2019 Express LocalDB (a light version of SQL Server Express) is installed. For more information on using a SQL server, see [Microsoft Entra Connect SQL server requirements](connect/how-to-connect-install-prerequisites#sql-server-used-by-azure-ad-connect) |

For more information on the cloud sync prerequisites, see [Microsoft Entra Connect prerequisites](connect/how-to-connect-install-prerequisites).

### Accounts

| Requirement | Description and more requirements |
| --- | --- |
| Enterprise administrator | Required to install Microsoft Entra Connect. |
| Hybrid Identity Administrator | Required to configure cloud sync. This account can't be a guest account. This account must be a school or organization account and can't be a Microsoft account. |
| Custom settings | If you use the custom settings installation path, you have more options. You can specify the following information:• [AD DS Connector account](connect/reference-connect-accounts-permissions)• [ADSync Service account](connect/reference-connect-accounts-permissions)• [Microsoft Entra Connector account](connect/reference-connect-accounts-permissions). For more information, see [Custom installation settings](connect/reference-connect-accounts-permissions#custom-settings). |

For more information on the Microsoft Entra Connect accounts, see [Microsoft Entra Connect: Accounts and permissions](connect/reference-connect-accounts-permissions).