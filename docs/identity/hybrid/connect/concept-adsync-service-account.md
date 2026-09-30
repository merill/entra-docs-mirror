---
layout: Conceptual
title: 'Microsoft Entra Connect: ADSync service account - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/concept-adsync-service-account
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes the ADSync service account and provides best practices regarding the account.
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5b4b90fc-4d34-6c97-985d-4e8c7af69b57
document_version_independent_id: 2b30436a-cb0d-aaa1-dbb4-018797ab9692
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/concept-adsync-service-account.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/concept-adsync-service-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/concept-adsync-service-account.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: fcdfaf4e-641e-1fe9-7b49-c097e3a6413d
---

# Microsoft Entra Connect: ADSync service account - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect installs an on-premises service which orchestrates synchronization between Active Directory and Microsoft Entra ID. The Microsoft Entra ID Sync synchronization service (ADSync) runs on a server in your on-premises environment. The credentials for the service are set by default in the Express installations but may be customized to meet your organizational security requirements. These credentials aren't used to connect to your on-premises forests or Microsoft Entra ID.

Choosing the ADSync service account is an important planning decision to make before installing Microsoft Entra Connect. Any attempt to change the credentials after installation will result in the service failing to start, losing access to the synchronization database, and failing to authenticate with your connected directories (Azure and AD DS). No synchronization occurs until the original credentials are restored.

The sync service can run under different accounts. It can run under a Virtual Service Account (VSA), a Managed Service Account (gMSA/sMSA), or a regular User Account. The supported options were changed with the 2017 April release and 2021 March release of Microsoft Entra Connect when you do a fresh installation. If you upgrade from an earlier release of Microsoft Entra Connect, these additional options aren't available.

| Type of account | Installation option | Description |
| --- | --- | --- |
| Virtual Service Account | Express and custom, 2017 April and later | A Virtual Service Account is used for all express installations, except for installations on a Domain Controller. When using custom installation, it's the default option unless another option is used. |
| Group Managed Service Account (gMSA) | Custom, 2017 April and later | If you use a remote SQL Server, then we recommend using a group Managed Service Account. |
| Standalone Managed Service Account (sMSA) | Express and custom, 2021 March and later | A standalone Managed Service Account prefixed with ADSyncMSA\_ is created during installation for express installations when installed on a Domain Controller. When using custom installation, it's the default option unless another option is used. |
| User Account | Express and custom, 2017 April to 2021 March | A User Account prefixed with AAD\_ is created during installation for express installations when installed on a Domain Controller. When using custom installation, it's the default option unless another option is used. |
| User Account | Express and custom, 2017 March and earlier | A User Account prefixed with AAD\_ is created during installation for express installations. When using custom installation, another account can be specified. |

Important

If you use Connect with a build from 2017 March or earlier, then you should not reset the password on the service account since Windows destroys the encryption keys for security reasons. You can't change the account to any other account without reinstalling Microsoft Entra Connect. If you upgrade to a build from 2017 April or later, then it's supported to change the password on the service account, but you can't change the account used.

Important

You can only set the service account on first installation. It isn't supported to change the service account after the installation has been completed. If you need to change the service account password, this is supported and instructions can be found [here](how-to-connect-sync-change-serviceacct-pass).

The following is a table of the default, recommended, and supported options for the sync service account.

Legend:

- **Bold** indicates the default option and, in most cases, the recommended option.
- *Italic* indicates the recommended option when it's not the default option.
- Non-bold - Supported option
- Local account - Local user account on the server
- Domain account - Domain user account
- sMSA - [standalone Managed Service account](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548356%28v=ws.10%29)
- gMSA - [group managed service account](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831782%28v=ws.11%29)

| Machine type | **LocalDB Express** | **LocalDB/LocalSQL Custom** | **Remote SQL Custom** |
| --- | --- | --- | --- |
| **domain-joined machine** | **VSA** | **VSA***sMSA* *gMSA* Local account Domain account | *gMSA*Domain account |
| Domain Controller | **sMSA** | **sMSA***gMSA* Domain account | *gMSA*Domain account |

## Virtual Service Account

A Virtual Service Account is a special type of managed local account that doesn't have a password and is automatically managed by Windows.

![Virtual service account](media/concept-adsync-service-account/account-1.png)

The Virtual Service Account is intended to be used with scenarios where the sync engine and SQL are on the same server. If you use remote SQL, then we recommend using a group managed service account instead.

The Virtual Service Account can't be used on a Domain Controller due to [Windows Data Protection API (DPAPI)](/en-us/previous-versions/ms995355%28v=msdn.10%29) issues.

## Managed Service Account

If you use a remote SQL Server, then we recommend to using a group managed service account. For more information on how to prepare your Active Directory for group managed service account, see [Group Managed Service Accounts Overview](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831782%28v=ws.11%29).

To use this option, on the [Install required components](how-to-connect-install-custom#install-required-components) page, select **Use an existing service account**, and select **Managed Service Account**.

![managed service account](media/concept-adsync-service-account/account-2.png)

It's also supported to use a standalone managed service account. However, these can only be used on the local machine and there's no benefit to using them over the default Virtual Service Account.

### Auto-generated standalone Managed Service Account

If you install Microsoft Entra Connect on a Domain Controller, a standalone Managed Service Account is created by the installation wizard (unless you specify the account to use in custom settings). The account is prefixed **ADSyncMSA\_** and used for the actual sync service to run as.

This account is a managed domain account that doesn't have a password and is automatically managed by Windows.

This account is intended to be used with scenarios where the sync engine and SQL are on the Domain Controller.

## User Account

The installation wizard creates a local service account (unless you specify the account to use in custom settings). The account is prefixed AAD\_ and used for the actual sync service to run as. If you install Microsoft Entra Connect on a Domain Controller, the account is created in the domain. The AAD\_ service account must be located in the domain if:

- You use a remote server running SQL Server
- You use a proxy that requires authentication

![user account](media/concept-adsync-service-account/account-3.png)

The account is created with a long complex password that doesn't expire.

This account is used to store passwords for the other accounts in a secure way. These other accounts passwords are stored encrypted in the database. The private keys for the encryption keys are protected with the cryptographic services secret-key encryption using Windows Data Protection API (DPAPI).

If you use a full SQL Server, then the service account is the DBO of the created database for the sync engine. The service won't function as intended with any other permission. A SQL sign-in is also created.

The account is also granted permission to files, registry keys, and other objects related to the Sync Engine.