---
layout: Conceptual
title: Install Microsoft Entra Connect using SQL delegated administrator permissions - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-sql-delegation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes an update to Microsoft Entra Connect that allows for installation using an account that only has SQL dbo permissions.
ms.reviewer: jparsons
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: d4dde3d5-a312-1994-75de-82e98fdd9267
document_version_independent_id: f9ca1813-94c8-e503-7bf8-526fca466396
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-install-sql-delegation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-install-sql-delegation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-install-sql-delegation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 37cb887d-b37d-8616-237f-e725c7f7a3b3
---

# Install Microsoft Entra Connect using SQL delegated administrator permissions - Microsoft Entra ID | Microsoft Learn

Before the latest Microsoft Entra Connect build, administrative delegation, when deploying configurations that required SQL, wasn't supported. Users who wanted to install Microsoft Entra Connect needed to have server administrator (SA) permissions on the SQL server.

With the latest release of Microsoft Entra Connect, the SQL administrator can now provision the database out of band, and the Microsoft Entra Connect administrator can install it with database owner rights.

## Before you begin

To use this feature, you need to realize that there are several moving parts and each one may involve a different administrator in your organization. The following table summarizes the individual roles and their respective duties in deploying Microsoft Entra Connect with this feature.

| Role | Description |
| --- | --- |
| Domain or Forest AD administrator | Creates the domain level service account that is used by Microsoft Entra Connect to run the sync service. For more information on service accounts, see [Accounts and permissions](reference-connect-accounts-permissions). |
| SQL administrator | Creates the ADSync database and grants login + dbo access to the Microsoft Entra Connect administrator and the service account created by the domain/forest admin. |
| Microsoft Entra Connect administrator | Installs Microsoft Entra Connect and specifies the service account during custom installation. |

## Steps for installing Microsoft Entra Connect using SQL delegated permissions

To provision the database out of band and install Microsoft Entra Connect with database owner permissions, use the following steps.

Note

Although it is not required, it is **highly recommended** that the Latin1\_General\_CI\_AS collation is selected when creating the database.

1. Have the SQL Administrator create the ADSync database with a case insensitive collation sequence **(Latin1\_General\_CI\_AS)**. The recovery model, compatibility level, and containment type are updated to the correct values when Microsoft Entra Connect is installed. However, the SQL Administrator must set the collation sequence correctly. Otherwise, Microsoft Entra Connect blocks the installation. To recover the SA must delete and recreate the database.

    ![Collation](media/how-to-connect-install-sql-delegation/sql4.png)
2. Grant the Microsoft Entra Connect administrator and the domain service account the following permissions:

    - SQL sign-in
    - **database owner(dbo)** rights.

    ![Permissions](media/how-to-connect-install-sql-delegation/sql3a.png)

    Note

    Microsoft Entra Connect does not support logins with a nested membership. This means your Microsoft Entra Connect administrator account and domain service account must be linked to a login that is granted dbo rights. It cannot simply be the member of a group that is assigned to a login with dbo rights.
3. Send an email to the Microsoft Entra Connect administrator indicating the SQL server and instance name that should be used when installing Microsoft Entra Connect.

## Additional information

Once the database is provisioned, the Microsoft Entra Connect administrator can install and configure on-premises synchronization at their convenience.

In case the SQL Administrator has restored ADSync database from a previous Microsoft Entra Connect backup, you need to install the new Microsoft Entra Connect server by using an existing database. For more information on installing Microsoft Entra Connect with an existing database, see [Install Microsoft Entra Connect using an existing ADSync database](how-to-connect-install-existing-database).