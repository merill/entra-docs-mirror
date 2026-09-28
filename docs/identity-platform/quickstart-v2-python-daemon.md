---
layout: Conceptual
title: 'Quickstart: Call Microsoft Graph from a Python daemon - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-v2-python-daemon
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how a Python process can get an access token and call an API protected by Microsoft identity platform, using the app's own identity
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2022-01-10T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: quickstart
locale: en-us
document_id: 537577a4-dbbe-a9e0-37e9-765adb7955d9
document_version_independent_id: 5d2e95b2-21e2-8aaa-8f77-6280772644c0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-v2-python-daemon.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-v2-python-daemon
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-v2-python-daemon.md
platformId: d93b21be-bd2a-1327-e695-920669a2c368
---

# Quickstart: Call Microsoft Graph from a Python daemon - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Acquire a token and call Microsoft Graph from a Python daemon app](quickstart-daemon-app-python-acquire-token)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

In this quickstart, you download and run a code sample that demonstrates how a Python application can get an access token using the app's identity to call the Microsoft Graph API and display a [list of users](/en-us/graph/api/user-list) in the directory. The code sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

## Prerequisites

To run this sample, you need:

- [Python 2.7+](https://www.python.org/downloads/release/python-2713) or [Python 3+](https://www.python.org/downloads/release/python-364/)
- [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python)

### Download and configure the quickstart app

#### Step 1: Configure your application in Azure portal

For the code sample in this quickstart to work, create a client secret and add Graph API's **User.Read.All** application permission.

![Already configured](media/quickstart-v2-netcore-daemon/green-check.png) Your application is configured with these attributes.

#### Step 2: Download the Python project

[Download the code sample](https://github.com/Azure-Samples/ms-identity-python-daemon/archive/master.zip)

Note

`Enter_the_Supported_Account_Info_Here`

##### Standard user

If you're a standard user of your tenant, ask a Global Administrator to grant admin consent for your application. To do this, give the following URL to your administrator:

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```

#### Step 4: Run the application

You'll need to install the dependencies of this sample once.

```console
pip install -r requirements.txt
```

Then, run the application via command prompt or console:

```console
python confidential_client_secret_sample.py parameters.json
```

You should see on the console output some Json fragment representing a list of users in your Microsoft Entra directory.

Important

This quickstart application uses a client secret to identify itself as confidential client. Because the client secret is added as a plain-text to your project files, for security reasons, it is recommended that you use a certificate instead of a client secret before considering the application as production application. For more information on how to use a certificate, see [these instructions](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/2-Call-MsGraph-WithCertificate/README.md) in the same GitHub repository for this sample, but in the second folder **2-Call-MsGraph-WithCertificate**.

## More information

### MSAL Python

[MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) is the library used to sign in users and request tokens used to access an API protected by Microsoft identity platform. As described, this quickstart requests tokens by using the application own identity instead of delegated permissions. The authentication flow used in this case is known as *[client credentials oauth flow](v2-oauth2-client-creds-grant-flow)*. For more information on how to use MSAL Python with daemon apps, see [this article](scenario-daemon-app-configuration).

You can install MSAL Python by running the following pip command.

```powershell
pip install msal
```

### MSAL initialization

You can add the reference for MSAL by adding the following code:

```Python
import msal
```

Then, initialize MSAL using the following code:

```Python
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential=config["secret"])
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `config["secret"]` | Is the client secret created for the application in Azure portal. |
> | `config["client_id"]` | Is the **Application (client) ID** for the application registered in the Azure portal. You can find this value in the app's **Overview** page in the Azure portal. |
> | `config["authority"]` | The STS endpoint for user to authenticate. Usually `https://login.microsoftonline.com/{tenant}` for public cloud, where {tenant} is the name of your tenant or your tenant Id. |
> 

For more information, please see the [reference documentation for `ConfidentialClientApplication`](https://msal-python.readthedocs.io/en/latest/#confidentialclientapplication).

### Requesting tokens

To request a token using app's identity, use `AcquireTokenForClient` method:

```Python
result = None
result = app.acquire_token_silent(config["scope"], account=None)

if not result:
    logging.info("No suitable token exists in cache. Let's get a new one from Azure AD.")
    result = app.acquire_token_for_client(scopes=config["scope"])
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `config["scope"]` | Contains the scopes requested. For confidential clients, this should use the format similar to `{Application ID URI}/.default` to indicate that the scopes being requested are the ones statically defined in the app object set in the Azure portal (for Microsoft Graph, `{Application ID URI}` points to `https://graph.microsoft.com`). For custom web APIs, `{Application ID URI}` is defined under the **Expose an API** section in **App registrations** in the Azure portal. |
> 

For more information, please see the [reference documentation for `AcquireTokenForClient`](https://msal-python.readthedocs.io/en/latest/#msal.ConfidentialClientApplication.acquire_token_for_client).

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).