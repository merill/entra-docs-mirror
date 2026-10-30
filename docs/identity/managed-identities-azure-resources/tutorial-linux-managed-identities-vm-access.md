---
layout: Conceptual
title: Tutorial - Use a Linux VM/VMSS to access Azure resources - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/tutorial-linux-managed-identities-vm-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: A tutorial that shows you how to use a Linux VM/VMSS to access Azure resources.
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.date: 2024-06-10T00:00:00.0000000Z
ms.custom: devx-track-arm-template, devx-track-azurecli, linux-related-content
zone_pivot_groups: identity-linux-vm-access
locale: en-us
document_id: 5dd20c93-fedd-80b2-3b59-c2b546d291b4
document_version_independent_id: 5dd20c93-fedd-80b2-3b59-c2b546d291b4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/tutorial-linux-managed-identities-vm-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/tutorial-linux-managed-identities-vm-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/tutorial-linux-managed-identities-vm-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/3876df09-7a38-488f-a709-a37472f2b598
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/9903f988-6d7c-450a-a74a-984d8652a27f
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
platformId: 739a579a-b117-0590-1f98-4d151f7b8b39
---

# Tutorial - Use a Linux VM/VMSS to access Azure resources - Managed identities for Azure resources | Microsoft Learn

## Prerequisites

- An understanding of managed identities. If you're not familiar with the managed identities for Azure resources feature, see this [overview](overview).
- An Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- *Owner* permissions at the appropriate scope (your subscription or resource group) to perform required resource creation and role management steps. If you need assistance with role assignment, see [Assign Azure roles to manage access to your Azure subscription resources](/en-us/azure/role-based-access-control/role-assignments-portal).
- A Linux virtual machine (VM) that has system assigned managed identities enabled.
    - If you need to create a VM for this tutorial, see [Create a virtual machine with system-assigned identity enabled](how-to-configure-managed-identities).

::: zone pivot="identity-linux-mi-vm-access-data-lake"

## Use a Linux VM system-assigned managed identity to access Azure Data Lake Store

This tutorial shows you how to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Data Lake Store.

You'll learn how to:

- Grant your VM access to Azure Data Lake Store.
- Get an access token by using the VM's system-assigned managed identity to access Azure Data Lake Store.

## Grant access

This section shows how to grant your VM access to files and folders in Azure Data Lake Store. For this step, you can use an existing Data Lake Store instance or create a new one. To create a Data Lake Store instance by using the Azure portal, follow the [Azure Data Lake Store quickstart](/en-us/azure/data-lake-store/data-lake-store-get-started-portal). There are also quickstarts that use Azure CLI and Azure PowerShell in the [Azure Data Lake Store documentation](/en-us/azure/data-lake-store/data-lake-store-overview).

In Data Lake Store, create a new folder and grant the Linux VM system-assigned managed identity permission to read, write, and execute files in that folder:

1. In the Azure portal, select **Data Lake Store** in the left pane.
2. Select the Data Lake Store instance that you want to use.
3. Select **Data Explorer** on the command bar.
4. The root folder of the Data Lake Store instance is selected. Select **Access** on the command bar.
5. Select **Add**. In the **Select** box, enter the name of your VM; for example, **DevTestVM**. Select your VM from the search results, then select **Select**.
6. Select **Select Permissions**. Select **Read** and **Execute**, add to **This folder**, add as **An access permission only**, then select **Ok**. The permission should be added successfully.
7. Close the **Access** pane.
8. Create a new folder, then select **New Folder** on the command bar and give the new folder a name; for example, **TestFolder**, then select **Ok**.
9. Select the folder that you created, then select **Access** on the command bar.
10. Select **Add**, then in the **Select** box, enter the name of your VM.
11. Select your VM from the search results, then select **Select**.
12. Select **Select Permissions**, then select **Read**, then **Write** and **Execute**.
13. Select to add to **This folder**, then add as **An access permission entry and a default permission entry**, then select **Ok**. The permission should be added successfully.

Managed identities for Azure resources can now perform all operations on files in the folder that you created. For more information on managing access to Data Lake Store, see [Access Control in Data Lake Store](/en-us/azure/data-lake-store/data-lake-store-access-control).

## Get an access token

This section shows how to obtain an access token and call the Data Lake Store file system. Azure Data Lake Store natively supports Microsoft Entra authentication, so it can directly accept access tokens obtained via using managed identities for Azure resources.

To authenticate to the Data Lake Store file system, you send an access token issued by Microsoft Entra ID to your Data Lake Store file system endpoint. The access token is in an authorization header in the format `Bearer \<ACCESS_TOKEN_VALUE\>`. To learn more about Data Lake Store support for Microsoft Entra authentication, see [Authentication with Data Lake Store using Microsoft Entra ID](/en-us/azure/data-lake-store/data-lakes-store-authentication-using-azure-active-directory).

Next, you authenticate to the REST API for the Data Lake Store file system by using cURL to make REST requests.

Note

The client SDKs for the Data Lake Store file system do not yet support managed identities for Azure resources.

To complete these steps, you need an SSH client. If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows) or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

1. In the portal, browse to your Linux VM, then in the **Overview** section, select **Connect**.
2. Connect to the VM by using the SSH client of your choice.
3. In the terminal window, using cURL make a request to the local managed identities Azure for Azure resources endpoint to get an access token for the Data Lake Store file system. The resource identifier for Data Lake Store is `https://datalake.azure.net/`. It's important to include the trailing slash in the resource identifier.

    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fdatalake.azure.net%2F' -H Metadata:true   
    ```

    A successful response returns the access token that you use to authenticate to Data Lake Store:

    ```bash
    {"access_token":"eyJ0eXAiOiJ...",
     "refresh_token":"",
     "expires_in":"3599",
     "expires_on":"1508119757",
     "not_before":"1508115857",
     "resource":"https://datalake.azure.net/",
     "token_type":"Bearer"}
    ```
4. By using cURL, make a request to your Data Lake Store file system's REST endpoint to list the folders in the root folder. This is the best way to check that everything is configured correctly. Copy the value of the access token from the previous step. It's important that the string `Bearer` in the Authorization header has a capital "B." You can find the name of your Data Lake Store instance in the **Overview** section of the **Data Lake Store** pane in the Azure portal.

    ```bash
    curl https://<YOUR_ADLS_NAME>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS -H "Authorization: Bearer <ACCESS_TOKEN>"
    ```

    A successful response looks like this:

    ```bash
    {"FileStatuses":{"FileStatus":[{"length":0,"pathSuffix":"TestFolder","type":"DIRECTORY","blockSize":0,"accessTime":1507934941392,"modificationTime":1508105430590,"replication":0,"permission":"770","owner":"bd0e76d8-ad45-4fe1-8941-04a7bf27f071","group":"bd0e76d8-ad45-4fe1-8941-04a7bf27f071"}]}}
    ```
5. Now upload a file to your Data Lake Store instance. First, create a file to upload.

    ```bash
    echo "Test file." > Test1.txt
    ```
6. By using cURL, make a request to your Data Lake Store file system's REST endpoint to upload the file to the folder that you created earlier. The upload involves a redirect, and cURL follows the redirect automatically.

    ```bash
    curl -i -X PUT -L -T Test1.txt -H "Authorization: Bearer <ACCESS_TOKEN>" 'https://<YOUR_ADLS_NAME>.azuredatalakestore.net/webhdfs/v1/<FOLDER_NAME>/Test1.txt?op=CREATE' 
    ```

    A successful response looks like this:

    ```bash
    HTTP/1.1 100 Continue
    HTTP/1.1 307 Temporary Redirect
    Cache-Control: no-cache, no-cache, no-store, max-age=0
    Pragma: no-cache
    Expires: -1
    Location: https://mytestadls.azuredatalakestore.net/webhdfs/v1/TestFolder/Test1.txt?op=CREATE&write=true
    x-ms-request-id: 756f6b24-0cca-47ef-aa12-52c3b45b954c
    ContentLength: 0
    x-ms-webhdfs-version: 17.04.22.00
    Status: 0x0
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=15724800; includeSubDomains
    Date: Sun, 15 Oct 2017 22:10:30 GMT
    Content-Length: 0
    
    HTTP/1.1 100 Continue
    
    HTTP/1.1 201 Created
    Cache-Control: no-cache, no-cache, no-store, max-age=0
    Pragma: no-cache
    Expires: -1
    Location: https://mytestadls.azuredatalakestore.net/webhdfs/v1/TestFolder/Test1.txt?op=CREATE&write=true
    x-ms-request-id: af5baa07-3c79-43af-a01a-71d63d53e6c4
    ContentLength: 0
    x-ms-webhdfs-version: 17.04.22.00
    Status: 0x0
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=15724800; includeSubDomains
    Date: Sun, 15 Oct 2017 22:10:30 GMT
    Content-Length: 0
    ```

Finally, you can now use other APIs for the Data Lake Store file system to append to files, download files, and more.

::: zone-end

::: zone pivot="identity-linux-mi-vm-access-storage"

## Use a Linux VM system-assigned managed identity to access Azure Storage

This tutorial shows you how to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Storage.

You'll learn how to:

- Create a storage account
- Create a blob container in a storage account
- Grant the Linux VM's Managed Identity access to an Azure Storage container
- Get an access token and use it to call Azure Storage

## Create a storage account

To run the CLI scripts in this example, you have two options:

- Use [Azure Cloud Shell](/en-us/azure/cloud-shell/overview) either from the Azure portal, or via the **Try It** button, located in the top-right corner of each code block.
- [Install the latest version of CLI 2.0](/en-us/cli/azure/install-azure-cli) (2.0.23 or later) if you prefer to use a local CLI console.

First, create a storage account.

1. Select the **+ Create a resource** button found on the upper left-hand corner of the Azure portal.
2. Select **Storage**, then **Storage account - blob, file, table, queue**.
3. Under **Name**, enter a name for the storage account.
4. **Deployment model** and **Account kind** should be set to **Resource manager** and **Storage (general purpose v1)**.
5. Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.
6. Select **Create**.

    ![Screenshot showing the new storage account creation screen.](media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## Create a blob container and upload a file to the storage account

Files require blob storage so you need to create a blob container in which to store the file. You then upload a file to the blob container in the new storage account.

1. Navigate to your newly created storage account.
2. Select **Blob Service**, then **Containers**.
3. Select **+ Container** on the top of the page.
4. Select **New container**, then enter a name for the container.
5. Make sure that **Public access level** is the default value.

    ![Screenshot showing the storage container creation screen.](media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)
6. Using an editor of your choice, create a file titled *hello world.txt* on your local machine. Open the file and add the text *Hello world!*, and then save it.
7. Select the container name, then **Upload**. This uploads the file to the newly created container.
8. In the **Upload blob** pane, in the **Files** section, select the folder icon and browse to the file **hello\_world.txt** on your local machine.
9. Select the file, then select **Upload**.

    ![Screenshot showing the upload text file section.](media/msi-tutorial-linux-vm-access-storage/upload-text-file.png)

## Grant your VM access to an Azure Storage container

You can use the VM's managed identity to retrieve the data in the Azure storage blob. Managed identities for Azure resources, can be used to authenticate to resources that support Microsoft Entra authentication. Grant access by assigning the [storage-blob-data-reader](/en-us/azure/role-based-access-control/built-in-roles#storage-blob-data-reader) role to the managed-identity at the scope of the resource group that contains your storage account.

For detailed steps, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

Note

For more information on the various roles that you can use to grant permissions to storage review [Authorize access to blobs and queues using Microsoft Entra ID](/en-us/azure/storage/blobs/authorize-access-azure-active-directory#assign-azure-roles-for-access-rights)

## Get an access token and use it to call Azure Storage

Azure Storage natively supports Microsoft Entra authentication, so it can directly accept access tokens obtained using a Managed Identity. This is part of Azure Storage's integration with Microsoft Entra ID, and is different from supplying credentials on the connection string.

To complete the following steps, you need to work from the VM created earlier and you need an SSH client to connect to it.

If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

1. In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page select **Connect**. Copy the string to connect to your VM.
2. **Connect** to the VM with the SSH client of your choice.
3. In the terminal window, use CURL to make a request to the local Managed Identity endpoint to get an access token for Azure Storage.

    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fstorage.azure.com%2F' -H Metadata:true
    ```
4. Use the access token to access Azure Storage. For example, to read the contents of the sample file that you previously uploaded to the container, replace the values of `<STORAGE ACCOUNT>`, `<CONTAINER NAME>`, and `<FILE NAME>` with the values you specified earlier, and `<ACCESS TOKEN>` with the token returned in the previous step.

    ```bash
    curl https://<STORAGE ACCOUNT>.blob.core.windows.net/<CONTAINER NAME>/<FILE NAME> -H "x-ms-version: 2017-11-09" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    The response contains the contents of the file:

    ```bash
    Hello world! :)
    ```

Lastly, you can also store the token in a variable and pass it to the second command as shown:

```bash
# Run the first curl command and capture its output in a variable
access_token=$(curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fstorage.azure.com%2F' -H Metadata:true | jq -r '.access_token')

# Run the second curl command with the access token
curl "https://<STORAGE ACCOUNT>.blob.core.windows.net/<CONTAINER NAME>/<FILE NAME>" \
  -H "x-ms-version: 2017-11-09" \
  -H "Authorization: Bearer $access_token"

```

::: zone-end

::: zone pivot="identity-linux-mi-vm-access-sas-key"

## Use a Linux VM system-assigned managed identity to access Azure Storage via a SAS credential

This tutorial shows you how to use a system-assigned managed identity for a Linux virtual machine (VM) to obtain a storage Shared Access Signature (SAS) credential; specifically, a [Service SAS credential](/en-us/azure/storage/common/storage-sas-overview?toc=/azure/storage/blobs/toc.json#types-of-shared-access-signatures).

Note

The SAS key generated in this tutorial will not be restricted/bound to the VM.

A Service SAS grants limited access to objects in a storage account without exposing an account access key. Access can be granted for a limited time and a specific service. You can use a SAS credential as usual when doing storage operations; for example, when using the Storage SDK. In this tutorial, you'll upload and download a blob using Azure Storage CLI.

You'll learn how to:

- Create a storage account
- Create a blob container in the storage account
- Grant your VM access to a storage account SAS in Resource Manager
- Get an access token using your VM's identity, and use it to retrieve the SAS from Resource Manager

## Create a storage account

If you don't already have one, you'll need to create a storage account. You can choose to skip this step and grant your VM system-assigned managed identity access to the keys of an existing storage account.

1. Select the **+/Create new service** button, located at the upper-left corner of the Azure portal.
2. Select **Storage**, then **Storage Account**, then the **Create storage account** panel appears.
3. Enter a **Name** for the storage account. Remember this name, as you'll need it later.
4. Make sure that **Deployment model** is set to *Resource Manager*, and **Account kind** is set to *General purpose*.
5. Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM.
6. Select **Create** to finish creating a storage account.

    ![Screenshot showing the new storage account creation screen.](media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## Create a blob container in the storage account

Later in the tutorial, you'll upload and download a file to the new storage account. Because files require blob storage, you need to create a blob container in which to store the file.

1. Navigate to your newly created storage account.
2. Select the **Containers** link in the left panel, under **Blob service**.
3. Select **+ Container** at the top of the page, then a **New container** panel appears.
4. Give the container a name, select an access level, then select **OK**. You'll need the name you specified later in the tutorial.

    ![Screenshot showing storage container creation screen.](media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## Grant your VM's system-assigned managed identity access to use a storage SAS

Azure Storage natively supports Microsoft Entra authentication, so you can use your VM's system-assigned managed identity to retrieve a storage SAS from Resource Manager. Then you can use the SAS to access storage.

In this section, you grant your VM's system-assigned managed identity access to your storage account SAS. Assign the [Storage Account Contributor](/en-us/azure/role-based-access-control/built-in-roles#storage-account-contributor) role to the managed-identity at the scope of the resource group that contains your storage account.

For detailed steps, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

Note

For more information on the various roles that you can use to grant permissions to storage review [Authorize access to blobs and queues using Microsoft Entra ID.](/en-us/azure/storage/blobs/authorize-access-azure-active-directory#assign-azure-roles-for-access-rights)

## Get an access token using the VM's identity and use it to call Azure Resource Manager

For the remainder of this tutorial, you work from the VM that you created earlier.

You need an SSH client to complete these steps. If you're using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/install-win10). If you need assistance configuring your SSH client's keys, see:

- [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows)
- [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

Once you have your SSH client, follow these steps:

1. In the Azure portal, navigate to **Virtual Machines**, then go to your Linux virtual machine.
2. From the **Overview** page, select **Connect** at the top of the screen.
3. Copy the string to connect to your VM.
4. Connect to your VM using your SSH client.
5. Enter your **Password** that you added when creating the **Linux VM**. You should then be successfully signed in.
6. Use CURL to get an access token for Azure Resource Manager.

The CURL request and response for the access token is below:

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true    
```

Note

In the previous request, the value of the `resource` parameter must be an exact match for what is expected by Microsoft Entra ID. When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.

In the following response, the access\_token element has been shortened for brevity.

```json
{
  "access_token":"eyJ0eXAiOiJ...",
  "refresh_token":"",
  "expires_in":"3599",
  "expires_on":"1504130527",
  "not_before":"1504126627",
  "resource":"https://management.azure.com",
  "token_type":"Bearer"
}
```

## Get a SAS credential from Azure Resource Manager to make storage calls

Next, use CURL to call Resource Manager using the access token we retrieved in the previous section. Use this to create a storage SAS credential. Once you have the SAS credential, you can call storage upload/download operations.

For this request, use the following HTTP request parameters to create the SAS credential:

```JSON
{
    "canonicalizedResource":"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>",
    "signedResource":"c",              // The kind of resource accessible with the SAS, in this case a container (c).
    "signedPermission":"rcw",          // Permissions for this SAS, in this case (r)ead, (c)reate, and (w)rite.  Order is important.
    "signedProtocol":"https",          // Require the SAS be used on https protocol.
    "signedExpiry":"<EXPIRATION TIME>" // UTC expiration time for SAS in ISO 8601 format, for example 2017-09-22T00:06:00Z.
}
```

Include these parameters in the body of the POST request for the SAS credential. For more information on the parameters for creating a SAS credential, see the [List Service SAS REST reference](/en-us/rest/api/storagerp/storage-accounts/list-service-sas).

Use the following CURL request to get the SAS credential. Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, `<STORAGE ACCOUNT NAME>`, `<CONTAINER NAME>`, and `<EXPIRATION TIME>` parameter values with your own values. Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier:

```bash
curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE ACCOUNT NAME>/listServiceSas/?api-version=2017-06-01 -X POST -d "{\"canonicalizedResource\":\"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>\",\"signedResource\":\"c\",\"signedPermission\":\"rcw\",\"signedProtocol\":\"https\",\"signedExpiry\":\"<EXPIRATION TIME>\"}" -H "Authorization: Bearer <ACCESS TOKEN>"
```

Note

The text in the prior URL is case sensitive, so ensure if you are using upper-lowercase for your resource groups to reflect it accordingly. Also, it’s important to know this is a POST request, not a GET request.

The CURL response returns the SAS credential:

```bash
{"serviceSasToken":"sv=2015-04-05&sr=c&spr=https&st=2017-09-22T00%3A10%3A00Z&se=2017-09-22T02%3A00%3A00Z&sp=rcw&sig=QcVwljccgWcNMbe9roAJbD8J5oEkYoq%2F0cUPlgriBn0%3D"} 
```

On a Linux VM, create a sample blob file to upload to your blob storage container using the following command:

```bash
echo "This is a test file." > test.txt
```

Next, authenticate with the CLI `az storage` command using the SAS credential, and then upload the file to the blob container. For this step, you'll need to [install the latest Azure CLI](/en-us/cli/azure/install-azure-cli) on your VM, if you haven't already.

```azurecli
 az storage blob upload --container-name 
                        --file 
                        --name
                        --account-name 
                        --sas-token
```

Response:

```JSON
Finished[#############################################################]  100.0000%
{
  "etag": "\"0x8D4F9929765C139\"",
  "lastModified": "2017-09-21T03:58:56+00:00"
}
```

You can also download the file using the Azure CLI and authenticating with the SAS credential.

Request:

```azurecli
az storage blob download --container-name
                         --file 
                         --name 
                         --account-name
                         --sas-token
```

Response:

```JSON
{
  "content": null,
  "metadata": {},
  "name": "testblob",
  "properties": {
    "appendBlobCommittedBlockCount": null,
    "blobType": "BlockBlob",
    "contentLength": 16,
    "contentRange": "bytes 0-15/16",
    "contentSettings": {
      "cacheControl": null,
      "contentDisposition": null,
      "contentEncoding": null,
      "contentLanguage": null,
      "contentMd5": "Aryr///Rb+D8JQ8IytleDA==",
      "contentType": "text/plain"
    },
    "copy": {
      "completionTime": null,
      "id": null,
      "progress": null,
      "source": null,
      "status": null,
      "statusDescription": null
    },
    "etag": "\"0x8D4F9929765C139\"",
    "lastModified": "2017-09-21T03:58:56+00:00",
    "lease": {
      "duration": null,
      "state": "available",
      "status": "unlocked"
    },
    "pageBlobSequenceNumber": null,
    "serverEncrypted": false
  },
  "snapshot": null
}
```

::: zone-end

::: zone pivot="identity-linux-mi-vm-access-key"

## Use a Linux VM system-assigned managed identity to access Azure Storage via access key

This tutorial shows you how to use a system-assigned managed identity for a Linux virtual machine (VM) to retrieve storage account access keys. You can use a storage access key as usual when doing storage operations; for example, when using the Storage SDK. For this tutorial, you upload and download blobs using Azure CLI.

You'll learn how to:

- Grant your VM access to storage account access keys in Resource Manager
- Get an access token using your VM's identity, and use it to retrieve the storage access keys from Resource Manager

## Create a storage account

If you don't have an existing storage account before starting this tutorial, you need to create one. If you do have an existing storage account, follow these steps to grant your VM system-assigned managed identity access to the keys for your existing storage account.

1. Select the **+/Create new service** button, located at the upper-left corner of the Azure portal.
2. Select **Storage**, then **Storage Account**, then the **Create storage account** panel appears.
3. Enter a **Name** for the storage account. Remember this name, as you'll need it later.
4. Make sure that **Deployment model** is set to *Resource Manager*, and **Account kind** is set to *General purpose*.
5. Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM.
6. Select **Create** to finish creating a storage account.

    ![Screenshot showing new storage account creation.](media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## Create a blob container in the storage account

Later in the tutorial, you'll upload and download a file to the new storage account. Because files require blob storage, you need to create a blob container in which to store the file.

1. Navigate to your newly created storage account.
2. Select the **Containers** link in the left panel, under **Blob service**.
3. Select **+ Container** at the top of the page, then a **New container** panel appears.
4. Give the container a name, select an access level, then select **OK**. You'll need the name you specified later in the tutorial.

    ![Screenshot showing the creation of a storage container.](media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## Grant your VM's system-assigned managed identity access to use storage account access keys

Azure Storage doesn't natively support Microsoft Entra authentication. However, you can use your VM's system-assigned managed identity to retrieve a storage SAS from Resource Manager, then use the SAS to access storage. In this step, you grant your VM's system-assigned managed identity access to your storage account SAS. Grant access by assigning the [Storage Account Contributor](/en-us/azure/role-based-access-control/built-in-roles#storage-account-contributor) role to the managed-identity at the scope of the resource group that contains your storage account.

For detailed steps, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

Note

For more information on the various roles that you can use to grant permissions to storage review [Authorize access to blobs and queues using Microsoft Entra ID.](/en-us/azure/storage/blobs/authorize-access-azure-active-directory#assign-azure-roles-for-access-rights)

## Get an access token using the VM's identity and use it to call Azure Resource Manager

For the remainder of the tutorial, we work from the VM we created earlier.

To complete these steps, you need an SSH client. If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/install). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

1. In the Azure portal, navigate to **Virtual Machines**, select your Linux virtual machine, then from the **Overview** page select **Connect** at the top. Copy the string to connect to your VM.
2. Connect to your VM using your SSH client.
3. Next, you need to enter the **Password** you added when creating the **Linux VM**.
4. Use CURL to get an access token for Azure Resource Manager.

    The CURL request and response for the access token is below:

    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true
    ```

    Note

    In the previous request, the value of the "resource" parameter must be an exact match for what is expected by Microsoft Entra ID. When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI. In the following response, the access\_token element as been shortened for brevity.

    ```json
    {
      "access_token": "eyJ0eXAiOiJ...",
      "refresh_token": "",
      "expires_in": "3599",
      "expires_on": "1504130527",
      "not_before": "1504126627",
      "resource": "https://management.azure.com",
      "token_type": "Bearer"
    }
    ```

## Get storage account access keys from Azure Resource Manager to make storage calls

Now use CURL to call Resource Manager using the access token we retrieved in the previous section, to retrieve the storage access key. Once we have the storage access key, we can call storage upload/download operations. Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<STORAGE ACCOUNT NAME>` parameter values with your own values. Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier:

```bash
curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE ACCOUNT NAME>/listKeys?api-version=2016-12-01 --request POST -d "" -H "Authorization: Bearer <ACCESS TOKEN>" 
```

Note

The text in the prior URL is case sensitive, so ensure if you are using upper-lowercase for your Resource Groups to reflect it accordingly. Additionally, it’s important to know that this is a POST request not a GET request and ensure you pass a value to capture a length limit with -d that can be NULL.

The CURL response gives you the list of Keys:

```bash
{"keys":[{"keyName":"key1","permissions":"Full","value":"iqDPNt..."},{"keyName":"key2","permissions":"Full","value":"U+uI0B..."}]} 
```

Create a sample blob file to upload to your blob storage container. On a Linux VM, you can do this with the following command.

```bash
echo "This is a test file." > test.txt
```

Next, authenticate with the CLI `az storage` command using the storage access key, and upload the file to the blob container. For this step, you need to [install the latest Azure CLI](/en-us/cli/azure/install-azure-cli) on your VM, if you haven't already.

```azurecli
az storage blob upload -c <CONTAINER NAME> -n test.txt -f test.txt --account-name <STORAGE ACCOUNT NAME> --account-key <STORAGE ACCOUNT KEY>
```

Response:

```JSON
Finished[#############################################################]  100.0000%
{
  "etag": "\"0x8D4F9929765C139\"",
  "lastModified": "2017-09-12T03:58:56+00:00"
}
```

Additionally, you can download the file using the Azure CLI and authenticating with the storage access key.

Request:

```azurecli
az storage blob download -c <CONTAINER NAME> -n test.txt -f test-download.txt --account-name <STORAGE ACCOUNT NAME> --account-key <STORAGE ACCOUNT KEY>
```

Response:

```JSON
{
  "content": null,
  "metadata": {},
  "name": "test.txt",
  "properties": {
    "appendBlobCommittedBlockCount": null,
    "blobType": "BlockBlob",
    "contentLength": 21,
    "contentRange": "bytes 0-20/21",
    "contentSettings": {
      "cacheControl": null,
      "contentDisposition": null,
      "contentEncoding": null,
      "contentLanguage": null,
      "contentMd5": "LSghAvpnElYyfUdn7CO8aw==",
      "contentType": "text/plain"
    },
    "copy": {
      "completionTime": null,
      "id": null,
      "progress": null,
      "source": null,
      "status": null,
      "statusDescription": null
    },
    "etag": "\"0x8D5067F30D0C283\"",
    "lastModified": "2017-09-28T14:42:49+00:00",
    "lease": {
      "duration": null,
      "state": "available",
      "status": "unlocked"
    },
    "pageBlobSequenceNumber": null,
    "serverEncrypted": false
  },
  "snapshot": null
}
```

::: zone-end

::: zone pivot="identity-linux-mi-vm-access-key-vault"

## Use a Linux VM system-assigned managed identity to access Azure Key Vault

This tutorial shows you how a Linux virtual machine (VM) can use a system-assigned managed identity to access [Azure Key Vault](/en-us/azure/key-vault/general/overview). Key Vault makes it possible for your client application to then use a secret to access resources not secured by Microsoft Entra ID. Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Microsoft Entra authentication, without including authentication information in your code.

You'll learn how to:

- Grant your VM access to a secret stored in a Key Vault
- Get an access token using the VM's identity and use it to retrieve the secret from the Key Vault

## Create a Key Vault

You also need a Linux Virtual machine that has system assigned managed identities enabled.

- If you need to create a virtual machine for this tutorial, you can follow the article titled [Create a Linux virtual machine with the Azure portal](/en-us/azure/virtual-machines/linux/quick-create-portal#create-virtual-machine)

This section shows how to grant your VM access to a secret stored in a Key Vault. Using managed identities for Azure resources, your code can get access tokens to authenticate to resources that support Microsoft Entra authentication.

However, not all Azure services support Microsoft Entra authentication. To use managed identities for Azure resources with those services, store the service credentials in Azure Key Vault, and use the VM's managed identity to access Key Vault to retrieve the credentials.

First, you need to create a Key Vault and grant your VM's system-assigned managed identity access to the Key Vault.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. At the top of the left navigation bar, select **Create a resource**.
3. In the **Search the Marketplace** box type in **Key Vault** and hit **Enter**.
4. Select **Key Vault** from the results.
5. Select **Create**.
6. Provide a **Name** for the new key vault.

    ![Screenshot showing the Azure Key vault creation screen.](media/tutorial-linux-vm-access-nonaad/create-key-vault.png)
7. Fill out all required information making sure that you choose the subscription and resource group where you created the virtual machine that you are using for this tutorial.
8. Select **Review+ create**, then select **Create**.

## Create a secret

Next, you need to add a secret to the Key Vault, so you can retrieve it later using code running in your VM. In this section, you'll use PowerShell. But the same concepts apply to any code executing in this virtual machine.

1. Navigate to your newly created Key Vault.
2. Select **Secrets**, then select **Add**.
3. Select **Generate/Import**.
4. In the **Create a secret** section, go to **Upload options** and make sure that **Manual** is selected.
5. Enter a name and value for the secret. The value can be anything you want.
6. Leave the activation date and expiration date clear, and make sure that **Enabled** is set to **Yes**.
7. Select **Create** to create the secret.

    ![Screenshot showing secret creation.](media/tutorial-linux-vm-access-nonaad/create-secret.png)

## Grant access

The managed identity used by the virtual machine needs access to read the secret stored in Key Vault.

1. Navigate to your newly created Key Vault.
2. Select **Access Policy** from the left navigation.
3. Select **Add Access Policy**.

    ![Screenshot of the key vault create access policy screen.](media/tutorial-linux-vm-access-nonaad/key-vault-access-policy.png)
4. In the **Add access policy** section under **Configure from template (optional)**, choose **Secret Management** from the drop-down menu.
5. Choose **Select Principal**, then in the search field enter the name of the VM you created earlier. Select the VM in the result list, then **Select**.
6. Select **Add**.
7. Select **Save**.

## Access data

To complete these steps, you need an SSH client. If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

Important

All Azure SDKs support the Azure.Identity library that makes it easy to acquire Microsoft Entra tokens to access target services. Learn more about [Azure SDKs](https://azure.microsoft.com/downloads/) and accessing the Azure.Identity library.

- [.NET](/en-us/dotnet/api/overview/azure/identity-readme)
- [Java](/en-us/java/api/overview/azure/identity-readme)
- [JavaScript](/en-us/javascript/api/overview/azure/identity-readme)
- [Python](/en-us/python/api/overview/azure/identity-readme)

1. In the portal, navigate to your Linux VM and in the **Overview**, select **Connect**.
2. **Connect** to the VM with the SSH client of your choice.
3. In the terminal window, use cURL to make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Key Vault. The CURL request for the access token is below.

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -H Metadata:true
  ```
The response includes the access token you need to access Resource Manager. 
  
Response:
  
```bash
{"access_token":"eyJ0eXAi...",
"refresh_token":"",
"expires_in":"3599",
"expires_on":"1504130527",
"not_before":"1504126627",
"resource":"https://vault.azure.net",
"token_type":"Bearer"} 
```

You can use this access token to authenticate to Azure Key Vault. The next CURL request shows how to read a secret from Key Vault using CURL and the Key Vault REST API. You need the URL of your Key Vault, which is in the **Essentials** section of the **Overview** page of the Key Vault. You also need the access token you obtained on the previous call. 

```bash
curl 'https://<YOUR-KEY-VAULT-URL>/secrets/<secret-name>?api-version=2016-10-01' -H "Authorization: Bearer <ACCESS TOKEN>" 
```

The response looks like this: 

```bash
{"value":"p@ssw0rd!","id":"https://mytestkeyvault.vault.azure.net/secrets/MyTestSecret/7c2204c6093c4d859bc5b9eff8f29050","attributes":{"enabled":true,"created":1505088747,"updated":1505088747,"recoveryLevel":"Purgeable"}} 
```

Once you retrieved the secret from the Key Vault, you can use it to authenticate to a service that requires a name and password.

## Clean up resources

When you're ready to clean up the resources, sign in to the [Azure portal](https://portal.azure.com), select **Resource groups**, then locate and select the resource group that was created in the process of this tutorial, such as `mi-test`. You can use the **Delete resource group** command or via [PowerShell or CLI.](/en-us/azure/azure-resource-manager/management/delete-resource-group)

::: zone-end

::: zone pivot="identity-linux-mi-vm-access-arm"

## Use a Linux VM system-assigned managed identity to access a resource group in resource manager

This tutorial explains how to create a system-assigned identity, assign it to a Linux Virtual Machine (VM), and then use that identity to access the [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) API. Managed Service Identities are automatically managed by Azure. They enable authentication to services that support Microsoft Entra authentication, without needing to embed credentials into your code.

You learn how to:

- Grant your VM access to Azure resource manager.
- Get an access token by using the VM's system-assigned managed identity to access resource manager.

1. Sign in to the [Azure portal](https://portal.azure.com) with your administrator account.
2. Navigate to the **Resource Groups** tab.
3. Select the **Resource Group** that you want to grant the VM's managed identity access.
4. In the left panel, select **Access control (IAM)**.
5. Select **Add**, then select **Add role assignment**.
6. In the **Role** tab, select **Reader**. This role allows view all resources, but doesn't allow you to make any changes.
7. In the **Members** tab, in the **Assign access to** option, select **Managed identity**, then select **+ Select members**.
8. Ensure the proper subscription is listed in the **Subscription** dropdown. For **Resource Group**, select **All resource groups**.
9. In the **Manage identity** dropdown, select **Virtual Machine**.
10. In the **Select** option, choose your VM in the dropdown, then select **Save**.

    ![Screenshot that shows adding the reader role to the managed identity.](media/msi-tutorial-linux-vm-access-arm/msi-permission-linux.png)

## Get an access token

Use the VM's system-assigned managed identity and call the resource manager to get an access token.

To complete these steps, you need an SSH client. If you're using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

1. In the Azure portal, navigate to your Linux VM.
2. In the **Overview**, select **Connect**.
3. **Connect** to the VM with the SSH client of your choice.
4. In the terminal window, using `curl`, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure resource manager. The `curl` request for the access token is below.

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/' -H Metadata:true
```

Note

The value of the `resource` parameter must be an exact match for what is expected by Microsoft Entra ID. In the case of the resource manager resource ID, you must include the trailing slash on the URI.

The response includes the access token you need to access Azure resource manager.

Response:

```json
{
  "access_token":"eyJ0eXAiOi...",
  "refresh_token":"",
  "expires_in":"3599",
  "expires_on":"1504130527",
  "not_before":"1504126627",
  "resource":"https://management.azure.com",
  "token_type":"Bearer"
}
```

Use this access token to access Azure resource manager. For example, to read the details of the resource group to which you previously granted this VM access. Replace the values of `<SUBSCRIPTION-ID>`, `<RESOURCE-GROUP>`, and `<ACCESS-TOKEN>` with the ones you created earlier.

Note

The URL is case-sensitive, so ensure if you are using the exact case as you used earlier when you named the resource group, and the uppercase “G” in `resourceGroup`.

```bash
curl https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>?api-version=2016-09-01 -H "Authorization: Bearer <ACCESS-TOKEN>" 
```

The response back with the specific resource group information: 

```json
{
"id":"/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/DevTest",
"name":"DevTest",
"location":"westus",
"properties":
{
  "provisioningState":"Succeeded"
  }
} 
```

::: zone-end

::: zone pivot="identity-linux-mi-vm-user-arm"

## Use a Linux VM user-assigned managed identity to access a resource group in Resource Manager

This tutorial explains how to create a user-assigned identity, assign it to a Linux Virtual Machine (VM), and then use that identity to access the [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) API. Managed Service Identities are automatically managed by Azure. They enable authentication to services that support Microsoft Entra authentication, without needing to embed credentials into your code.

You'll learn how to:

- Grant your VM access to Azure Resource Manager.
- Get an access token by using the VM's system-assigned managed identity to access Resource Manager.

Create a user-assigned managed identity using [az identity create](/en-us/cli/azure/identity#az-identity-create). The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name. Be sure to replace the `<RESOURCE GROUP>` and `<UAMI NAME>` parameter values with your own values:

Important

When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

```azurecli
az identity create -g <RESOURCE GROUP> -n <UAMI NAME>
```

The response contains details for the user-assigned managed identity created, similar to the following example. Note the `id` value for your user-assigned managed identity, as it will be used in the next step:

```json
{
"clientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
"clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<UAMI NAME>/credentials?tid=5678&oid=9012&aid=aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
"id": "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<UAMI NAME>",
"location": "westcentralus",
"name": "<UAMI NAME>",
"principalId": "9012",
"resourceGroup": "<RESOURCE GROUP>",
"tags": {},
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
"type": "Microsoft.ManagedIdentity/userAssignedIdentities"
}
```

## Assign an identity to your Linux VM

A user-assigned managed identity can be used by clients on multiple Azure resources. Use the following commands to assign the user-assigned managed identity to a single VM. Use the `Id` property returned in the previous step for the `-IdentityID` parameter.

Assign the user-assigned managed identity to your Linux VM using [az vm identity assign](/en-us/cli/azure/vm). Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values. Use the `id` property returned in the previous step for the `--identities` parameter value.

```azurecli
az vm identity assign -g <RESOURCE GROUP> -n <VM NAME> --identities "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<UAMI NAME>"
```

## Grant access to a resource group in Azure Resource Manager

Managed identities are identities that your code can use to request access tokens to authenticate to resource APIs that support Microsoft Entra authentication. In this tutorial, your code will access the Azure Resource Manager API.

Before your code can access the API, you need to grant the identity access to a resource in Azure Resource Manager. In this case, the resource group in which the VM is contained. Update the value for `<SUBSCRIPTION ID>` and `<RESOURCE GROUP>` as appropriate for your environment. Additionally, replace `<UAMI PRINCIPALID>` with the `principalId` property returned by the `az identity create` command in [Create a user-assigned managed identity](/en-us/cli/azure/identity#az-identity-create):

```azurecli
az role assignment create --assignee <UAMI PRINCIPALID> --role 'Reader' --scope "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP> "
```

The response contains details for the role assignment created, similar to the following example:

```json
{
  "id": "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Authorization/roleAssignments/00000000-0000-0000-0000-000000000000",
  "name": "00000000-0000-0000-0000-000000000000",
  "properties": {
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "/subscriptions/<SUBSCRIPTION ID>/providers/Microsoft.Authorization/roleDefinitions/00000000-0000-0000-0000-000000000000",
    "scope": "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>"
  },
  "resourceGroup": "<RESOURCE GROUP>",
  "type": "Microsoft.Authorization/roleAssignments"
}

```

## Get an access token using the VM's identity and use it to call Resource Manager

For the remainder of the tutorial, you work from the VM you created earlier.

To complete these steps, you need an SSH client. If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about).

1. Sign in to the [Azure portal](https://portal.azure.com).
2. In the portal, navigate to **Virtual Machines** and go to the Linux virtual machine and in the **Overview**, click **Connect**. Copy the string to connect to your VM.
3. Connect to the VM with the SSH client of your choice. If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).
4. In the terminal window, use CURL to make a request to the Azure Instance Metadata Service (IMDS) identity endpoint to get an access token for Azure Resource Manager.

    The CURL request to acquire an access token is shown in the following example. Be sure to replace `<CLIENT ID>` with the `clientId` property returned by the `az identity create` command in [Create a user-assigned managed identity](/en-us/cli/azure/identity#az-identity-create):

    ```bash
    curl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com/&client_id=<UAMI CLIENT ID>"
    ```

    Note

    The value of the `resource` parameter must be an exact match for what is expected by Microsoft Entra ID. When using the Resource Manager resource ID, you must include the trailing slash on the URI.

    The response includes the access token you need to access Azure Resource Manager.

    Response example:

    ```bash
    {
    "access_token":"eyJ0eXAiOi...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://management.azure.com",
    "token_type":"Bearer"
    } 
    ```
5. Use the access token to access Azure Resource Manager, and read the properties of the resource group to which you previously granted your user-assigned managed identity access. Be sure to replace `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>` with the values you specified earlier, and `<ACCESS TOKEN>` with the token returned in the previous step.

    Note

    The URL is case-sensitive, so be sure to use the exact same case you used earlier when you named the resource group, and the uppercase "G" in `resourceGroups`.

    ```bash
    curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>?api-version=2016-09-01 -H "Authorization: Bearer <ACCESS TOKEN>" 
    ```

    The response contains the specific resource group information, similar to the following example:

    ```bash
    {
    "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/DevTest",
    "name":"DevTest",
    "location":"westus",
    "properties":{"provisioningState":"Succeeded"}
    } 
    ```

::: zone-end

## Learn more

- [What are managed identities for Azure resources?](overview)
- [Quickstart: Use a user-assigned managed identity on a VM to access Azure Resource Manager](tutorial-linux-managed-identities-vm-access)
- [Create, list, or delete a user-assigned managed identity using Azure PowerShell](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-powershell)