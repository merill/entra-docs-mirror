---
layout: Conceptual
title: Troubleshoot legacy Microsoft Entra hybrid joined devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/troubleshoot-hybrid-join-windows-legacy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Troubleshooting Microsoft Entra hybrid joined down-level devices.
ms.topic: troubleshooting
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: 
locale: en-us
document_id: 19ccc59d-2fdc-c81d-220c-db2e643431d7
document_version_independent_id: a2224f12-fbc7-853b-0705-2037bdbec2be
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/troubleshoot-hybrid-join-windows-legacy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/troubleshoot-hybrid-join-windows-legacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/troubleshoot-hybrid-join-windows-legacy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 84b02f4a-da85-ad29-48d2-a5bea9ca8b10
---

# Troubleshoot legacy Microsoft Entra hybrid joined devices - Microsoft Entra ID | Microsoft Learn

This article is applicable only to the following devices:

- Windows 7
- Windows 8.1
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

For important information about the support of older OS versions, see [Supported versions of Windows client](/en-us/windows/release-health/supported-versions-windows-client) and [Known issues and notifications for Windows 8.1 and Windows Server 2012 R2](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2).

For Windows 10 or newer and Windows Server 2016, see [Troubleshooting Microsoft Entra hybrid joined Windows 10 and Windows Server 2016 devices](troubleshoot-hybrid-join-windows-current).

This article assumes that you [configured Microsoft Entra hybrid joined devices](hybrid-join-plan) to support the following scenarios:

- Device-based Conditional Access

This article provides you with troubleshooting guidance on how to resolve potential issues.

**What you should know:**

- Microsoft Entra hybrid join for downlevel Windows devices works differently than it does in Windows 10 or newer. Many customers don't realize that they need AD FS (for federated domains) or Seamless SSO configured (for managed domains).
- Seamless SSO doesn't work in private browsing mode on Firefox and Microsoft Edge browsers. It also doesn't work on Internet Explorer if the browser is running in Enhanced Protected mode or if Enhanced Security Configuration is enabled.
- For customers with federated domains, if the Service Connection Point (SCP) was configured such that it points to the managed domain name (for example, contoso.onmicrosoft.com, instead of contoso.com), then Microsoft Entra hybrid join for downlevel Windows devices doesn't work.
- The same physical device appears multiple times in Microsoft Entra ID when multiple domain users sign-in the downlevel Microsoft Entra hybrid joined devices. For example, if *Person1* and *Person2* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.
- You can also get multiple entries for a device on the user info tab because of a reinstallation of the operating system or a manual re-registration.
- The initial registration / join of devices is configured to perform an attempt at either sign-in or lock / unlock. There could be 5-minute delay triggered by a task scheduler task.
- Make sure [KB4284842](https://support.microsoft.com/help/4284842) is installed on Windows 7 SP1 or Windows Server 2008 R2 SP1. This update prevents future authentication failures due to customer's access loss to protected keys after changing password.
- Microsoft Entra hybrid join might fail after a user has their UPN changed, breaking the Seamless SSO authentication process. During the join process, you might see that it's still sending the previous UPN to Microsoft Entra ID, unless browser session cookies are cleared or user explicitly signs out and removes old UPN.

## Step 1: Retrieve the registration status

**To verify the registration status:**

1. Sign on with the user account that performed the Microsoft Entra hybrid join.
2. Open the command prompt
3. Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe" /i`

This command displays a dialog box that provides you with details about the join status.

![Screenshot of the Workplace Join for Windows dialog box. Text that includes an email address states that a certain device is joined to a workplace.](media/troubleshoot-hybrid-join-windows-legacy/01.png)

## Step 2: Evaluate the Microsoft Entra hybrid join status

If the device wasn't Microsoft Entra hybrid joined, you can attempt to do Microsoft Entra hybrid join by clicking on the "Join" button. If the attempt to do Microsoft Entra hybrid join fails, the details about the failure are shown.

**The most common issues are:**

- A misconfigured AD FS or Microsoft Entra ID or Network issues

    ![Screenshot of the Workplace Join for Windows dialog box. Text reports that an error occurred during account authentication.](media/troubleshoot-hybrid-join-windows-legacy/02.png)

    - Autoworkplace.exe is unable to silently authenticate with Microsoft Entra ID or AD FS. This issue could be caused by missing or misconfigured AD FS (for federated domains) or missing or misconfigured Microsoft Entra seamless single sign-on (for managed domains) or network issues.
    - It could be that multifactor authentication (MFA) is enabled/configured for the user and WIAORMULTIAUTHN isn't configured at the AD FS server.
    - Another possibility is that home realm discovery (HRD) page is waiting for user interaction, which prevents **autoworkplace.exe** from silently requesting a token.
    - It could be that AD FS and Microsoft Entra URLs are missing in IE's intranet zone on the client.
    - Network connectivity issues might be preventing **autoworkplace.exe** from reaching AD FS or the Microsoft Entra URLs.
    - **Autoworkplace.exe** requires the client to have direct line of sight from the client to the organization's on-premises AD domain controller, which means that Microsoft Entra hybrid join succeeds only when the client is connected to organization's intranet.
    - If your organization uses Microsoft Entra seamless single sign-on, `https://autologon.microsoftazuread-sso.com` isn't present on the device's IE intranet settings.
    - The internet setting `Do not save encrypted pages to disk` is checked.
- You aren't signed on as a domain user

    ![Screenshot of the Workplace Join for Windows dialog box. Text reports that an error occurred during account verification.](media/troubleshoot-hybrid-join-windows-legacy/03.png)

    There are a few different reasons why this issue can occur:

    - The signed in user isn't a domain user (for example, a local user). Microsoft Entra hybrid join on down-level devices is supported only for domain users.
    - The client isn't able to connect to a domain controller.
- A quota is reached

    ![Screenshot of the Workplace Join for Windows dialog box. Text reports an error because the user reached the maximum number of joined devices.](media/troubleshoot-hybrid-join-windows-legacy/04.png)
- The service isn't responding

    ![Screenshot of the Workplace Join for Windows dialog box. Text reports that an error occurred because the server didn't respond.](media/troubleshoot-hybrid-join-windows-legacy/05.png)

You can also find the status information in the event log under: **Applications and Services Log\Microsoft-Workplace Join**

**The most common causes for a failed Microsoft Entra hybrid join are:**

- Your computer isn't connected to your organization’s internal network or to a VPN with a connection to your on-premises AD domain controller.
- You're logged on to your computer with a local computer account.
- Service configuration issues:
    - The AD FS server isn't configured to support **WIAORMULTIAUTHN**.
    - Your computer's forest has no Service Connection Point object that points to your verified domain name in Microsoft Entra ID
    - Or if your domain is managed, then Seamless SSO wasn't configured or working.
    - A user reached the limit of devices.