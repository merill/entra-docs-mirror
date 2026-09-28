---
layout: Conceptual
title: Set up a Node.js web application for profile editing - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-web-app-node-edit-profile-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up your Node.js web application for profile editing with multifactor authentication protection in your external tenant
manager: dougeby
ms.topic: how-to
ms.date: 2025-03-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 8cc60cb2-d650-3cf5-8371-28619b2591fc
document_version_independent_id: 8cc60cb2-d650-3cf5-8371-28619b2591fc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-web-app-node-edit-profile-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-web-app-node-edit-profile-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-web-app-node-edit-profile-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 6effdc32-e415-d200-1412-50fc86ae1701
---

# Set up a Node.js web application for profile editing - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After customer users successfully sign in into your external-facing app, you can enable them to edit their profiles. You enable the customer users to manage their profiles by using [Microsoft Graph API's](/en-us/graph/api/user-get)`/me` endpoint. Calling the `/me` endpoint requires a signed-in user and therefore a delegated permission.

To make sure that only the user makes changes to their profile, the user needs to complete an MFA challenge.

In this guide, you learn how to set up your web app to support profile editing with multifactor authentication (MFA) protection:

- The app uses Conditional Access policy to enable MFA requirement.
- The web app setup contains two web services, the client web app and a middle-tier service app.
- The client web app signs in the user and reads and displays the user's profile.
- The middle-tier service app acquires an access token, then edits the profile on behalf of the user.

**Updatable properties**

To customize the fields your customer users can edit in their profile, choose from the properties listed in the *Update profile* row of the table in [Microsoft Graph APIs and permissions](../external-id/customers/reference-user-permissions#microsoft-graph-apis-and-permissions).

## Prerequisites

- Complete the steps in [Tutorial: Set up your external tenant to sign in users in a Node.js web app](tutorial-web-app-node-sign-in-prepare-app) tutorial series. The tutorial shows you how to register an app in your external tenant, and build a web app that signs in users. We refer to this web application as the client web app
- Complete the steps in [Sign in users and edit profile in a sample Node.js web app](quickstart-web-app-node-sign-in-edit-profile). This article shows you how to set up your external tenant for profile editing.

## Update the client web app

Add the following files to your Node.js client we app (*App* directory):

- Create *views/gatedUpdateProfile.hbs* and *views/updateProfile.hbs*.
- Create *fetch.js*.

### Update app UI components

1. In your code editor, open *App/views/index.hbs* file, then add an **Edit profile** link by using the following code snippet:

    ```html
    <a href="/users/gatedUpdateProfile">Edit profile</a>
    ```

    After you make the update, your *App/views/index.hbs* file should look similar to the following file:

    ```html
    <h1>{{title}}</h1>
    {{#if isAuthenticated }}
    <p>Hi {{username}}!</p>
    <a href="/users/id">View ID token claims</a>
    <br>
    <a href="/users/gatedUpdateProfile">Profile editing</a>
    <br>
    <a href="/auth/signout">Sign out</a>
    {{else}}
    <p>Welcome to {{title}}</p>
    <a href="/auth/signin">Sign in</a>
    {{/if}}
    ```
2. In your code editor, open *App/views/gatedUpdateProfile.hbs* file, then add the following code:

    ```html
    <h1>Microsoft Graph API</h1>
    <h3>/me endpoint response</h3>
    <div style="display: flex; justify-content: left;">
        <div style="size: 400px;">
            <label>Id :</label>
            <label> {{profile.id}}</label>
            <br />
            <label for="email">Email :</label>
            <label> {{profile.mail}}</label>
            <br />
            <label for="userName">Display Name :</label>
            <label> {{profile.displayName}}</label>
            <br />
            <label for="userName">Given Name :</label>
            <label> {{profile.givenName}}</label>
            <br />    
            <label for="userSurname">Surname :</label>
            <label> {{profile.surname}}</label>
            <br />
        </div>
        <div>
            <br />
            <br />
            <a href="/users/updateProfile">
                <button>Edit Profile</button>
            </a>
        </div>
    </div>
    <br />
    <br />
    <a href="/">Go back</a>
    ```

    - This file contains an HTML form that represents the [editable user details](../external-id/customers/reference-user-permissions#microsoft-graph-apis-and-permissions).
    - The user needs to select the **Edit Profile** button to update their display name, but the user must complete an MFA challenge if they've not already done so.
3. In your code editor, open *App/views/updateProfile.hbs* file, then add the following code:

    ```html
    <h1>Microsoft Graph API</h1>
    <h3>/me endpoint response</h3>
    <div style="display: flex; justify-content: left;">
        <div style="size: 400px;">
            <form id="userInfoForm" action="/users/update" method="POST">
                <label>Id :</label>
                <label> {{profile.id}}</label>
                <br />
                <label>Email :</label>
                <label> {{profile.mail}}</label>
                <br />
                <label for="userName">Display Name :</label>
                <input
                    type="text"
                    id="displayName"
                    name="displayName"
                    value="{{profile.displayName}}"
                />
                <br />
                <label for="userName">Given Name :</label>
                <input
                    type="text"
                    id="givenName"
                    name="givenName"
                    value="{{profile.givenName}}"
                />
                <br />    
                <label for="userSurname">Surname :</label>
                <input
                    type="text"
                    id="surname"
                    name="surname"
                    value="{{profile.surname}}"
                />
                <br />    
                <button type="submit" id="button">Save</button>
            </form>
        </div>
        <br />
    </div>
    <a href="/">Go back</a>
    ```

This file contains an HTML form that represents the [editable user details](../external-id/customers/reference-user-permissions#microsoft-graph-apis-and-permissions), but only visible after the customer user completes MFA challenge.

### Install app dependencies

In your terminal, install more Node packages, `axios`, `cookie-parser`, `body-parser`, `method-override`, by running the following command:

```console
npm install axios cookie-parser body-parser method-override 
```

## Set up the mid-tier app

In this section, you set up the mid-tier app.

1. Create *API* directory.
2. To create your mid-tier app project, navigate into the *API* directory, then run the following command:

    ```console
    npm init -y
    ```
3. In the *API* directory, create new files, *authConfig.js*, *fetch.js* and *index.js*.
4. To install mid-tier app dependencies, run the following command:

```console
npm install express express-session axios cookie-parser http-errors @azure/msal-node body-parser uuid 
```