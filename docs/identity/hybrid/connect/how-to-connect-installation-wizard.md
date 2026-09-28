---
layout: Conceptual
title: Re-running the Microsoft Entra Connect install wizard - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-installation-wizard
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Explains how the installation wizard works the second time you run it.
keywords: The Azure AD Connect installation wizard lets you configure maintenance settings the second time you run it
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: ffeea52e-9322-e177-449b-44ad91fb0519
document_version_independent_id: 71fc712b-c214-ba8e-4a8e-3a55a21a8317
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-installation-wizard.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-installation-wizard
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-installation-wizard.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a86bf4aa-5605-134a-60e7-228e793a4a4d
---

# Re-running the Microsoft Entra Connect install wizard - Microsoft Entra ID | Microsoft Learn

The first time you run the Microsoft Entra Connect installation wizard, it walks you through how to configure your installation. If you run the installation wizard again, it offers options for maintenance.

Important

Be aware that you can't run the installation wizard while a synchronization is in progress. Please verify that a synchronization is not running before launching the wizard.

You can find the installation wizard in the start menu named **Microsoft Entra Connect**.

![Start menu](media/how-to-connect-installation-wizard/startmenu.png)

When you start the installation wizard, you see a page with these options:

![Page with a list of other tasks](media/how-to-connect-installation-wizard/additionaltasks.png)

If you have installed ADFS with Microsoft Entra Connect, you have even more options. The other options you have for ADFS are documented in [ADFS management](how-to-connect-fed-management#manage-ad-fs).

Select one of the tasks and click **Next** to continue.

Important

While the installation is wizard open, all operations in the sync engine are suspended. Make sure you close the installation wizard as soon as you have completed your configuration changes.

## View current configuration

This option gives you a quick view of your currently configured options.

![Page with a list of all options and their state](media/how-to-connect-installation-wizard/viewconfig.png)

Click **Previous** to go back. If you select **Exit**, you close the installation wizard.

## Customize synchronization options

This option is used to make changes to the sync configuration. You see a subset of options from the custom configuration installation path. You see this option even if you used express installation initially.

- [Add more directories](how-to-connect-install-custom#connect-your-directories).
- [Change Domain and OU filtering](how-to-connect-install-custom#domain-and-ou-filtering).
- Remove Group filtering.
- [Change optional features](how-to-connect-install-custom#optional-features).

The other options from the initial installation can't be changed and aren't available. These options are:

- Change the attribute to use for userPrincipalName and sourceAnchor.
- Change the joining method for objects from different forest.
- Enable group-based filtering.

## Refresh directory schema

This option is used if you have changed the schema in one of your on-premises AD DS forests. For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects. In this case, you need to instruct Microsoft Entra Connect to read the schema again from AD DS and update its cache. This action also regenerates the Sync Rules. If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.

When you select this option, all the directories in your configuration are listed. You can keep the default setting and refresh all forests or unselect some of them.

![Page with a list of all directories in the environment](media/how-to-connect-installation-wizard/refreshschema.png)

## Configure staging mode

This option allows you to enable and disable staging mode on the server. More information about staging mode and how it's used can be found in [Operations](how-to-connect-sync-staging-server).

The option shows if staging is currently enabled or disabled:![Screenshot that shows staging mode disabled.](media/how-to-connect-installation-wizard/stagingmodecurrentstate.png)

To change the state, select this option and select or unselect the checkbox.![Option that is also showing the current state of staging mode](media/how-to-connect-installation-wizard/stagingmodeenable.png)

## Change user sign-in

This option allows you to change the user sign-in method to and from password hash sync, pass-through authentication or federation. You can't change to **do not configure**.

For more information on this option, see [user sign-in](plan-connect-user-signin#changing-the-user-sign-in-method).