---
layout: Conceptual
title: Use managed identities from a virtual machine to access Azure Cosmos DB - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/tutorial-vm-managed-identities-cosmos
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn how to use managed identities with Windows VMs using the Azure portal, CLI, PowerShell, Azure Resource Manager template
ms.topic: tutorial
ms.date: 2023-03-31T00:00:00.0000000Z
ms.tool: azure-cli, azure-powershell
ms.devlang: azurecli
ms.custom: ep-miar, devx-track-azurepowershell, devx-track-azurecli, devx-track-arm-template, devx-track-linux, sfi-image-nochange
locale: en-us
document_id: 66bfdfe6-9851-eef4-9d94-8b1eedb20928
document_version_independent_id: 13f12982-54bd-78d9-b542-bf9390f79189
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/tutorial-vm-managed-identities-cosmos.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli,azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/tutorial-vm-managed-identities-cosmos
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/tutorial-vm-managed-identities-cosmos.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd668c2f-f5b3-4573-8ad1-019570e3e2db
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://authoring-docs-microsoft.poolparty.biz/devrel/cc82e69d-afbe-4554-9f4c-6705fc860c42
platformId: a8274c5f-f7c1-6630-a615-65ba1d1f7571
---

# Use managed identities from a virtual machine to access Azure Cosmos DB - Managed identities for Azure resources | Microsoft Learn

In this article, we set up a virtual machine to use managed identities to connect to Azure Cosmos DB. [Azure Cosmos DB](/en-us/azure/cosmos-db/introduction) is a fully managed NoSQL database for modern app development. [Managed identities for Azure resources](overview) allow your applications to authenticate when accessing services that support Microsoft Entra authentication using an identity managed by Azure.

## Prerequisites

- A basic understanding of Managed identities. If you would like to learn more about managed identities for Azure resources before you continue, review the managed identities [overview](overview).
- You must have an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You may need either [PowerShell](/en-us/powershell/azure/new-azureps-module-az) or the [CLI](/en-us/cli/azure/install-azure-cli).
- [Visual Studio Community Edition](https://visualstudio.microsoft.com/vs/community/) or some other development environment of your choosing.

## Create a resource group

Create a resource group called **mi-test**. We use this resource group for all resources used in this tutorial.

- [Create a resource group using the Azure portal](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal#create-resource-groups)
- [Create a resource group using the CLI](/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli#create-resource-groups)
- [Create a resource group using PowerShell](/en-us/azure/azure-resource-manager/management/manage-resource-groups-powershell#create-resource-groups)

## Create an Azure VM with a managed identity

For this tutorial, you need an Azure virtual machine(VM). Create a virtual machine with a system-assigned managed identity enabled called **mi-vm-01**. You may also [create a user-assigned managed identity](how-manage-user-assigned-managed-identities) called **mi-ua-01** in the resource group we created earlier (**mi-test**). If you use a user-assigned managed identity, you can assign it to a VM during creation.

### Create a VM with a system-assigned managed identity

To create an Azure VM with the system-assigned managed identity enabled, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra role assignments are required.

# [Portal](#tab/azure-portal)
- From the **Azure portal** search for **virtual machines**.
- Choose **Create**
- In the Basics tab, provide the required information.
- Choose **Next: Disks &gt;**
- Continue filling out information as needed and in the **Management** tab find the **Identity** section and check the box next to **System assigned managed identity**

![Image showing how to enable system assigned managed identities while creating a VM.](media/how-to-manage-identities-vm-cosmos/create-vm-system-assigned-managed-identities.png)

For more information, review the Azure virtual machines documentation:

- [Linux](/en-us/azure/virtual-machines/linux/quick-create-portal)
- [Windows](/en-us/azure/virtual-machines/windows/quick-create-portal)

# [PowerShell](#tab/azure-powershell)
[New-AZVM](/en-us/powershell/module/az.compute/new-azvm) creates resources you reference if they don't exist. To create a VM with a system assigned managed identity enabled pass the parameter **-SystemAssignedIdentity** as shown below.

```powershell

New-AzVm `
    -ResourceGroupName "My VM" `
    -Name "My resource group" `
    -Location "East US" `
    -VirtualNetworkName "myVnet" `
    -SubnetName "mySubnet" `
    -SecurityGroupName "myNetworkSecurityGroup" `
    -SystemAssignedIdentity
    -OpenPorts 80,3389
```

- [Quickstart: Create a Windows virtual machine in Azure with PowerShell](/en-us/azure/virtual-machines/windows/quick-create-powershell)
- [Quickstart: Create a Linux virtual machine in Azure with PowerShell](/en-us/azure/virtual-machines/linux/quick-create-powershell)

# [Azure CLI](#tab/azure-cli)
Create a VM using [Azure CLI vm create command](/en-us/cli/azure/vm/#az-vm-create). The following example creates a VM named *myVM* with a system-assigned managed identity, as requested by the `--assign-identity` parameter. The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in. Update these values as appropriate for your environment:

```azurecli
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --generate-ssh-keys --assign-identity --admin-username azureuser --admin-password myPassword12
```

- [Create a Linux virtual machine with a system assigned managed identity](/en-us/azure/virtual-machines/linux/quick-create-cli)
- [Create a Windows virtual machine with a system assigned managed identity](/en-us/azure/virtual-machines/windows/quick-create-cli)

# [Resource Manager Template](#tab/azure-resource-manager)
To enable system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section and add the `"identity"` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property. Use the following syntax:

```json
"identity": {
    "type": "SystemAssigned"
},
```

When you're done, the following sections should be added to the `resource` section of your template. Your template should resemble the example shown below:

```json
 "resources": [
     {
         //other resource provider properties...
         "apiVersion": "2018-06-01",
         "type": "Microsoft.Compute/virtualMachines",
         "name": "[variables('myVM')]",
         "location": "[myResourceGroup().location]",
         "identity": {
             "type": "SystemAssigned",
             }                        
     }
 ]
```

---

### Create a VM with a user-assigned managed identity

The steps below show you how to create a virtual machine with a user-assigned managed identity configured.

# [Portal](#tab/azure-portal)
Today, the Azure portal doesn't support assigning a user-assigned managed identity during the creation of a VM. You should create a virtual machine and then assign a user assigned managed identity to it.

[Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm#user-assigned-managed-identity)

# [PowerShell](#tab/azure-powershell)
Create a Windows virtual machine with a user assigned managed identity specified.

```powershell
New-AzVm `
    -ResourceGroupName "<Your resource group>" `
    -Name "<Your VM name>" `
    -Location "East US" `
    -VirtualNetworkName "<myVnet>" `
    -SubnetName "mySubnet" `
    -SecurityGroupName "myNetworkSecurityGroup" `
    -UserAssignedIdentity "/subscriptions/<Your subscription>/resourceGroups/<Your resource group>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<Your user assigned managed identity>" `
    -OpenPorts 80,3389

```

Create a Linux virtual machine with a user assigned managed identity specified.

```powershell
New-AzVm `
    -Name "<Linux VM name>" `
    -image CentOS85Gen2
    -ResourceGroupName "<Your resource group>" `
    -Location "East US" `
    -VirtualNetworkName "myVnet" `
    -SubnetName "mySubnet" `
    -Linux `
    -SecurityGroupName "myNetworkSecurityGroup" `
    -UserAssignedIdentity "/subscriptions/<Your subscription>/resourceGroups/<Your resource group>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<Your user assigned managed identity>" `
    -OpenPorts 22

```

The user assigned managed identity should be specified using its [resourceID](how-manage-user-assigned-managed-identities).

# [Azure CLI](#tab/azure-cli)
```azurecli
az vm create --resource-group <MyResourceGroup> --name <myVM> --image <SKU Linux Image> --admin-username <USER NAME> --admin-password <PASSWORD> --assign-identity <USER ASSIGNED IDENTITY NAME>
```

[Configure managed identities for Azure resources on a VM using the Azure CLI](qs-configure-cli-windows-vm#user-assigned-managed-identity)

# [Resource Manager Template](#tab/azure-resource-manager)
Depending on your API version, you have to take [different steps](qs-configure-template-windows-vm#user-assigned-managed-identity). If your apiVersion is 2018-06-01, your user-assigned managed identities are stored in the userAssignedIdentities dictionary format. The `<identityName>` value is the name of a variable that you define in the variables section of your template. In the variable, you point to the user assigned managed identity that you want to assign.

```json
    "variables": {
     "identityName": "my-user-assigned"    
        
    },
```

Under the resources element, add the following entry to assign a user-assigned managed identity to your VM. Be sure to replace `<identityName>` with the name of the user-assigned managed identity you created.

```json

"resources": [
     {
         //other resource provider properties...
         "apiVersion": "2018-06-01",
         "type": "Microsoft.Compute/virtualMachines",
         "name": "[variables('vmName')]",
         "location": "[resourceGroup().location]",
         "identity": {
             "type": "userAssigned",
             "userAssignedIdentities": {
                "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<identityName>'))]": {}
             }
         }
     }
 ]
```

---

## Create an Azure Cosmos DB account

Now that we have a VM with either a user-assigned managed identity or a system-assigned managed identity we need an Azure Cosmos DB account available where you have administrative rights. If you need to create an Azure Cosmos DB account for this tutorial, the [Azure Cosmos DB quickstart](/en-us/azure/cosmos-db/sql/create-cosmosdb-resources-portal) provides detailed steps on how to do that.

Note

Managed identities may be used to access any Azure resource that supports Microsoft Entra authentication. This tutorial assumes that your Azure Cosmos DB account will be configured as shown below.

| Setting | Value | Description |
| --- | --- | --- |
| Subscription | Subscription name | Select the Azure subscription that you want to use for this Azure Cosmos DB account. |
| Resource Group | Resource group name | Select **mi-test**, or select **Create new**, then enter a unique name for the new resource group. |
| Account Name | A unique name | Enter a name to identify your Azure Cosmos DB account. Because *documents.azure.com* is appended to the name that you provide to create your URI, use a unique name.The name can only contain lowercase letters, numbers, and the hyphen (-) character. It must be between 3-44 characters in length. |
| API | The type of account to create | Select **Azure Cosmos DB for NoSQL** to create a document database and query by using SQL syntax. [Learn more about the SQL API](/en-us/azure/cosmos-db/introduction). |
| Location | The region closest to your users | Select a geographic location to host your Azure Cosmos DB account. Use the location that is closest to your users to give them the fastest access to the data. |

Note

If you are testing you may want to apply Azure Cosmos DB free tier discount. With the Azure Cosmos DB free tier, you will get the first 1000 RU/s and 25 GB of storage for free in an account. Learn more about [free tier](https://azure.microsoft.com/pricing/details/cosmos-db/). Keep in mind that for the purpose of this tutorial this choice makes no difference.

## Grant access

At this point, we should have both a virtual machine configured with a managed identity and an Azure Cosmos DB account. Before we continue, we need to grant the managed identity a couple of different roles.

- First grant access to the Azure Cosmos DB management plane using [Azure RBAC](/en-us/azure/cosmos-db/role-based-access-control). The managed identity needs to have the DocumentDB Account Contributor role assigned to create Databases and containers.
- You also need to grant the managed identity a contributor role using [Azure Cosmos DB RBAC](/en-us/azure/cosmos-db/how-to-setup-rbac). You can see specific steps below.

Note

We will use the **Cosmos DB Built-in Data contributor** role. To grant access, you need to associate the role definition with the identity. In our case, the managed identity associated with our virtual machine.

# [Portal](#tab/azure-portal)
**At this time there is no role assignment option available in the Azure portal**

# [PowerShell](#tab/azure-powershell)
```powershell
$resourceGroupName = "<myResourceGroup>"
$accountName = "<myCosmosAccount>" 
$contributorRoleDefinitionId = "00000000-0000-0000-0000-000000000002" # This is the ID of the Cosmos DB Built-in Data contributor role definition
$principalId = "1111111-1111-11111-1111-11111111" # This is the object ID of the managed identity.
New-AzCosmosDBSqlRoleAssignment -AccountName $accountName `
    -ResourceGroupName $resourceGroupName `
    -RoleDefinitionId $contributorRoleDefinitionId `
    -Scope "/" `
    -PrincipalId $principalId
```

When the role assignment step completes, you should see results similar to the ones shown below.

![screenshot shows the results of the role assignment.](media/how-to-manage-identities-vm-cosmos/results-role-assignment.png)

# [Azure CLI](#tab/azure-cli)
```azurecli

resourceGroupName='<myResourceGroup>'
accountName='<myCosmosAccount>'
readOnlyRoleDefinitionId = '00000000-0000-0000-0000-000000000002' # This is the ID of the Cosmos DB Built-in Data contributor role definition
principalId = "1111111-1111-11111-1111-11111111" # This is the object ID of the managed identity.
az cosmosdb sql role assignment create --account-name $accountName --resource-group $resourceGroupName --scope "/" --principal-id $principalId --role-definition-id $readOnlyRoleDefinitionId

```

# [Resource Manager Template](#tab/azure-resource-manager)
```JSON
{
  "id": "/subscriptions/mySubscriptionId/resourceGroups/myResourceGroupName/providers/Microsoft.DocumentDB/databaseAccounts/myAccountName/sqlRoleAssignments/00000000-0000-0000-0000-000000000002",
  "name": "myRoleAssignmentId",
  "type": "Microsoft.DocumentDB/databaseAccounts/sqlRoleAssignments",
  "properties": {
    "roleDefinitionId": "/subscriptions/mySubscriptionId/resourceGroups/myResourceGroupName/providers/Microsoft.DocumentDB/databaseAccounts/myAccountName/sqlRoleDefinitions/00000000-0000-0000-0000-000000000002",
    "scope": "/subscriptions/mySubscriptionId/resourceGroups/myResourceGroupName/providers/Microsoft.DocumentDB/databaseAccounts/myAccountName/dbs/purchases/colls/redmond-purchases",
    "principalId": "myPrincipalId"
  }
}

```

---

## Access data

Getting access to Azure Cosmos DB using managed identities may be achieved using the Azure.identity library to enable authentication in your application. You can call [ManagedIdentityCredential](/en-us/dotnet/api/azure.identity.managedidentitycredential) directly or use [DefaultAzureCredential](/en-us/dotnet/api/azure.identity.defaultazurecredential).

The ManagedIdentityCredential class attempts to authentication using a managed identity assigned to the deployment environment. The [DefaultAzureCredential](/en-us/dotnet/api/overview/azure/identity-readme) class goes through different authentication options in order. The second authentication option that DefaultAzureCredential attempts is Managed identities.

In the example shown below, you create a database, a container, an item in the container, and read back the newly created item using the virtual machine's system assigned managed identity. If you want to use a user-assigned managed identity, you need to specify the user-assigned managed identity by specifying the managed identity's client ID.

```csharp
string userAssignedClientId = "<your managed identity client Id>";
var tokenCredential = new DefaultAzureCredential(new DefaultAzureCredentialOptions { ManagedIdentityClientId = userAssignedClientId });
```

To use the sample below, you need to have the following NuGet packages:

- Azure.Identity
- Microsoft.Azure.Cosmos
- Microsoft.Azure.Management.CosmosDB

In addition to the NuGet packages above, you also need to enable **Include prerelease** and then add **Azure.ResourceManager.CosmosDB**.

```csharp
using Azure.Identity;
using Azure.ResourceManager.CosmosDB;
using Azure.ResourceManager.CosmosDB.Models;
using Microsoft.Azure.Cosmos;
using System;
using System.Threading.Tasks;

namespace MITest
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // Replace the placeholders with your own values
            var subscriptionId = "Your subscription ID";
            var resourceGroupName = "You resource group";
            var accountName = "Cosmos DB Account name";
            var databaseName = "mi-test";
            var containerName = "container01";

            // Authenticate to Azure using Managed Identity (system-assigned or user-assigned)
            var tokenCredential = new DefaultAzureCredential();

            // Create the Cosmos DB management client using the subscription ID and token credential
            var managementClient = new CosmosDBManagementClient(tokenCredential)
            {
                SubscriptionId = subscriptionId
            };

            // Create the Cosmos DB data client using the account URL and token credential
            var dataClient = new CosmosClient($"https://{accountName}.documents.azure.com:443/", tokenCredential);

            // Create a new database using the management client
            var createDatabaseOperation = await managementClient.SqlResources.StartCreateUpdateSqlDatabaseAsync(
                resourceGroupName,
                accountName,
                databaseName,
                new SqlDatabaseCreateUpdateParameters(new SqlDatabaseResource(databaseName), new CreateUpdateOptions()));
            await createDatabaseOperation.WaitForCompletionAsync();

            // Create a new container using the management client
            var createContainerOperation = await managementClient.SqlResources.StartCreateUpdateSqlContainerAsync(
                resourceGroupName,
                accountName,
                databaseName,
                containerName,
                new SqlContainerCreateUpdateParameters(new SqlContainerResource(containerName), new CreateUpdateOptions()));
            await createContainerOperation.WaitForCompletionAsync();

            // Create a new item in the container using the data client
            var partitionKey = "pkey";
            var id = Guid.NewGuid().ToString();
            await dataClient.GetContainer(databaseName, containerName)
                .CreateItemAsync(new { id = id, _partitionKey = partitionKey }, new PartitionKey(partitionKey));

            // Read back the item from the container using the data client
            var pointReadResult = await dataClient.GetContainer(databaseName, containerName)
                .ReadItemAsync<dynamic>(id, new PartitionKey(partitionKey));

            // Run a query to get all items from the container using the data client
            await dataClient.GetContainer(databaseName, containerName)
                .GetItemQueryIterator<dynamic>("SELECT * FROM c")
                .ReadNextAsync();
        }
    }
}

```

Language-specific examples using ManagedIdentityCredential:

### .NET

Initialize your Azure Cosmos DB client:

```csharp
CosmosClient client = new CosmosClient("<account-endpoint>", new ManagedIdentityCredential());
```

Then [read and write data](/en-us/azure/cosmos-db/sql/sql-api-dotnet-v3sdk-samples).

### Java

Initialize your Azure Cosmos DB client:

```java
CosmosAsyncClient Client = new CosmosClientBuilder().endpoint("<account-endpoint>") .credential(new ManagedIdentityCredential()) .build();
```

Then read and write data as described in [these samples](/en-us/azure/cosmos-db/sql/sql-api-java-sdk-samples)

### JavaScript

Initialize your Azure Cosmos DB client:

```javascript
const client = new CosmosClient({ "<account-endpoint>", aadCredentials: new ManagedIdentityCredential() });
```

Then read and write data as described in [these samples](/en-us/azure/cosmos-db/sql/sql-api-nodejs-samples)

## Clean up steps

# [Portal](#tab/azure-portal)
1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select the resource you want to delete.
3. Select **Delete**.
4. When prompted, confirm the deletion.

# [PowerShell](#tab/azure-powershell)
```azurepowershell
Remove-AzResource `
  -ResourceGroupName ExampleResourceGroup `
  -ResourceName ExampleVM `
  -ResourceType Microsoft.Compute/virtualMachines
```

# [Azure CLI](#tab/azure-cli)
```azurecli
az resource delete \
  --resource-group ExampleResourceGroup \
  --name ExampleVM \
  --resource-type "Microsoft.Compute/virtualMachines"
```

# [Resource Manager Template](#tab/azure-resource-manager)
Section purposely left empty

---