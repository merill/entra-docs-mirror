---
layout: Conceptual
title: Microsoft Entra provisioning to applications via PowerShell - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/on-premises-powershell-connector
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This document describes how to configure Microsoft Entra ID to provision users with external systems that offer Windows PowerShell based APIs.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: arvinh
ms.custom: sfi-image-nochange
locale: en-us
document_id: 172f666e-a498-e304-9b5d-7ba2f04fd2e0
document_version_independent_id: 2d2c99e7-145c-075a-d44c-4ddbd9e3923f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/on-premises-powershell-connector.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/on-premises-powershell-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/on-premises-powershell-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b91dd517-dabd-8afe-adb3-344455bb22b4
---

# Microsoft Entra provisioning to applications via PowerShell - Microsoft Entra ID | Microsoft Learn

The following documentation provides configuration and tutorial information. It demonstrates how the generic PowerShell connector and the Extensible Connectivity (ECMA) Connector host are used to integrate Microsoft Entra ID with external systems that offer Windows PowerShell-based APIs.

For additional information, see [Windows PowerShell Connector technical reference](/en-us/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-powershell)

## Prerequisites for provisioning via PowerShell

The following sections detail the prerequisites for this tutorial.

### Download the PowerShell setup files

[Download the PowerShell setup files from our GitHub repository](https://github.com/microsoft/MIMPowerShellConnectors/tree/master/src/ECMA2HostCSV). The setup files consist of the configuration file, the input file, schema file and the scripts used.

### On-premises prerequisites

The connector provides a bridge between the capabilities of the ECMA Connector Host and Windows PowerShell. Before you use the Connector, make sure you have the following on the server hosting the connector

- A Windows Server 2016 or a later version.
- At least 3 GB of RAM, to host a provisioning agent.
- .NET Framework 4.7.2
- Windows PowerShell 2.0, 3.0, or 4.0
- Connectivity between hosting server, the connector, and the target system that the PowerShell scripts interact with.
- The execution policy on the server must be configured to allow the connector to run Windows PowerShell scripts. Unless the scripts the connector runs are digitally signed, configure the execution policy by running this command:`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`
- Deploying this connector requires one or more PowerShell scripts. Some Microsoft products may provide scripts for use with this connector, and the support statement for those scripts would be provided by that product. If you're developing your own scripts for use with this connector, you need to have familiarity with the [Extensible Connectivity Management Agent API](/en-us/previous-versions/windows/desktop/forefront-2010/hh859557%28v=vs.100%29?redirectedfrom=MSDN) to develop and maintain those scripts. If you're integrating with third party systems using your own scripts in a production environment, we recommend you work with the third party vendor or a deployment partner for help, guidance and support for this integration.

### Cloud requirements

- A Microsoft Entra tenant with Microsoft Entra ID P1 or Premium P2 (or EMS E3 or E5). Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).
- The Hybrid Identity Administrator role for configuring the provisioning agent and the Application Administrator or Cloud Application Administrator roles for configuring provisioning in the Azure portal.
- The Microsoft Entra users, to be provisioned, must already be populated with any attributes required by the schema.

## Download, install, and configure the Microsoft Entra Connect Provisioning Agent Package

If you've downloaded the provisioning agent and configured it for another on-premises application, then continue reading in the next section.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync** &gt; **Agents**.

[![Screenshot of new UX screen.](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png)](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png#lightbox)

1. Select **Download on-premises agent**, review the terms of service, then select **Accept terms & download**.

    Note

    Please use different provisioning agents for on-premises application provisioning and Microsoft Entra Connect cloud sync / HR-driven provisioning. All three scenarios should not be managed on the same agent.
2. Open the provisioning agent installer, agree to the terms of service, and select **Install**.
3. When the Microsoft Entra provisioning agent configuration wizard opens, continue to the **Select Extension** tab and select **On-premises application provisioning** when prompted for the extension you want to enable.
4. The provisioning agent uses the operating system's web browser to display a popup window for you to authenticate to Microsoft Entra ID, and potentially also your organization's identity provider. If you're using Internet Explorer as the browser on Windows Server, then you may need to add Microsoft web sites to your browser's trusted site list to allow JavaScript to run correctly.
5. Provide credentials for a Microsoft Entra administrator when you're prompted to authorize. The user is required to have at least the [Hybrid Identity Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) role.
6. Select **Confirm** to confirm the setting. Once installation is successful, you can select **Exit**, and also close the Provisioning Agent Package installer.

## Configure the On-premises ECMA app

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **New application**.
4. Search for the **On-premises ECMA app** application, give the app a name, and select **Create** to add it to your tenant.
5. Navigate to the **Provisioning** page of your application.
6. Select **Get started**.
7. On the **Provisioning** page, change the mode to **Automatic**.
8. On the **On-Premises Connectivity** section, select the agent that you just deployed and select **Assign Agent(s)**.
9. Keep this browser window open, as you complete the next step of configuration using the configuration wizard.

## Place the InputFile.txt and Schema.xml file in locations

Before you can create the PowerShell connector for this tutorial, you need to copy the InputFile.txt and Schema.xml file into the correct locations. These files are the ones you needed to download in section Download the PowerShell setup files.

| File | location |
| --- | --- |
| InputFile.txt | `C:\Program Files\Microsoft ECMA2Host\Service\ECMA\MAData` |
| Schema.xml | `C:\Program Files\Microsoft ECMA2Host\Service\ECMA` |

## Configure the Microsoft Entra ECMA Connector Host certificate

1. On the Windows Server where the provisioning agent is installed, right select the **Microsoft ECMA2Host Configuration Wizard** from the start menu, and run as administrator. Running as a Windows administrator is necessary for the wizard to create the necessary Windows event logs.
2. After the ECMA Connector Host Configuration starts, if it's the first time you have run the wizard, it will ask you to create a certificate. Leave the default port **8585** and select **Generate certificate** to generate a certificate. The autogenerated certificate self-signs as part of the trusted root. The certificate SAN matches the host name.
3. Select **Save**.

## Create the PowerShell Connector

### General Screen

1. Launch the Microsoft ECMA2Host Configuration Wizard from the start menu.
2. At the top, select **Import** and select the configuration.xml file from step 1.
3. The new connector should be created and appear in red. Select **Edit**.
4. Generate a secret token used for authenticating Microsoft Entra ID to the connector. It should be 12 characters minimum and unique for each application. If you don't already have a secret generator, you can use a PowerShell command such as the following to generate an example random string.

    ```powershell
    -join (((48..90) + (96..122)) * 16 | Get-Random -Count 16 | % {[char]$_})
    ```
5. On the **Properties** page, all of the information should be populated. The table is provided as reference. Select **Next**.

    | Property | Value |
    | --- | --- |
    | Name | The name you chose for the connector, which should be unique across all connectors in your environment. For example, `PowerShell`. |
    | Autosync timer (minutes) | 120 |
    | Secret Token | Enter your secret token here. It should be 12 characters minimum. |
    | Extension DLL | For the PowerShell connector, select **Microsoft.IAM.Connector.PowerShell.dll**. |

[![Screenshot of general screen.](media/on-premises-powershell-connector/powershell-1.png)](media/on-premises-powershell-connector/powershell-1.png#lightbox)

### Connectivity

The connectivity tab allows you to supply configuration parameters for connecting to a remote system. Configure the connectivity tab with the information provided in the table.

- On the **Connectivity** page, all of the information should be populated. The table is provided as reference. Select **Next**.

[![Screenshot of the connectivity screen.](media/on-premises-powershell-connector/powershell-2.png)](media/on-premises-powershell-connector/powershell-2.png#lightbox)

| Parameter | Value | Purpose |
| --- | --- | --- |
| Server | &lt;Blank&gt; | Server name that the connector should connect to. |
| Domain | &lt;Blank&gt; | Domain of the credential to store for use when the connector is run. |
| User | &lt;Blank&gt; | Username of the credential to store for use when the connector is run. |
| Password | &lt;Blank&gt; | Password of the credential to store for use when the connector is run. |
| Impersonate Connector Account | Unchecked | When true, the synchronization service runs the Windows PowerShell scripts in the context of the credentials supplied. When possible, it's recommended that the **$Credentials** parameter is passed to each script is used instead of impersonation. |
| Load User Profile When Impersonating | Unchecked | Instructs Windows to load the user profile of the connector’s credentials during impersonation. If the impersonated user has a roaming profile, the connector doesn't load the roaming profile. |
| Logon Type When Impersonating | None | Logon type during impersonation. For more information, see the [dwLogonType](/en-us/windows/win32/api/winbase/nf-winbase-logonusera#parameters) documentation. |
| Signed Scripts Only | Unchecked | If true, the Windows PowerShell connector validates that each script has a valid digital signature. If false, ensure that the Synchronization Service server’s Windows PowerShell execution policy is RemoteSigned or Unrestricted. |
| Common Module Script Name (with extension) | xADSyncPSConnectorModule.psm1 | The connector allows you to store a shared Windows PowerShell module in the configuration. When the connector runs a script, it extracts the Windows PowerShell module to the file system so that each script can import it. |
| Common Module Script | [AD Sync PowerShell Connector Module code](https://github.com/microsoft/MIMPowerShellConnectors/blob/master/src/ECMA2HostCSV/Scripts/CommonModule.psm1) as value. This module will be automatically created by the ECMA2Host when the connector is running. |  |
| Validation Script | &lt;Blank&gt; | The Validation Script is an optional Windows PowerShell script that can be used to ensure that connector configuration parameters supplied by the administrator are valid. |
| Schema Script | [GetSchema code](https://github.com/microsoft/MIMPowerShellConnectors/blob/master/src/ECMA2HostCSV/Scripts/Schema%20Script.ps1) as value. |  |
| Additional Config Parameter Names | FileName,Delimiter,Encoding | In addition to the standard configuration settings, you can define additional custom configuration settings that are specific to the instance of the Connector. These parameters can be specified at the connector, partition, or run step levels and accessed from the relevant Windows PowerShell script. |
| Additional Encrypted Config Parameter Names | &lt;Blank&gt; |  |

### Capabilities

The capabilities tab defines the behavior and functionality of the connector. The selections made on this tab can't be modified when the connector is created. Configure the capabilities tab with the information provided in the table.

- On the **Capabilities** page, all of the information should be populated. The table is provided as reference. Select **Next**.

[![Screenshot of the capabilities screen.](media/on-premises-powershell-connector/powershell-4.png)](media/on-premises-powershell-connector/powershell-4.png#lightbox)

| Parameter | Value | Purpose |
| --- | --- | --- |
| Distinguished Name Style | None | Indicates if the connector supports distinguished names and if so, what style. |
| Export Type | ObjectReplace | Determines the type of objects that are presented to the Export script. |
| Data Normalization | None | Instructs the Synchronization Service to normalize anchor attributes before they are provided to scripts. |
| Object Confirmation | Normal | This is ignored. |
| Use DN as Anchor | Unchecked | If the Distinguished Name Style is set to LDAP, the anchor attribute for the connector space is also the distinguished name. |
| Concurrent Operations of Several Connectors | Checked | When checked, multiple Windows PowerShell connectors can run simultaneously. |
| Partitions | Unchecked | When checked, the connector supports multiple partitions and partition discovery. |
| Hierarchy | Unchecked | When checked, the connector supports an LDAP style hierarchical structure. |
| Enable Import | Checked | When checked, the connector imports data via import scripts. |
| Enable Delta Import | Unchecked | When checked, the connector can request deltas from the import scripts. |
| Enable Export | Checked | When checked, the connector exports data via export scripts. |
| Enable Full Export | Checked | Not supported. This will be ignored. |
| No Reference Values In First Export Pass | Unchecked | When checked, reference attributes are exported in a second export pass. |
| Enable Object Rename | Unchecked | When checked, distinguished names can be modified. |
| Delete-Add As Replace | Checked | Not supported. This will be ignored. |
| Enable Export Password in First Pass | Unchecked | Not supported. This will be ignored. |

### Global Parameters

The Global Parameters tab enables you to configure the Windows PowerShell scripts the connector runs. You can also configure global values for custom configuration settings defined on the Connectivity tab. Configure the global parameters tab with the information provided in the table.

- On the **Global Parameters** page, all of the information should be populated. The table is provided as reference. Select **Next**.

[![Screenshot of the global screen.](media/on-premises-powershell-connector/powershell-5.png)](media/on-premises-powershell-connector/powershell-5.png#lightbox)

| Parameter | Value |
| --- | --- |
| Partition Script | &lt;Blank&gt; |
| Hierarchy Script | &lt;Blank&gt; |
| Begin Import Script | &lt;Blank&gt; |
| Import Script | [Paste the import script as the value](https://github.com/microsoft/MIMPowerShellConnectors/blob/master/src/ECMA2HostCSV/Scripts/Import%20Scripts.ps1) |
| End Import Script | &lt;Blank&gt; |
| Begin Export Script | &lt;Blank&gt; |
| Export Script | [Paste the import script as the value](https://github.com/microsoft/MIMPowerShellConnectors/blob/master/src/ECMA2HostCSV/Scripts/Export%20Script.ps1) |
| End Export Script | &lt;Blank&gt; |
| Begin Password Script | &lt;Blank&gt; |
| Password Extension Script | &lt;Blank&gt; |
| End Password Script | &lt;Blank&gt; |
| FileName\_Global | InputFile.txt |
| Delimiter\_Global | ; |
| Encoding\_Global | &lt;Blank&gt; (defaults to UTF8) |

### Partitions, Run Profiles, Export, FullImport

Keep the defaults and select **next**.

### Object types

Configure the object types tab with the information provided in the table.

- On the **Object types** page, all of the information should be populated. The table is provided as reference. Select **Next**.

[![Screenshot of the object types screen.](media/on-premises-powershell-connector/powershell-13.png)](media/on-premises-powershell-connector/powershell-13.png#lightbox)

| Parameter | Value |
| --- | --- |
| Target Object | Person |
| Anchor | AzureObjectID |
| Query Attribute | AzureObjectID |
| DN | AzureObjectID |

### Select Attributes

Ensure that the following attributes are selected:

- On the **Select Attributes** page, all of the information should be populated. The table is provided as reference. Select **Next**.
- AzureObjectID
- IsActive
- DisplayName
- EmployeeId
- Title
- UserName
- Email

[![Screenshot of the select attributes screen.](media/on-premises-powershell-connector/powershell-15.png)](media/on-premises-powershell-connector/powershell-15.png#lightbox)

### Deprovisioning

On the Deprovisioning page, you can specify if you wish to have Microsoft Entra ID remove users from the directory when they go out of scope of the application. If so, under Disable flow, select Delete, and under Delete flow, select Delete. If Set attribute value is chosen, the attributes selected on the previous page won't be available to select on the Deprovisioning page.

- On the **Deprovisioning** page, all of the information should be populated. The table is provided as reference. Select **Next**.

[![Screenshot of the deprovisioning screen.](media/on-premises-powershell-connector/powershell-16.png)](media/on-premises-powershell-connector/powershell-16.png#lightbox)

## Ensure ECMA2Host service is running and can read from file via PowerShell

Follow these steps to confirm the connector host is started and has identified any existing users from the target system.

1. On the server running the Microsoft Entra ECMA Connector Host, select **Start**.
2. Select **run** if needed, then enter **services.msc** in the box.
3. In the **Services** list, ensure that **Microsoft ECMA2Host** is present and running. If it's not running, select **Start**.
4. On the server running the Microsoft Entra ECMA Connector Host, launch PowerShell.
5. Change to the folder where the ECMA host was installed, such as `C:\Program Files\Microsoft ECMA2Host`.
6. Change to the subdirectory `Troubleshooting`.
7. Run the script `TestECMA2HostConnection.ps1` in the directory as shown, and provide as arguments the connector name and the `ObjectTypePath` value `cache`. If your connector host is not listening on TCP port 8585, then you may also need to provide the `-Port` argument as well. When prompted, type the secret token configured for that connector. 

    ```
    PS C:\Program Files\Microsoft ECMA2Host\Troubleshooting> $cout = .\TestECMA2HostConnection.ps1 -ConnectorName PowerShell -ObjectTypePath cache; $cout.length -gt 9
    Supply values for the following parameters:
    SecretToken: ************
    ```
8. If the script displays an error or warning message, then check that the service is running, and the connector name and secret token match those values you configured in the configuration wizard.
9. If the script displays the output `False`, then the connector hasn't seen any entries in the source target system for existing users. If this is a new target system installation, then this behavior is to be expected, and you can continue at the next section.
10. However, if the target system already contains one or more users but the script displayed `False`, then this status indicates the connector couldn't read from the target system. If you attempt to provision, then Microsoft Entra ID may not correctly match users in that source directory with users in Microsoft Entra ID. Wait several minutes for the connector host to finish reading objects from the existing target system, and then rerun the script. If the output continues to be `False`, then check the configuration of your connector and the permissions in the target system are allowing the connector to read existing users.

## Test the connection from Microsoft Entra ID to the connector host

1. Return to the web browser window where you were configuring the application provisioning in the portal.

    Note

    If the window had timed out, then you need to re-select the agent.

    1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
    2. Browse to **Entra ID** &gt; **Enterprise apps**.
    3. Select the **On-premises ECMA app** application.
    4. Select **Provisioning**.
    5. If **Get started** appears, then change the mode to **Automatic**, on the **On-Premises Connectivity** section, select the agent that you just deployed and select **Assign Agent(s)**, and wait 10 minutes. Otherwise go to **Edit Provisioning**.
2. Under the **Admin credentials** section, enter the following URL. Replace the `connectorName` portion with the name of the connector on the ECMA host, such as `PowerShell`. If you provided a certificate from your certificate authority for the ECMA host, then replace `localhost` with the host name of the server where the ECMA host is installed.

    | Property | Value |
    | --- | --- |
    | Tenant URL | https://localhost:8585/ecma2host\_connectorName/scim |
3. Enter the **Secret Token** value that you defined when you created the connector.

    Note

    If you just assigned the agent to the application, please wait 10 minutes for the registration to complete. The connectivity test won't work until the registration completes. Forcing the agent registration to complete by restarting the provisioning agent on your server can speed up the registration process. Go to your server, search for **services** in the Windows search bar, identify the **Microsoft Entra Connect Provisioning Agent** service, right-select the service, and restart.
4. Select **Test Connection**, and wait one minute.
5. After the connection test is successful and indicates that the supplied credentials are authorized to enable provisioning, select **Save**.

## Configure the application connection

Return to the web browser window where you were configuring the application provisioning.

Note

If the window had timed out, then you need to re-select the agent.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select the **On-premises ECMA app** application.
4. Select **Provisioning**.
5. If **Get started** appears, then change the mode to **Automatic**, on the **On-Premises Connectivity** section, select the agent that you deployed and select **Assign Agent(s)**. Otherwise go to **Edit Provisioning**.
6. Under the **Admin credentials** section, enter the following URL. Replace the `{connectorName}` portion with the name of the connector on the ECMA connector host, such as **CSV**. The connector name is case sensitive and should be the same case as was configured in the wizard. You can also replace `localhost` with your machine hostname.

    | Property | Value |
    | --- | --- |
    | Tenant URL | `https://localhost:8585/ecma2host_CSV/scim` |
7. Enter the **Secret Token** value that you defined when you created the connector.

    Note

    If you just assigned the agent to the application, please wait 10 minutes for the registration to complete. The connectivity test won't work until the registration completes. Forcing the agent registration to complete by restarting the provisioning agent on your server can speed up the registration process. Go to your server, search for **services** in the Windows search bar, identify the **Microsoft Entra Connect Provisioning Agent Service**, right-select the service, and restart.
8. Select **Test Connection**, and wait one minute.
9. After the connection test is successful and indicates that the supplied credentials are authorized to enable provisioning, select **Save**.

## Configure attribute mappings

Now you need to map attributes between the representation of the user in Microsoft Entra ID and the representation of a user in the on-premises InputFile.txt.

You'll use the Azure portal to configure the mapping between the Microsoft Entra user's attributes and the attributes that you previously selected in the ECMA Host configuration wizard.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select the **On-premises ECMA app** application.
4. Select **Provisioning**.
5. Select **Edit provisioning**, and wait 10 seconds.
6. Expand **Mappings** and select **Provision Microsoft Entra users**. If this is the first time you've configured the attribute mappings for this application, there will be only one mapping present, for a placeholder.
7. To confirm that the schema is available in Microsoft Entra ID, select the **Advanced Options** dropdown and select **Edit target User attributes**. Ensure that all the attributes selected in the configuration wizard are listed. If not, then wait several minutes for the schema to refresh, and then reload the page. Once you see the attributes listed, then cancel from this page to return to the mappings list.
8. Now, on the select on the **userPrincipalName** PLACEHOLDER mapping. This mapping is added by default when you first configure on-premises provisioning. Change the value to match the following:

    | Mapping type | Source attribute | Target attribute |
    | --- | --- | --- |
    | Direct | userPrincipalName | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:UserName |
9. Now select **Add New Mapping**, and repeat the next step for each mapping.
10. Specify the source and target attributes for each of the mappings in the following table.

    | Mapping type | Source attribute | Target attribute |
    | --- | --- | --- |
    | Direct | objectId | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:AzureObjectID |
    | Direct | userPrincipalName | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:UserName |
    | Direct | displayName | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:DisplayName |
    | Direct | employeeId | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:EmployeeId |
    | Direct | jobTitle | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:Title |
    | Direct | mail | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:Email |
    | Expression | Switch([IsSoftDeleted],, "False", "True", "True", "False") | urn:ietf:params:scim:schemas:extension:ECMA2Host:2.0:User:IsActive |

    [![Screenshot of attribute mappings.](media/on-premises-powershell-connector/powershell-8.png)](media/on-premises-powershell-connector/powershell-8.png#lightbox)
11. Once all of the mappings have been added, select **Save**.

## Assign users to an application

Now that you have the Microsoft Entra ECMA Connector Host talking with Microsoft Entra ID, and the attribute mapping configured, you can move on to configuring who's in scope for provisioning.

Important

If you were signed in using a Hybrid Identity Administrator role, you need to sign-out and sign-in with an account that's at least the Application Administrator role for this section. The Hybrid Identity Administrator role doesn't have permissions to assign users to applications.

If there are existing users in the InputFile.txt, then you should create application role assignments for those existing users. To learn more about how to create application role assignments in bulk, see [governing an application's existing users in Microsoft Entra ID](../../id-governance/identity-governance-applications-existing-users).

Otherwise, if there are no current users of the application, then select a test user from Microsoft Entra who will be provisioned to the application.

1. Ensure that the user selected has all the properties, mapped to the required attributes of the schema.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
3. Browse to **Entra ID** &gt; **Enterprise apps**.
4. Select the **On-premises ECMA app** application.
5. On the left, under **Manage**, select **Users and groups**.
6. Select **Add user/group**.
7. Under **Users**, select **None Selected**.
8. Select users from the right and select the **Select** button.
9. Now select **Assign**.

## Test provisioning

Now that your attributes are mapped and users are assigned, you can test on-demand provisioning with one of your users.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select the **On-premises ECMA app** application.
4. Select **Provisioning**.
5. Select **Provision on demand**.
6. Search for one of your test users, and select **Provision**.
7. After several seconds, then the message **Successfully created user in target system** appears, with a list of the user attributes.

## Start provisioning users

1. After on-demand provisioning is successful, change back to the provisioning configuration page. Ensure that the scope is set to only assigned users and groups, turn provisioning **On**, and select **Save**.
2. Wait several minutes for provisioning to start. It might take up to 40 minutes. After the provisioning job is completed, as described in the next section, if you're done testing, you can change the provisioning status to **Off**, and select **Save**. This action stops the provisioning service from running in the future.