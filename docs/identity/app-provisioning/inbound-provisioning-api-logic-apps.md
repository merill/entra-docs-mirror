---
layout: Conceptual
title: API-driven inbound provisioning with Azure Logic Apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/inbound-provisioning-api-logic-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to implement API-driven inbound provisioning with Azure Logic Apps.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: cmmdesai
ms.custom: sfi-image-nochange
locale: en-us
document_id: d4ffe69a-c715-325e-72fc-8b12205e46ae
document_version_independent_id: e622991d-80bb-733d-2ba4-9f691a78d91b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/inbound-provisioning-api-logic-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/inbound-provisioning-api-logic-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/inbound-provisioning-api-logic-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: 87a147a5-7cdf-4bd9-d6cb-c4b3f4071a47
---

# API-driven inbound provisioning with Azure Logic Apps - Microsoft Entra ID | Microsoft Learn

This tutorial describes how to use Azure Logic Apps workflow to implement Microsoft Entra ID [API-driven inbound provisioning](inbound-provisioning-api-concepts). Using the steps in this tutorial, you can convert a CSV file containing HR data into a bulk request payload and send it to the Microsoft Entra provisioning [/bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API endpoint. The article also provides guidance on how the same integration pattern can be used with any system of record.

## Integration scenario

### Business requirement

Your system of record periodically generates CSV file exports containing worker data. You want to implement an integration that reads data from the CSV file and automatically provisions user accounts in your target directory (on-premises Active Directory for hybrid users and Microsoft Entra ID for cloud-only users).

### Implementation requirement

From an implementation perspective:

- You want to use an Azure Logic Apps workflow to read data from the CSV file exports available in an Azure File Share and send it to the inbound provisioning API endpoint.
- In your Azure Logic Apps workflow, you don't want to implement the complex logic of comparing identity data between your system of record and target directory.
- You want to use Microsoft Entra provisioning service to apply your IT managed provisioning rules to automatically create/update/enable/disable accounts in the target directory (on-premises Active Directory or Microsoft Entra ID).

[![Graphic of Azure Logic Apps-based integration.](media/inbound-provisioning-api-logic-apps/logic-apps-integration-overview.png)](media/inbound-provisioning-api-logic-apps/logic-apps-integration-overview.png#lightbox)

### Integration scenario variations

While this tutorial uses a CSV file as a system of record, you can customize the sample Azure Logic Apps workflow to read data from any system of record. Azure Logic Apps provides a wide range of [built-in connectors](/en-us/azure/logic-apps/connectors/built-in/reference/) and [managed connectors](/en-us/connectors/connector-reference/connector-reference-logicapps-connectors) with pre-built triggers and actions that you can use in your integration workflow.

Here's a list of enterprise integration scenario variations, where API-driven inbound provisioning can be implemented with a Logic Apps workflow.

| # | System of record | Integration guidance on using Logic Apps to read source data |
| --- | --- | --- |
| 1 | Files stored on SFTP server | Use either the [built-in SFTP connector](/en-us/azure/logic-apps/connectors/built-in/reference/sftp/) or [managed SFTP SSH connector](/en-us/azure/connectors/connectors-sftp-ssh) to read data from files stored on the SFTP server. |
| 2 | Database table | If you're using an Azure SQL server or on-premises SQL Server, use the [SQL Server](/en-us/azure/connectors/connectors-create-api-sqlazure) connector to read your table data.  If you're using an Oracle database, use the [Oracle database](/en-us/azure/connectors/connectors-create-api-oracledatabase) connector to read your table data. |
| 3 | On-premises and cloud-hosted SAP S/4 HANA or  Classic on-premises SAP systems, such as R/3 and ECC | Use the [SAP connector](/en-us/azure/logic-apps/logic-apps-using-sap-connector) to retrieve identity data from your SAP system. For examples on how to configure this connector, refer to [common SAP integration scenarios](/en-us/azure/logic-apps/sap-create-example-scenario-workflows) using Azure Logic Apps and the SAP connector. |
| 4 | IBM MQ | Use the [IBM MQ connector](/en-us/azure/connectors/connectors-create-api-mq) to receive provisioning messages from the queue. |
| 5 | Dynamics 365 Human Resources | Use the [Dataverse connector](/en-us/azure/connectors/connect-common-data-service) to read data from [Dataverse tables](/en-us/dynamics365/human-resources/hr-developer-entities) used by Microsoft Dynamics 365 Human Resources. |
| 6 | Any system that exposes REST APIs | If you don't find a connector for your system of record in the Logic Apps connector library, You can create your own [custom connector](/en-us/azure/logic-apps/logic-apps-create-api-app) to read data from your system of record. |

After reading the source data, apply your pre-processing rules and convert the output from your system of record into a bulk request that can be sent to the Microsoft Entra provisioning [bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API endpoint.

Important

If you'd like to share your API-driven inbound provisioning + Logic Apps integration workflow with the community, create a [Logic app template](/en-us/azure/logic-apps/logic-apps-create-azure-resource-manager-templates), document steps on how to use it and submit a pull request for inclusion in the GitHub repository [`entra-id-inbound-provisioning`](https://github.com/AzureAD/entra-id-inbound-provisioning).

## How to use this tutorial

The Logic Apps deployment template published in the [Microsoft Entra inbound provisioning GitHub repository](https://github.com/AzureAD/entra-id-inbound-provisioning/tree/main/LogicApps/CSV2SCIMBulkUpload) automates several tasks. It also has logic for handling large CSV files and chunking the bulk request to send 50 records in each request. Here's how you can test it and customize it per your integration requirements.

Note

The sample Azure Logic Apps workflow is provided "as-is" for implementation reference. If you have questions related to it or if you'd like to enhance it, please use the [GitHub project repository](https://github.com/AzureAD/entra-id-inbound-provisioning).

| # | Automation task | Implementation guidance | Advanced customization |
| --- | --- | --- | --- |
| 1 | Read worker data from the CSV file. | The Logic Apps workflow uses an Azure Function to read the CSV file stored in an Azure File Share. The Azure Function converts CSV data into JSON format. If your CSV file format is different, update the workflow step "Parse JSON" and "Construct SCIMUser". | If your system of record is different, check guidance provided in the section Integration scenario variations on how to customize the Logic Apps workflow by using an appropriate connector. |
| 2 | Pre-process and convert data to SCIM format. | By default, the Logic Apps workflow converts each record in the CSV file to a SCIM Core User + Enterprise User representation. If you plan to use custom SCIM schema extensions, update the step "Construct SCIMUser" to include your custom SCIM schema extensions. | If you want to run C# code for advanced formatting and data validation, use [custom Azure Functions](/en-us/azure/logic-apps/logic-apps-azure-functions). |
| 3 | Use the right authentication method | You can either [use a service principal](inbound-provisioning-api-grant-access#configure-a-service-principal) or [use managed identity](inbound-provisioning-api-grant-access#configure-a-managed-identity) to access the inbound provisioning API. Update the step "Send SCIMBulkPayload to API endpoint" with the right authentication method. | - |
| 4 | Provision accounts in on-premises Active Directory or Microsoft Entra ID. | Configure [API-driven inbound provisioning app](inbound-provisioning-api-configure-app). This generates a unique [/bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API endpoint. Update the step "Send SCIMBulkPayload to API endpoint" to use the right bulkUpload API endpoint. | If you plan to use bulk request with custom SCIM schema, then extend the provisioning app schema to include your custom SCIM schema attributes. |
| 5 | Scan the provisioning logs and retry provisioning for failed records. | This automation isn't yet implemented in the sample Logic Apps workflow. To implement it, refer to the [provisioning logs Graph API](/en-us/graph/api/resources/provisioningobjectsummary). | - |
| 6 | Deploy your Logic Apps based automation to production. | Once you have verified your API-driven provisioning flow and customized the Logic Apps workflow to meet your requirements, deploy the automation in your environment. | - |

## Step 1: Create an Azure Storage account to host the CSV file

The steps documented in this section are optional. If you already have an existing storage account or would like to read the CSV file from another source like SharePoint site or Blob storage, update the Logic App to use your connector of choice.

1. Sign in to the [Azure portal](https://portal.azure.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Search for "Storage accounts" and create a new storage account. [![Screenshot of creating new storage account.](media/inbound-provisioning-api-logic-apps/storage-accounts.png)](media/inbound-provisioning-api-logic-apps/storage-accounts.png#lightbox)
3. Assign a resource group and give it a name. [![Screenshot of resource group assignment.](media/inbound-provisioning-api-logic-apps/assign-resource-group.png)](media/inbound-provisioning-api-logic-apps/assign-resource-group.png#lightbox)
4. After the storage account is created, go to the resource.
5. Select "File share" menu option and create a new file share. [![Screenshot of creating new file share.](media/inbound-provisioning-api-logic-apps/create-new-file-share.png)](media/inbound-provisioning-api-logic-apps/create-new-file-share.png#lightbox)
6. Verify that the file share creation is successful. [![Screenshot of file share created.](media/inbound-provisioning-api-logic-apps/verify-file-share-creation.png)](media/inbound-provisioning-api-logic-apps/verify-file-share-creation.png#lightbox)
7. Upload a sample CSV file to the file share using the upload option.
8. Here's a screenshot of the columns in the CSV file. [![Screenshot of columns in Excel.](media/inbound-provisioning-api-powershell/columns.png)](media/inbound-provisioning-api-powershell/columns.png#lightbox)

## Step 2: Configure Azure Function CSV2JSON converter

1. In the browser associated with your Azure portal, open the GitHub repository URL - https://github.com/joelbyford/CSVtoJSONcore.
2. Select the link "Deploy to Azure" to deploy this Azure Function to your Azure tenant. [![Screenshot of deploying Azure Function.](media/inbound-provisioning-api-logic-apps/deploy-azure-function.png)](media/inbound-provisioning-api-logic-apps/deploy-azure-function.png#lightbox)
3. Specify the resource group under which to deploy this Azure function. [![Screenshot of configuring Azure Function resource group.](media/inbound-provisioning-api-logic-apps/azure-function-resource-group.png)](media/inbound-provisioning-api-logic-apps/azure-function-resource-group.png#lightbox)

    If you get the error "[This region has quota of 0 instances](/en-us/answers/questions/751909/azure-function-app-region-has-quota-of-0-instances)", try selecting a different region.
4. Ensure that the deployment of the Azure Function as an App Service is successful.
5. Go to the resource group and open the WebApp configuration. Ensure it's in "Running" state. Copy the default domain name associated with the Web App. [![Screenshot of Azure Function Web App domain name.](media/inbound-provisioning-api-logic-apps/web-app-domain-name.png)](media/inbound-provisioning-api-logic-apps/web-app-domain-name.png#lightbox)
6. Run the following PowerShell script to test if the CSVtoJSON endpoint works as expected. Set the correct values for the variables `$csvFilePath` and `$uri` in the script.

    ```powershell
    # Step 1: Read the CSV file 
    $csvFilePath = "C:\Path-to-CSV-file\hr-user-data.csv" 
    $csvContent = Get-Content -Path $csvFilePath 
    
    # Step 2: Set up the request 
    $uri = "https://az-function-webapp-your-domain/csvtojson" 
    $headers = @{ 
         "Content-Type" = "text/csv" 
    } 
    $body = $csvContent -join "`n"  # Join the CSV lines into a single string 
    
    # Step 3: Send the POST request 
    $response = Invoke-WebRequest -Uri $uri -Method POST -Headers $headers -Body $body 
    
    # Output and format the JSON response 
    $response.Content | ConvertFrom-JSON | ConvertTo-JSON 
    ```
7. If the Azure Function deployment is successful, then the last line of the script outputs the JSON version of the CSV file.

    [![Screenshot of Azure Function response.](media/inbound-provisioning-api-logic-apps/azure-function-response.png)](media/inbound-provisioning-api-logic-apps/azure-function-response.png#lightbox) .
8. To allow Logic Apps to invoke this Azure Function, in the CORS setting for the WebApp enter asterisk (\*) and "Save" the configuration. [![Screenshot of Azure Function CORS setting.](media/inbound-provisioning-api-logic-apps/azure-function-cors-setting.png)](media/inbound-provisioning-api-logic-apps/azure-function-cors-setting.png#lightbox)

## Step 3: Configure API-driven inbound user provisioning

- Configure [API-driven inbound user provisioning](inbound-provisioning-api-configure-app).

## Step 4: Configure your Azure Logic Apps workflow

1. Select the button below to deploy the Azure Resource Manager template for the CSV2SCIMBulkUpload Logic Apps workflow.
2. Under instance details, update the highlighted items, copy-pasting values from the previous steps. [![Screenshot of Azure Logic Apps instance details.](media/inbound-provisioning-api-logic-apps/logic-apps-instance-details.png)](media/inbound-provisioning-api-logic-apps/logic-apps-instance-details.png#lightbox)
3. For the `Azurefile_access Key` parameter, open your Azure file storage account and copy the access key present under "Security and Networking".[![Screenshot of Azure File access keys.](media/inbound-provisioning-api-logic-apps/azure-file-access-keys.png)](media/inbound-provisioning-api-logic-apps/azure-file-access-keys.png#lightbox)
4. Select "Review and Create" option to start the deployment.
5. Once the deployment is complete, you see the following message. [![Screenshot of Azure Logic Apps deployment complete.](media/inbound-provisioning-api-logic-apps/logic-apps-deployment-complete.png)](media/inbound-provisioning-api-logic-apps/logic-apps-deployment-complete.png#lightbox)

## Step 5: Configure system assigned managed identity

1. Visit the Settings -&gt; Identity blade of your Logic Apps workflow.
2. Enable **System assigned managed identity**. [![Screenshot of enabling managed identity.](media/inbound-provisioning-api-logic-apps/enable-managed-identity.png)](media/inbound-provisioning-api-logic-apps/enable-managed-identity.png#lightbox)
3. You'll see a prompt to confirm the use of the managed identity. Select **Yes**.
4. Grant the managed identity [permissions to perform bulk upload](inbound-provisioning-api-grant-access#configure-a-managed-identity).

## Step 6: Review and adjust the workflow steps

1. Open the Logic App in the designer view. [![Screenshot of Azure Logic Apps designer view.](media/inbound-provisioning-api-logic-apps/designer-view.png)](media/inbound-provisioning-api-logic-apps/designer-view.png#lightbox)
2. Review the configuration of each step in the workflow to make sure it's correct.
3. Open the "Get file content using path" step and correct it to browse to the Azure File Storage in your tenant. [![Screenshot of get file content.](media/inbound-provisioning-api-logic-apps/get-file-content.png)](media/inbound-provisioning-api-logic-apps/get-file-content.png#lightbox)
4. Update the connection if necessary.
5. Make sure your "Convert CSV to JSON" step is pointing to the right Azure Function Web App instance. [![Screenshot of Azure Function call invocation to convert from CSV to JSON.](media/inbound-provisioning-api-logic-apps/convert-file-format.png)](media/inbound-provisioning-api-logic-apps/convert-file-format.png#lightbox)
6. If your CSV file content / headers is different, then update the "Parse JSON" step with the JSON output that you can retrieve from your API call to the Azure Function. Use PowerShell output from Step 2. [![Screenshot of Parse JSON step.](media/inbound-provisioning-api-logic-apps/parse-json-step.png)](media/inbound-provisioning-api-logic-apps/parse-json-step.png#lightbox)
7. In the step "Construct SCIMUser", ensure that the CSV fields map correctly to the SCIM attributes that will be used for processing.

    [![Screenshot of Construct SCIM user step.](media/inbound-provisioning-api-logic-apps/construct-scim-user.png)](media/inbound-provisioning-api-logic-apps/construct-scim-user.png#lightbox)
8. In the step "Send SCIMBulkPayload to API endpoint", ensure you're using the right API endpoint and authentication mechanism.

    [![Screenshot of invoking bulk upload API with managed identity.](media/inbound-provisioning-api-logic-apps/invoke-bulk-upload-api.png)](media/inbound-provisioning-api-logic-apps/invoke-bulk-upload-api.png#lightbox)

## Step 7: Run trigger and test your Logic Apps workflow

1. In the "Generally Available" version of the Logic Apps designer, select on Run Trigger to manually execute the workflow. [![Screenshot of running the Logic App.](media/inbound-provisioning-api-logic-apps/run-logic-app.png)](media/inbound-provisioning-api-logic-apps/run-logic-app.png#lightbox)
2. After the execution is complete, review what action Logic Apps performed in each iteration.
3. In the final iteration, you should see the Logic Apps upload data to the inbound provisioning API endpoint. Look for `202 Accept` status code. You can copy-paste and verify the bulk upload request. [![Screenshot of the Logic Apps execution result.](media/inbound-provisioning-api-logic-apps/execution-results.png)](media/inbound-provisioning-api-logic-apps/execution-results.png#lightbox)