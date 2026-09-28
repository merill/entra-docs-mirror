---
layout: Conceptual
title: Quickstart - Edit profile in a sample Node.js web app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-web-app-node-sign-in-edit-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure a sample web app to edit user's profile. The edit profile operation requires a customer user to complete multifactor authentication (MFA)
manager: dougeby
ms.topic: quickstart
ms.date: 2024-11-28T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 4c7ba8f9-d8b0-cd1f-a523-c2f09ad3e6e7
document_version_independent_id: 4c7ba8f9-d8b0-cd1f-a523-c2f09ad3e6e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-web-app-node-sign-in-edit-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-web-app-node-sign-in-edit-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-web-app-node-sign-in-edit-profile.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 3ae43495-f4a6-d8e9-49c9-f6cb8cdac9a3
---

# Quickstart - Edit profile in a sample Node.js web app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this Quickstart, you use a sample Node.js web app to learn how to add sign in and edit profile in a web app. The sample web app uses [Microsoft Authentication Library for Node (MSAL Node)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) and Microsoft Graph API to complete the sign in and edit profile operation. The edit profile operation requires a user to complete an multifactor authentication (MFA).

## Prerequisites

- Complete the steps and prerequisites in [Quickstart: Sign in users in a sample web app](quickstart-web-app-sign-in?pivots=external&amp;tabs=node-external) article. This Quickstart shows you how to sign in users by using a sample Node.js web app.
- Register a new app for your web API in the [Microsoft Entra admin center](https://entra.microsoft.com), with the name *edit-profile-service*, configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add a client secret to your app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).

## Configure API scopes and roles

By registering the web API, you must configure API scopes to define the permissions that a client application can request to access the web API. Additionally, you need to set up app roles to specify the roles available for users or applications, and grant the necessary API permissions to the web app to enable it to call the web API.

### Configure EditProfileService app API scopes

The EditProfileService app needs to expose permissions that a client app acquires to call the web API.

An API needs to publish a minimum of one scope, also called [Delegated Permission](permissions-consent-overview), for the client apps to obtain an access token for a user successfully. To publish a scope, follow these steps:

1. From the **App registrations** page, select the API application that you created (such as *edit-profile-service*) to open its **Overview** page.
2. Under **Manage**, select **Expose an API**.
3. At the top of the page, next to **Application ID URI**, select the **Add** link to generate a URI that is unique for this app.
4. Accept the proposed Application ID URI such as `api://{clientId}`, and select **Save**. When your web application requests an access token for the web API, it adds the URI as the prefix for each scope that you define for the API.
5. Under **Scopes defined by this API**, select **Add a scope**.
6. Enter the following values that define a read access to the API, then select **Add scope** to save your changes:

    | Property | Value |
    | --- | --- |
    | Scope name | *EditProfileService.ReadWrite* |
    | Who can consent | **Admins only** |
    | Admin consent display name | *Client edits profile through edit profile service* |
    | Admin consent description | *The scope to allow client web app to edit profile through calling the edit profile service*. |
    | State | **Enabled** |

### Grant User.ReadWrite permission to the EditProfileService app

*User.ReadWrite* is a Microsoft Graph API permission that enables a user to update their profile. To grant the *User.ReadWrite* permission to the EditProfileService app, use the following steps:

1. From the **App registrations** page, select the application that you created (such as *edit-profile-service*) to open its **Overview** page.
2. Under **Manage**, select **API permissions**.
3. Select the **Microsoft APIs** tab, then under **Commonly used Microsoft APIs**, select **Microsoft Graph**.
4. Select **Delegated permissions**, then search for, and select **User.ReadWrite** from the list of permissions.
5. Select the **Add permissions** button.
6. You've assigned the *User.ReadWrite* permissions correctly to your EditProfileService app. However, since the tenant is an external tenant, the customer users themselves can't consent to these permissions. As the administrator of the tenant, you must consent to this permission on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both scopes.

## Grant API permissions to the client web app

In this section, you grant API permissions to the client web app that you registered earlier (in prerequisites).

Grant your client web app the *EditProfileService.ReadWrite* permission. This permission is exposed by the EditProfileService app, and it protects the update profile operation with MFA. To grant the *EditProfileService.ReadWrite* permission to client web app, use the following steps:

1. From the **App registrations** page, select the API application that you created (such as *ciam-client-app*) to open its **Overview** page.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Select the **APIs my organization uses** tab.
5. In the list of APIs, select the API such as *edit-profile-service*.
6. Select **Delegated permissions** option.
7. From the permissions list, select **EditProfileService.ReadWrite**.
8. Select the **Add permissions** button.
9. From the **Configured permissions** list, select the **EditProfileService.ReadWrite** permission, then copy the permission's full URI for later use. The full permission URI looks something similar to `api://{clientId}/{EditProfileService.ReadWrite}`.
10. You've assigned the \**EditProfileService.ReadWrite* permissions correctly to your client web app. However, since the tenant is an external tenant, the customer users themselves can't consent to these permissions. As the administrator of the tenant, you must consent to this permission on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both scopes.

## Create Conditional Access MFA policy

Your EditProfileService app that you registered earlier is the resource that you protect with MFA.

To create an MFA Conditional Access (CA) policy, use the steps in [Add multifactor authentication to an app](../external-id/customers/how-to-multifactor-authentication-customers). Use the following settings when you create your policy:

- For the **Name**, use *MFA policy*.
- For the Target resources, select the EditProfileService app that you registered earlier, such as *edit-profile-service*.

## Clone or download sample web app

You already cloned the [sample app](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial) from the prerequisites, but if you've not already done so, you can either clone it from GitHub or download it as a `.zip` file.

[Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip) or clone the sample web app from GitHub by running the following command:

```Console
git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
```

## Configure the sample web app

This code sample contains two apps, the client web app and the API app (EditProfileService app). You need to update these apps to use your external tenant settings. To do so, use the following steps:

1. In your code editor, open `1-Authentication\7-edit-profile-with-mfa-express\App\authConfig.js` file, then find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the client web app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](/en-us/entra/external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).
    - `Enter_the_Client_Secret_Here` and replace it with the app secret value of the client web app you copied earlier.
    - `graph_end_point` and replace it with the Microsoft Graph API endpoint, that's `https://graph.microsoft.com/`.
    - `Add_your_protected_scope_here` and replace it with the API app (EditProfileService app) scope. The value looks similar to *api://{clientId}/EditProfileService.ReadWrite*. `{clientId}` is the Application (client) ID value of the *EditProfileService* you registered earlier.
2. In your code editor, open `1-Authentication\7-edit-profile-with-mfa-express\Api\authConfig.js` file, then find the placeholder:

    - `Enter_the_Tenant_Subdomain_Here` and replace it with Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).
    - `Enter_the_Tenant_ID_Here` and replace it with Tenant ID. If you don't have your Tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).
    - `Enter_the_Edit_Profile_Service_Application_Id_Here` and replace it with is the Application (client) ID value of the *EditProfileService* application.
    - `Enter_the_Client_Secret_Here` and replace it with the client secret value created as part of the prerequisites.
    - `graph_end_point` and replace it with the Microsoft Graph API endpoint, that's `https://graph.microsoft.com/`.

## Install project dependencies and run app

To test your app, install project dependencies for both the client app and the service/API app, then run them.

1. To run the client app, open your terminal window, then run the following commands:

    ```Console
    cd 1-Authentication\7-edit-profile-with-mfa-express\App
    npm install
    npm start
    ```
2. To run the edit service/API app, change directory to the edit service/API app, *1-Authentication\7-edit-profile-with-mfa-express\Api*, then run the following commands:

    ```Console
    npm install
    npm start
    ```
3. Open your browser, then go to http://localhost:3000. If you experience SSL certificate errors, create a `.env` file, then add the following configuration:

    ```Console
    # Use this variable only in the development environment. 
    # Remove the variable when you move the app to the production environment.
    NODE_TLS_REJECT_UNAUTHORIZED='0'
    ```
4. Select the **Sign In** button, then you sign in.
5. On the sign-in page, type your **Email address**, select **Next**, type your **Password**, then select **Sign in**. If you don't have an account, select **No account? Create one** link, which starts the sign-up flow.
6. To update profile, select the **Profile editing** link. You see a page similar to the following screenshot:

    ![Screenshot of user update profile.](media/how-to-web-app-node-edit-profile-update-profile/edit-user-profile.png)
7. To edit profile, select the **Edit Profile** button. If you haven't already done so, the app prompts you to complete an MFA challenge.
8. Make changes to any of the profile details, then select **Save** button.