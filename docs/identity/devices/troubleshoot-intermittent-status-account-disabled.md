---
layout: Conceptual
title: Troubleshoot STATUS_ACCOUNT_DISABLED in Microsoft Entra - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/troubleshoot-intermittent-status-account-disabled
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to diagnose intermittent STATUS_ACCOUNT_DISABLED errors on Microsoft Entra hybrid joined Windows devices and restore user sign-in.
ms.topic: troubleshooting
ms.date: 2026-09-01T00:00:00.0000000Z
ms.reviewer: mozmaili
ms.custom: has-adal-ref, sfi-ropc-nochange, sfi-image-nochange, msecd-doc-authoring-1018
ai-usage: ai-assisted
locale: en-us
document_id: 5a17f454-306e-0b25-a1b1-690edc626cee
document_version_independent_id: 5a17f454-306e-0b25-a1b1-690edc626cee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/troubleshoot-intermittent-status-account-disabled.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/troubleshoot-intermittent-status-account-disabled
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/troubleshoot-intermittent-status-account-disabled.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 941a1026-3bf9-a112-f840-fa09e2199b21
---

# Troubleshoot STATUS_ACCOUNT_DISABLED in Microsoft Entra - Microsoft Entra ID | Microsoft Learn

This article provides troubleshooting guidance to help you resolve potential issues with Windows devices that are Microsoft Entra hybrid joined and receive intermittent STATUS\_ACCOUNT\_DISABLED errors when users attempt to sign in or unlock the device.

## Symptoms

In a Microsoft Entra hybrid joined environment, you might occasionally receive the error message STATUS\_ACCOUNT\_DISABLED ('The user is disabled') when attempting to sign in or unlock the device.

However, the user account in question is not disabled.

The issue typically self-resolves after waiting a few minutes and trying to unlock again, or rebooting, or signing out completely and signing back in instead of trying to unlock.

In addition, you see the following events in the event log:

```text
Log:  Microsoft-Windows-AAD/Operational
Event ID 1081
Level: Error

OAuth response error: invalid_grant
Error description: AADSTS50034: The user account {user} does not exist in the
{guid} directory. To sign into this application, the account
must be added to the directory.
```

```text
Log:  Microsoft-Windows-Hello-for-Business/Operational
Event ID 7001

A user failed to sign into the device with the following information:
Username: SYSTEM  User SID: S-1-5-18
Credential Type: Software Key  Deployment Type: Cloud Trust
Software Lockout Counter: 0
Authentication Error Status: 0xC000006D  Authentication Error Substatus: 0xC0000072

 0xC000006D / 0xC0000072  = STATUS_LOGON_FAILURE / STATUS_ACCOUNT_DISABLED.
```

The issue does not occur in Entra-native deployments.

## Cause

Microsoft Entra hybrid join caches some user data locally on the Windows client. Events such as primary refresh token (PRT) expiration and VSM session key rollover can make this cache stale. Rebuilding the cache requires communication with the on-premises Active Directory domain controller. That communication can fail when:

- The computer recently resumed from hibernation.
- The computer recently resumed from a deep sleep state.
- Virtual private network (VPN) or network adapter connectivity isn't ready when the client tries to communicate with the on-premises domain controller.
- The VPN requires a user to sign in before it connects, such as when using a user VPN instead of a device VPN.

When this communication fails, the Windows client sends Microsoft Entra ID the user's Security Account Manager (SAM) account name instead of the full user principal name (UPN). Microsoft Entra ID doesn't recognize a SAM account name without the domain, so the sign-in attempt fails. The Windows client then maps Microsoft Entra error AADSTS50034 (user not found) to STATUS\_ACCOUNT\_DISABLED, which can cause confusion.

Although Microsoft may improve this behavior in future updates, it is currently viewed as by design. Microsoft recommends all future deployments be Entra-native, where this problem doesn't exist.