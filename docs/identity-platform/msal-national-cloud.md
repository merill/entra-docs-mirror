---
layout: Conceptual
title: Use MSAL in a national cloud app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-national-cloud
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The Microsoft Authentication Library (MSAL) enables application developers to acquire tokens in order to call secured web APIs. These web APIs can be Microsoft Graph, other Microsoft APIs, partner web APIs, or your own web API. MSAL supports multiple application architectures and platforms.
manager: pmwongera
ms.custom: 
ms.date: 2021-09-21T00:00:00.0000000Z
ms.reviewer: negoe,
ms.topic: concept-article
locale: en-us
document_id: e0a53bf5-59da-f65e-fd17-d6299b7e4209
document_version_independent_id: dc62686f-98bc-20a5-22a0-5607829f2d62
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-national-cloud.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-national-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-national-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 335271d0-dbcb-4b71-8b42-f10398ce4165
---

# Use MSAL in a national cloud app - Microsoft identity platform | Microsoft Learn

[National clouds](authentication-national-cloud), also known as Sovereign clouds, are physically isolated instances of Azure. These regions of Azure help make sure that data residency, sovereignty, and compliance requirements are honored within geographical boundaries.

In addition to the Microsoft worldwide cloud, the Microsoft Authentication Library (MSAL) enables application developers in national clouds to acquire tokens in order to authenticate and call secured web APIs. These web APIs can be Microsoft Graph or other Microsoft APIs.

Including the global Azure cloud, Microsoft Entra ID is deployed in the following national clouds: 

- Azure Government
- Microsoft Azure operated by 21Vianet
- Azure Germany ([Closing on October 29, 2021](https://www.microsoft.com/cloud-platform/germany-cloud-regions))

This guide demonstrates how to sign in to work and school accounts, get an access token, and call the Microsoft Graph API in the [Azure Government cloud](https://azure.microsoft.com/global-infrastructure/government/) environment.

## Azure Germany (Microsoft Cloud Deutschland)

Warning

Azure Germany (Microsoft Cloud Deutschland) will be [closed on October 29, 2021](https://www.microsoft.com/cloud-platform/germany-cloud-regions). Services and applications you choose *not* to migrate to a region in global Azure before that date will become inaccessible.

If you haven't migrated your application from Azure Germany, follow [Microsoft Entra information for the migration from Azure Germany](/en-us/microsoft-365/enterprise/ms-cloud-germany-transition-azure-ad) to get started.

## Prerequisites

Before you start, make sure that you meet these prerequisites.

### Choose the appropriate identities

[Azure Government](/en-us/azure/azure-government/) applications can use Microsoft Entra Government identities and Microsoft Entra Public identities to authenticate users. Because you can use any of these identities, decide which authority endpoint you should choose for your scenario:

- Microsoft Entra Public: Commonly used if your organization already has a Microsoft Entra Public tenant to support Microsoft 365 (Public or GCC) or another application.
- Microsoft Entra Government: Commonly used if your organization already has a Microsoft Entra Government tenant to support Office 365 (GCC High or DoD) or is creating a new tenant in Microsoft Entra Government.

After you decide, a special consideration is where you perform your app registration. If you choose Microsoft Entra Public identities for your Azure Government application, you must register the application in your Microsoft Entra Public tenant.

### Get an Azure Government subscription

To get an Azure Government subscription, see [Managing and connecting to your subscription in Azure Government](/en-us/azure/azure-government/compare-azure-government-global-azure).

If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.

For details about using a national cloud with a particular programming language, choose the tab matching your language:

# [.NET](#tab/dotnet)
You can use MSAL.NET to sign in users, acquire tokens, and call the Microsoft Graph API in national clouds.

The following tutorials demonstrate how to build an ASP.NET Core web app. The app uses OpenID Connect to sign in users with a work and school account in an organization that belongs to a national cloud.

- To sign in users and acquire tokens, follow this tutorial: [Build an ASP.NET Core web app signing-in users in sovereign clouds with the Microsoft identity platform](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/1-WebApp-OIDC/1-4-Sovereign#build-an-aspnet-core-web-app-signing-in-users-in-sovereign-clouds-with-the-microsoft-identity-platform).
- To call the Microsoft Graph API, follow this tutorial: [Using the Microsoft identity platform to call the Microsoft Graph API from an ASP.NET Core web app, on behalf of a user signing-in using their work and school account in Microsoft National Cloud](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-4-Sovereign-Call-MSGraph#using-the-microsoft-identity-platform-to-call-the-microsoft-graph-api-from-an-an-aspnet-core-2x-web-app-on-behalf-of-a-user-signing-in-using-their-work-and-school-account-in-microsoft-national-cloud).

# [JavaScript](#tab/javascript)
To enable your MSAL.js application for sovereign clouds:

- Register your application in a specific portal, depending on the cloud. For more information on how to choose the portal refer [App registration endpoints](authentication-national-cloud#app-registration-endpoints)
- Use any of the [samples](https://github.com/Azure-Samples/ms-identity-javascript-tutorial) from the repo with a few changes to the configuration, depending on the cloud, which is mentioned next.
- Use a specific authority, depending on the cloud you registered the application in. For more information on authorities for different clouds, refer to [Microsoft Entra authentication endpoints](authentication-national-cloud#azure-ad-authentication-endpoints).
- Calling the Microsoft Graph API requires an endpoint URL specific to the cloud you are using. To find Microsoft Graph endpoints for all the national clouds, refer to [Microsoft Graph and Graph Explorer service root endpoints](/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints).

Here's an example authority:

```json
"authority": "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here"
```

Here's an example of a Microsoft Graph endpoint, with scope:

```json
"endpoint" : "https://graph.microsoft.us/v1.0/me"
"scope": "User.Read"
```

Here's the minimal code for authenticating a user with a sovereign cloud and calling Microsoft Graph:

```javascript
const msalConfig = {
    auth: {
        clientId: "Enter_the_Application_Id_Here",
        authority: "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here",
        redirectUri: "/",
    }
};

// Initialize MSAL
const msalObj = new PublicClientApplication(msalConfig);

// Get token using popup experience
try {
    const graphToken = await msalObj.acquireTokenPopup({
        scopes: ["User.Read"]
    });
} catch(error) {
    console.log(error)
}

// Call the Graph API
const headers = new Headers();
const bearer = `Bearer ${graphToken}`;

headers.append("Authorization", bearer);

fetch("https://graph.microsoft.us/v1.0/me", {
    method: "GET",
    headers: headers
})
```

# [Python](#tab/python)
To enable your MSAL Python application for sovereign clouds:

- Register your application in a specific portal, depending on the cloud. For more information on how to choose the portal refer [App registration endpoints](authentication-national-cloud#app-registration-endpoints)
- Use any of the [samples](https://github.com/AzureAD/microsoft-authentication-library-for-python/tree/dev/sample) from the repo with a few changes to the configuration, depending on the cloud, which is mentioned next.
- Use a specific authority, depending on the cloud you registered the application in. For more information on authorities for different clouds, refer [Microsoft Entra authentication endpoints](authentication-national-cloud#azure-ad-authentication-endpoints).

    Here's an example authority:

    ```json
    "authority": "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here"
    ```
- Calling the Microsoft Graph API requires an endpoint URL specific to the cloud you are using. To find Microsoft Graph endpoints for all the national clouds, refer to [Microsoft Graph and Graph Explorer service root endpoints](/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints).

    Here's an example of a Microsoft Graph endpoint, with scope:

    ```json
    "endpoint" : "https://graph.microsoft.us/v1.0/me"
    "scope": "User.Read"
    ```

# [Java](#tab/java)
To enable your MSAL for Java application for sovereign clouds:

- Register your application in a specific portal, depending on the cloud. For more information on how to choose the portal refer [App registration endpoints](authentication-national-cloud#app-registration-endpoints)
- Use any of the [samples](https://github.com/AzureAD/microsoft-authentication-library-for-java/tree/dev/msal4j-sdk/src/samples) from the repo with a few changes to the configuration, depending on the cloud, which are mentioned next.
- Use a specific authority, depending on the cloud you registered the application in. For more information on authorities for different clouds, refer [Microsoft Entra authentication endpoints](authentication-national-cloud#azure-ad-authentication-endpoints).

Here's an example authority:

```json
"authority": "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here"
```

- Calling the Microsoft Graph API requires an endpoint URL specific to the cloud you are using. To find Microsoft Graph endpoints for all the national clouds, refer to [Microsoft Graph and Graph Explorer service root endpoints](/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints).

Here's an example of a graph endpoint, with scope:

```json
"endpoint" : "https://graph.microsoft.us/v1.0/me"
"scope": "User.Read"
```

# [Objective-C](#tab/objc)
MSAL for iOS and macOS can be used to acquire tokens in national clouds, but it requires additional configuration when creating `MSALPublicClientApplication`.

For instance, if you want your application to be a multi-tenant application in a national cloud (here US Government), you could write:

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

# [Swift](#tab/swift)
MSAL for iOS and macOS can be used to acquire tokens in national clouds, but it requires additional configuration when creating `MSALPublicClientApplication`.

For instance, if you want your application to be a multi-tenant application in a national cloud (here US Government), you could write:

```swift
let authority = try? MSALAADAuthority(cloudInstance: .usGovernmentCloudInstance, audienceType: .azureADMultipleOrgsAudience, rawTenant: nil)

let config = MSALPublicClientApplicationConfig(clientId: "<your-client-id-here>", redirectUri: "<your-redirect-uri-here>", authority: authority)
if let application = try? MSALPublicClientApplication(configuration: config) { /* Use application */}
```

---