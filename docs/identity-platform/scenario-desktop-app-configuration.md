---
layout: Conceptual
title: Configure desktop apps that call web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-desktop-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure the code of a desktop app that calls web APIs
manager: pmwongera
ms.date: 2024-04-09T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: d7608fb0-1466-594c-dfe8-be9e4a9c3fdf
document_version_independent_id: afe5a75f-decf-fd40-9d05-f5bb9c1c7bdf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-desktop-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-desktop-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-desktop-app-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: f3884286-6420-140f-ccab-a920ca9588d0
---

# Configure desktop apps that call web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article contains instructions to help you configure the code with the application's coordinates.

## Prerequisites

- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

## Add a platform redirect URI

To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication** &gt; **Add a platform** &gt; **Mobile and desktop applications**
2. Depending on the authentication method you're using, choose one of the following options:
    - For apps using embedded browsers, use the exact value: `https://login.microsoftonline.com/common/oauth2/nativeclient`
    - For apps using system browsers, use the exact value: `http://localhost`
    - Objective-C or Swift apps for macOS: `msauth.<your.app.bundle.id>://auth`.
    - Node.js Electron apps: `msal{Your_Application/Client_Id}://auth`

Note

For [Web Authentication Manager (WAM)](scenario-desktop-acquire-token-wam) apps, no redirect URI is needed in MSAL.

## Enable public client flow

To distinguish device code flow, integrated Windows authentication, and a username and a password from a confidential client application using a client credential flow used in daemon applications, none of which requires a redirect URI, configure it as a public client application. To achieve this configuration

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

## Microsoft libraries supporting desktop apps

The following Microsoft libraries support desktop apps:

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| Electron | [MSAL Node.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | [msal-node](https://www.npmjs.com/package/@azure/msal-node) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | Public preview |
| Java | [MSAL4J](https://github.com/AzureAD/microsoft-authentication-library-for-java) | [msal4j](https://mvnrepository.com/artifact/com.microsoft.azure/msal4j) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| macOS (Swift/Obj-C) | [MSAL for iOS and macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [MSAL](https://cocoapods.org/pods/MSAL) | [Tutorial](tutorial-v2-ios) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| UWP | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) | [Tutorial](tutorial-v2-windows-uwp) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| WPF | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) | [Tutorial](tutorial-v2-windows-desktop) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |

^1^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

## Public client application

From a code point of view, desktop applications are public client applications. The configuration will be a bit different based on whether you use interactive authentication or not.

# [.NET](#tab/dotnet)
You'll need to build and manipulate MSAL.NET `IPublicClientApplication`.

![IPublicClientApplication](media/scenarios/public-client-application.png)

### Exclusively by code

The following code instantiates a public client application and signs in users in the Microsoft Azure public cloud with a work or school account or a personal Microsoft account.

```csharp
IPublicClientApplication app = PublicClientApplicationBuilder.Create(clientId)
    .Build();
```

If you intend to use interactive authentication or device code flow, as seen previously, use the `.WithRedirectUri` modifier.

```csharp
IPublicClientApplication app;
app = PublicClientApplicationBuilder.Create(clientId)
        .WithDefaultRedirectUri()
        .Build();
```

### Use configuration files

The following code instantiates a public client application from a configuration object, which could be filled in programmatically or read from a configuration file.

```csharp
PublicClientApplicationOptions options = GetOptions(); // your own method
IPublicClientApplication app = PublicClientApplicationBuilder.CreateWithApplicationOptions(options)
        .WithDefaultRedirectUri()
        .Build();
```

### More elaborated configuration

You can elaborate the application building by adding a number of modifiers. For instance, if you want your application to be a multitenant application in a national cloud, such as US Government shown here, you could write:

```csharp
IPublicClientApplication app;
app = PublicClientApplicationBuilder.Create(clientId)
        .WithDefaultRedirectUri()
        .WithAadAuthority(AzureCloudInstance.AzureUsGovernment,
                         AadAuthorityAudience.AzureAdMultipleOrgs)
        .Build();
```

MSAL.NET also contains a modifier for Active Directory Federation Services 2019:

```csharp
IPublicClientApplication app;
app = PublicClientApplicationBuilder.Create(clientId)
        .WithAdfsAuthority("https://consoso.com/adfs")
        .Build();
```

Finally, if you want to acquire tokens for an Azure Active Directory (Azure AD) B2C tenant, specify your tenant as shown in the following code snippet:

```csharp
IPublicClientApplication app;
app = PublicClientApplicationBuilder.Create(clientId)
        .WithB2CAuthority("https://fabrikamb2c.b2clogin.com/tfp/{tenant}/{PolicySignInSignUp}")
        .Build();
```

### Learn more

To learn more about how to configure an MSAL.NET desktop application:

- For a list of all modifiers available on `PublicClientApplicationBuilder`, see the reference documentation [PublicClientApplicationBuilder](/en-us/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder#methods).
- For a description of all the options exposed in `PublicClientApplicationOptions`, see [PublicClientApplicationOptions](/en-us/dotnet/api/microsoft.identity.client.publicclientapplicationoptions) in the reference documentation.

### Complete example with configuration options

Imagine a .NET console application that has the following `appsettings.json` configuration file:

```json
{
  "Authentication": {
    "AzureCloudInstance": "AzurePublic",
    "AadAuthorityAudience": "AzureAdMultipleOrgs",
    "ClientId": "00001111-aaaa-2222-bbbb-3333cccc4444"
  },

  "WebAPI": {
    "MicrosoftGraphBaseEndpoint": "https://graph.microsoft.com"
  }
}
```

You have little code to read in this file by using the .NET-provided configuration framework:

```csharp
public class SampleConfiguration
{
 /// <summary>
 /// Authentication options
 /// </summary>
 public PublicClientApplicationOptions PublicClientApplicationOptions { get; set; }

 /// <summary>
 /// Base URL for Microsoft Graph (it varies depending on whether the application runs
 /// in Microsoft Azure public clouds or national or sovereign clouds)
 /// </summary>
 public string MicrosoftGraphBaseEndpoint { get; set; }

 /// <summary>
 /// Reads the configuration from a JSON file
 /// </summary>
 /// <param name="path">Path to the configuration json file</param>
 /// <returns>SampleConfiguration as read from the json file</returns>
 public static SampleConfiguration ReadFromJsonFile(string path)
 {
  // .NET configuration
  IConfigurationRoot Configuration;
  var builder = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile(path);
  Configuration = builder.Build();

  // Read the auth and graph endpoint configuration
  SampleConfiguration config = new SampleConfiguration()
  {
   PublicClientApplicationOptions = new PublicClientApplicationOptions()
  };
  Configuration.Bind("Authentication", config.PublicClientApplicationOptions);
  config.MicrosoftGraphBaseEndpoint =
  Configuration.GetValue<string>("WebAPI:MicrosoftGraphBaseEndpoint");
  return config;
 }
}
```

Now, to create your application, write the following code:

```csharp
SampleConfiguration config = SampleConfiguration.ReadFromJsonFile("appsettings.json");
var app = PublicClientApplicationBuilder.CreateWithApplicationOptions(config.PublicClientApplicationOptions)
           .WithDefaultRedirectUri()
           .Build();
```

Before the call to the `.Build()` method, you can override your configuration with calls to `.WithXXX` methods, as seen previously.

# [Java](#tab/java)
Here's the class used in MSAL Java development samples to configure the samples: [TestData](https://github.com/AzureAD/microsoft-authentication-library-for-java/tree/dev/msal4j-sdk/src/samples/public-client/).

```Java
PublicClientApplication pca = PublicClientApplication.builder(CLIENT_ID)
        .authority(AUTHORITY)
        .build();
```

# [MacOS](#tab/macOS)
The following code instantiates a public client application and signs in users in the Microsoft Azure public cloud with a work or school account or a personal Microsoft account.

### Quick configuration

Objective-C:

```objc
NSError *msalError = nil;

MSALPublicClientApplicationConfig *config = [[MSALPublicClientApplicationConfig alloc] initWithClientId:@"<your-client-id-here>"];
MSALPublicClientApplication *application = [[MSALPublicClientApplication alloc] initWithConfiguration:config error:&msalError];
```

Swift:

```swift
let config = MSALPublicClientApplicationConfig(clientId: "<your-client-id-here>")
if let application = try? MSALPublicClientApplication(configuration: config){ /* Use application */}
```

### More elaborated configuration

You can elaborate the application building by adding a number of modifiers. For instance, if you want your application to be a multitenant application in a national cloud, such as US Government shown here, you could write:

Objective-C:

```objc
MSALAADAuthority *aadAuthority =
                [[MSALAADAuthority alloc] initWithCloudInstance:MSALAzureUsGovernmentCloudInstance
                                                   audienceType:MSALAzureADMultipleOrgsAudience
                                                      rawTenant:nil
                                                          error:nil];

MSALPublicClientApplicationConfig *config =
                [[MSALPublicClientApplicationConfig alloc] initWithClientId:@"<your-client-id-here>"
                                                                redirectUri:@"<your-redirect-uri-here>"
                                                                  authority:aadAuthority];

NSError *applicationError = nil;
MSALPublicClientApplication *application =
                [[MSALPublicClientApplication alloc] initWithConfiguration:config error:&applicationError];
```

Swift:

```swift
let authority = try? MSALAADAuthority(cloudInstance: .usGovernmentCloudInstance, audienceType: .azureADMultipleOrgsAudience, rawTenant: nil)

let config = MSALPublicClientApplicationConfig(clientId: "<your-client-id-here>", redirectUri: "<your-redirect-uri-here>", authority: authority)
if let application = try? MSALPublicClientApplication(configuration: config) { /* Use application */}
```

# [Node.js](#tab/nodejs)
Configuration parameters can be loaded from many sources, like a JavaScript file or from environment variables. Below, an *authConfig.js* file is used.

```js
/*
 * Copyright (c) Microsoft Corporation. All rights reserved.
 * Licensed under the MIT License.
 */

const { LogLevel } = require("@azure/msal-node");

/**
 * Configuration object to be passed to MSAL instance on creation.
 * For a full list of MSAL.js configuration parameters, visit:
 * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/configuration.md
 */
const AAD_ENDPOINT_HOST = "Enter_the_Cloud_Instance_Id_Here"; // include the trailing slash

const msalConfig = {
    auth: {
        clientId: "Enter_the_Application_Id_Here",
        authority: `${AAD_ENDPOINT_HOST}Enter_the_Tenant_Info_Here`,
    },
    system: {
        loggerOptions: {
            loggerCallback(loglevel, message, containsPii) {
                console.log(message);
            },
            piiLoggingEnabled: false,
            logLevel: LogLevel.Verbose,
        },
    },
};

/**
 * Add here the endpoints and scopes when obtaining an access token for protected web APIs. For more information, see:
 * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/resources-and-scopes.md
 */
const GRAPH_ENDPOINT_HOST = "Enter_the_Graph_Endpoint_Here"; // include the trailing slash

const protectedResources = {
    graphMe: {
        endpoint: `${GRAPH_ENDPOINT_HOST}v1.0/me`,
        scopes: ["User.Read"],
    }
};

module.exports = {
    msalConfig: msalConfig,
    protectedResources: protectedResources,
};
```

Import the configuration object from *authConfig.js* file. MSAL Node can be initialized minimally as below. See the available [configuration options](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/configuration.md).

```JavaScript
const { PublicClientApplication } = require('@azure/msal-node');
const { msalConfig } = require('./authConfig')

/**
* Initialize a public client application. For more information, visit:
* https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-public-client-application.md
*/
clientApplication = new PublicClientApplication(msalConfig);
```

# [Python](#tab/python)
```Python
config = json.load(open(sys.argv[1]))

app = msal.PublicClientApplication(
    config["client_id"], authority=config["authority"],
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

---