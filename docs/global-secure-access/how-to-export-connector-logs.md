---
layout: Conceptual
title: Export connector logs to the Log Analytics workspace - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-export-connector-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Extract connector logs and send those logs to the Log Analytics workspace in the customer’s Azure subscription.
ms.topic: how-to
ms.date: 2024-12-03T00:00:00.0000000Z
ms.reviewer: sumeetmittal
locale: en-us
document_id: d388fb47-f904-3a2c-e2e9-cebb6f6443bb
document_version_independent_id: d388fb47-f904-3a2c-e2e9-cebb6f6443bb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-export-connector-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-export-connector-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-export-connector-logs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 16556694-060e-a4f6-ab4f-d07aa07756c7
---

# Export connector logs to the Log Analytics workspace - Global Secure Access | Microsoft Learn

This article describes how to extract private network connector logs from connector machines that are deployed on the customer's network. Once extracted, those logs can be sent to the Log Analytics workspace in the customer’s Azure subscription. Extracting these logs is performed using Azure Arc and its extensions. Customers retain control and management of the logs in their Azure environment, which ensures that customers keep full ownership and security of their data.

## Prerequisites

To complete the steps in this process, you must have the following prerequisites in place:

- An active Azure subscription.
- An on-premises Windows machine running Microsoft Entra Private Network Connector that you want to connect to Azure Log Analytics. For more information, see [Understand the Microsoft Entra private network connector](concept-connectors).
- Access to navigate and execute commands in the Azure portal.
- A Microsoft Azure Arc account to manage on-premises and multicloud resources. For more information, see [Azure Arc overview](/en-us/azure/azure-arc/overview).

## Extract connector logs

To extract connector logs, you must enable verbose logging on the connector machine and then stream the logs to Log Analytics.

### Enable verbose logging on the connector machine

Verbose logs are useful when debugging Microsoft Entra Private Network Connector side issues for Entra Private Access. Verbose logging isn't enabled in the connector by default.

To enable verbose logging:

1. Locate the installation directory of the connector at `C:\Program Files\Microsoft Entra Private Network Connector`.
2. Create a folder in the local directory with write permissions **On**.

    To verify write permissions:

    1. Right-click on the folder you created, then click **Properties**.
    2. Go to the **Security** tab and make sure the **Write** property is checked for **Allow**. If **Write** isn't checked, select **edit**.
    3. On the pop-up window, select **allow** for the **write** row, then click **apply**.
3. Right-click on a text editor application such as Notepad or Notepad++, and select **Run as Administrator**.
4. Open the file `MicrosoftEntraPrivateNetworkConnector.exe.config` to edit.
5. From the following section, select the code from `<system.diagnostics>` to `</system.diagnostics>` and add it to the `MicrosoftEntraPrivateNetworkConnector.exe.config` file.

```json

<?xml version="1.0" encoding="utf-8" ?> 

<configuration> 

  <runtime> 

     <gcServer enabled="true"/> 

  </runtime> 

  <appSettings> 

    <add key="TraceFilename" value="MicrosoftEntraPrivateNetworkConnector.log" /> 

  </appSettings> 

<system.diagnostics> 

  <trace autoflush="true" indentsize="4"> 

    <listeners> 

      <add name="consoleListener" type="System.Diagnostics.ConsoleTraceListener" /> 

      <add name="textWriterListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="C:\logs\connector_logs.log" /> 

      <remove name="Default" /> 

    </listeners> 

  </trace> 

</system.diagnostics> 

</configuration>

```

Next, you need to Stop and Start the Connector service for the above changes to take effect.

1. Type **Services** in the search box in the taskbar, then go to **Services**.
2. Look for the **Microsoft Entra Private Network Connector** service from the Services list and select it.
3. Choose **Stop** the agent service, then **Start** the agent service again. At this point, you see a text file labeled `connector_logs.log` in the C:\logs\ folder.

Note

When verbose logging isn't enabled, the default log file location is stored at `C:\Users\<user>\AppData\Local\Temp`. When verbose logging is enabled, the log file is stored at `C:\logs\connector_logs.log`. Verbose logging can be enabled or disabled by adding or removing the lines specified in step 4. You must restart the service agent each time for the logging changes to take effect.

### Set up Azure Arc on the on-premises machine

1. Get the script for enabling Azure Arc for the on-premises machine:
    1. Go to the [Azure portal](https://portal.azure.com/).
    2. Search for **Azure Arc** in the search bar.
    3. Go to **Azure Arc resources &gt; Machines**.
    4. Click on **Add/Create &gt; Add a Machine**.
    5. Add a single server &gt; click on **Generate Script**.
    6. Fill in the information, then click **Download and Run Script**.
2. Install the Azure Arc Agent on the on-premises connector machine:
    1. Download the Azure Arc agent setup script from the Azure portal.
    2. Search for **Windows PowerShell ISE** in the search box on the Task bar. Right click on the application, then click **Run as administrator**. From PowerShell, open the downloaded file labeled `OnboardingScript.ps1`.
    3. Run the script. You can bypass the execution policy if needed by running: powershell -ExecutionPolicy Bypass -File "FilePath"
    4. Log in on the pop-up window to authenticate using the Azure account credentials. The screen returns a message that reads: `Authentication complete. You can return to the application. Feel free to close this browser tab.`

### Set up data collection endpoint (DCE)

1. Go to the [Azure portal](https://portal.azure.com/).
2. In the search bar, search for **Data Collection Endpoint**.
3. Click **Create**.
4. Provide a name and region for the DCE.
5. Click **Review + create** and then **Create**.

### Set up Log Analytics workspace

1. Go to the [Azure portal](https://portal.azure.com/).
2. Create a Log Analytics workspace:
    1. In the search bar, type **Log Analytics** and select **Log Analytics workspaces**.
    2. Click **Create**.
    3. Fill in the necessary details:
        - **Subscription**: Select your subscription.
        - **Resource Group**: Select an existing resource group or create a new one.
        - **Name**: Provide a unique name for the Log Analytics workspace.
        - **Region**: Choose the region closest to your on-premises machine.
    4. Click **Review + create**, then **Create**.
3. Create a table under the new workspace.
    1. Select the workspace name you created.
    2. Navigate to **Workspace** &gt; \*\* **Settings** &gt; **Tables**.
    3. Click **+ Create** &gt; **New Custom Log (Direct Ingest)**.
    4. Fill in the necessary details:
        - **Table Name**: Provide a Table Name.
        - **Description**: Provide an optional description for your table.
        - **Table Plan**: Choose Appropriate Table Plan.
        - **Data Collection rule**: If you don't have the existing DCR, click on Create a new data collection rule.
            - **Subscription**: Select your subscription.
            - **Resource Group**: Select an existing resource group or create a new one.
            - **Region**: Choose the region.
            - **Name**: Provide a unique name for the DCR.
        - **Data Collection endpoint**: Choose the data collection endpoint created above.
        - **Schema and transformation**: Upload a sample log file in json format. Look at the logs file on the virtual machine and convert it into a sample json. e.g., create a sample.json with below content and upload.
        - **Create**: Review and Create the Table

```json
		[			{				"RawData": "MicrosoftEntraPrivateNetworkConnectorService.exe Information: 0 : Main was called"			},			{				"RawData": "MicrosoftEntraPrivateNetworkConnectorService.exe Warning: 0 : TraceMaxMessages must be an integer value and minimum of '50000'"			},			{				"RawData": "MicrosoftEntraPrivateNetworkConnectorService.exe Information: 0 : Tracing to text file: 'Error'"			}		] 

```

### Set up data collection rule (DCR)

1. Go to the [Azure portal](https://portal.azure.com/).
2. In the search bar, search for **Data Collection Rule**.
3. Select the DCR you created as part of the table creation.
4. Go to Settings: Resources
    1. Click **Add resources**.
    2. Open your subscription.
    3. Select your resource group from the list.
    4. Click apply. You should see your VM name list in the resources.
5. Go to Settings: Data sources
    1. Click **Add data source**.
    2. For the Data source type, select **Custom Text logs**.
    3. Specify the paths to the logs on your on-premises Windows machine (for example, C:\logs\ connector\_logs.log).
    4. Enter the table name you created under log analytics workspace. To get the table name, open a new tab and navigate to the Azure portal and search for **Log Analytics Workspaces**. Select the table you created. Click on **setting** and open the tables. Find the name of the **custom table (classic)**.
    5. Select **Record delimiter**: End-of-line
    6. In **Transform**: add "source | extend RawData = RawData"
    7. Click **Save**, then **Next: Destination**.
6. Configure Destination:
    1. Destination **Type-&gt; Azure Monitor Logs**.
    2. Select your subscription.
    3. Select your Log Analytics workspace as the destination.
    4. Click **Save**.

### Verify data collection

- Check Data in Log Analytics:

    After you've installed and configured the agent, it may take some time for data to start appearing.

    1. In the Azure portal, go to your Log Analytics workspace &gt; Select your Workspace.
    2. Navigate to **Logs**, click exit on the pop-up hub &gt; Choose **KQL mode** &gt; Type Query (Table Name | take 10).
    3. Select **Run**. You see your logs. This setup allows you to collect text logs from on-premises Windows machines and send them to Azure Log Analytics using Azure Arc. The data collection rule ensures the logs are collected as per the defined paths, and the agent sends them to your Log Analytics workspace.

## Share access to your workspace

Once you have the logs into the Log Analytics workspace, you can securely open access the logs to an external user (outside of your tenant) by sharing your workspace. One use case is to grant access to support personnel (as required) for any support issues. Support personnel can be from Microsoft CSS (Customer Service & Support), Engineering OCE (On Call Engineer), or the customer’s own support network. Giving access to your workspace can help with swiftly diagnosing the problem, positively impacting the Mean Time to Recovery (MTTR) and Mean Time to Mitigate (MTTM), and by extension, customer satisfaction.

Here are the steps to provide access to an external user:

### Prerequisites

- **Azure Subscription**: Ensure you have an active Azure subscription.
- **Log Analytics Workspace**: An existing Log Analytics workspace that you want to share.
- **Microsoft Entra ID Guest User**: The external user must be added as a guest user in your Microsoft Entra ID.

### Add external user as a guest in Microsoft Entra ID

1. Navigate to Microsoft Entra ID:
    1. Go to the [Azure portal](https://portal.azure.com/).
    2. In the search bar, type **Microsoft Entra ID**, then select it.
2. Add a New Guest User:
    1. In the Microsoft Entra ID dashboard, select **Manage** &gt; **Users**.
    2. Click on **+ New user**, then select **Invite external user**.
    3. Enter the external user's email address and fill in the required information.
    4. Click **Invite** to send an invitation to the external user. The external user receives an email invitation to join your Microsoft Entra ID page as a guest.

### Assign roles to the guest user in Log Analytics workspace

1. Navigate to the Log Analytics Workspace:
    - In the Azure portal, search for **Log Analytics workspaces**, then select the workspace you want to share.
2. Identity Access Control (IAM):
    1. In the workspace blade, select **Access control (IAM)** from the left-hand menu.
    2. Click on **+ Add**, then select **Add role assignment**.
3. Assign a Role:
    1. Select a role to assign to the guest user. Common roles for accessing Log Analytics include:
    2. Log Analytics Reader: Allows the user to read and query logs.
    3. Log Analytics Contributor: Allows the user to read, query, and modify logs.
4. Add the Guest User:
    1. In the Members section, click **Select members**.
    2. Search for the guest user you added earlier by their email address.
    3. Select the guest user and click **Select**.
5. Review and Assign:
    - Review the role assignment and click **Review + assign** to complete the process.

### Ensure permissions are properly set

- Verify Permissions: The guest user should now have access to the Log Analytics workspace with the permissions assigned.
    - You can verify by going to **Access control (IAM)** in the Log Analytics workspace and checking the role assignments.

### External user access and query logs

1. External User Access:
    - The external user needs to accept the invitation sent to their email and log into the Azure portal using their credentials.
2. Accessing Log Analytics:
    1. Once logged in, the external user navigates to the Log Analytics workspace shared with them.
    2. They can use the Log Analytics workspace's **Logs** feature to query and analyze logs based on the permissions granted.

### Other considerations

- **Security**: Follow the principle of least privilege and ensure that you grant only the necessary permissions to the guest user.
- **Monitoring and Auditing**: Regularly monitor and audit access to your Log Analytics workspace to ensure compliance and security.

By following these steps, you can securely open your Azure Log Analytics workspace to a user outside of your tenant, allowing them to access and query logs as needed.

## Useful Links

- [Understand the Microsoft Entra private network connector](concept-connectors)
- [Learn about Microsoft Entra Private Access](concept-private-access)