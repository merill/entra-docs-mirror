---
layout: Conceptual
title: 'Microsoft Entra Connect: Select your installation type - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-select-installation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic walks you through how to select the installation type to use for Microsoft Entra Connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 33d00970-45db-9781-259b-c0974fd7474a
document_version_independent_id: 7daad9eb-fe4f-6863-fbbf-ebedbf265053
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-install-select-installation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-install-select-installation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-install-select-installation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 9e1206c9-258d-9c13-5484-84404f7f5037
---

# Microsoft Entra Connect: Select your installation type - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect has two installation types for new installation: Express and customized. This article helps you to decide which option to use during installation.

## Express

Express is the most common option and is used by about 90% of all new installations. It was designed to provide a configuration that works for the most common customer scenarios.

It assumes:

- You have a single Active Directory forest on-premises.
- You have an enterprise administrator account you can use for the installation.
- You have less than 100,000 objects in your on-premises Active Directory.

You get:

- [Password hash synchronization](how-to-connect-password-hash-synchronization) from on-premises to Microsoft Entra ID for single sign-on.
- A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](concept-azure-ad-connect-sync-default-configuration).
- Synchronization of all eligible objects in all domains and all OUs.
- [Automatic upgrade](how-to-connect-install-automatic-upgrade) is enabled to make sure you always use the latest available version.

Options where you can still use Express:

- If you don't want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...**\*. Then run the installation wizard again and change the OUs in [configuration options](how-to-connect-installation-wizard#customize-synchronization-options) and enable scheduled sync.
- You want to enable one of the features in Microsoft Entra ID P1 or P2, such as Password writeback. First go through express to get the initial installation completed. Then run the installation wizard again and change the [configuration options](how-to-connect-installation-wizard#customize-synchronization-options).

## Custom

The customized path allows many more options than express. It should be used in all cases where the configuration described in previous section for express is not representative for your organization.

Use when:

- You don't have access to an enterprise admin account in Active Directory.
- You have more than one forest or you plan to synchronize more than one forest in the future.
- You have domains in your forest not reachable from the Connect server.
- You plan to use federation or pass-through authentication for user sign-in.
- You have more than 100,000 objects and need to use a full SQL Server.
- You plan to use group-based filtering and not only domain or OU-based filtering.

## Upgrade from DirSync

If you're currently using DirSync, then follow the steps in [Upgrade from DirSync](how-to-dirsync-upgrade-get-started) to upgrade your existing configuration. There are two different upgrade options:

- In-place upgrade to install Connect on the same server.
- Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.

## Upgrade from Azure AD Sync

If you're currently using Azure AD Sync, then you can follow the [same steps](how-to-upgrade-previous-version) as when you upgrade from one Connect version to a newer. There are two different upgrade options:

- In-place upgrade to install Connect on the same server.
- Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.

## Migrate from MIM

If you're currently using Microsoft Identity Manager 2016 with the Microsoft Entra Connector, then your only option is a migration. Follow the steps described in [swing-migration](how-to-upgrade-previous-version#swing-migration). In the steps, replace any mention of Azure AD Sync with MIM 2016.