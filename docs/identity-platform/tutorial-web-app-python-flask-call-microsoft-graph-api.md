---
layout: Conceptual
title: 'Tutorial: Call Microsoft Graph API from a Python Flask web app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-web-app-python-flask-call-microsoft-graph-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Call Microsoft Graph API from a Python Flask web app
manager: pmwongera
ms.date: 2025-02-24T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: a84263dd-b504-c9c2-dd37-3e94c935ae49
document_version_independent_id: a84263dd-b504-c9c2-dd37-3e94c935ae49
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-web-app-python-flask-call-microsoft-graph-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-web-app-python-flask-call-microsoft-graph-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-web-app-python-flask-call-microsoft-graph-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 71a44b74-ede5-3c3c-4473-410acc5ea3d1
---

# Tutorial: Call Microsoft Graph API from a Python Flask web app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you call Microsoft Graph API from a Python Flask web app. In the [previous tutorial](tutorial-web-app-python-flask-sign-in-out), you added the sign-in and sign-out experiences to the application. Once a user signs in, the app acquires an access token to call Microsoft Graph API.

In this tutorial, you:

- Update an existing Python Flask web app to acquire an access token
- Use the access token to call Microsoft Graph API.

## Prerequisites

Complete the steps in [Tutorial: Add add sign-in to a Python Flask web app by using Microsoft identity platform](tutorial-web-app-node-sign-in-sign-out).

## Define scopes and API endpoint

In this example, we call the Microsoft Graph API to get the signed-in user's profile information. If your app is in a workforce tenant, on sign-in, the user consents to the scopes required by the app to access the Microsoft Graph API. If your app is in an external tenant, ensure you [grant admin consent on behalf of users in your tenant](quickstart-register-app#grant-admin-consent-external-tenants-only). The app then uses the access token to call the API and display the results.

In your *.env* file, add the endpoint we're calling and the scopes required to call the Microsoft Graph API:

```
SCOPE=User.Read
ENDPOINT=https://graph.microsoft.com/v1.0/me
```

Read the new configs in your app by updating the *app\_config.py* file.

```python
# other configs go here
SCOPE = os.getenv("SCOPE")
ENDPOINT = os.getenv("ENDPOINT")
```

## Call a protected API

1. Pass the API endpoint to the homepage. This enables you to call your endpoint. Update the `/` route to look like shown in the following code snippet:

    ```python
    @app.route("/")
    @auth.login_required
    def index(*, context):
        return render_template(
            'index.html',
            user=context['user'],
            title="Flask Web App Sample",
            api_endpoint=os.getenv("ENDPOINT") # added this line
        )
    ```
2. Call the protected Microsoft Graph API as shown in the following code snippet. We pass the list of scopes that our app needs to use. If scopes are present, the context contains an access token. The access token is used to call the downstream API. Add this code to the *app.py* file:

    ```python
    @app.route("/call_api")
    @auth.login_required(scopes=os.getenv("SCOPE", "").split())
    def call_downstream_api(*, context):
        api_result = requests.get(  # Use access token to call a web api
            os.getenv("ENDPOINT"),
            headers={'Authorization': 'Bearer ' + context['access_token']},
            timeout=30,
        ).json() if context.get('access_token') else "Did you forget to set the SCOPE environment variable?"
        return render_template('display.html', title="API Response", result=api_result)
    ```

    If the app successfully obtains an access token, it makes an HTTP request to the downstream API using the `requests.get(...)` method. In the request, our downstream API URL is specified in `app_config.ENDPOINT` and the access token passed in the `Authorization` field of the request header.

    A successful request to the downstream API (Microsoft Graph API) returns a JSON response stored in an `api_result` variable and passed to the `display.html` template for rendering.

## Display API results

Create a file called *display.html* in the *templates* folder. This page displays the result of the call to the Microsoft Graph endpoint. Add the following code to the *display.html* file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Microsoft Identity Python Web App: API</title>
</head>
<body>
    <a href="javascript:window.history.go(-1)">Back</a> <!-- Displayed on top of a potentially large JSON response, so it will remain visible -->
    <h1>{{title}}</h1>
    <pre>{{ result |tojson(indent=4) }}</pre> <!-- Just a generic json viewer -->
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

## Call API

1. Select the **Call an API** link on the home page. The app calls the Microsoft Graph API to get the signed-in user's profile information. The app displays the result of the call to the API.
2. Select **Logout** to sign out of the app. You're prompted to pick an account to sign out from. Select the account you used to sign in.

## Reference material

The [ms_identity_python](https://github.com/azure-samples/ms-identity-python) abstracts the details of the MSAL library. For more information, see [MSAL Python documentation](/en-us/entra/msal/python/). This reference material helps you understand how you initialize an app and acquire tokens using MSAL Python.