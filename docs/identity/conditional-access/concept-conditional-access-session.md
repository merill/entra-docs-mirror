---
layout: Conceptual
title: 'Conditional Access: Manage Session Controls Effectively - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-session
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how session controls in Microsoft Entra Conditional Access policies enable secure, limited experiences for cloud apps based on device compliance.
ms.topic: concept-article
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: joflore
locale: en-us
document_id: 609a0eda-f113-8b77-67ee-c5e8bd94cbac
document_version_independent_id: 7468d74e-9a7e-2a11-ba35-da46103a1b80
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-conditional-access-session.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-conditional-access-session
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-conditional-access-session.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
2PlusCloud:
- Azure
- M365
- Power
platformId: ec6f92db-29d2-e9b3-0e8a-c13b009591e7
---

# Conditional Access: Manage Session Controls Effectively - Microsoft Entra ID | Microsoft Learn

## Overview

In a Conditional Access policy, an admin can use session controls to enable limited experiences in specific cloud applications.

![Screenshot of a Conditional Access policy with a grant control requiring multifactor authentication.](media/concept-conditional-access-session/conditional-access-session.png)

In a Microsoft Entra External ID [external tenant](/en-us/entra/external-id/customers/concept-supported-features-customers#conditional-access), you can use the following session controls:

- Sign-in frequency
- Persistent browser session

## Application enforced restrictions

Organizations can use this control to require Microsoft Entra ID to pass device information to the selected cloud apps. The device information allows cloud apps to know if a connection is from a compliant or domain-joined device and update the session experience. When selected, the cloud app uses the device information to provide users with a limited or full experience. Limited if the device isn't managed or compliant, and full if the device is managed and compliant.

For a list of supported applications and steps to configure policies, see the following articles:

- [Idle session timeout for Microsoft 365](/en-us/microsoft-365/admin/manage/idle-session-timeout-web-apps#details-about-idle-session-timeout).
- Learn how to enable limited access with [SharePoint Online](/en-us/sharepoint/control-access-from-unmanaged-devices).
- Learn how to enable limited access with [Exchange Online](/en-us/microsoft-365/security/office-365-security/secure-email-recommended-policies#limit-access-to-exchange-online-from-outlook-on-the-web).

## Conditional Access application control

Conditional Access App Control uses a reverse proxy architecture and is uniquely integrated with Microsoft Entra Conditional Access. Microsoft Entra Conditional Access lets you enforce access controls on your organization’s apps based on specific conditions. The conditions define which users, groups, cloud apps, locations, and networks a Conditional Access policy applies to. After determining the conditions, route users to [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps) to protect data with Conditional Access App Control by applying access and session controls.

Conditional Access App Control enables user app access and sessions to be monitored and controlled in real time based on access and session policies. Use access and session policies in the Defender for Cloud Apps portal to refine filters and set actions.

Enforce this control with Microsoft Defender for Cloud Apps, where admins can [deploy Conditional Access App Control for featured apps](/en-us/defender-cloud-apps/proxy-deployment-aad) and [use Microsoft Defender for Cloud Apps session policies](/en-us/defender-cloud-apps/session-policy-aad).

For Microsoft Edge for Business, enforce this control with [Microsoft Purview Data Loss Prevention](/en-us/purview/dlp-browser-dlp-learn), where admins can [help prevent users from sharing sensitive info with cloud apps in Edge for Business](/en-us/purview/dlp-create-policy-prevent-cloud-sharing-from-edge-biz). The Conditional Access App Control **Custom** setting is necessary for apps included in these policies.

## Sign-in frequency

Sign-in frequency specifies how long a user can stay signed in before being prompted to sign in again when accessing a resource. Admins can set a time period (hours or days) or require reauthentication every time.

The sign-in frequency setting works with apps that use OAuth 2.0 or OIDC protocols. Most Microsoft native apps for Windows, Mac, and mobile, including the following web applications, follow this setting.

- Word, Excel, PowerPoint Online
- OneNote Online
- Office.com
- Microsoft 365 Admin portal
- Exchange Online
- SharePoint and OneDrive
- Teams web client
- Dynamics CRM Online
- Azure portal

For more information, see [Configure authentication session management with Conditional Access](concept-session-lifetime#user-sign-in-frequency).

## Persistent browser session

A persistent browser session lets users stay signed in after closing and reopening their browser window.

For more information, see [Configure authentication session management with Conditional Access](concept-session-lifetime#persistence-of-browsing-sessions).

## Customize continuous access evaluation

[Continuous access evaluation](concept-continuous-access-evaluation) is auto enabled as part of an organization's Conditional Access policies. For organizations who wish to disable continuous access evaluation, this configuration is now an option within the session control within Conditional Access. Continuous access evaluation policies apply to all users or specific users and groups. Admins can make the following selection while creating a new policy or while editing an existing Conditional Access policy.

- **Disable** works only when **All resources (formerly 'All cloud apps')** are selected, no conditions are selected, and **Disable** is selected under **Session** &gt; **Customize continuous access evaluation** in a Conditional Access policy. You can disable all users or specific users and groups.

[![Screenshot of CAE settings in a new Conditional Access policy.](media/concept-conditional-access-session/continuous-access-evaluation-session-controls.png)](media/concept-conditional-access-session/continuous-access-evaluation-session-controls.png#lightbox)

## Disable resilience defaults

During an outage, Microsoft Entra ID extends access to existing sessions while enforcing Conditional Access policies.

If resilience defaults are disabled, access is denied when existing sessions expire. For more information, see [Conditional Access: Resilience defaults](resilience-defaults).

## Require token protection for sign-in sessions

Token protection, sometimes called token binding in the industry, attempts to reduce attacks using token theft by ensuring a token is usable only from the intended device. If an attacker steals a token through hijacking or replay, they can impersonate the victim until the token expires or is revoked. Token theft is rare, but its impact can be significant. For more information, see [Conditional Access: Token protection](concept-token-protection).

## Use Global Secure Access security profile

Using a security profile with Conditional Access combines identity controls with network security in Microsoft's Security Service Edge (SSE) product, [Microsoft Entra Internet Access](../../global-secure-access/concept-internet-access#security-profiles). Selecting this Session control lets you bring identity and context awareness to security profiles, which are groupings of various policies created and managed in Global Secure Access.