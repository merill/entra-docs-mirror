---
layout: Conceptual
title: Embedded native authentication web fallback overview - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication-web-fallback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Understand unsupported native interactions, separate browser sign-in, and the boundaries between restarting and resuming authentication.
ms.topic: concept-article
ms.date: 2026-11-13T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: b90c1737-f4e4-678c-5d39-48787d3d9b8a
document_version_independent_id: b90c1737-f4e4-678c-5d39-48787d3d9b8a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication-web-fallback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication-web-fallback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication-web-fallback.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: ad613520-1214-69f0-18d3-51891905be7c
---

# Embedded native authentication web fallback overview - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

**Authentication approach:** Embedded native authentication.

An Embedded native authentication interaction can require behavior that your app can't complete natively. Browser fallback is a recovery path that starts a separate, configured browser sign-in. It doesn't resume the native transaction.

Important

The Native Authentication API V2 is in preview. The [Native Authentication API V1](reference-native-authentication-api-v1) remains generally available. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

## Service-required and client-initiated fallback

The API uses states, actions, and links to describe the next interaction. A client can present available actions or apply application flow logic to select an allowed operation.

The Native Authentication API can return the following response:

```json
{
    "state": "redirect"
}
```

This response can contain only `state`. It doesn't supply a continuation token or a browser handoff URL. Stop the native transaction instead of requiring `action`, `continuationToken`, or `_links` on this response.

At the OAuth boundary, browser-required handling can instead use `invalid_grant` with `web_redirect_required`. Handle that OAuth error separately from native JSON states.

A client can also reach a response it can't safely process: an unknown required action, a missing required field, an unsupported credential interaction, or malformed data. Offer a separately configured browser sign-in if your app has one, or show a clear failure without marking the user signed in.

Unknown optional properties or links are different. Ignore those additions while processing the required fields; their presence alone doesn't require a switch to the browser.

## Transaction and user-experience boundaries

A separate browser sign-in restarts authentication; it doesn't preserve native progress.

Native continuation tokens belong to the active transaction and current operation. They aren't general-purpose browser sign-in tokens. Don't add passwords, one-time passcodes (OTPs), native continuation tokens, or security tokens to browser URLs. Let the configured authorization flow handle its registered redirect. Keep authorization codes and other credentials out of logs and telemetry. Use the configured interactive authorization flow, not an arbitrary URL supplied by untrusted content.

The browser flow can have different interactions from the native flow. Don't mark the app signed in until its configured authentication integration reports success. If the user cancels or the browser flow fails, retain a clear signed-out or incomplete state.

## Browser integration

Use a supported browser-delegated integration to open the browser and handle its registered redirect. The [mobile quickstart](quickstart-mobile-app-sign-in?pivots=external) and [single-page app quickstart](quickstart-single-page-app-sign-in?pivots=external) describe those integration paths. Keep browser completion, cancellation, and error handling separate from native transaction processing.

For an application configured with Bring Your Own UX (BYO UX), normal browser authorization uses the configured self-hosted page. A native `redirect` response isn't a URL or parameter for bypassing that configuration to Microsoft-hosted pages. Use the configured browser authorization flow rather than a constructed bypass URL.

If your app doesn't have a supported browser path, explain that the interaction can't be completed. Don't automatically replay credentials or switch the active transaction to V1.

## V1 fallback

V1 clients need to support web fallback. The client declares its supported interactions through challenge types. For example, an email-with-password user flow requires both `oob` and `password`; omitting either can cause the service to require browser authentication. See [V1 challenge types](reference-native-authentication-api-v1#v1-challenge-types-and-capabilities).

For existing SDK integrations, use the [SDK library references](reference-native-authentication-api-v1#sdk-references) for fallback interfaces. V1 fallback starts a separate browser sign-in, not a resumable native-to-browser continuation.