---
layout: Conceptual
title: Xamarin Android system browser considerations (MSAL.NET) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-net-system-browser-android-considerations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about considerations for using system browsers on Xamarin Android with the Microsoft Authentication Library for .NET (MSAL.NET).
manager: pmwongera
ms.custom: 
ms.date: 2024-06-05T00:00:00.0000000Z
ms.reviewer: negoe
ms.topic: concept-article
locale: en-us
document_id: 950b9f9f-dd0e-47eb-cfe1-3035625a4ec7
document_version_independent_id: e1fe884d-d853-3a52-53ad-9be20eb7d8fb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-net-system-browser-android-considerations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-net-system-browser-android-considerations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-net-system-browser-android-considerations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0c462af-0ef9-4821-b36f-ba3d94736e2b
- https://authoring-docs-microsoft.poolparty.biz/devrel/caec7b7f-4941-4578-b79f-c63b1c1f5af4
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1209ac18-fe8e-4ac6-b056-073f0e2c78ab
- https://authoring-docs-microsoft.poolparty.biz/devrel/754dea88-f800-4835-b6b5-280cb5d81e88
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: d830eb25-99d0-46b4-3c9d-d51428656052
---

# Xamarin Android system browser considerations (MSAL.NET) - Microsoft identity platform | Microsoft Learn

This article discusses what you should consider when you use the system browser on Xamarin Android with the Microsoft Authentication Library for .NET (MSAL.NET).

Note

MSAL.NET versions 4.61.0 and above do not provide support for Universal Windows Platform (UWP), Xamarin Android, and Xamarin iOS. We recommend you migrate your Xamarin applications to modern frameworks like MAUI. Read more about the deprecation in [Announcing the Upcoming Deprecation of MSAL.NET for Xamarin and UWP](https://devblogs.microsoft.com/identity/uwp-xamarin-msal-net-deprecation/).

Starting with MSAL.NET 2.4.0 Preview, MSAL.NET supports browsers other than Chrome. It no longer requires Chrome be installed on the Android device for authentication.

We recommend that you use browsers that support custom tabs. Here are some examples of these browsers:

| Browsers that have custom tabs support | Package name |
| --- | --- |
| Chrome | com.android.chrome |
| Microsoft Edge | com.microsoft.emmx |
| Firefox | org.mozilla.firefox |
| Ecosia | com.ecosia.android |
| Kiwi | com.kiwibrowser.browser |
| Brave | com.brave.browser |

In addition to identifying browsers that offer custom tabs support, our testing indicates that a few browsers that don't support custom tabs also work for authentication. These browsers include Opera, Opera Mini, InBrowser, and Maxthon.

## Tested devices and browsers

The following table lists the devices and browsers that have been tested for authentication compatibility.

| Device | Browser | Result |
| --- | --- | --- |
| Huawei/One+ | Chrome\* | Pass |
| Huawei/One+ | Edge\* | Pass |
| Huawei/One+ | Firefox\* | Pass |
| Huawei/One+ | Brave\* | Pass |
| One+ | Ecosia\* | Pass |
| One+ | Kiwi\* | Pass |
| Huawei/One+ | Opera | Pass |
| Huawei | OperaMini | Pass |
| Huawei/One+ | InBrowser | Pass |
| One+ | Maxthon | Pass |
| Huawei/One+ | DuckDuckGo | User canceled authentication |
| Huawei/One+ | UC Browser | User canceled authentication |
| One+ | Dolphin | User canceled authentication |
| One+ | CM Browser | User canceled authentication |
| Huawei/One+ | None installed | AndroidActivityNotFound exception |

\* Supports custom tabs

## Known issues

If the user has no browser enabled on the device, MSAL.NET will throw an `AndroidActivityNotFound` exception.

- **Mitigation**: Ask the user to enable a browser on their device. Recommend a browser that supports custom tabs.

If authentication fails (for example, if authentication launches with DuckDuckGo), MSAL.NET will return `AuthenticationCanceled MsalClientException`.

- **Root problem**: A browser that supports custom tabs wasn't enabled on the device. Authentication launched with a browser that couldn't complete authentication.
- **Mitigation**: Ask the user to enable a browser on their device. Recommend a browser that supports custom tabs.