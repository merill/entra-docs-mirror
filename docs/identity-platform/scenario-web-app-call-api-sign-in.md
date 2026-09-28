---
layout: Conceptual
title: Remove accounts from the token cache on sign-out - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-web-app-call-api-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to remove accounts from the token cache during global sign-out in web apps that call web APIs using the Microsoft identity platform.
manager: pmwongera
ms.date: 2025-03-21T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
ms.custom: 
locale: en-us
document_id: 37376fe1-f1bd-276c-78c5-4a94119bab5e
document_version_independent_id: c0154eff-a6c1-5567-d7aa-7f92e052f168
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-web-app-call-api-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-web-app-call-api-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-web-app-call-api-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 3922a227-935c-68d2-5905-d11077b2a514
---

# Remove accounts from the token cache on sign-out - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Sign-out is different for a web app that calls web APIs. When the user signs out from your application, or from any application, you must remove the tokens associated with that user from the token cache. Refer to [Sign in users in a sample web app](quickstart-web-app-sign-in) for details on how to implement sign-in in a web app.

## Intercept the callback after single sign-out

To clear the token-cache entry associated with the account that signed out, your application can intercept the after `logout` event. Web apps store access tokens for each user in a token cache. By intercepting the after `logout` callback, your web application can remove the user from the cache.

# [ASP.NET Core](#tab/aspnetcore)
Microsoft.Identity.Web takes care of implementing sign-out for you. For details see [Microsoft.Identity.Web source code](https://github.com/AzureAD/microsoft-identity-web/blob/c29f1a7950b940208440bebf0bcb524a7d6bee22/src/Microsoft.Identity.Web/WebAppExtensions/WebAppCallsWebApiAuthenticationBuilderExtensions.cs#L168-L176)

# [ASP.NET](#tab/aspnet)
The ASP.NET sample doesn't remove accounts from the cache on global sign-out.

# [Java](#tab/java)
The Java sample doesn't remove accounts from the cache on global sign-out.

# [Node.js](#tab/nodejs)
The Node sample doesn't remove accounts from the cache on global sign-out.

# [Python](#tab/python)
The Python sample doesn't remove accounts from the cache on global sign-out.

---