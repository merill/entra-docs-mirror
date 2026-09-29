---
layout: Conceptual
title: How to Use Conditions in Conditional Access Policies - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-conditions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Explore Conditional Access conditions, including risk, device, network, and agent execution environment signals, to secure your organization's resources with tailored policies.
ms.topic: concept-article
ms.date: 2026-06-02T00:00:00.0000000Z
ms.reviewer: lhuangnorth, sandeo
ai-usage: ai-assisted
locale: en-us
document_id: 625bb1b2-81fd-9804-c0b5-3cd2904decd9
document_version_independent_id: e4468b05-200e-24ae-75e9-29fb2b3a6ddc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-conditional-access-conditions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-conditional-access-conditions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-conditional-access-conditions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 6141d2a0-2384-19c3-e815-d30491567299
---

# How to Use Conditions in Conditional Access Policies - Microsoft Entra ID | Microsoft Learn

## Overview

In a Conditional Access policy, admins use one or more signals to improve policy decisions.

[![Screenshot of available conditions for a Conditional Access policy in the Microsoft Entra admin center.](media/concept-conditional-access-conditions/conditional-access-conditions.png)](media/concept-conditional-access-conditions/conditional-access-conditions.png#lightbox)

Admins combine multiple conditions to create specific, fine-grained Conditional Access policies.

When users access a sensitive application, admins might consider multiple conditions in their access decisions, such as:

- Risk information from Microsoft Entra ID Protection
- Agent execution environment
- Network location
- Device information

## Agent risk (Preview)

Admins with access to [ID Protection](../../id-protection/overview-identity-protection) can evaluate agent risk as part of a Conditional Access policy. Agent risk shows the likelihood that an agent is compromised.

## User risk

Admins with access to [ID Protection](../../id-protection/overview-identity-protection) can evaluate user risk as part of a Conditional Access policy. User risk shows the likelihood that an identity or account is compromised. Learn more about user risk in [What is risk](../../id-protection/concept-identity-protection-risks) and [How to configure and enable risk policies](../../id-protection/howto-identity-protection-configure-risk-policies).

## Sign-in risk

Admins with access to [ID Protection](../../id-protection/overview-identity-protection) can evaluate sign-in risk as part of a Conditional Access policy. Sign-in risk shows the probability that an authentication request isn't made by the identity owner. Learn more about sign-in risk in the articles [What is risk](../../id-protection/concept-identity-protection-risks) and [How to configure and enable risk policies](../../id-protection/howto-identity-protection-configure-risk-policies).

## Insider risk

Admins with access to [Microsoft Purview adaptive protection](/en-us/purview/insider-risk-management-adaptive-protection) can incorporate risk signals from Microsoft Purview into Conditional Access policy decisions. Insider risk takes into account your data governance, data security, and risk and compliance configurations from Microsoft Purview. These signals are based on contextual factors such as:

- User behavior
- Historical patterns
- Anomaly detections

This condition lets admins use Conditional Access policies to take actions such as blocking access, requiring stronger authentication methods, or requiring terms of use acceptance.

This functionality incorporates parameters that specifically address potential risks arising from within an organization. Configuring Conditional Access to consider insider risk lets admins tailor access permissions based on contextual factors such as user behavior, historical patterns, and anomaly detection.

For more information, see [configure and enable an insider risk-based policy](policy-risk-based-insider-block).

## Agent execution environments (Preview)

Use the **Agent execution environments** condition to scope a Conditional Access policy to agents' user account sessions initiated from endpoints. This condition helps you avoid applying endpoint-dependent controls to agents that run directly in the cloud and don't have a device to evaluate.

When a policy uses this condition, agents that aren't running on a device are excluded from evaluation. Use this condition with other endpoint-based conditions, such as **Device platforms**, **Filter for devices**, and **Network**, when you want to enforce controls only for agents running on managed endpoints.

## Device platforms

Warning

Conditional Access identifies the device platform using information provided by the device, such as user agent strings. Because user agent strings can be modified, this information isn't verified. Use device platform with Microsoft Intune device compliance policies or as part of a block statement. By default, it applies to all device platforms. You should use Conditional Access policies using this condition with another policy (like one requiring device compliance or app protection policies) to mitigate the risk of user agent spoofing.

For agents' user accounts, this condition applies only when the agent session is initiated from an endpoint. Use it with the **Agent execution environments** condition to avoid targeting agents that run directly in cloud infrastructure.

Conditional Access supports these device platforms:

- Android
- iOS
- Windows
- macOS
- Linux

If you block legacy authentication using the **Other clients** condition, you can also set the device platform condition.

Selecting macOS or Linux device platforms isn't supported when you select **Require approved client app** or **Require app protection policy** as the only grant controls, or when you select **Require all the selected controls**.

Important

Microsoft recommends creating a Conditional Access policy for unsupported device platforms. For example, to block access to corporate resources from **Chrome OS** or other unsupported clients, configure a policy with a Device platforms condition that includes any device, excludes supported device platforms, and sets Grant control to Block access.

## Locations

[The locations condition has moved.](concept-assignment-network)

For agents' user accounts, the **Network** condition applies only to agents running on endpoints that provide the required network signal, such as a device with a [Global Secure Access](/en-us/entra/global-secure-access/overview-what-is-global-secure-access) client.

## Client apps

By default, all newly created Conditional Access policies apply to all client app types even if the client apps condition isn’t configured.

Note

The behavior of the client apps condition was updated in August 2020. If you have existing Conditional Access policies, they remain unchanged. However, if you select an existing policy, the **Configure** toggle is removed and the client apps the policy applies to are selected.

Important

Sign-ins from legacy authentication clients don’t support multifactor authentication (MFA) and don’t pass device state information, so they're blocked by Conditional Access grant controls, like requiring MFA or compliant devices. If you have accounts that must use legacy authentication, you must either exclude those accounts from the policy, or configure the policy to only apply to modern authentication clients.

The **Configure** toggle when set to **Yes** applies to checked items, when set to **No** it applies to all client apps, including modern and legacy authentication clients. This toggle doesn’t appear in policies created before August 2020.

- Modern authentication clients
    - Browser
        - These clients include web-based applications that use protocols like SAML, WS-Federation, OpenID Connect, or services registered as an OAuth confidential client.
    - Mobile apps and desktop clients
        - This option includes applications like the Office desktop and phone applications.
- Legacy authentication clients
    - Exchange ActiveSync clients
        - This selection includes all use of the Exchange ActiveSync (EAS) protocol. When policy blocks the use of Exchange ActiveSync, the affected user receives a single quarantine email. This email provides information on why they’re blocked and includes remediation instructions if able.
        - Admins can apply policy only to supported platforms (such as iOS, Android, and Windows) through the Conditional Access Microsoft Graph API.
    - Other clients
        - This option includes clients that use basic/legacy authentication protocols that don’t support modern authentication.
            - SMTP - Used by POP and IMAP clients to send email messages.
            - Autodiscover - Used by Outlook and EAS clients to find and connect to mailboxes in Exchange Online.
            - Exchange Online PowerShell - Used to connect to Exchange Online with remote PowerShell. If you block Basic authentication for Exchange Online PowerShell, you need to use the Exchange Online PowerShell Module to connect. For instructions, see [Connect to Exchange Online PowerShell using multifactor authentication](/en-us/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/mfa-connect-to-exchange-online-powershell).
            - Exchange Web Services (EWS) - A programming interface used by Outlook, Outlook for Mac, and non-Microsoft apps.
            - IMAP4 - Used by IMAP email clients.
            - MAPI over HTTP (MAPI/HTTP) - Used by Outlook 2010 and later.
            - Offline Address Book (OAB) - A copy of address list collections that are downloaded and used by Outlook.
            - Outlook Anywhere (RPC over HTTP) - Used by Outlook 2016 and earlier.
            - Outlook Service - Used by the Mail and Calendar app for Windows 10.
            - POP3 - Used by POP email clients.
            - Reporting Web Services - Used to retrieve report data in Exchange Online.

These conditions are commonly used to:

- Require a managed device
- Block legacy authentication
- Block web applications but allow mobile or desktop apps

### Supported browsers

This setting works with all browsers. However, to satisfy a device policy, like a compliant device requirement, the following operating systems and browsers are supported. Operating Systems and browsers out of mainstream support aren’t shown on this list:

| Operating Systems | Browsers |
| --- | --- |
| Windows 10 + | Microsoft Edge, Chrome, [Firefox 91+](https://support.mozilla.org/kb/windows-sso) |
| Windows Server 2025 | Microsoft Edge, Chrome |
| Windows Server 2022 | Microsoft Edge, Chrome |
| Windows Server 2019 | Microsoft Edge, Chrome |
| iOS | Microsoft Edge, Safari (see the notes) |
| Android | Microsoft Edge, Chrome |
| macOS | Microsoft Edge, Chrome, [Firefox 133+](https://support.mozilla.org/kb/firefox-enterprise-133-release-notes), Safari |
| Linux Desktop | Microsoft Edge |

These browsers support device authentication, allowing the device to be identified and validated against a policy. The device check fails if the browser is running in private mode or if cookies are disabled.

Note

Microsoft Edge 85+ requires the user to be signed in to the browser to properly pass device identity. Otherwise, it behaves like Chrome without the [Microsoft Single Sign On extension](https://chromewebstore.google.com/detail/windows-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji). This sign-in might not occur automatically in a hybrid device join scenario.

Safari is supported for device-based Conditional Access on a managed device, but it can't satisfy the **Require approved client app** or **Require app protection policy** conditions. A managed browser like Microsoft Edge satisfies approved client app and app protection policy requirements. On iOS with non-Microsoft MDM solutions, only the Microsoft Edge browser supports device policy.

[Firefox 91+](https://support.mozilla.org/kb/windows-sso) is supported for device-based Conditional Access, but "Allow Windows single sign-on for Microsoft, work, and school accounts" needs to be enabled.

[Chrome 111+](https://chromeenterprise.google/policies/#CloudAPAuthEnabled) is supported for device-based Conditional Access, but "CloudApAuthEnabled" needs to be enabled.

macOS devices using the Firefox browser must be running macOS version 10.15 or newer and have the [Microsoft Enterprise SSO plug-in installed](/en-us/mem/intune-service/user-help/enroll-your-device-in-intune-macos-cp) and [configured appropriately](/en-us/entra/identity-platform/apple-sso-plugin#microsoft-intune-configuration).

#### Why do I see a certificate prompt in the browser

On iOS, Android, and macOS devices are identified using a client certificate. This certificate is provisioned when the device is registered. When a user first signs in through the browser the user is prompted to select the certificate. The user must select this certificate before using the browser.

#### Chrome support

##### Windows

For Chrome support in **Windows 10 Creators Update (version 1703)** or later, install the [Microsoft Single Sign On](https://chrome.google.com/webstore/detail/windows-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji) extension or enable Chrome's [CloudAPAuthEnabled](https://chromeenterprise.google/policies/#CloudAPAuthEnabled). These configurations are required when a Conditional Access policy requires device-specific details for Windows platforms specifically.

To automatically enable the CloudAPAuthEnabled policy in Chrome, create the following registry key:

- Path: `HKEY_LOCAL_MACHINE\Software\Policies\Google\Chrome`
- Name: `CloudAPAuthEnabled`
- Value: `0x00000001`
- PropertyType: `DWORD`

To automatically deploy the Microsoft Single Sign On extension to Chrome browsers, create the following registry key using the [ExtensionInstallForcelist](https://chromeenterprise.google/policies/?policy=ExtensionInstallForcelist) policy in Chrome:

- Path: `HKEY_LOCAL_MACHINE\Software\Policies\Google\Chrome\ExtensionInstallForcelist`
- Name: `1`
- Type: `REG_SZ (String)`
- Data: `ppnbnpeolgkicgegkbkbjmhlideopiji;https://clients2.google.com/service/update2/crx`

##### macOS

macOS devices using the Enterprise SSO plugin require the [Microsoft Single Sign On](https://chromewebstore.google.com/detail/windows-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji) extension to support SSO and device-based Conditional Access in Google Chrome.

For MDM based deployments of Google Chrome and extension management, refer to [Set up Chrome browser on Mac](https://support.google.com/chrome/a/answer/7550274?hl=en&amp;sjid=4022223857702261083-NA) and [ExtensionInstallForcelist](https://chromeenterprise.google/policies/?policy=ExtensionInstallForcelist).

### Supported mobile applications and desktop clients

Admins can select **Mobile apps and desktop clients** as client app.

This setting has an effect on access attempts made from the following mobile apps and desktop clients:

| Client apps | Target Service | Platform |
| --- | --- | --- |
| Dynamics CRM app | Dynamics CRM | Windows 10, iOS, and Android |
| Mail/Calendar/People app, Outlook 2016, Outlook 2013 (with modern authentication) | Exchange Online | Windows 10 |
| MFA and location policy for apps. Device-based policies aren’t supported. | Any My Apps app service | Android and iOS |
| Microsoft Teams Services - this client app controls all services that support Microsoft Teams and all its Client Apps - Windows Desktop, iOS, Android, WP, and web client | Microsoft Teams | Windows 10, iOS, Android, and macOS |
| Office 2016 apps, Universal Office apps, Office 2013 (with modern authentication), [OneDrive sync client](/en-us/sharepoint/enable-conditional-access) | SharePoint Online | Windows 10 |
| Office 2016 (Word, Excel, PowerPoint, OneNote only). | SharePoint | macOS |
| Office 2019 | SharePoint | Windows 10, macOS |
| Office mobile apps | SharePoint | Android, iOS |
| Office Yammer app | Yammer | Windows 10, iOS, Android |
| Outlook 2019 | SharePoint | Windows 10, macOS |
| Outlook 2016 (Office for macOS) | Exchange Online | macOS |
| Outlook mobile app | Exchange Online | Android, iOS |
| Power BI app | Power BI service | Windows 10, Android, and iOS |
| Azure DevOps Services (formerly Visual Studio Team Services, or VSTS) app | Azure DevOps Services (formerly Visual Studio Team Services, or VSTS) | Windows 10, iOS, and Android |

Note

For Apple devices, as Microsoft Entra ID transitions the storage of device identity keys from Apple Keychain to Apple Secure Enclave, the Microsoft Enterprise SSO plug‑in for Apple devices must be enabled for applications that do not use the Microsoft Authentication Library (MSAL), including Safari. Enabling the Enterprise SSO plug‑in ensures that these applications can participate in device-based authentication required by Conditional Access policies, such as Require device to be marked as compliant and Filter for devices condition. For more information about this transition to Apple Secure Enclave, see [Microsoft Enterprise SSO plug‑in for Apple devices – Microsoft identity platform on Microsoft Learn](/en-us/entra/identity-platform/apple-sso-plugin#device-identity-key-storage)

### Exchange ActiveSync clients

- Admins can only select Exchange ActiveSync clients when assigning policy to users or groups. Selecting **All users**, **All guest and external users**, or **Directory roles** causes all users to be subject of the policy.
- When admins create a policy assigned to Exchange ActiveSync clients, **Exchange Online** should be the only cloud application assigned to the policy.
- Admins can narrow the scope of this policy to specific platforms using the **Device platforms** condition.

If the access control assigned to the policy uses **Require approved client app**, the user is directed to install and use the Outlook mobile client. In the case that **Multifactor authentication**, **Terms of use**, or **custom controls** are required, affected users are blocked, because basic authentication doesn’t support these controls.

For more information, see the following articles:

- [Block legacy authentication with Conditional Access](policy-block-legacy-authentication)
- [Requiring approved client apps with Conditional Access](policy-all-users-device-compliance)

### Other clients

By selecting **Other clients**, you can specify a condition that affects apps that use basic authentication with mail protocols like IMAP, MAPI, POP, SMTP, and older Office apps that don't use modern authentication.

## Device state (deprecated)

**This condition is deprecated.** Customers should use the **Filter for devices** condition in the Conditional Access policy to satisfy scenarios previously achieved using the device state condition.

Important

Device state and filters for devices can't be used together in Conditional Access policy. Filters for devices provide more granular targeting, including support for targeting device state information through the `trustType` and `isCompliant` property.

## Filter for devices

When admins configure filter for devices as a condition, they can include or exclude devices based on a filter using a rule expression on device properties. You can author the rule expression for filter for devices using the rule builder or rule syntax. This process is similar to the one used for rules for dynamic membership groups. For more information, see [Conditional Access: Filter for devices](concept-condition-filters-for-devices).

For agents' user accounts, this condition applies only when the agent session is initiated from an endpoint. Use it with the **Agent execution environments** condition when you need to target specific approved devices for agents running on endpoints.

## Authentication flows (preview)

Authentication flows control how your organization uses certain authentication and authorization protocols and grants. These flows can provide a seamless experience for devices that lack local input, such as shared devices or digital signage. Use this control to configure transfer methods like [device code flow or authentication transfer](concept-authentication-flows).