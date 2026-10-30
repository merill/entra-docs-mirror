---
layout: Conceptual
title: Implement role-based access control in applications - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-implement-rbac-for-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to implement role-based access control in your applications.
manager: pmwongera
ms.date: 2024-10-29T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: dc75dbfb-20e7-2151-ece7-a4518df00ff9
document_version_independent_id: bf002af9-ac37-c0a7-4e7c-41d923d173bd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-implement-rbac-for-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-implement-rbac-for-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-implement-rbac-for-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: eeee1c07-a3cb-f511-4833-540b708a1503
---

# Implement role-based access control in applications - Microsoft identity platform | Microsoft Learn

Role-based access control (RBAC) allows users or groups to have specific permissions to access and manage resources. Typically, implementing RBAC to protect a resource includes protecting either a web application, a single-page application (SPA), or an API. This protection could be for the entire application or API, specific areas and features, or API methods. For more information about the basics of authorization, see [Authorization basics](authorization-basics).

As discussed in [Role-based access control for application developers](custom-rbac-for-developers), there are three ways to implement RBAC using the Microsoft identity platform:

- **App Roles** – using the [App Roles feature in an application](howto-add-app-roles-in-apps#declare-roles-for-an-application) using logic within the application to interpret incoming app role assignments.
- **Groups** – using group assignments of an incoming identity using logic within the application to interpret the group assignments.
- **Custom Data Store** – retrieve and interpret role assignments using logic within the application.

The preferred approach is to use *App Roles* as it is the easiest to implement. This approach is supported directly by the SDKs that are used in building apps utilizing the Microsoft identity platform. For more information on how to choose an approach, see [Choose an approach](custom-rbac-for-developers#choose-an-approach).

## Define app roles

The first step for implementing RBAC for an application is to define the app roles for it and assign users or groups to it. This process is outlined in [How to: Add app roles to your application and receive them in the token](howto-add-app-roles-in-apps). After defining the app roles and assigning users or groups to them, access the role assignments in the tokens coming into the application and act on them accordingly.

## Implement RBAC in ASP.NET Core

ASP.NET Core supports adding RBAC to an ASP.NET Core web application or web API. Adding RBAC allows for easy implementation by using [role checks](/en-us/aspnet/core/security/authorization/roles?view=aspnetcore-5.0&amp;preserve-view=true#adding-role-checks) with the ASP.NET Core *Authorize* attribute. It's also possible to use ASP.NET Core’s support for [policy-based role checks](/en-us/aspnet/core/security/authorization/roles?view=aspnetcore-5.0&amp;preserve-view=true#policy-based-role-checks).

### ASP.NET Core MVC web application

Implementing RBAC in an ASP.NET Core MVC web application is straightforward. It mainly involves using the *Authorize* attribute to specify which roles should be allowed to access specific controllers or actions in the controllers. Follow these steps to implement RBAC in an ASP.NET Core MVC application:

1. Create an application registration with app roles and assignments as outlined in *Define app roles* above.
2. Do one of the following steps:

    - Create a new ASP.NET Core MVC web application project using the **dotnet cli**. Specify the `--auth` flag with either `SingleOrg` for single tenant authentication or `MultiOrg` for multi-tenant authentication, the `--client-id` flag with the client if from the application registration, and the `--tenant-id` flag with the tenant if from the Microsoft Entra tenant:

        ```bash
        dotnet new mvc --auth SingleOrg --client-id <YOUR-APPLICATION-CLIENT-ID> --tenant-id <TENANT-ID>  
        ```
    - Add the Microsoft.Identity.Web and Microsoft.Identity.Web.UI libraries to an existing ASP.NET Core MVC project:

        ```bash
        dotnet add package Microsoft.Identity.Web 
        dotnet add package Microsoft.Identity.Web.UI 
        ```
3. Follow the instructions specified in [Quickstart: Add sign-in with Microsoft to an ASP.NET Core web app](quickstart-v2-aspnet-core-webapp?view=aspnetcore-5.0&amp;preserve-view=true) to add authentication to the application.
4. Add role checks on the controller actions as outlined in [Adding role checks](/en-us/aspnet/core/security/authorization/roles?view=aspnetcore-5.0&amp;preserve-view=true#adding-role-checks).
5. Test the application by trying to access one of the protected MVC routes.

### ASP.NET Core web API

Implementing RBAC in an ASP.NET Core web API mainly involves utilizing the *Authorize* attribute to specify which roles should be allowed to access specific controllers or actions in the controllers. Follow these steps to implement RBAC in the ASP.NET Core web API:

1. Create an application registration with app roles and assignments as outlined in *Define app roles* above.
2. Do one of the following steps:

    - Create a new ASP.NET Core MVC web API project using the **dotnet cli**. Specify the `--auth` flag with either `SingleOrg` for single tenant authentication or `MultiOrg` for multi-tenant authentication, the `--client-id` flag with the client if from the application registration, and the `--tenant-id` flag with the tenant if from the Microsoft Entra tenant:

        ```bash
        dotnet new webapi --auth SingleOrg --client-id <YOUR-APPLICATION-CLIENT-ID> --tenant-id <TENANT-ID> 
        ```
    - Add the Microsoft.Identity.Web and Swashbuckle.AspNetCore libraries to an existing ASP.NET Core web API project:

        ```bash
        dotnet add package Microsoft.Identity.Web
        dotnet add package Swashbuckle.AspNetCore 
        ```
3. Follow the instructions specified in [Quickstart: Add sign-in with Microsoft to an ASP.NET Core web app](quickstart-v2-aspnet-core-webapp?view=aspnetcore-5.0&amp;preserve-view=true) to add authentication to the application.
4. Add role checks on the controller actions as outlined in [Adding role checks](/en-us/aspnet/core/security/authorization/roles?view=aspnetcore-5.0&amp;preserve-view=true#adding-role-checks).
5. Call the API from a client application. See [Angular single-page application calling ASP.NET Core web API and using App Roles to implement Role-Based Access Control](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/samples/msal-angular-samples) for an end to end sample.

## Implement RBAC in other platforms

### Angular SPA

Implementing RBAC in an Angular SPA involves the use of the [Microsoft Authentication Library for Angular](https://www.npmjs.com/package/@azure/msal-angular) to authorize access to the Angular routes contained within the application. An example is shown in the [MSAL Angular v3 Samples](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/samples/msal-angular-samples).

Note

Client-side RBAC implementations should be paired with server-side RBAC to prevent unauthorized applications from accessing sensitive resources.

### Node.js with Express application

Implementing RBAC in a Node.js with express application involves the use of MSAL to authorize access to the Express routes contained within the application. An example is shown in the [Enable your Node.js web app to sign-in users and call APIs with the Microsoft identity platform](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial#chapter-4-control-access-to-your-app-using-app-roles-and-security-groups) sample.