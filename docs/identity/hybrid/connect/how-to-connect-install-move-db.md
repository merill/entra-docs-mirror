---
layout: Conceptual
title: Move the Microsoft Entra Connect database from SQL Server Express to remote SQL Server - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-move-db
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to move the Microsoft Entra Connect database from the default local SQL Server Express server to a computer running remote SQL Server.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: db38b9bb-99c9-0d1e-11d3-b187d70136a6
document_version_independent_id: d45c98e2-9de9-a90e-1061-ded80f9d03eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-install-move-db.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-install-move-db
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-install-move-db.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cec1c05e-b258-f31a-a1e4-1ae904ea4be7
---

# Move the Microsoft Entra Connect database from SQL Server Express to remote SQL Server - Microsoft Entra ID | Microsoft Learn

This article describes how to move the Microsoft Entra Connect database from the local SQL Server Express server to a computer running remote SQL Server. You can use the steps described in this article to accomplish this task.

## About the scenario

In this scenario, Microsoft Entra Connect version 1.1.819.0 is installed on a single Windows Server 2016 domain controller. Microsoft Entra Connect is using the built-in SQL Server 2012 Express Edition for its database. The database will be moved to a SQL Server 2017 server.

![Diagram that shows the scenario architecture.](media/how-to-connect-install-move-db/move1.png)

## Move the Microsoft Entra Connect database

Use the following steps to move the Microsoft Entra Connect database to a computer running remote SQL Server:

1. On the Microsoft Entra Connect server, go to **Services** and stop the Microsoft Entra ID Sync service.
2. Go to the *%ProgramFiles%\Microsoft Azure AD Sync\Data* folder and copy the *ADSync.mdf* and *ADSync\_log.ldf* files to the computer running remote SQL Server.
3. Restart the Microsoft Entra ID Sync service on the Microsoft Entra Connect server.
4. Uninstall Microsoft Entra Connect by going to **Control Panel** &gt; **Programs** &gt; **Programs and Features**. Select **Microsoft Entra Connect**, and then select **Uninstall**.
5. On the computer running remote SQL Server, open SQL Server Management Studio.
6. Right-click **Databases** and select **Attach**.
7. In **Attach Databases**, select **Add** and go to the *ADSync.mdf* file. Select **OK**.

    ![Screenshot that shows the options in the Attach Databases pane.](media/how-to-connect-install-move-db/move2.png)
8. When the database is attached, go back to the Microsoft Entra Connect server and install Microsoft Entra Connect.
9. When the MSI installation is finished, the Microsoft Entra Connect wizard starts in express settings mode. Select the **Exit** icon to close the page.

    ![Screenshot that shows the Welcome to Microsoft Entra Connect page with Express Settings in the left menu highlighted.](media/how-to-connect-install-move-db/db1.png)
10. Open a new Command Prompt window or PowerShell session. Go to the folder *&lt;drive&gt;\program files\Microsoft Azure AD Connect*. Run the command `.\AzureADConnect.exe /useexistingdatabase` to start the Microsoft Entra Connect wizard in **Use existing database** setup mode.

    ![Screenshot that shows the command described in the step in PowerShell.](media/how-to-connect-install-move-db/db2.png)
11. In **Welcome to Microsoft Entra Connect**, review and agree to the license terms and privacy notice, and then select **Continue**.

    ![Screenshot that shows the Welcome to Microsoft Entra Connect page.](media/how-to-connect-install-move-db/db3.png)
12. In **Install required components**, the **Use an existing SQL Server** option is enabled. Specify the name of the SQL Server instance that's hosting the ADSync database. If the SQL engine instance that's used to host the ADSync database isn't the default instance in SQL Server, you must specify the name of the SQL engine instance.

    Also, if SQL browsing isn't enabled, you must specify the SQL engine instance port number. For example:

    ![Screenshot that shows the options on the Install required components page.](media/how-to-connect-install-move-db/db4.png)
13. In **Connect to Microsoft Entra ID**, you must provide the credentials of a Hybrid Identity Administrator for your directory in Microsoft Entra ID.

    We recommend that you use an account in the default `onmicrosoft.com` domain. This account is used only to create a service account in Microsoft Entra ID. The account isn't used after the wizard is finished.

    ![Screenshot that shows the options on the Connect to Microsoft Entra ID page.](media/how-to-connect-install-move-db/db5.png)
14. In **Connect your directories**, the existing Windows Server Active Directory (Windows Server AD) forest that's configured for directory sync is listed with a red X icon beside it. To sync changes from Windows Server AD, an Active Directory Domain Services (AD DS) account is required. Select **Change Credentials** to specify the AD DS account for the Windows Server AD forest.

    The Microsoft Entra Connect wizard can't retrieve the credentials of the AD DS account that are stored in the ADSync database because the credentials are encrypted. The credentials can be decrypted only by the earlier instance of the Microsoft Entra Connect server.

    ![Screenshot that shows the options on the Connect your directories page.](media/how-to-connect-install-move-db/db6.png)
15. In the dialog, choose one of the following options:

    1. Enter the credentials for an Enterprise Admin and let Microsoft Entra Connect create the AD DS account for you.
    2. Create the AD DS account yourself and enter its credentials in Microsoft Entra Connect.

        ![Screenshot that shows the Windows Server AD forest account dialog with Create new AD account selected.](media/how-to-connect-install-move-db/db7.png)

    After you select an option and enter the credentials, select **OK**.
16. After the credentials are entered, the red X icon is replaced with a green checkmark icon. Select **Next**.

    ![Screenshot that shows the Connect your directories page after you enter account credentials.](media/how-to-connect-install-move-db/db8.png)
17. In **Ready to configure**, select **Install**.

    ![Screenshot that shows the Microsoft Entra Connect Welcome page.](media/how-to-connect-install-move-db/db9.png)
18. When installation is finished, the Microsoft Entra Connect server is automatically enabled for staging mode. We recommend that you review the server configuration and pending exports for unexpected changes before you disable staging mode.