---
layout: Conceptual
title: Tutorial - Web app accesses Microsoft Graph as the app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/multi-service-web-app-access-microsoft-graph-as-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this tutorial, you learn how to access data in Microsoft Graph from a web app running in Azure App Service using managed identities.
manager: pmwongera
ms.date: 2024-02-17T00:00:00.0000000Z
ms.reviewer: stsoneff
ms.subservice: 
ms.topic: tutorial
ms.custom: sfi-image-nochange
locale: en-us
document_id: 15507fb4-6ebe-f0f0-96b6-f6c578747d3f
document_version_independent_id: b2ae30fa-60ae-a30a-b17b-2de525cf0370
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/multi-service-web-app-access-microsoft-graph-as-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/multi-service-web-app-access-microsoft-graph-as-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/multi-service-web-app-access-microsoft-graph-as-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 599ef478-b5b9-e7ed-c864-a1dc1628e879
---

# Tutorial - Web app accesses Microsoft Graph as the app - Microsoft identity platform | Microsoft Learn

Learn how to access Microsoft Graph from a web app running on Azure App Service.

![Diagram that shows accessing Microsoft Graph.](media/multi-service-web-app-access-microsoft-graph/web-app-access-graph.svg)

You want to call Microsoft Graph for the web app. A safe way to give your web app access to data is to use a [system-assigned managed identity](../identity/managed-identities-azure-resources/overview). A managed identity from Microsoft Entra ID allows App Service to access resources through role-based access control (RBAC), without requiring app credentials. After assigning a managed identity to your web app, Azure takes care of the creation and distribution of a certificate. You don't have to worry about managing secrets or app credentials.

In this tutorial, you:

- Create a system-assigned managed identity on a web app.
- Add Microsoft Graph API permissions to a managed identity.
- Call Microsoft Graph from a web app by using managed identities.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

- A web application running on Azure App Service that has the [App Service authentication/authorization module enabled](multi-service-web-app-authentication-app-service).

## Enable managed identity on app

If you create and publish your web app through Visual Studio, the managed identity was enabled on your app for you. In your app service, select **Identity** in the left pane and then select **System assigned**. Verify that **Status** is set to **On**. If not, select **Save** and then select **Yes** to enable the system-assigned managed identity. When the managed identity is enabled, the status is set to **On** and the object ID is available.

Take note of the **Object ID** value, which you'll need in the next step.

![Screenshot that shows the system-assigned identity.](media/multi-service-web-app-access-microsoft-graph/create-system-assigned-identity.png)

## Grant access to Microsoft Graph

When accessing the Microsoft Graph, the managed identity needs to have proper permissions for the operation it wants to perform. Currently, there's no option to assign such permissions through the Microsoft Entra admin center. The following script will add the requested Microsoft Graph API permissions to the managed identity service principal object.

# [PowerShell](#tab/azure-powershell)
```powershell
# Install the module.
# Install-Module Microsoft.Graph -Scope CurrentUser

# The tenant ID
$TenantId = "aaaabbbb-0000-cccc-1111-dddd2222eeee"

# The name of your web app, which has a managed identity.
$webAppName = "SecureWebApp-20201106120003" 
$resourceGroupName = "SecureWebApp-20201106120003ResourceGroup"

# The name of the app role that the managed identity should be assigned to.
$appRoleName = "User.Read.All"

# Get the web app's managed identity's object ID.
Connect-AzAccount -Tenant $TenantId
$managedIdentityObjectId = (Get-AzWebApp -ResourceGroupName $resourceGroupName -Name $webAppName).identity.principalid

Connect-MgGraph -TenantId $TenantId -Scopes 'Application.Read.All','AppRoleAssignment.ReadWrite.All'

# Get Microsoft Graph app's service principal and app role.
$serverApplicationName = "Microsoft Graph"
$serverServicePrincipal = (Get-MgServicePrincipal -Filter "DisplayName eq '$serverApplicationName'")
$serverServicePrincipalObjectId = $serverServicePrincipal.Id

$appRoleId = ($serverServicePrincipal.AppRoles | Where-Object {$_.Value -eq $appRoleName }).Id

# Assign the managed identity access to the app role.
New-MgServicePrincipalAppRoleAssignment `
    -ServicePrincipalId $managedIdentityObjectId `
    -PrincipalId $managedIdentityObjectId `
    -ResourceId $serverServicePrincipalObjectId `
    -AppRoleId $appRoleId
```

# [Azure CLI](#tab/azure-cli)
```azurecli
az login

webAppName="SecureWebApp-20201106120003"

spId=$(az resource list -n $webAppName --query [*].identity.principalId --out tsv)

graphResourceId=$(az ad sp list --display-name "Microsoft Graph" --query [0].id --out tsv)

appRoleId=$(az ad sp list --display-name "Microsoft Graph" --query "[0].appRoles[?value=='User.Read.All' && contains(allowedMemberTypes, 'Application')].id" --output tsv)

uri=https://graph.microsoft.com/v1.0/servicePrincipals/$spId/appRoleAssignments

body="{'principalId':'$spId','resourceId':'$graphResourceId','appRoleId':'$appRoleId'}"

az rest --method post --uri $uri --body $body --headers "Content-Type=application/json"
```

---

After executing the script, you can verify in the [Microsoft Entra admin center](https://entra.microsoft.com) that the requested API permissions are assigned to the managed identity.

Go to **Applications**, and then select **Enterprise applications**. This pane displays all the service principals in your tenant. **Add a filter** for "Application type == Managed Identities" and select the service principal for the managed identity.

If you're following this tutorial, there are two service principals with the same display name (SecureWebApp2020094113531, for example). The service principal that has a **Homepage URL** represents the web app in your tenant. The service principal that appears in **Managed Identities** should *not* have a **Homepage URL** listed and the **Object ID** should match the object ID value of the managed identity in the previous step.

Select the service principal for the managed identity.

![Screenshot that shows the All applications option.](media/multi-service-web-app-access-microsoft-graph/enterprise-apps-all-applications.png)

In **Overview**, select **Permissions**, and you'll see the added permissions for Microsoft Graph.

![Screenshot that shows the Permissions pane.](media/multi-service-web-app-access-microsoft-graph/enterprise-apps-permissions.png)

## Call Microsoft Graph

# [C#](#tab/programming-language-csharp)
The [ChainedTokenCredential](/en-us/dotnet/api/azure.identity.chainedtokencredential), [ManagedIdentityCredential](/en-us/dotnet/api/azure.identity.managedidentitycredential), and [EnvironmentCredential](/en-us/dotnet/api/azure.identity.environmentcredential) classes are used to get a token credential for your code to authorize requests to Microsoft Graph. Create an instance of the [ChainedTokenCredential](/en-us/dotnet/api/azure.identity.chainedtokencredential) class, which uses the managed identity in the App Service environment or the development environment variables to fetch tokens and attach them to the service client. The following code example gets the authenticated token credential and uses it to create a service client object, which gets the users in the group.

To see this code as part of a sample application, see the [sample on GitHub](https://github.com/Azure-Samples/ms-identity-easyauth-dotnet-storage-graphapi/tree/main/3-WebApp-graphapi-managed-identity).

### Install the Microsoft.Identity.Web.GraphServiceClient client library package

Install the [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) and [Microsoft.Identity.Web.GraphServiceClient NuGet](https://www.nuget.org/packages/Microsoft.Identity.Web.GraphServiceClient) packages in your project by using the .NET command-line interface (CLI) or the Package Manager Console in Visual Studio.

#### .NET CLI

Open a command line, and switch to the directory that contains your project file.

Run the install commands.

```dotnetcli
dotnet add package Microsoft.Identity.Web.GraphServiceClient
dotnet add package Microsoft.Graph
```

#### Package Manager Console

Open the project/solution in Visual Studio, and open the console by using the **Tools** &gt; **NuGet Package Manager** &gt; **Package Manager Console** command.

Run the install commands.

```powershell
Install-Package Microsoft.Identity.Web.GraphServiceClient
Install-Package Microsoft.Graph
```

### Example

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc.RazorPages;
using Microsoft.Extensions.Logging;
using Microsoft.Graph;
using Azure.Identity;

...

public IList<MSGraphUser> Users { get; set; }

public async Task OnGetAsync()
{
    // Create the Graph service client with a ChainedTokenCredential which gets an access
    // token using the available Managed Identity or environment variables if running
    // in development.
    var credential = new ChainedTokenCredential(
        new ManagedIdentityCredential(),
        new EnvironmentCredential());

    string[] scopes = new[] { "https://graph.microsoft.com/.default" };

    var graphServiceClient = new GraphServiceClient(
        credential, scopes);

    List<MSGraphUser> msGraphUsers = new List<MSGraphUser>();
    try
    {
        //var users = await graphServiceClient.Users.Request().GetAsync();
        var users = await graphServiceClient.Users.GetAsync();
        foreach (var u in users.Value)
        {
            MSGraphUser user = new MSGraphUser();
            user.userPrincipalName = u.UserPrincipalName;
            user.displayName = u.DisplayName;
            user.mail = u.Mail;
            user.jobTitle = u.JobTitle;

            msGraphUsers.Add(user);
        }
    }
    catch (Exception ex)
    {
        string msg = ex.Message;
    }

    Users = msGraphUsers;
}
```

# [Node.js](#tab/programming-language-nodejs)
The `DefaultAzureCredential` class from [@azure/identity](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/identity/identity/README.md) package is used to get a token credential for your code to authorize requests to Azure Storage. Create an instance of the `DefaultAzureCredential` class, which uses the managed identity to fetch tokens and attach them to the service client. The following code example gets the authenticated token credential and uses it to create a service client object, which gets the users in the group.

### Example

```nodejs
const graphHelper = require('../utils/graphHelper');
const { DefaultAzureCredential } = require("@azure/identity");

exports.getUsersPage = async(req, res, next) => {

    const defaultAzureCredential = new DefaultAzureCredential();
    
    try {
        const tokenResponse = await defaultAzureCredential.getToken("https://graph.microsoft.com/.default");

        const graphClient = graphHelper.getAuthenticatedClient(tokenResponse.token);

        const users = await graphClient
            .api('/users')
            .get();

        res.render('users', { user: req.session.user, users: users });   
    } catch (error) {
        next(error);
    }
}
```

To query Microsoft Graph, the sample uses the [Microsoft Graph JavaScript SDK](https://github.com/microsoftgraph/msgraph-sdk-javascript).

```nodejs
getAuthenticatedClient = (accessToken) => {
    // Initialize Graph client
    const client = graph.Client.init({
        // Use the provided access token to authenticate requests
        authProvider: (done) => {
            done(null, accessToken);
        }
    });

    return client;
}
```

---

## Clean up resources

If you're finished with this tutorial and no longer need the web app or associated resources, [clean up the resources you created](multi-service-web-app-clean-up-resources).