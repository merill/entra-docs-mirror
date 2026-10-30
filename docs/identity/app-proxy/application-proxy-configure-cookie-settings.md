---
layout: Conceptual
title: Application proxy cookie settings - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-cookie-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Microsoft Entra ID uses access and session cookies to access on-premises applications through application proxy. This article explains how to use and configure the cookie settings.
ms.custom: no-azure-ad-ps-ref
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 02cd51a8-14fd-3c14-1975-db4a4d305269
document_version_independent_id: 5260e87d-d006-4c3d-e230-16b97cda028c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-cookie-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-cookie-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-cookie-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3aefd64e-84c1-7cf1-6a38-1e63eeea2494
---

# Application proxy cookie settings - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID uses access and session cookies to access on-premises applications through application proxy. Learn how to configure the application proxy cookie settings.

## What are the cookie settings?

[Application proxy](overview-what-is-app-proxy) uses the following access and session cookie settings.

| Cookie setting | Default | Description | Recommendations |
| --- | --- | --- | --- |
| Use HTTP-Only Cookie | **No** | **Yes** lets application proxy include the HTTPOnly flag in HTTP response headers. This flag provides extra security benefits, for example, it prevents client-side scripting (CSS) from copying or modifying the cookies.Before the HTTP-Only setting was available, application proxy encrypted and transmitted cookies over a secured Transport Layer Security (TLS) channel to protect against modification. | Use **Yes** because of the extra security benefits.Use **No** for clients or user agents that do require access to the session cookie. For example, use **No** for Remote Desktop Protocol (RDP) or Microsoft Terminal Services Client (MSTSC) that connects to a Remote Desktop Gateway server through application proxy. |
| Use Secure Cookie | **Yes** | **Yes** allows application proxy to include the Secure flag in HTTP response headers. Secure Cookies enhances security by transmitting cookies over a TLS secured channel such as HTTPS. TLS prevents cookie transmission in clear text. | Use **Yes** because of the extra security benefits. |
| Use Persistent Cookie | **No** | **Yes** allows application proxy to set its access cookies to not expire when the web browser is closed. The persistence lasts until the access token expires, or until the user manually deletes the persistent cookies. | Use **No** because of the security risk associated with keeping users authenticated.Use **Yes** only for older applications that can't share cookies between processes. It's better to update your application to handle sharing cookies between processes instead of using persistent cookies. For example, you might need persistent cookies to allow a user to open Office documents in explorer view from a SharePoint site. Without persistent cookies, this operation might fail if the access cookies aren't shared between the browser, the explorer process, and the Office process. |

## SameSite Cookies

Cookies that don't specify the [SameSite](https://web.dev/articles/samesite-cookies-explained) attribute are treated as if they're set to **SameSite=Lax**. The `SameSite` attribute declares how cookies should be restricted to a same-site context. When set to `Lax`, the cookie is only sent to same-site requests or top-level navigation. However, application proxy requires these cookies to be preserved in the third-party context to keep users signed in during their session. Due to the requirement, updates were made:

- Setting the **SameSite** attribute to **None** ensures application proxy session cookies are sent in the third-party context.
- Setting the **Use Secure Cookie** setting to use **Yes** as the default. Chrome rejects cookies that don't use the `Secure` flag. This default setting applies to all existing applications published through application proxy. Application proxy access cookies are set to Secure and only transmitted over HTTPS. This secure cookie default only applies to the session cookies.

Additionally, if your back-end application has cookies that need third-party context, you must explicitly opt in by changing your application to use `SameSite=None`. Application proxy translates the `Set-Cookie` header to its URLs and respects the settings.

## Set cookie settings with Microsoft Entra admin center

To set the cookie settings using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application proxy**.
3. Under **Additional Settings**, set the cookie setting to **Yes** or **No**.
4. Select **Save** to apply your changes.

## View current cookie settings with PowerShell

To see the current cookie settings for the application, use this PowerShell command: 

```powershell
Get-MgBetaApplication -ApplicationId <Id> | FL *
```

## Set cookie settings with PowerShell

In the following PowerShell commands, `<Id>` is the **Id** of the application.

**Http-Only Cookie**

```powershell
Set-EntraBetaApplicationProxyApplication -ApplicationId <Id> -IsHttpOnlyCookieEnabled $true 
Set-EntraBetaApplicationProxyApplication -ApplicationId <Id> -IsHttpOnlyCookieEnabled $false
```

**Secure Cookie**

```powershell
Set-EntraBetaApplicationProxyApplication -ApplicationId <Id> -IsSecureCookieEnabled $true 
Set-EntraBetaApplicationProxyApplication -ApplicationId <Id> -IsSecureCookieEnabled $false
```

**Persistent Cookies**

```powershell
Set-EntraBetaApplicationProxyApplication -ApplicationId <Id> -IsPersistentCookieEnabled $true 
Set-EntraBetaApplicationProxyApplication -ApplicationId <Id> -IsPersistentCookieEnabled $false
```