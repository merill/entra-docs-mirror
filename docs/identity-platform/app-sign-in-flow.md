---
layout: Conceptual
title: App sign-in flow with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/app-sign-in-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the sign-in flow of web, desktop, and mobile apps in Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2023-08-11T00:00:00.0000000Z
ms.reviewer: jmprieur, sureshja, ludwignick
ms.topic: concept-article
locale: en-us
document_id: 4a584d7a-899f-30bd-af7d-c6f71265dcc1
document_version_independent_id: 598b33f4-9ee8-8415-259b-a378aceb4dca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/app-sign-in-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/app-sign-in-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/app-sign-in-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4e40e8a1-5249-5470-088b-44a71fce4929
---

# App sign-in flow with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

This topic discusses the basic sign-in flow for web, desktop, and mobile apps using Microsoft identity platform. See [Authentication flows and app scenarios](authentication-flows-app-scenarios) to learn about sign-in scenarios supported by Microsoft identity platform.

## Web app sign-in flow

When a user navigates in the browser to a web app, the following happens:

- The web app determines whether the user is authenticated.
- If the user isn't authenticated, the web app delegates to Microsoft Entra ID to sign in the user. That sign in will be compliant with the policy of the organization, which may mean asking the user to enter their credentials, using [multi-factor authentication](../identity/authentication/concept-mfa-howitworks) (sometimes referred to as two-factor authentication or 2FA), or not using a password at all (for example using Windows Hello).
- The user is asked to consent to the access that the client app needs. This is why client apps need to be registered with Microsoft Entra ID, so that the Microsoft identity platform can deliver tokens representing the access that the user has consented to.

When the user has successfully authenticated:

- The Microsoft identity platform sends a token to the web app.
- A cookie is saved, associated with a Microsoft Entra domain, that contains the identity of the user in the browser's cookie jar. The next time an app uses the browser to navigate to the Microsoft identity platform authorization endpoint, the browser presents the cookie so that the user doesn't have to sign in again. This is also the way that SSO is achieved. The cookie is produced by Microsoft Entra ID and can only be understood by Microsoft Entra ID.
- The web app then validates the token. If the validation succeeds, the web app displays the protected page and saves a session cookie in the browser's cookie jar. When the user navigates to another page, the web app knows that the user is authenticated based on the session cookie.

The following sequence diagram summarizes this interaction:

![web app authentication process](media/authentication-scenarios/web-app-how-it-appears-to-be.png)

### How a web app determines if the user is authenticated

Web app developers can indicate whether all or only certain pages require authentication. For example, in ASP.NET/ASP.NET Core, this is done by adding the `[Authorize]` attribute to the controller actions.

This attribute causes ASP.NET to check for the presence of a session cookie containing the identity of the user. If a cookie isn't present, ASP.NET redirects authentication to the specified identity provider. If the identity provider is Microsoft Entra ID, the web app redirects authentication to `https://login.microsoftonline.com`, which displays a sign-in dialog.

### How a web app delegates sign-in to the Microsoft identity platform and obtains a token

User authentication happens via the browser. The OpenID protocol uses standard HTTP protocol messages.

- The web app sends an HTTP 302 (redirect) to the browser to use Microsoft identity platform.
- When the user is authenticated, the Microsoft identity platform sends the token to the web app by using a redirect through the browser.
- The redirect is provided by the web app in the form of a redirect URI. This redirect URI is registered with the Microsoft Entra application object. There can be several redirect URIs because the application may be deployed at several URLs. So the web app will also need to specify the redirect URI to use.
- Microsoft Entra ID verifies that the redirect URI sent by the web app is one of the registered redirect URIs for the app.

## Desktop and mobile app sign-in flow

The flow described above applies, with slight differences, to desktop and mobile applications.

Desktop and mobile applications can use an embedded Web control, or a system browser, for authentication. The following diagram shows how a Desktop or mobile app uses the Microsoft Authentication Library (MSAL) to acquire access tokens and call web APIs.

![Desktop app how it appears to be](media/authentication-scenarios/desktop-app-how-it-appears-to-be.png)

MSAL uses a browser to get tokens. As with web apps, authentication is delegated to Microsoft identity platform.

Because Microsoft Entra ID saves the same identity cookie in the browser as it does for web apps, if the native or mobile app uses the system browser it will immediately get SSO with the corresponding web app.

By default, MSAL uses the system browser. The exception is .NET Framework desktop applications where an embedded control is used to provide a more integrated user experience.