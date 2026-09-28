---
layout: Conceptual
title: 'Quickstart: Get token & call Microsoft Graph in a console app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/daemon-quickstart-portal-netcore
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how a .NET sample app can use the client credentials flow to get a token and call Microsoft Graph.
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2024-09-24T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: concept-article
locale: en-us
document_id: e63d9409-5e6a-b35c-28f5-aab1e3a65b2e
document_version_independent_id: a548137e-86c0-c241-ae16-f3fa913b8f28
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/daemon-quickstart-portal-netcore.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/daemon-quickstart-portal-netcore
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/daemon-quickstart-portal-netcore.md
platformId: abb80e4c-60fe-e67d-ee9b-77ae92ecb2fc
---

# Quickstart: Get token & call Microsoft Graph in a console app - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Acquire a token and call Microsoft Graph in a .NET console app](quickstart-daemon-dotnet-acquire-token)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Get a token and call the Microsoft Graph API by using a console app's identity

In this quickstart, you download and run a code sample that demonstrates how a .NET console application can get an access token to call the Microsoft Graph API and display a [list of users](/en-us/graph/api/user-list) in the directory. The code sample also demonstrates how a job or a Windows service can run with an application identity, instead of a user's identity. The sample console application in this quickstart is also a daemon application, so it's a confidential client application.

## Prerequisites

[.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)

### Download and configure your quickstart app

#### Step 1: Configure your application in the Azure portal

For the code sample in this quickstart to work, create a client secret and add the Graph API's **User.Read.All** application permission.

![Already configured](media/quickstart-v2-netcore-daemon/green-check.png) Your application is configured with these attributes.

#### Step 2: Download your Visual Studio project

Run the project by using Visual Studio 2019.

Tip

To avoid errors caused by path length limitations in Windows, we recommend extracting the archive or cloning the repository into a directory near the root of your drive.

Note

`Enter_the_Supported_Account_Info_Here`

##### Standard user

If you're a standard user of your tenant, ask a Global Administrator to grant admin consent for your application. To do this, give the following URL to your administrator:

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```

You might see the error "AADSTS50011: No reply address is registered for the application" after you grant consent to the app by using the preceding URL. This error happens because this application and the URL don't have a redirect URI. You can ignore it.

#### Step 4: Run the application

If you're using Visual Studio, press **F5** to run the application. Otherwise, run the application via command prompt, console, or terminal:

```dotnetcli
cd {ProjectFolder}\1-Call-MSGraph\daemon-console
dotnet run
```

In that code:

- `{ProjectFolder}` is the folder where you extracted the .zip file. An example is `C:\Azure-Samples\active-directory-dotnetcore-daemon-v2`.

You should see a list of users in Microsoft Entra ID as result.

This quickstart application uses a client secret to identify itself as a confidential client. The client secret is added as a plain-text file to your project files. For security reasons, we recommend that you use a certificate instead of a client secret before considering the application as a production application. For more information on how to use a certificate, see [these instructions](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/#variation-daemon-application-using-client-credentials-with-certificates) in the GitHub repository for this sample.

## More information

This section gives an overview of the code required to sign in users. This overview can be useful to understand how the &gt; code works, what the main arguments are, and how to add sign-in to an existing .NET console application.

### How the sample works

![Diagram that shows how the sample app generated by this quickstart works.](media/quickstart-v2-netcore-daemon/netcore-daemon-intro.svg)

### MSAL.NET

Microsoft Authentication Library (MSAL, in the [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) package) is the library that's used to sign in users and request tokens for accessing an API protected by the Microsoft identity platform. This quickstart requests tokens by using the application's own identity instead of delegated permissions. The authentication flow in this case is known as a [client credentials OAuth flow](v2-oauth2-client-creds-grant-flow). For more information on how to use MSAL.NET with a client credentials flow, see [this article](https://aka.ms/msal-net-client-credentials).

You can install MSAL.NET by running the following command in the Visual Studio Package Manager Console:

```dotnetcli
dotnet add package Microsoft.Identity.Client
```

### MSAL initialization

You can add the reference for MSAL by adding the following code:

```csharp
using Microsoft.Identity.Client;
```

Then, initialize MSAL by using the following code:

```csharp
IConfidentialClientApplication app;
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
                                          .WithClientSecret(config.ClientSecret)
                                          .WithAuthority(new Uri(config.Authority))
                                          .Build();
```

| Element | Description |
| --- | --- |
| `config.ClientSecret` | The client secret created for the application in the Azure portal. |
| `config.ClientId` | The application (client) ID for the application registered in the Azure portal. You can find this value on the app's **Overview** page in the Azure portal. |
| `config.Authority` | (Optional) The security token service (STS) endpoint for the user to authenticate. It's usually `https://login.microsoftonline.com/{tenant}` for the public cloud, where `{tenant}` is the name of your tenant or your tenant ID. |

For more information, see the [reference documentation for `ConfidentialClientApplication`](/en-us/dotnet/api/microsoft.identity.client.iconfidentialclientapplication).

### Requesting tokens

To request a token by using the app's identity, use the `AcquireTokenForClient` method:

```csharp
result = await app.AcquireTokenForClient(scopes)
                  .ExecuteAsync();
```

| Element | Description |
| --- | --- |
| `scopes` | Contains the requested scopes. For confidential clients, this value should use a format similar to `{Application ID URI}/.default`. This format indicates that the requested scopes are the ones that are statically defined in the app object set in the Azure portal. For Microsoft Graph, `{Application ID URI}` points to `https://graph.microsoft.com`. For custom web APIs, `{Application ID URI}` is defined in the Azure portal, under \*\*Application Registration \*\* &gt; **Expose an API**. |

For more information, see the [reference documentation for `AcquireTokenForClient`](/en-us/dotnet/api/microsoft.identity.client.confidentialclientapplication.acquiretokenforclient).

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).