---
layout: Conceptual
title: Export a Microsoft Identity Manager connector for use with the Microsoft Entra ECMA Connector Host - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/on-premises-migrate-microsoft-identity-manager
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Describes how to create and export a connector from MIM Sync to be used with the Microsoft Entra ECMA Connector Host.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 64379e35-1257-d93f-d9e3-41dcecc7aa8e
document_version_independent_id: dcdcba30-88ea-613d-2894-22292d06c51f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/on-premises-migrate-microsoft-identity-manager.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/on-premises-migrate-microsoft-identity-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/on-premises-migrate-microsoft-identity-manager.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fecfc034-c4c2-43e6-be47-948bd4addcea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cf36da-59bd-4744-91e9-295292c63e5e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e824c2f5-ae8e-4f26-2ffd-4dc23f17f4b9
---

# Export a Microsoft Identity Manager connector for use with the Microsoft Entra ECMA Connector Host - Microsoft Entra ID | Microsoft Learn

You can import into the Microsoft Entra ECMA Connector Host a configuration for a specific connector from a Microsoft Identity Manager Synchronization Service (MIM Sync) installation.

## Create a connector configuration in MIM Sync

This section is included for illustrative purposes, if you wish to set up MIM Sync with a connector. The MIM Sync installation is only used for the initial configuration, not for the ongoing synchronization from Microsoft Entra ID. If you already have MIM Sync with your ECMA connector configured, skip to the next section.

1. Prepare a Windows Server 2016 server, which is distinct from the server that will be used for running the Microsoft Entra ECMA Connector Host. This host server should either have a SQL Server 2016 database colocated or have network connectivity to a SQL Server 2016 database. One way to set up this server is by deploying an Azure virtual machine with the image **SQL Server 2016 SP1 Standard on Windows Server 2016**. This server doesn't need internet connectivity other than remote desktop access for setup purposes.
2. Create an account for use during the MIM Sync installation. It can be a local account on that Windows Server instance. To create a local account, open **Control Panel** &gt; **User Accounts**, and add the user account **mimsync**.
3. Add the account created in the previous step to the local Administrators group.
4. Give the account created earlier the ability to run a service. Start **Local Security Policy** and select **Local Policies** &gt; **User Rights Assignment** &gt; **Log on as a service**. Add the account mentioned earlier.
5. Install MIM Sync on this host.
6. After the installation of MIM Sync is complete, sign out and sign back in.
7. Install your connector on the same server as MIM Sync. For illustration purposes, use either of the Microsoft-supplied SQL or LDAP connectors for download from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=51495).
8. Start the Synchronization Service UI. Select **Management Agents**. Select **Create**, and specify the connector management agent. Be sure to select a connector management agent that's ECMA based.
9. Give the connector a name, and configure the parameters needed to import and export data to the connector. Be sure to configure that the connector can import and export single-valued string attributes of a user or person object type.

## Export a connector configuration from MIM Sync

1. On the MIM Sync server computer, start the Synchronization Service UI, if it isn't already running. Select **Management Agents**.
2. Select the connector, and select **Export Management Agent**. Save the XML file, and the DLL and related software for your connector, to the Windows server that will be holding the ECMA Connector Host.

At this point, the MIM Sync server is no longer needed.

## Import a connector configuration

1. Install the ECMA Connector host and provisioning agent on a Windows Server, using the [provisioning users into SQL based applications](on-premises-sql-connector-configure#3-install-and-configure-the-azure-ad-connect-provisioning-agent) or [provisioning users into LDAP directories](on-premises-ldap-connector-configure#install-and-configure-the-azure-ad-connect-provisioning-agent) articles.
2. Sign in to the Windows server as the account that the Microsoft Entra ECMA Connector Host runs as.
3. Change to the directory C:\Program Files\Microsoft ECMA2host\Service\ECMA. Ensure there are one or more DLLs already present in that directory. Those DLLs correspond to Microsoft-delivered connectors.
4. Copy the MA DLL for your connector, and any of its prerequisite DLLs, to that same ECMA subdirectory of the Service directory.
5. Change to the directory C:\Program Files\Microsoft ECMA2Host\Wizard. Run the program Microsoft.ECMA2Host.ConfigWizard.exe to set up the ECMA Connector Host configuration.
6. A new window appears with a list of connectors. By default, no connectors will be present. Select **New connector**.
7. Specify the management agent XML file that was exported from MIM Sync earlier. Continue with the configuration and schema-mapping instructions from the section "Create a connector" in either the [provisioning users into SQL based applications](on-premises-sql-connector-configure#6-create-a-generic-sql-connector) or [provisioning users into LDAP directories](on-premises-ldap-connector-configure#configure-a-generic-ldap-connector) articles.