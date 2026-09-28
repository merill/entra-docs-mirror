---
layout: Conceptual
title: 'Tutorial: Sign-in users to a Python Flask web app by using Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-web-app-python-flask-sign-in-out
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to sign-in users to a Python Flask web app by using Microsoft identity platform
manager: pmwongera
ms.topic: tutorial
ms.date: 2025-02-24T00:00:00.0000000Z
locale: en-us
document_id: c4fa4afc-aaa9-ce31-1988-e38b7bd5860e
document_version_independent_id: c4fa4afc-aaa9-ce31-1988-e38b7bd5860e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-web-app-python-flask-sign-in-out.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-web-app-python-flask-sign-in-out
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-web-app-python-flask-sign-in-out.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 34e61151-1cbe-efd5-1879-88330073fd7e
---

# Tutorial: Sign-in users to a Python Flask web app by using Microsoft identity platform - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial guides you on securing a Python Flask Web app.

In this tutorial, you:

- Create a Python Flask project
- Install the required dependencies
- Configure your Flask web app to use Microsoft identity platform for authentication
- Test the sign-in and sign-out experience in your Flask web app

## Prerequisites

# [Workforce tenant](#tab/workforce-tenant)
- A workforce tenant. You can use your [Default Directory](quickstart-create-new-tenant) or set up a new tenant.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add a client secret to your app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).

# [External tenant](#tab/external-tenant)
- Ensure you have [an app registration](quickstart-register-app) in your tenant. Make sure you have the following from your app registration details:
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add a client secret to your app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).
- Extract the *Directory (tenant) subdomain* where you registered your web app. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
- Associate your app with a user flow in the Microsoft Entra admin center. This user flow can be used across multiple applications. For more information, see [Create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers) and [Add your application to the user flow](../external-id/customers/how-to-user-flow-add-application).

---

- [Python 3+](https://www.python.org/).
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

## Create a Flask project

1. Create a folder to host your Flask application, such as *flask-web-app*.
2. Open a console window, and change to the directory to your Flask web app folder using the command

    ```bash
    cd flask-web-app
    ```
3. Set up virtual environment

    Depending on your operating system, run the following commands to set up your virtual environment and activate it:

    For windows operating system:

    ```bash
    py -m venv .venv
    .venv\scripts\activate
    ```

    For macOS or Linux operating system:

    ```Bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```

## Install app dependencies

To install app dependencies, run the following commands:

```console
pip install flask
pip install python-dotenv
pip install requests
pip install "ms_identity_python[flask] @ git+https://github.com/azure-samples/ms-identity-python@0.9"
```

The *ms\_identity\_python* library that you install automatically installs Microsoft Authentication Library (MSAL) for Python as its dependency. MSAL Python is the library that enables you to authenticate users and manage their access tokens.

After installing the required libraries, update your requirements file by running the following command:

```console
pip freeze > requirements.txt
```

## Configure the application for authentication

Web applications that sign in users by using the Microsoft identity platform are configured through a configuration file, *.env*. In Python Flask, it must specify the following values:

# [Workforce tenant](#tab/workforce-tenant)
| Environment variable | Description |
| --- | --- |
| `AUTHORITY` | The URL of the cloud instance where the application is registered. Format: `https://{Instance}/{TenantId}`. Use one of the following Instance values:- `https://login.microsoftonline.com/` (Azure public cloud)- `https://login.microsoftonline.us/` (Azure US government)- `https://login.microsoftonline.de/` (Microsoft Entra Germany)- `https://login.partner.microsoftonline.cn/` (Microsoft Entra China, operated by 21Vianet) |
| `TENANT_ID` | The identifier of the tenant where the app is registered. Prefer the tenant ID from the app registration, or use one of:- `organizations`: sign in users in any work or school account- `common`: sign in users with any work or school account or Microsoft personal account- `consumers`: sign in users with a Microsoft personal account only |
| `CLIENT_ID` | Identifier of the application (client) as obtained from the app registration. |
| `CLIENT_SECRET` | The secret value obtained from [add credentials](how-to-add-credentials) in the Microsoft Entra admin center. |
| `REDIRECT_URI` | The URI where the Microsoft identity platform sends security tokens after authentication. |

# [External tenant](#tab/external-tenant)
| Environment variable | Description |
| --- | --- |
| `AUTHORITY` | The URL of the external tenant where the application is registered. Format: `https://<tenant_subdomain>.ciamlogin.com/` (or `https://<tenant_subdomain>.onmicrosoft.com/`). See [Create an external tenant](/en-us/entra/external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details) to obtain your tenant subdomain. |
| `CLIENT_ID` | Identifier of the application (client) from the app registration. |
| `CLIENT_SECRET` | The client secret value obtained from [add credentials](how-to-add-credentials) in the Microsoft Entra admin center. |
| `REDIRECT_URI` | The URI where the Microsoft identity platform sends security tokens after authentication. |

---

### Update the configuration file

1. Create a *.env* file in your root folder to safely store your app's configuration. Your *.env* file should contain the following environment variables:

# [Workforce tenant](#tab/workforce-tenant)
```env
    CLIENT_ID="<Enter_your_client_id>"
    CLIENT_SECRET="<Enter_your_client_secret>"
    AUTHORITY="https://login.microsoftonline.com/<Enter_tenant_id>"
    REDIRECT_URI="<Enter_redirect_uri>"
    ```

Replace the placeholders with the following values:

    - Replace `<Enter_your_client_id>` with the *Application (client) ID* of the client web app that you registered.
    - Replace `<Enter_tenant_id>` with the *Directory (Tenant) ID* where you registered your web app.
    - Replace `<Enter_your_client_secret>` with the *Client secret* value for the web app you created. In this tutorial, we use secrets for demonstration purposes. In production, use more secure approaches such as [certificates or federated identity credentials](how-to-add-credentials).
    - Replace `<Enter_redirect_uri>` with the redirect URI that you registered earlier. This tutorial sets the redirect URI path to `http://localhost:3000/getAToken`.

# [External tenant](#tab/external-tenant)
```env
    CLIENT_ID="<Enter_your_client_id>"
    CLIENT_SECRET="<Enter_your_client_secret>"
    AUTHORITY=https://<Enter_your_subdomain>.ciamlogin.com/<Enter_your_subdomain>.onmicrosoft.com
    REDIRECT_URI="<Enter_redirect_uri>"
    ```

Replace the placeholders with the following values:

    - Replace `<Enter_your_client_id>` with the *Application (client) ID* of the client web app that you registered.
    - Replace `<Enter_your_subdomain>` with the *Directory (tenant) subdomain* where you registered your web app.
    - Replace `<Enter_your_client_secret>` with the *Client secret* value for the web app you created. In this tutorial, we use secrets for demonstration purposes. In production, use more secure approaches such as [certificates or federated identity credentials](how-to-add-credentials).
    - Replace `<Enter_redirect_uri>` with the redirect URI that you registered earlier. This tutorial sets the redirect URI path to `http://localhost:3000/getAToken`.

---
2. Create an *app\_config.py* file to read the environment variables and add other configs that you need.

    ```python
    import os
    
    AUTHORITY = os.getenv("AUTHORITY")
    CLIENT_ID = os.getenv("CLIENT_ID")
    CLIENT_SECRET = os.getenv("CLIENT_SECRET")
    REDIRECT_URI = os.getenv("REDIRECT_URI")
    SESSION_TYPE = "filesystem" # Tells the Flask-session extension to store sessions in the filesystem. Don't use in production apps.
    ```

## Configure app endpoints

At this stage, you create your web app endpoints and add the business logic to your application.

1. Create a file called *app.py* in your root folder.
2. Import required dependencies at the top of the *app.py* file.

    ```python
    import os
    import requests
    from flask import Flask, render_template
    from identity.flask import Auth
    import app_config
    ```
3. Initialize your Flask app and configure it to use the session storage type you specified in your *app\_config.py* file.

    ```python
    app = Flask(__name__)
    app.config.from_object(app_config)
    ```
4. Initialize client the app client. A Flask web app is a confidential client. We pass the client secret because confidential clients can safely store it. Under the hood, the identity library calls the `ConfidentialClientApplication` class of the MSAL library.

    ```python
    auth = Auth(
        app,
        authority=app.config["AUTHORITY"],
        client_id=app.config["CLIENT_ID"],
        client_credential=app.config["CLIENT_SECRET"],
        redirect_uri=app.config["REDIRECT_URI"]
    )
    ```
5. Add the required endpoints to your Flask app. The web app uses the authorization code flow to sign in the user. The *ms\_identity\_python* MSAL wrapper library helps with interacting with the MSAL library hence making it easier to add sign in and sign out to your app. We add an index page and protect it using the `login_required` decorator provided by the *ms\_identity\_python* library. The `login_required` decorator ensures that only authenticated users can access the index page.

    ```python
    @app.route("/")
    @auth.login_required
    def index(*, context):
        return render_template(
            'index.html',
            user=context['user'],
            title="Flask Web App Sample",
        )
    ```

    User is guaranteed to be present because we decorated this view with `@login_required`.

## Create the app templates

Create a folder called *templates* in your root folder. In the templates folder, create a file called *index.html*. This is the app's homepage. Add the following code to the *index.html* file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
</head>
<body>
    <h1>{{ title }}</h1>
    <h2>Welcome {{ user.get("name") }}!</h2>

    <img src="https://github.com/Azure-Samples/ms-identity-python-webapp-django/raw/main/static/topology.png" alt="Topology">

    <ul>
    {% if api_endpoint %}
        <!-- If an API endpoint is declared and scopes defined, this link will show. We set this in the call an API tutorial. For this tutorial, we do not define this endpoint. -->
        <li><a href='/call_api'>Call an API</a></li>
    {% endif %}

    <li><a href="{{ url_for('identity.logout') }}">Logout</a></li>
    </ul>

    <hr>
    <footer style="text-align: right">{{ title }}</footer>
</body>
</html>
```

## Run and test the sample web app

# [Workforce tenant](#tab/workforce-tenant)
1. In your terminal, run the following command:

    ```console
    python3 -m flask run --debug --host=localhost --port=3000
    ```

    You can use the port of your choice. This port should be similar to the port of the redirect URI you registered earlier.
2. Open your browser, then go to `http://localhost:3000`. You see a sign-in page.
3. Sign in with your Microsoft account by following the steps. You're requested to provide an email address and password to sign in.
4. If there are any scopes needed by the application, a consent screen is presented. The application requests permission to maintain access to data you allow access to and to sign you in. Select **Accept**. This screen doesn't appear if no scopes are defined.

# [External tenant](#tab/external-tenant)
1. In your terminal, run the following command:

    ```console
    python3 -m flask run --debug --host=localhost --port=3000
    ```

    You can use the port of your choice. This port should be similar to the port of the redirect URI you registered earlier.
2. Open your browser, then go to `http://localhost:3000`. You see a sign-in page.
3. On the sign-in page, type your **Email address**, select **Next**, type your **Password**, then select **Sign in**. If you don't have an account, select **No account? Create one** link, which starts the sign-up flow.
4. If you choose the sign-up option, you go through the sign-up flow. To complete the whole sign-up flow, fill in your email, one-time passcode, new password and more account details.
5. If there are any scopes needed by the application, a consent screen is presented. The application requests permission to maintain access to data you allow access to, and to sign you in and then read your profile, as shown in the screenshot. Select **Accept**.

---

After you sign in or sign up, you're redirected back to the web app. You see a page that looks similar to the following screenshot:

![Screenshot of flask web app sample after successful authentication.](media/tutorial-web-app-python-flask-sign-in-out/flask-home-page.png)

Select **Logout** to sign out of the app. You're prompted to pick an account to sign out from. Select the account you used to sign in.

## Use custom URL domain (Optional)

# [Workforce tenant](#tab/workforce-tenant)
Workforce tenants don't support custom URL domains.

# [External tenant](#tab/external-tenant)
Use a custom URL domain to fully brand the authentication URL. From a user perspective, users remain on your domain during the authentication process, rather than being redirected to *ciamlogin.com* domain name.

Use the following steps to use a custom URL domain:

1. Use the steps in [Enable custom URL domains for apps in external tenants](../external-id/customers/how-to-custom-url-domain) to enable custom URL domain for your external tenant.
2. In your *.env* file, add the variable `OIDC_AUTHORITY` variable and delete the `AUTHORITY` variable. Set its value to *https://Enter\_the\_Custom\_Domain\_Here/Enter\_the\_Tenant\_ID\_Here/v2.0*. Replace `Enter_the_Custom_Domain_Here` with your custom URL domain and `Enter_the_Tenant_ID_Here` with your tenant ID. If you don't have your tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
3. In your app\_config.py file, add the following code to read the `OIDC_AUTHORITY` environment variable. You can delete the `AUTHORITY` variable.

    ```python
    # other configs go here
    OIDC_AUTHORITY = os.getenv("OIDC_AUTHORITY")
    ```
4. In your *app.py* file, update the auth object to use *oidc\_authority* argument instead of *authority*.

    ```python
    auth = Auth(
        app,
        oidc_authority=app.config["OIDC_AUTHORITY"],
        client_id=app.config["CLIENT_ID"],
        client_credential=app.config["CLIENT_SECRET"],
        redirect_uri=app.config["REDIRECT_URI"]
    )
    ```

## Reference material

The [ms_identity_python](https://github.com/azure-samples/ms-identity-python) abstracts the details of the MSAL library. For more information, see [MSAL Python documentation](/en-us/entra/msal/python/). This reference material helps you understand how you initialize an app and acquire tokens using MSAL Python.

---