---
layout: Conceptual
title: 'Tutorial: Prepare a web application for authentication - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-web-app-dotnet-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to create and prepare an ASP.NET Core application for authentication with the Microsoft identity platform, and secure it with a self-signed certificate.
manager: pmwongera
ms.date: 2025-04-15T00:00:00.0000000Z
ms.topic: tutorial
ms.custom: sfi-image-nochange
locale: en-us
document_id: 69195a1b-0f0d-5b82-7302-f6984b3316dc
document_version_independent_id: 69195a1b-0f0d-5b82-7302-f6984b3316dc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-web-app-dotnet-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-web-app-dotnet-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-web-app-dotnet-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: e214f098-b34d-ded3-7648-18de70d1c7bc
---

# Tutorial: Prepare a web application for authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you create an ASP.NET Core web app and configure it for authentication. This is part 1 of a series that demonstrates how to build an ASP.NET Core web application and prepare it for authentication using the Microsoft Entra admin center. This application can be used for employees in a workforce tenant or for customers using an external tenant

In this tutorial, you:

- Create an ASP.NET Core web app
- Create a self-signed certificate
- Configure the settings for the application
- Define platform settings and URLs

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). This account must have permissions to manage applications. Use any of the following roles needed to register the application:
    - Application Administrator
    - Application Developer
- Although any integrated development environment (IDE) that supports ASP.NET Core applications can be used, this tutorial uses **Visual Studio Code**. You can download it [here](https://visualstudio.microsoft.com/downloads/).
- A minimum requirement of [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet).
- An ASP.NET Core developer certificate. Install one using [dotnet dev-certs](/en-us/dotnet/core/additional-tools/self-signed-certificates-guide#with-dotnet-dev-certs)

# [Workforce tenant](#tab/workforce-tenant)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Web** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `https://localhost:5001/signin-oidc`
    - **Front channel logout URL**: `https://localhost:5001/signout-oidc`
- For development purposes, [create a self signed certificate](howto-create-self-signed-certificate). Refer to [add credentials](how-to-add-credentials) to upload the certificate and record the certificate **Thumbprint**. **Do not use a self signed certificate** for production apps. Use a trusted certificate authority.

# [External tenant](#tab/external-tenant)
- An external tenant. If you don't have one, [create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Web** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `https://localhost:5001/signin-oidc`
    - **Front channel logout URL**: `https://localhost:5001/signout-oidc`
- For development purposes, [create a self signed certificate](howto-create-self-signed-certificate). Refer to [add credentials](how-to-add-credentials) to upload the certificate and record the certificate **Thumbprint**. **Do not use a self signed certificate** for production apps. Use a trusted certificate authority.
- Associate your app with a user flow in the Microsoft Entra admin center. This user flow can be used across multiple applications. For more information, see [Create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers) and [Add your application to the user flow](../external-id/customers/how-to-user-flow-add-application).

---

## Create an ASP.NET Core project

In this section, you create an ASP.NET Core project in Visual Studio Code.

1. Open Visual Studio Code and select **File &gt; Open Folder...**. Navigate to and select the location in which to create your project.
2. Open a new terminal by selecting **Terminal &gt; New Terminal**.
3. Enter the following command to make a Model View Controller (MVC) ASP.NET Core project.

    ```console
    dotnet new mvc -n identity-client-web-app
    ```

## Install identity packages

This application uses [Microsoft.Identity.Web](/en-us/entra/msal/dotnet/microsoft-identity-web/) and the related NuGet package must be installed.

Use the following snippet to change into the new *identity-client-web-app* folder and install the relevant NuGet package:

```console
cd identity-client-web-app
dotnet add package Microsoft.Identity.Web.UI
```

## Configure the application for authentication

Web applications that sign in users by using the Microsoft identity platform are configured through a configuration file, *appsettings.json*. In ASP.NET Core, it must specify the following values:

# [Workforce tenant](#tab/workforce-tenant)
| Setting | Description |
| --- | --- |
| `Instance` | The authentication endpoint to run your app in national clouds. Use one of: - `https://login.microsoftonline.com/` (Azure public cloud) - `https://login.microsoftonline.us/` (Azure US government) - `https://login.microsoftonline.de/` (Microsoft Entra Germany) - `https://login.partner.microsoftonline.cn/` (Microsoft Entra China operated by 21Vianet) |
| `TenantId` | The identifier of the tenant where the app is registered. **Recommended:** use the tenant ID from the app registration. **Alternatives:**- `organizations` (any work or school account) - `common` (work/school or Microsoft personal account) - `consumers` (Microsoft personal accounts only). |
| `ClientId` | Identifier of the application (client) obtained from the application registration. |
| `CertificateThumbprint` | Thumbprint of the certificate uploaded in the Microsoft Entra admin center (see [add credentials](how-to-add-credentials)). |
| `CallbackPath` | Path used to redirect responses; set to `/signin-oidc` for this tutorial. |
| `DownstreamApi` | Identifier that defines an endpoint for accessing Microsoft Graph. Combine the application URI with the required scope (for example, `user.read`). |

# [External tenant](#tab/external-tenant)
| Setting | Description |
| --- | --- |
| `Authority` | URL of the external tenant where the application is registered. Format: `https://<tenant_subdomain>.ciamlogin.com/`. To obtain your tenant subdomain details, see [Create an external tenant](/en-us/entra/external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details). |
| `ClientId` | Identifier of the application (client) obtained from the application registration. |
| `CertificateThumbprint` | Thumbprint of the certificate obtained from [add credentials](how-to-add-credentials) in the Microsoft Entra admin center. |

---

### Update the configuration file

In your IDE, open *appsettings.json* and replace the file contents with the following snippet. Replace the text in quotes with the values that were recorded earlier.

# [Workforce tenant](#tab/workforce-tenant)
```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "Enter_the_Tenant_Id_Here",
    "ClientId": "Enter_the_Application_Id_Here",
    "ClientCertificates": [
      {
        "SourceType": "StoreWithThumbprint",
        "CertificateStorePath": "CurrentUser/My",
        "CertificateThumbprint": "Enter the certificate thumbprint obtained the Microsoft Entra admin center"
      }   
    ],
    "CallbackPath": "/signin-oidc"
  },
    "DownstreamApi": {
      "BaseUrl": "https://graph.microsoft.com/v1.0/",
      "RelativePath": "me",
      "Scopes": [ 
        "user.read" 
      ]
    },
    "Logging": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft.AspNetCore": "Warning"
      }
    },
    "AllowedHosts": "*"
  }
```

# [External tenant](#tab/external-tenant)
```json
{
  "AzureAd": {
    "Authority": "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/",
    "ClientId": "Enter_the_Application_Id_Here",
    "ClientCertificates": [
      {
        "SourceType": "StoreWithThumbprint",
        "CertificateStorePath": "CurrentUser/My",
        "CertificateThumbprint": "Enter the certificate thumbprint obtained the Microsoft Entra admin center"
      }   
    ],
    "CallbackPath": "/signin-oidc",
    "SignedOutCallbackPath": "/signout-callback-oidc"
  },
  "DownstreamApi": {
    "BaseUrl": "https://graph.microsoft.com/v1.0/",
    "RelativePath": "me",
    "Scopes": [ 
      "user.read" 
    ]
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

---

### Update the redirect URI

From the prerequisites, the redirect URI is set to `https://localhost:5001/signin-oidc`. This needs to be updated in the application launch settings. You can use the redirect URI that is created during the local application setup, or any other available port number, provided it matches the redirect URI in the application registration.

1. In the **Properties** folder, open the *launchSettings.json* file.
2. Find the `https` object, and update the value of `applicationURI` with the correct port number, in this case, `5001`. The line should look similar to the following snippet:

    ```json
    "applicationUrl": "https://localhost:5001;http://localhost:{port}",
    ```