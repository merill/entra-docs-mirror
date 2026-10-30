---
layout: Conceptual
title: Translate links and URLs for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-hard-coded-link-translation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Translate hard-coded internal URLs in on-premises applications published through Microsoft Entra application proxy. Covers Edge integration, browser extensions, and link translation settings.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: ac477036-6a9b-d53a-f97a-ae6ab04aa08e
document_version_independent_id: 40652157-0c0a-24e7-5e16-ae7349a9f7de
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-hard-coded-link-translation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-hard-coded-link-translation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-hard-coded-link-translation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 44e114b2-ae6d-9e8f-1027-f79eb6f9af60
---

# Translate links and URLs for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra application proxy makes your on-premises apps available to users who are remote or on their own devices. Some apps, however, were developed with local links embedded in the HTML. These links don't work correctly when the app is used remotely. When you have several on-premises applications that point to each other, your users expect the links to keep working when they're not at the office.

The best way to make sure that links work the same both inside and outside of your corporate network is to configure the external URLs of your apps to be the same as their internal URLs. Use [custom domains](how-to-configure-custom-domain) to configure your external URLs to have your corporate domain name instead of the default application proxy domain.

If you can't use custom domains in your tenant, there are several other options for providing this functionality. All of the other options are also compatible with custom domains and each other, so you can configure custom domains and other solutions.

Note

Link translation isn't supported for hard-coded internal URLs generated through JavaScript.

**Option 1: Use Microsoft Edge** – This solution is only applicable if you plan to recommend or require that users access the application through the Microsoft Edge browser. It handles all published URLs.

**Option 2: Use the MyApps Extension** – This solution requires users to install a client-side browser extension, but it handles all published URLs and works with most popular browsers.

**Option 3: Use the link translation setting** – The option is an admin side setting that is invisible to users. However, it handles URLs only in HTML and CSS.

These three features keep your links working no matter where your users are. When you have apps that point directly to internal endpoints or ports, you can map these internal URLs to the published external application proxy URLs.

Note

The last option is only for tenants that, for whatever reason, can't use custom domains to have the same internal and external URLs for their apps. Before you enable this feature, see if [custom domains in Microsoft Entra application proxy](how-to-configure-custom-domain) can work for you.

Or, if the application you need to configure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](/en-us/SharePoint/administration/configure-alternate-access-mappings) for another approach to mapping links.

### Option 1: Microsoft Edge Integration

You can use Microsoft Edge to further protect your application and content. To use this solution, you need to require/recommend users access the application through Microsoft Edge. Microsoft Edge recognizes all internal URLs published with application proxy and redirects them to the corresponding external URL. The redirection ensures that hard coded internal URLs work. If a user goes to the browser and directly types the internal URL, it works even if the user is remote.

To learn more, including how to configure this option, see [Manage web access by using Microsoft Edge for iOS and Android with Microsoft Intune](/en-us/mem/intune/apps/manage-microsoft-edge) documentation.

### Option 2: MyApps Browser Extension

With the MyApps Browser Extension, all internal URLs published with application proxy recognize the extension and redirected to the corresponding external URL. The redirection ensures that all the hard coded internal URLs work. If a user goes to the browser address bar and directly types the internal URL, it works even if the user is remote.

To use this feature, the user needs to download the extension and be logged in. There's no other configuration needed for admins or the users.

To learn more, including how to configure this option, see the [MyApps Browser Extension](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510#download-and-install-the-my-apps-secure-sign-in-extension) documentation.

Note

The MyApps Browser Extension doesn't support link translation for wildcard URLs.

### Option 3: Link Translation Setting

The application proxy service searches through HTML and CSS for published internal links and translates them when link translation is enabled. Link translation provides an uninterrupted experience. Using the MyApps Browser Extension is preferred to the Link Translation Setting since it gives a more performant experience.

Note

If you're using option 2 or 3, only one of these settings should be enabled at a time.

## How link translation works

After authentication, when the proxy server passes the application data to the user, application proxy scans the application for hard-coded links and replaces them with their respective, published external URLs.

Application proxy assumes that applications are encoded in UTF-8. If that's not the case, specify the encoding type in an HTTP response header, like `Content-Type:text/html;charset=utf-8`.

### Which links are affected?

The link translation feature only looks for links that are in code tags in the body of an app. Application proxy has a separate feature for translating cookies or URLs in headers.

There are two common types of internal links in on-premises applications:

- **Relative internal links** that point to a shared resource in a local file structure like `/claims/claims.html`. These links automatically work in apps that are published through application proxy, and continue to work with or without link translation.
- **Hard-coded internal links** to other on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`. The link translation feature works on hard-coded internal links, and changes them to point to the external URLs that remote users need to go through.

The complete list of attributes in HTML code tags that application proxy supports link translation for include:

- `a (href)`
- `audio (src)`
- `base (href)`
- `button (formaction)`
- `div (data-background, style, data-src)`
- `embed (src)`
- `form (action)`
- `frame (src)`
- `head (profile)`
- `html (manifest)`
- `iframe (longdesc, src)`
- `img (longdesc, src)`
- `input (formaction, src, value)`
- `link (href)`
- `menuitem (icon)`
- `meta (content)`
- `object (archive, data, codebase)`
- `script (src)`
- `source (src)`
- `track (src)`
- `video (src, poster)`

Additionally, within CSS the URL attribute is also translated.

### How do apps link to each other?

Link translation is enabled for each application, so that you have control over the user experience at the per-app level. Turn on link translation for an app when you want the links *from* that app to be translated, not links *to* that app.

For example, suppose that you have three applications published through application proxy that all link to each other: Benefits, Expenses, and Travel. There's a fourth app, Feedback that isn't published through application proxy.

When you enable link translation for the Benefits app, the links to Expenses and Travel are redirected to the external URLs for those apps. However, the link to Feedback isn't redirected because there's no external URL. Links from Expenses and Travel back to Benefits don't work, because link translation isn't enabled for those two apps.

![Links from Benefits to other apps when link translation is enabled.](media/application-proxy-configure-hard-coded-link-translation/one_app.png)

### Which links aren't translated?

To improve performance and security, some links aren't translated:

- Links not inside of code tags.
- Links not in HTML or CSS.
- Links in URL-encoded format.
- Internal links opened from other programs. Links sent through email or instant message, or included in other documents, aren't translated. The users need to know to go to the external URL.

If you need to support one of these two scenarios, use the same internal and external URLs instead of link translation.

## Enable link translation

Getting started with link translation is as easy as clicking a button:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the app you want to manage.
4. Turn **Translate URLs in application body** to **Yes**.

    ![Application proxy settings page with Translate URLs in Application Body set to Yes.](media/application-proxy-configure-hard-coded-link-translation/select_yes.png)
5. Select **Save** to apply your changes.

Now, when your users access this application, the proxy scans for internal URLs that are published through application proxy on your tenant.