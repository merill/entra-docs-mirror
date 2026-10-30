---
layout: Conceptual
title: Create a Node.js web app that calls a web API - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-web-app-node-sign-in-call-api-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to prepare your Node.js client web app to call a protected API using access tokens from Microsoft Entra External ID.
manager: dougeby
ms.topic: how-to
ms.date: 2025-03-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 33c67f67-0747-4cbb-61eb-57495acd3c06
document_version_independent_id: 33c67f67-0747-4cbb-61eb-57495acd3c06
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-web-app-node-sign-in-call-api-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-web-app-node-sign-in-call-api-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-web-app-node-sign-in-call-api-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: a8e1ed1a-8bc0-032e-ed96-45152636a742
---

# Create a Node.js web app that calls a web API - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this article, you prepare the app project you created in [Tutorial: Prepare your external tenant to sign in users in a Node.js web app](tutorial-web-app-node-sign-in-prepare-app) to call a web API. This article is the second part of a four-part guide series.

## Prerequisites

- Complete the steps in the first part of this guide series, [Prepare external tenant to call an API in a Node.js web application](how-to-web-app-node-sign-in-call-api-prepare-tenant).

## Update project files

Create more files, *fetch.js*, *todolistController.js*, *todos.js*, *todos.hbs* and *.env*, then organize them to achieve the following project structure:

```powershell
    ciam-sign-in-call-api-node-express-web-app/
    ├── .env
    └── server.js
    └── app.js
    └── authConfig.js
    └── fetch.js
    └── package.json
    └── auth/
        └── AuthProvider.js
    └── controller/
        └── authController.js
        └── todolistController.js
    └── routes/
        └── auth.js
        └── index.js
        └── todos.js
        └── users.js
    └── views/
        └── layouts.hbs
        └── error.hbs
        └── id.hbs
        └── index.hbs   
        └── todos.hbs 
    └── public/stylesheets/
        └── style.css
```

## Install app dependencies

In your terminal, install more Node packages, `axios`, `cookie-parser`, `body-parser`, `method-override`, by running the following command:

```console
    npm install axios cookie-parser body-parser method-override 
```

### Update app UI components

1. In your code editor, open *views/index.hbs* file, then add a *View your todolist* link:

    ```html
        <a href="/todos">View your todolist</a>
    ```

    Your *views/index.hbs* file now looks similar to the following file:

    ```html
        <h1>{{title}}</h1>
        {{#if isAuthenticated }}
        <p>Hi {{username}}!</p>
        <a href="/users/id">View your ID token claims</a>
        <br>
        <a href="/todos">View your todolist</a>
        <br>
        <a href="/auth/signout">Sign out</a>
        {{else}}
        <p>Welcome to {{title}}</p>
        <a href="/auth/signin">Sign in</a>
        {{/if}}
    ```

    We add a link to a UI that enables you interact with the *ciam-ToDoList-api*. We define the express route for this endpoint later in this guide.
2. In your code editor, open `views/todos.hbs` file, then add the following code:

    ```html
        <h1>Todolist</h1>
        <div>
            <form action="/todos" method="POST">
                <input type="text" name="description" class="form-control" placeholder="Enter a task" aria-label="Enter a task"
                    aria-describedby="button-addon">
                <button type="submit" id="button-addon">Add</button>
            </form>
        </div>
        <div class="row" style="margin: 10px;">
            <ol id="todoListItems" class="list-group"> 
                {{#each todos}} 
                <li class="todoListItem" id="todoListItem">
                    <span>{{description}}</span>
                    <form action='/todos?_method=DELETE' method='POST'>
                        <span><input type='hidden' name='_id' value='{{id}}'></span>
                        <span><button type='submit'>Remove</button></span>
                    </form>
                </li> 
                {{/each}} 
            </ol>
        </div>
        <a href="/">Go back</a>
    ```

    This view allows the user to perform tasks that initiate an API call. For instance, after a user signs in, and the app acquires an access token, the user can create a resource (task) in the API app by submitting a form.