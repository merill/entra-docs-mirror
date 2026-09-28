---
layout: Conceptual
title: Prepare apps for Microsoft Entra COOP policy - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-prepare-app-coop-enforcement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: AhmeMohamed
ms.author: ahmemohamed
ms.service: identity-platform
description: Learn how to make your app compatible with Microsoft Entra Cross-Origin-Opener-Policy and manage policy enforcement while you migrate.
manager: pmwongera
ms.topic: how-to
ms.custom: msecd-doc-authoring-1026
ms.date: 2026-09-24T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 7d60804e-8417-df06-0e4e-deb92770407b
document_version_independent_id: 7d60804e-8417-df06-0e4e-deb92770407b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-prepare-app-coop-enforcement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-prepare-app-coop-enforcement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-prepare-app-coop-enforcement.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: a576163f-96d2-3d76-65ca-d90638109c8a
---

# Prepare apps for Microsoft Entra COOP policy - Microsoft identity platform | Microsoft Learn

Cross-Origin-Opener-Policy (COOP) is a browser security rule that isolates a top-level document from cross-origin windows. This isolation prevents social engineering attacks in which a malicious page opens a legitimate application. After the application navigates to sign-in, the malicious page can hijack the sign-in flow and mislead the user about which application is being accessed.

This article helps you make your app compatible with Microsoft Entra COOP policy so that users can keep signing in without interruption. It's for developers whose apps use Microsoft Authentication Library for JavaScript (MSAL.js) popup methods or a similar SDK.

## How the COOP policy affects sign-in

Microsoft Entra COOP policy is a breaking change for new applications that depend on popup-based sign-in. Microsoft Entra disconnects popups from their openers. This change prevents a malicious page from opening a legitimate application and then hijacking its sign-in flow.

## Check the new app enforcement timeline

Microsoft Entra COOP policy applies to all Microsoft Entra web protocols on new apps created after January 31, 2027. If you create new applications, make sure they're compatible before January 31, 2027.

## Update the authentication method

The recommended fix is to become COOP-compatible by updating your authentication method to avoid parent-window messaging. If you use MSAL.js, upgrade to the latest supported version (v5). MSAL.js v5 uses COOP-compatible window communication.

For migration instructions, see [Migrate from MSAL Browser v4 to v5](/en-us/entra/msal/javascript/browser/v4-migration).

1. Update your MSAL.js package to the latest supported version (v5).
2. Test interactive sign-in to confirm that popups complete successfully with COOP enabled.

## Manage COOP policy enforcement

If you can't upgrade to MSAL.js v5 right away or use a different library, temporarily continue using your existing flow by managing COOP enforcement. Use the Microsoft Graph self-service API while you implement a COOP-compatible authentication flow or upgrade to MSAL.js v5.

The `coopEnforcement` application property lets you opt out of enforcement without opening a support request. After your application is COOP-ready, use the same property to opt back in.

Warning

Opting out of the COOP policy doesn't fix the underlying vulnerability. While the policy is disabled, the application remains exposed to the cross-origin attacks that the COOP headers help prevent.

Only opt out if the application severs the parent-window relationship before redirecting to sign-in and ensures that only trusted sites can open the sign-in popup. Re-enable enforcement as soon as the application uses a compatible flow.

1. Follow [Configure application authentication behaviors by using Microsoft Graph](/en-us/graph/applications-authenticationbehaviors?tabs=http) to opt out while you migrate.
2. Implement a COOP-compatible authentication flow or upgrade to MSAL.js v5.
3. Test the application's authentication flows.
4. Use the `coopEnforcement` property to opt back in.