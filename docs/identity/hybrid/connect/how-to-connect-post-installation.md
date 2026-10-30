---
layout: Conceptual
title: 'Microsoft Entra Connect: Next steps and how to manage Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-post-installation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to extend the default configuration and operational tasks for Microsoft Entra Connect.
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: b8f737c8-8520-1f47-2ec0-5e75447ddf3f
document_version_independent_id: b0ac39a1-b55a-ecbd-fd72-eecdcd70278f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-post-installation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-post-installation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-post-installation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 00a35fa9-21ba-a3b0-6450-70e609481cf4
---

# Microsoft Entra Connect: Next steps and how to manage Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

Use the operational procedures in this article to customize Microsoft Entra Connect to meet your organization's needs and requirements.

## Add additional sync admins

By default, only the user who did the installation and local admins are able to manage the installed sync engine. For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.

## Assign licenses to Microsoft Entra ID P1 or P2 and Enterprise Mobility Suite users

Now that your users are synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Microsoft 365.

### To assign a Microsoft Entra ID P1 or P2 or Enterprise Mobility Suite License

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. On the left, select **Active Directory**.
3. On the **Active Directory** page, double-select the directory that has the users you want to set up.
4. At the top of the directory page, select **Licenses**.
5. On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then select **Assign**.
6. In the dialog box, select the users you want to assign licenses to, and then select the check mark icon to save the changes.

## Verify the scheduled synchronization task

Use the [Microsoft Entra admin center](https://entra.microsoft.com) to check the status of a synchronization.

### To verify the scheduled synchronization task

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Connect sync**.
3. At the top of the page, note the last synchronization.

![Directory sync time](media/how-to-connect-post-installation/verify2.png)

## Start a scheduled synchronization task

If you need to run a synchronization task, you can do this by:

1. Double-select on the Microsoft Entra Connect desktop shortcut to start the wizard.
2. Select **Configure**.
3. On the tasks screen, select the **Customize synchronization options** and select **Next**
4. Enter your Microsoft Entra credentials
5. Select **Next**. Click **Next**. Select **Next**.
6. On the **Ready to Configure** screen, ensure that the **Start the synchronization process when configuration completes** box is selected.
7. Select **Configure**.

For more information on the Microsoft Entra Connect Sync Scheduler, see [Microsoft Entra Connect Scheduler](how-to-connect-sync-feature-scheduler).

## Additional tasks available in Microsoft Entra Connect

After your initial installation of Microsoft Entra Connect, you can always start the wizard again from the Microsoft Entra Connect start page or desktop shortcut. Going through the wizard again provides some new options in the form of additional tasks.

The following table provides a summary of these tasks and a brief description of each task.

![List of additional tasks](media/how-to-connect-post-installation/addtasks2.png)

| Additional task | Description |
| --- | --- |
| **Privacy Settings** | View what telemetry data is being shared with Microsoft. |
| **View current configuration** | View your current Microsoft Entra Connect solution. This includes general settings, synchronized directories, and sync settings. |
| **Customize synchronization options** | Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back. |
| **Configure device options** | Device options available for synchronization |
| **Refresh directory schema** | Allows you to add new on-premises directory objects for synchronization |
| **Configure Staging Mode** | Stage information that isn't immediately synchronized and isn't exported to Microsoft Entra ID or on-premises Active Directory. With this feature, you can preview the synchronizations before they occur. |
| **Change user sign-in** | Change the authentication method users are using to sign-in |
| **Manage federation** | Manage your AD FS infrastructure, renew certificates, and add AD FS servers |
| **Troubleshoot** | Help with troubleshooting Microsoft Entra Connect issues |