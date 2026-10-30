---
layout: Conceptual
title: Learn about Continuous Access Evaluation (CAE) for Application Proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/concept-continuous-access-evaluation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Learn how Continuous Access Evaluation (CAE) works with Application Proxy to enforce near-real-time access policies for on-premises applications.
ms.topic: concept-article
ms.date: 2026-04-01T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: b9bab627-a3c9-e4fe-b367-b978c20f0366
document_version_independent_id: b9bab627-a3c9-e4fe-b367-b978c20f0366
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/concept-continuous-access-evaluation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/concept-continuous-access-evaluation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/concept-continuous-access-evaluation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5751d9de-b2e6-6948-f587-864689fabf46
---

# Learn about Continuous Access Evaluation (CAE) for Application Proxy - Microsoft Entra ID | Microsoft Learn

Continuous Access Evaluation (CAE) is a security feature that provides real-time access control based on policy changes and user risk. CAE enforces access policies in near real time by continuously evaluating session validity. When a policy change, user risk update, or other critical security event occurs, CAE revokes access tokens and refresh tokens, ensuring that user access always complies with the latest security requirements.

Unlike traditional CAE, which requires each workload to adopt special libraries and is limited to first-party applications, CAE for Application Proxy extends these benefits to any on-premises applications published through Application Proxy, without requiring the application to be CAE-aware.

## How CAE protects access

CAE for Application Proxy responds to critical identity and security events so administrators can limit access promptly. The following events trigger enforcement in near real time:

- User termination or password change/reset: CAE revokes user sessions and refresh tokens to prevent continued access.
- Network location change: CAE reevaluates and enforces Conditional Access location policies when a user's network context changes.
- Token export to a machine outside of a trusted network: CAE enforces Conditional Access location policies to block token use or require additional controls when a token is used from an untrusted machine.

## Understand how CAE for Application Proxy works

When CAE is enabled for Application Proxy, the request and enforcement flow proceeds as follows:

1. A user requests access to an on-premises application through Application Proxy.
2. Microsoft Entra ID authenticates the request.
3. After successful authentication, the user receives access tokens that are typically valid for 60–90 minutes.
4. CAE continuously evaluates the active session for policy changes, risk signals, and revocation events.
5. If a trigger occurs (for example, password reset, account disablement, or elevated risk), CAE revokes the session and requires the user to sign in again.

This workflow enables near-real-time enforcement of access policies for published applications without requiring application changes.

## Microsoft Entra ID signals that trigger CAE reauthentication

Application Proxy receives signals from Microsoft Entra ID in near real time for these events:

- A user account is deleted or disabled.
- A user’s password is changed or reset.
- Multifactor authentication (MFA) is enabled for the user.
- An administrator revokes all refresh tokens for the user.

When Application Proxy receives any of these signals, it prompts the user to reauthenticate. If reauthentication succeeds, the user regains access to resources published through Application Proxy.

## Disable CAE for Application Proxy

### Disable CAE for specific Application Proxy applications

CAE for Application Proxy is enabled by default for all Application Proxy applications. You can disable CAE for individual applications either by using Microsoft Graph or in the Microsoft Entra admin center.

To disable CAE for an individual Application Proxy application, update the application's `onPremisesPublishing` settings in Microsoft Graph.

Send the following PATCH request:

```http
PATCH https://graph.microsoft.com/beta/applications/{objectId}/onPremisesPublishing
Content-Type: application/json

{
    "isContinuousAccessEvaluationEnabled": false
}
```

A successful request returns the following response:

```http
HTTP/1.1 204 No Content
```

Ensure that the account or app calling Microsoft Graph has permission to update the application (for example, `Application.ReadWrite.All`).

You can also disable CAE for Application Proxy in the Microsoft Entra admin center.

[![Screenshot of the Disable continuous access evaluation checkbox on the Advanced tab of the Add your own on-premises application page in the Microsoft Entra admin center.](media/concept-continuous-access-evaluation/disable-continuous-access-evaluation.png)](media/concept-continuous-access-evaluation/disable-continuous-access-evaluation.png#lightbox)

### Disable CAE for the entire tenant

Microsoft Entra ID Conditional Access controls tenant-wide CAE behavior. By default, CAE is enabled for all applications that support it. To disable CAE for all services, update your Conditional Access configuration. For steps, see [Enable or disable CAE](/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation#enable-or-disable-cae).

Note

CAE is opportunistic unless you enable Strict Enforcement in Conditional Access and apply it to the Application Proxy application. With a non-strict policy, Application Proxy can fall back to issuing a regular access token on reauthentication. Because of this fallback behavior, disabling tenant-wide CAE is rarely necessary.

## Known limitations

For detailed information about known issues and limitations, see the [Application Proxy FAQ](/en-us/entra/identity/app-proxy/application-proxy-faq).