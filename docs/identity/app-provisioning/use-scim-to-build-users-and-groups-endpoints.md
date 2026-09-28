---
layout: Conceptual
title: Build a SCIM endpoint for user provisioning to apps from Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/use-scim-to-build-users-and-groups-endpoints
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn to develop a SCIM endpoint, integrate your SCIM API with Microsoft Entra ID, and automatically provision users and groups into your cloud applications.
ms.topic: tutorial
ms.date: 2026-04-27T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
locale: en-us
document_id: b633a23e-8b4e-5f76-687b-d9c32ca482dc
document_version_independent_id: ed365cbe-971b-6010-21fe-e9ce987eac6c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/use-scim-to-build-users-and-groups-endpoints.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/use-scim-to-build-users-and-groups-endpoints
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/use-scim-to-build-users-and-groups-endpoints.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
platformId: 8fc4c45c-e579-a2cc-9857-e49ddecbcae9
---

# Build a SCIM endpoint for user provisioning to apps from Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This tutorial describes how to deploy the SCIM [reference code](https://aka.ms/scimreferencecode) with [Azure App Service](/en-us/azure/app-service/). Then, test the code by using a tool like cURL or by integrating with the Microsoft Entra provisioning service. The tutorial is intended for developers who want to get started with SCIM, or anyone interested in testing a [SCIM endpoint](use-scim-to-provision-users-and-groups).

Important

The .NET reference code linked from this tutorial targets .NET Core 3.1, which is [no longer supported by Microsoft](https://dotnet.microsoft.com/platform/support/policy/dotnet-core). The upstream repository provides the sample "as is" with no guarantee of active maintenance ([SCIM Reference Code README](https://github.com/AzureAD/SCIMReferenceCode#readme)). To build or modify the sample against a currently supported .NET runtime, you might need to upgrade the target framework and dependencies. For known issues and feature requests, see the [open issues on the upstream repository](https://github.com/AzureAD/SCIMReferenceCode/issues).

In this tutorial, you learn how to:

- Deploy your SCIM endpoint in Azure.
- Test your SCIM endpoint.

## Deploy your SCIM endpoint in Azure

The steps here deploy the SCIM endpoint to a service by using [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) and [Visual Studio Code](https://code.visualstudio.com/) with [Azure App Service](/en-us/azure/app-service/). The SCIM reference code can run locally, hosted by an on-premises server, or deployed to another external service. For information about provisioning an SCIM endpoint, see [Tutorial: Develop and plan provisioning for a SCIM endpoint](use-scim-to-provision-users-and-groups).

### Get and deploy the sample app

Go to the [reference code](https://github.com/AzureAD/SCIMReferenceCode) from GitHub and select **Clone or download**. Select **Open in Desktop**, or copy the link, open Visual Studio, and select **Clone or check out code** to enter the copied link and make a local copy. Save the files into a folder where the total length of the path is 260 or fewer characters.

# [Visual Studio](#tab/visual-studio)
1. In Visual Studio, make sure to sign in to the account that has access to your hosting resources.
2. In Solution Explorer, open *Microsoft.SCIM.sln* and right-click the *Microsoft.SCIM.WebHostSample* file. Select **Publish**.

    ![Screenshot that shows the sample file.](media/use-scim-to-build-users-and-groups-endpoints/cloud-publish.png)

    Note

    To run this solution locally, double-click the project and select **IIS Express** to launch the project as a webpage with a local host URL. For more information, see [IIS Express Overview](/en-us/iis/extensions/introduction-to-iis-express/iis-express-overview).
3. Select **Create profile** and make sure that **App Service** and **Create new** are selected.

    ![Screenshot that shows the Publish window.](media/use-scim-to-build-users-and-groups-endpoints/cloud-publish-2.png)
4. Step through the dialog options and rename the app to a name of your choice. This name is used in both the app and the SCIM endpoint URL.

    ![Screenshot that shows creating a new app service.](media/use-scim-to-build-users-and-groups-endpoints/cloud-publish-3.png)
5. Select the resource group to use and select **Publish**.

    ![Screenshot that shows publishing a new app service.](media/use-scim-to-build-users-and-groups-endpoints/cloud-publish-4.png)

# [Visual Studio Code](#tab/visual-studio-code)
1. In Visual Studio Code, make sure to sign in to the account that has access to your hosting resources.
2. In Visual Studio Code, open the folder that contains the *Microsoft.SCIM.sln* file.
3. Open the Visual Studio Code integrated [terminal](https://code.visualstudio.com/docs/terminal/basics) and run the [dotnet restore](/en-us/nuget/consume-packages/install-use-packages-dotnet-cli#restore-packages) command. This command restores the packages listed in the project files.
4. In the terminal, change the directory using the `cd Microsoft.SCIM.WebHostSample` command
5. To run your app locally, in the terminal, run the .NET CLI command. The [dotnet run](/en-us/dotnet/core/tools/dotnet-run) runs the Microsoft.SCIM.WebHostSample project using the [development environment](/en-us/aspnet/core/fundamentals/environments#set-environment-on-the-command-line).

    ```dotnetcli
    dotnet run --environment Development
    ```
6. If not installed, add [Azure App Service for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) extension.
7. To deploy the Microsoft.SCIM.WebHostSample app to Azure App Services, [create a new App Services](/en-us/azure/app-service/quickstart-dotnetcore?tabs=net60&amp;pivots=development-environment-vscode#2-publish-your-web-app).
8. In the Visual Studio Code terminal, run the .NET CLI command. This command generates a deployable publish folder for the app in the bin/debug/publish directory.

    ```dotnetcli
    dotnet publish -c Debug
    ```
9. In the Visual Studio Code explorer, right-click on the generated **publish** folder, and select Deploy to Web App.
10. A new workflow opens in the command palette at the top of the screen. Select the **Subscription** you would like to publish your app to.
11. Select the **App Service** web app you created earlier.
12. If Visual Studio Code prompts you to confirm, select **Deploy**. The deployment process may take a few moments. When the process completes, a notification should appear in the bottom right corner prompting you to browse to the deployed app.

---

### Configure the App Service

Go to the application in **Azure App Service** &gt; **Configuration** and select **New application setting** to add the *Token\_\_TokenIssuer* setting with the value `https://sts.windows.net/<tenant_id>/`. Replace `<tenant_id>` with your Microsoft Entra tenant ID.

![Screenshot that shows the Application settings window.](media/use-scim-to-build-users-and-groups-endpoints/app-service-settings.png)

When you test your endpoint with an enterprise application in the [Microsoft Entra admin center](use-scim-to-provision-users-and-groups#integrate-your-scim-endpoint-with-the-azure-ad-provisioning-service), you have two options. You can keep the environment in `Development` and provide the testing token from the `/scim/token` endpoint, or you can change the environment to `Production` and leave the token field empty.

That's it! Your SCIM endpoint is now published, and you can use the Azure App Service URL to test the SCIM endpoint.

## Test your SCIM endpoint

Requests to a SCIM endpoint require authorization. The SCIM standard has multiple options available. Requests can use cookies, basic authentication, TLS client authentication, or any of the methods listed in [RFC 7644](https://tools.ietf.org/html/rfc7644#section-2).

Be sure to avoid methods that aren't secure, such as username and password, in favor of a more secure method such as OAuth. Microsoft Entra ID supports long-lived bearer tokens (for gallery and non-gallery applications) and the OAuth authorization grant (for gallery applications).

Note

The authorization methods provided in the repo are for testing only. When you integrate with Microsoft Entra ID, you can review the authorization guidance. See [Plan provisioning for a SCIM endpoint](use-scim-to-provision-users-and-groups).

The development environment enables features that are unsafe for production, such as reference code to control the behavior of the security token validation. The token validation code uses a self-signed security token, and the signing key is stored in the configuration file. See the **Token:IssuerSigningKey** parameter in the *appsettings.Development.json* file.

```json
"Token": {
    "TokenAudience": "Microsoft.Security.Bearer",
    "TokenIssuer": "Microsoft.Security.Bearer",
    "IssuerSigningKey": "A1B2C3D4E5F6A1B2C3D4E5F6",
    "TokenLifetimeInMins": "120"
}
```

Note

When you send a **GET** request to the `/scim/token` endpoint, a token is issued using the configured key. That token can be used as a bearer token for subsequent authorization.

The default token validation code is configured to use a Microsoft Entra token and requires the issuing tenant be configured by using the **Token:TokenIssuer** parameter in the *appsettings.json* file.

```json
"Token": {
    "TokenAudience": "8adf8e6e-67b2-4cf2-a259-e3dc5476c621",
    "TokenIssuer": "https://sts.windows.net/<tenant_id>/"
}
```