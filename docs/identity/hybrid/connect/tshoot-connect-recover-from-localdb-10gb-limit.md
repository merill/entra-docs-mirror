---
layout: Conceptual
title: 'Microsoft Entra Connect: How to recover from LocalDB 10GB limit issue - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-connect-recover-from-localdb-10gb-limit
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes how to recover Microsoft Entra Connect Synchronization Service when it encounters LocalDB 10GB limit issue.
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: b123ab46-7169-7f3d-9ac8-91ff435c22d5
document_version_independent_id: 49f5b604-5b7a-872b-0e13-30e6a8ebb3dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-connect-recover-from-localdb-10gb-limit.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-connect-recover-from-localdb-10gb-limit
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-connect-recover-from-localdb-10gb-limit.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: efd7d7f0-a94d-6d7c-2f1f-d7e5c3203367
---

# Microsoft Entra Connect: How to recover from LocalDB 10GB limit issue - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect requires a SQL Server database to store identity data. You can either use the default SQL Server 2019 Express LocalDB installed with Microsoft Entra Connect or use your own full SQL. SQL Server Express imposes a 10-GB size limit. When using LocalDB and this limit is reached, Microsoft Entra Connect Synchronization Service can no longer start or synchronize properly. This article provides the recovery steps.

## Symptoms

There are two common symptoms:

- Microsoft Entra Connect Synchronization Service **is running** but fails to synchronize with *“stopped-database-disk-full”* error.
- Microsoft Entra Connect Synchronization Service **is unable to start**. When you attempt to start the service, it fails with event 6323 and error message *"The server encountered an error because SQL Server is out of disk space."*

## Short-term recovery steps

This section provides the steps to reclaim DB space required for Microsoft Entra Connect Synchronization Service to resume operation. The steps include:

1. Determine the Synchronization Service status
2. Shrink the database
3. Delete run history data
4. Shorten retention period for run history data

### Determine the Synchronization Service status

First, determine whether the Synchronization Service is still running or not:

1. Log in to your Microsoft Entra Connect server as administrator.
2. Go to **Service Control Manager**.
3. Check the status of **Microsoft Entra ID Sync**.
4. If it is running, do not stop or restart the service. Skip Shrink the database step and go to Delete run history data step.
5. If it is not running, try to start the service. If the service starts successfully, skip Shrink the database step and go to Delete run history data step. Otherwise, continue with Shrink the database step.

### Shrink the database

Use the Shrink operation to free up enough DB space to start the Synchronization Service. It frees up DB space by removing whitespaces in the database. This step is best-effort as it is not guaranteed that you can always recover space. To learn more about Shrink operation, read this article [Shrink a database](/en-us/sql/relational-databases/databases/shrink-a-database).

Important

Skip this step if you can get the Synchronization Service to run. It is not recommended to shrink the SQL DB as it can lead to poor performance due to increased fragmentation.

The name of the database created for Microsoft Entra Connect is **ADSync**. To perform a Shrink operation, you must log in either as the sysadmin or DBO of the database. During Microsoft Entra Connect installation, the following accounts are granted sysadmin rights:

- Local Administrators
- The user account that was used to run Microsoft Entra Connect installation.
- The Sync Service account that is used as the operating context of Microsoft Entra Connect Synchronization Service.
- The local group ADSyncAdmins that was created during installation.

1. Back up the database by copying **ADSync.mdf** and **ADSync\_log.ldf** files located under `%ProgramFiles%\Microsoft Azure AD Sync\Data` to a safe location.
2. Start a new PowerShell session.
3. Navigate to folder `%ProgramFiles%\Microsoft SQL Server\110\Tools\Binn`.
4. Start **sqlcmd** utility by running the command `./SQLCMD.EXE -S "(localdb)\.\ADSync" -U <Username> -P <Password>`, using the credential of a sysadmin or the database DBO.
5. To shrink the database, at the sqlcmd prompt (`1>`), enter `DBCC Shrinkdatabase(ADSync,1);`, followed by `GO` in the next line.
6. If the operation is successful, try to start the Synchronization Service again. If you can start the Synchronization Service, go to Delete run history data step. If not, contact Support.

### Delete run history data

By default, Microsoft Entra Connect retains up to seven days’ worth of run history data. In this step, we delete the run history data to reclaim DB space so that Microsoft Entra Connect Synchronization Service can start syncing again.

1. Start **Synchronization Service Manager** by going to START → Synchronization Service.
2. Go to the **Operations** tab.
3. Under **Actions**, select **Clear Runs**.
4. You can either choose **Clear all runs** or **Clear runs before... &lt;date&gt;** option. It is recommended that you start by clearing run history data that are older than two days. If you continue to run into DB size issue, then choose the **Clear all runs** option.

### Shorten retention period for run history data

This step is to reduce the likelihood of running into the 10-GB limit issue after multiple sync cycles.

1. Open a new PowerShell session.
2. Run `Get-ADSyncScheduler` and take note of the PurgeRunHistoryInterval property, which specifies the current retention period.
3. Run `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` to set the retention period to two days. Adjust the retention period as appropriate.

## Long-term solution – Migrate to full SQL

In general, the issue is indicative that 10-GB database size is no longer sufficient for Microsoft Entra Connect to synchronize your on-premises Active Directory to Microsoft Entra ID. It is recommended that you switch to using the full version of SQL server. You cannot directly replace the LocalDB of an existing Microsoft Entra Connect deployment with the database of the full version of SQL. Instead, you must deploy a new Microsoft Entra Connect server with the full version of SQL. It is recommended that you do a swing migration where the new Microsoft Entra Connect server (with SQL DB) is deployed as a staging server, next to the existing Microsoft Entra Connect server (with LocalDB).

- For instruction on how to configure remote SQL with Microsoft Entra Connect, refer to article [Custom installation of Microsoft Entra Connect](how-to-connect-install-custom).
- For instructions on swing migration for Microsoft Entra Connect upgrade, refer to article [Microsoft Entra Connect: Upgrade from a previous version to the latest](how-to-upgrade-previous-version#swing-migration).