---
layout: Conceptual
title: 'Conditional Access Policy: Using Network Signals - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-assignment-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Discover how to configure Conditional Access policies with network-based signals, including trusted locations, IP ranges, and GPS-based settings.
ms.topic: concept-article
ms.date: 2026-04-01T00:00:00.0000000Z
ms.reviewer: lhuangnorth, inbarc
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2e67c377-d615-8779-b3f9-420fc4efd81d
document_version_independent_id: 3bcdc8e6-2ab6-5c62-dd5c-cc9a024f3428
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-assignment-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-assignment-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-assignment-network.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 316c32b9-30ac-e939-8c98-20a695ce3ad2
---

# Conditional Access Policy: Using Network Signals - Microsoft Entra ID | Microsoft Learn

## Overview

Admins can create policies that target specific network locations as a signal along with other conditions in their decision making process. They can include or exclude these network locations as part of their policy configuration. These network locations might include public IPv4 or IPv6 network information, countries or regions, unknown areas that don't map to specific countries or regions, or [Global Secure Access compliant network](../../global-secure-access/how-to-compliant-network).

[![Diagram showing Conditional Access signals and the decision to enforce organizational policy.](media/common-conditional-access-media/conditional-access-signal-decision-enforcement.png)](media/common-conditional-access-media/conditional-access-signal-decision-enforcement.png#lightbox)

Note

Conditional Access policies are enforced after first-factor authentication is complete. Conditional Access isn't intended to be an organization's front line of defense for scenarios like denial of service (DoS) attacks, but it can use signals from these events to determine access.

Organizations might use these locations for common tasks, such as:

- Requiring multifactor authentication for users accessing a service when they're off the corporate network.
- Blocking access from specific countries your organization never operates from.

A user's location is determined using their public IP address or the GPS coordinates provided by the Microsoft Authenticator app. Conditional Access policies apply to all locations by default.

Tip

The **Location** condition moved and was renamed **Network**. Initially, this condition appears at both the **Assignment** level and under **Conditions**.

Updates or changes appear in both locations. The functionality remains the same, and existing policies using **Location** continue to work without changes.

[![Screenshot showing the network assignment condition in a Conditional Access policy.](media/concept-assignment-network/network-assignment.png)](media/concept-assignment-network/network-assignment.png#lightbox)

## When configured in policy

When you configure the location condition, you can distinguish between:

- Any network or location
- All trusted networks and locations
- All Compliant Network locations
- Selected networks and locations

### Any network or location

Selecting **Any location** applies a policy to all IP addresses, including any address on the internet. This setting isn't limited to IP addresses you set up as named locations. When you select **Any location**, you can exclude specific locations from a policy. For example, apply a policy to all locations except trusted locations to limit the scope to locations outside the corporate network.

### All trusted networks and locations

This option applies to:

- All locations marked as trusted locations.
- Multifactor authentication trusted IPs, if configured.

#### Multifactor authentication trusted IPs

Using the trusted IPs section of multifactor authentication's service settings isn't recommended. This control accepts only IPv4 addresses and is designed for specific scenarios covered in the article [Configure Microsoft Entra multifactor authentication settings](../authentication/howto-mfa-mfasettings#trusted-ips).

If you have these trusted IPs configured, they show up as **MFA Trusted IPs** in the list of locations for the location condition.

### All Compliant Network locations

Organizations with access to Global Secure Access features see another location listed, consisting of users and devices that comply with your organization's security policies. For more information, see [Enable Global Secure Access signaling for Conditional Access](/en-us/entra/global-secure-access/how-to-compliant-network#enable-global-secure-access-signaling-for-conditional-access). Use it with Conditional Access policies to perform a compliant network check for access to resources.

### Selected networks and locations

With this option, select one or more named locations. For a policy with this setting to apply, a user must connect from one of the selected locations. When you choose **Select**, a list of defined locations opens. This list shows the name, type, and whether the network location is marked as trusted.

## How are these locations defined?

Locations are in the [Microsoft Entra admin center](https://entra.microsoft.com) under **Entra ID** &gt; **Conditional Access** &gt; **Named locations**. Admins with at least the [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) role can create and update named locations.

[![Screenshot of named locations in the Microsoft Entra admin center.](media/concept-assignment-network/named-locations.png)](media/concept-assignment-network/named-locations.png#lightbox)

Named locations might include an organization's headquarters network ranges, VPN network ranges, or ranges you want to block. Named locations contain IPv4 address ranges, IPv6 address ranges, or countries.

### IPv4 and IPv6 address ranges

To define a named location by public IPv4 or IPv6 address ranges, provide:

- A **Name** for the location.
- One or more public IP ranges.
- Optionally **Mark as trusted location**.

Note

IPv6 addresses must be entered in CIDR notation. For example:

- Single IPv6 address: `2001:db8::1/128`
- IPv6 subnet range: `2001:db8:abcd:0012::/64` IPv6 ranges represent a block of public addresses and follow standard IPv6 CIDR formatting.

Named locations defined by IPv4 or IPv6 address ranges have the following limitations:

- No more than 195 named locations.
- No more than 2000 IP ranges per named location.
- Only CIDR masks greater than /8 are allowed when defining an IP range.

For devices on a private network, the IP address isn't the client IP of the user’s device on the intranet (like 10.55.99.3), it's the address used by the network to connect to the public internet (like 198.51.100.3).

#### Trusted locations

Admins can mark IP-based locations, like your organization's public network ranges, as trusted. This marking is used by features in several ways.

- Conditional Access policies can include or exclude these locations.
- Sign-ins from trusted named locations improve the accuracy of Microsoft Entra ID Protection's risk calculation.

Locations marked as trusted can't be deleted without first removing the trusted designation.

### Countries

Organizations can determine a geographic country or region location by IP address or GPS coordinates.

To define a named location by country or region, do the following:

- Provide a **Name** for the location.
- Choose to determine location by IP address or GPS coordinates.
- Add one or more countries/regions.
- Optionally choose to **Include unknown countries/regions**.

[![Screenshot of creating a new location using countries.](media/concept-assignment-network/new-location-countries.png)](media/concept-assignment-network/new-location-countries.png#lightbox)

When selecting **Determine location by IP address**, Microsoft Entra ID resolves the user's IPv4 or [IPv6](/en-us/troubleshoot/azure/active-directory/azure-ad-ipv6-support) address to a country or region, based on a periodically updated mapping table.

To use **Determine location by GPS coordinates**, users need the Microsoft Authenticator app installed on their mobile device. Every hour, the system contacts the user’s Microsoft Authenticator app to collect the GPS location of their mobile device.

- The first time the user must share their location from the Microsoft Authenticator app, they receive a notification in the app. The user must open the app and grant location permissions. For the next 24 hours, if the user is still accessing the resource and granted the app permission to run in the background, the device's location is shared silently once per hour.
- After 24 hours, the user must open the app and approve the notification.
- Every time the user shares their GPS location, the app does jailbreak detection using the same logic as the Microsoft Intune MAM SDK. If the device is jailbroken, the location isn't considered valid, and the user isn't granted access.
    - The Microsoft Authenticator app on Android uses the Google Play Integrity API to facilitate jailbreak detection. If the Google Play Integrity API is unavailable, the request is denied and the user isn't able to access the requested resource unless the Conditional Access policy is disabled. For more information about the Microsoft Authenticator app, see the article [Common questions about the Microsoft Authenticator app](https://support.microsoft.com/account-billing/common-questions-about-the-microsoft-authenticator-app-12d283d1-bcef-4875-9ae5-ac360e2945dd).
- Users can modify the GPS location as reported by iOS and Android devices. As a result, the Microsoft Authenticator app denies authentications where the user might be using a different location than the actual GPS location of the mobile device where the app is installed. Users who modify the location of their device get a denial message for GPS location-based policies.
- The country code returned depends on the device platform API: For example one platform might report US for Puerto Rico, while another reports PR.

Note

A Conditional Access policy with GPS-based named locations in report-only mode prompts users to share their GPS location, not sharing this information may result in a block.

GPS location can be used with [passwordless phone sign-in](../authentication/concept-authentication-authenticator-app) only if MFA push notifications are also enabled. Users can use Microsoft Authenticator to sign in, but they also need to approve subsequent MFA push notifications to share their GPS location.

GPS location doesn't work when only [passwordless authentication methods](../authentication/concept-authentication-passkeys-fido2) are set.

Multiple Conditional Access policies might prompt users for their GPS location before all are applied. Because of the way Conditional Access policies are applied, a user might be denied access if they pass the location check but fail another policy. For more information about policy enforcement, see the article [Building a Conditional Access policy](concept-conditional-access-policies).

Important

Users might receive prompts every hour letting them know that Microsoft Entra ID is checking their location in the Authenticator app. This feature should only be used to protect very sensitive apps where this behavior is acceptable or where access must be restricted for a specific country/region.

#### Include unknown countries/regions

Some IP addresses can't be mapped to a specific country or region. To capture these IP locations, select the box **Include unknown countries/regions** when defining a geographic location. This option allows you to choose if these IP addresses should be included in the named location. Use this setting when the policy using the named location should apply to unknown locations.

## Restore deleted locations

If a Conditional Access policy or location is deleted, it can be restored within the 30 day soft-delete period. For more information about restoring Conditional Access policies and named locations, see the article [Recover from deletions](../../architecture/recover-from-deletions#conditional-access-policies).

## Common questions

### Is there Graph API support

Graph API support for named locations is available. For more information, see the [namedLocation API](/en-us/graph/api/resources/namedlocation).

### What if I use a cloud proxy or VPN

When you use a cloud-hosted proxy or VPN solution, the IP address Microsoft Entra ID uses while evaluating a policy is the IP address of the proxy. The X-Forwarded-For (XFF) header, which contains the user’s public IP address, isn't used because there's no validation that it comes from a trusted source. This lack of validation could allow faking an IP address.

When a cloud proxy is in place, a policy that requires a [Microsoft Entra hybrid joined or compliant device](policy-alt-all-users-compliant-hybrid-or-mfa#create-a-conditional-access-policy) can be easier to manage. Keeping an up-to-date list of IP addresses used by your cloud-hosted proxy or VPN solution is nearly impossible.

We recommend organizations utilize Global Secure Access to enable [source IP restoration](/en-us/entra/global-secure-access/how-to-source-ip-restoration) to avoid this change in address and simplify management.

### When is a location evaluated

Conditional Access policies are evaluated when:

- A user initially signs in to a web app, mobile or desktop application.
- A mobile or desktop application that uses modern authentication, uses a refresh token to acquire a new access token. By default, this check occurs once an hour.

This check means for mobile and desktop applications using modern authentication, a change in location is detected within an hour of changing the network location. For mobile and desktop applications that don’t use modern authentication, the policy applies on each token request. The frequency of the request can vary based on the application. Similarly, for web applications, policies apply at initial sign-in and are good for the lifetime of the session at the web application. Because of differences in session lifetimes across applications, the time between policy evaluation varies. Each time the application requests a new sign-in token, the policy is applied.

By default, Microsoft Entra ID issues tokens hourly. After users move off the corporate network, within an hour the policy is enforced for applications using modern authentication.

### When you might block locations

A policy that uses the location condition to block access is considered restrictive, and should be done with care after thorough testing. Some instances of using the location condition to block authentication might include:

- Blocking countries/regions where your organization never does business.
- Blocking specific IP ranges, such as the following:
    - Known malicious IPs before a firewall policy can be changed.
    - Highly sensitive or privileged actions and cloud applications.
    - Based on user specific IP range like access to accounting or payroll applications.