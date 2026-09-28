---
layout: Conceptual
title: 'Quickstart: Add sign-in with Microsoft to a Python web app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/web-app-quickstart-portal-python
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, learn how a Python web app can sign in users, get an access token from the Microsoft identity platform, and call the Microsoft Graph API.
ROBOTS: NOINDEX
manager: dougeby
ms.custom: 
ms.date: 2023-12-19T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: 9123dbff-3f30-8191-8298-d15dd5f7c887
document_version_independent_id: f19e339f-ab20-ac0a-c88c-c3bdc33f1566
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/web-app-quickstart-portal-python.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/web-app-quickstart-portal-python
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/web-app-quickstart-portal-python.md
platformId: a6a82491-a378-ccd0-3685-3a7b0e805de3
---

# Quickstart: Add sign-in with Microsoft to a Python web app - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Add sign-in with Microsoft to a Python web app](quickstart-web-app-python-flask)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Add sign-in with Microsoft to a Python web app

In this quickstart, you download and run a code sample that demonstrates how a Python web application can sign in users and get an access token to call the Microsoft Graph API. Users with a personal Microsoft Account or an account in any Microsoft Entra organization can sign into the application.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Python 2.7+](https://www.python.org/downloads/release/python-2713/) or [Python 3+](https://www.python.org/downloads/release/python-364/)
- [Flask](https://flask.palletsprojects.com/en/stable/), [Flask-Session](https://pypi.org/project/Flask-Session/), [requests](https://github.com/psf/requests/graphs/contributors)
- [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python)

#### Step 1: Configure your application in Microsoft Entra admin center

For the code sample in this quickstart to work:

1. Add a reply URL as `http://localhost:5000/getAToken`.
2. Create a Client Secret.
3. Add Microsoft Graph API's User.ReadBasic.All delegated permission.

![Already configured](media/quickstart-v2-aspnet-webapp/green-check.png) Your application is configured with this attribute

#### Step 2: Download your project

Download the project and extract the zip file to a local folder closer to the root folder - for example, **C:\Azure-Samples**

Note

`Enter_the_Supported_Account_Info_Here`

#### Step 3: Run the code sample

1. You will need to install MSAL Python library, Flask framework, Flask-Sessions for server-side session management and requests using pip as follows:

    ```shell
    pip install -r requirements.txt
    ```
2. Run `app.py` from shell or command line:

    ```shell
    python app.py
    ```

    Important

    This quickstart application uses a client secret to identify itself as confidential client. Because the client secret is added as a plain-text to your project files, for security reasons, it is recommended that you use a certificate instead of a client secret before considering the application as production application. For more information on how to use a certificate, see [these instructions](certificate-credentials).

## More information

### Getting MSAL

MSAL is the library used to sign in users and request tokens used to access an API protected by the Microsoft identity platform. You can add MSAL Python to your application using Pip.

```Shell
pip install msal
```

### MSAL initialization

You can add the reference to MSAL Python by adding the following code to the top of the file where you will be using MSAL:

```Python
import msal
```

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).