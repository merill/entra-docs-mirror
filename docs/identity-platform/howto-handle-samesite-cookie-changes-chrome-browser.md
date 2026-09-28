---
layout: Conceptual
title: How to handle SameSite cookie changes in Chrome browser - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-handle-samesite-cookie-changes-chrome-browser
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to handle SameSite cookie changes in Chrome browser.
manager: pmwongera
ms.custom: 
ms.date: 2024-02-09T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: how-to
locale: en-us
document_id: f1c4f43c-843e-c1da-9e7e-af1eeccb9abd
document_version_independent_id: fed9d3c7-d831-2a38-149e-a9b5c69ec62f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-handle-samesite-cookie-changes-chrome-browser.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-handle-samesite-cookie-changes-chrome-browser
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-handle-samesite-cookie-changes-chrome-browser.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: a8376356-81c5-474c-2207-3de145864371
---

# How to handle SameSite cookie changes in Chrome browser - Microsoft identity platform | Microsoft Learn

## What is SameSite?

`SameSite` is a property that can be set in HTTP cookies to prevent Cross Site Request Forgery(CSRF) attacks in web applications:

- When `SameSite` is set to **Lax**, the cookie is sent in requests within the same site and in GET requests from other sites. It isn't sent in GET requests that are cross-domain.
- A value of **Strict** ensures that the cookie is sent in requests only within the same site.

By default, the `SameSite` value is NOT set in browsers and that's why there are no restrictions on cookies being sent in requests. An application would need to opt-in to the CSRF protection by setting **Lax** or **Strict** per their requirements.

## SameSite changes and impact on authentication

Recent [updates to the standards on SameSite](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) propose protecting apps by making the default behavior of `SameSite` when no value is set to Lax. This mitigation means cookies will be restricted on HTTP requests except GET made from other sites. Additionally, a value of **None** is introduced to remove restrictions on cookies being sent. These updates will soon be released in an upcoming version of the Chrome browser.

When web apps authenticate with the Microsoft identity platform using the response mode "form\_post", the login server responds to the application using an HTTP POST to send the tokens or auth code. Because this request is a cross-domain request (from `login.microsoftonline.com` to your domain - for instance `https://contoso.com/auth`), cookies that were set by your app now fall under the new rules in Chrome. The cookies that need to be used in cross-site scenarios are cookies that hold the *state* and *nonce* values, that are also sent in the login request. There are other cookies dropped by Microsoft Entra ID to hold the session.

If you don't update your web apps, this new behavior will result in authentication failures.

## Mitigation and samples

To overcome the authentication failures, web apps authenticating with the Microsoft identity platform can set the `SameSite` property to `None` for cookies that are used in cross-domain scenarios when running on the Chrome browser. Other browsers (see [here](https://www.chromium.org/updates/same-site/incompatible-clients) for a complete list) follow the previous behavior of `SameSite` and won't include the cookies if `SameSite=None` is set. That's why, to support authentication on multiple browsers web apps will have to set the `SameSite` value to `None` only on Chrome and leave the value empty on other browsers.

This approach is demonstrated in the following sample code.

# [.NET](#tab/dotnet)
The following table presents the pull requests that worked around the SameSite changes in our ASP.NET and ASP.NET Core samples.

| Sample | Pull request |
| --- | --- |
| [ASP.NET Core web app incremental tutorial](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2) | [Same site cookie fix #261](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/pull/261) |
| [ASP.NET MVC web app sample](https://github.com/Azure-Samples/ms-identity-aspnet-webapp-openidconnect) | [Same site cookie fix #35](https://github.com/Azure-Samples/ms-identity-aspnet-webapp-openidconnect/pull/35) |
| [active-directory-dotnet-admin-restricted-scopes-v2](https://github.com/azure-samples/active-directory-dotnet-admin-restricted-scopes-v2) | [Same site cookie fix #28](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2/pull/28) |

For details on how to handle SameSite cookies in ASP.NET and ASP.NET Core, see also:

- [Work with SameSite cookies in ASP.NET Core](/en-us/aspnet/core/security/samesite) .
- [ASP.NET Blog on SameSite issue](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)

# [Python](#tab/python)
| Sample |
| --- |
| [ms-identity-python-webapp](https://github.com/Azure-Samples/ms-identity-python-webapp) |

# [Java](#tab/java)
| Sample | Pull request |
| --- | --- |
| [ms-identity-java-webapp](https://github.com/Azure-Samples/ms-identity-java-webapp) | [Same site cookie fix #24](https://github.com/Azure-Samples/ms-identity-java-webapp/pull/24) |
| [ms-identity-java-webapi](https://github.com/Azure-Samples/ms-identity-java-webapi) | [Same site cookie fix #4](https://github.com/Azure-Samples/ms-identity-java-webapi/pull/4) |

---