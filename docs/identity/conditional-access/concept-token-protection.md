---
layout: Conceptual
title: How Token Protection Enhances Conditional Access Policies - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-token-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Protect your resources with token protection in Conditional Access policies. Understand requirements, limitations, and deployment best practices.
ms.topic: concept-article
ms.date: 2026-08-14T00:00:00.0000000Z
ms.reviewer: sgrandhi
ms.custom:
- sfi-image-nochange
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:08/20/2025
- ai-gen-description
locale: en-us
document_id: 9ec45091-ab65-7d9d-8915-26f5e56aa274
document_version_independent_id: 13a637da-8ded-72a0-464c-61efdef2a199
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-token-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-token-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-token-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 4ae14c29-9de0-88eb-b2fc-f1e043d7d774
---

# How Token Protection Enhances Conditional Access Policies - Microsoft Entra ID | Microsoft Learn

## Overview

Token Protection is a Conditional Access session control that attempts to reduce token replay attacks by ensuring only device bound sign-in session tokens, like [Primary Refresh Tokens (PRTs)](../devices/concept-primary-refresh-token), are accepted by Microsoft Entra ID when applications request access to protected resources.

When a user registers a supported device with Microsoft Entra, a PRT is issued and cryptographically bound to that device. This binding ensures that even if a threat actor steals the token, it can't be used from another device. With Token Protection enforced, Microsoft Entra validates that only these bound sign-in session tokens are used by supported applications.

Note

Use Token Protection as part of a broader defense-in-depth strategy against token theft. For more information, see [Protecting tokens in Microsoft Entra](../devices/protecting-tokens-microsoft-entra-id).

## Platform availability

| Platform | Native applications | Browser-based applications |
| --- | --- | --- |
| Windows | Generally Available | Preview for supported web apps that access Azure Resource Manager |
| iOS / iPadOS | Generally Available | Not supported |
| macOS | Generally Available | Preview for supported web apps that access Azure Resource Manager |

Note

Browser-based application support is currently limited to selected web apps, browsers, and device configurations that access Azure Resource Manager. For requirements and the list of supported applications, see [Token Protection deployment guide - Web apps](deployment-guide-token-protection-web-apps).

## Supported resources

For native applications, Token Protection policy can be enforced on the following cloud resources:

- Exchange Online
- SharePoint Online
- Microsoft Teams

On Windows, enforcement is also supported for:

- Azure Virtual Desktop
- Windows 365

For browser-based applications in preview, enforcement is supported for Azure Resource Manager, configured in Conditional Access as the **Windows Azure Service Management API** resource. Only selected web applications that access Azure Resource Manager are supported. For details, see [Token Protection deployment guide - Web apps](deployment-guide-token-protection-web-apps).

### Supported devices

**Windows**:

- Windows 10 or newer devices that are Microsoft Entra joined, Microsoft Entra hybrid joined, or Microsoft Entra registered. See the known limitations section in the appropriate deployment guide for unsupported device types.
- Windows Server 2019 or newer that are hybrid Microsoft Entra joined.
- For detailed steps on how to register your device, see [Register your personal device on your work or school network](https://support.microsoft.com/account-billing/register-your-personal-device-on-your-work-or-school-network-8803dd61-a613-45e3-ae6c-bd1ab25bf8a8).
- Browser-based application support (Preview) has additional operating system, browser, extension, and configuration requirements. See [Token Protection deployment guide - Web apps](deployment-guide-token-protection-web-apps).

**Apple (Preview)**:

- macOS 14.0 or later. Requires the Microsoft Enterprise single sign-on (SSO) plug-in. Alternatively, you can also use Platform SSO. Only MDM-managed devices are supported.
- iOS / iPadOS 16.0 or later. Requires the Microsoft Enterprise SSO plug-in. Only MDM-managed devices are supported.
- For detailed steps on how to set up, see [Enabling Microsoft Enterprise SSO plug-in](../../identity-platform/apple-sso-plugin) and configuring [Platform SSO for macOS](/en-us/intune/intune-service/configuration/platform-sso-macos).
- Browser-based application support (Preview) on macOS has additional browser, extension, and configuration requirements. See [Token Protection deployment guide - Web apps](deployment-guide-token-protection-web-apps).

## Deployment

To minimize the likelihood of user disruption due to app or device incompatibility, follow these recommendations:

- Start with a pilot group of users and expand over time.
- Create a Conditional Access policy in [report-only mode](concept-conditional-access-report-only) before enforcing token protection.
- Capture both interactive and non-interactive sign-in logs.
- Analyze these logs long enough to cover normal application use.
- Add known, reliable users to an enforcement policy.

This process helps assess your users' client and app compatibility for token protection enforcement.

### Deployment guides

Select the guide for your target platform:

- **Windows**: [Token Protection deployment guide - Windows](deployment-guide-token-protection-windows)
- **iOS, iPadOS, and macOS**: [Token Protection deployment guide - Apple](deployment-guide-token-protection-apple)
- **Web apps that access Azure Resource Manager (Preview)**: [Token Protection deployment guide - Web apps](deployment-guide-token-protection-web-apps)