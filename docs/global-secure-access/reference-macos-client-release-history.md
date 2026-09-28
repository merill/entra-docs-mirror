---
layout: Conceptual
title: Global Secure Access Client for macOS Release Notes - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-macos-client-release-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: This article tracks the release notes and download instructions for the Global Secure Access client for macOS.
ms.topic: reference
ms.date: 2026-08-21T00:00:00.0000000Z
ms.reviewer: lirazbarak
ms.custom: msecd-doc-authoring-1024
ai-usage: ai-assisted
locale: en-us
document_id: ec95de65-8dc2-aca0-ab10-f22eb417fe43
document_version_independent_id: ec95de65-8dc2-aca0-ab10-f22eb417fe43
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-macos-client-release-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-macos-client-release-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-macos-client-release-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
platformId: 844aa622-9cb9-42f7-edda-e77cfdf2f17d
---

# Global Secure Access Client for macOS Release Notes - Global Secure Access | Microsoft Learn

This article lists the released versions of the Global Secure Access client for macOS and the changes in each version.

## Download the latest version

You can download the current version of the Global Secure Access client from the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Client download**.
3. Select the **macOS** tab.
4. Select **Download Client**. ![Screenshot of the client download screen with the Download Client button highlighted.](media/reference-macos-client-release-history/macos-client-download-screen.png)

## Version 1.1.26060207

Released for download on August 24, 2026.

### Functional changes

- Added support for controlling traffic to the Home Network.
- Added a new **Connections** page.
- Added agentic detection support, which enables security policies on agent traffic.

### Other changes

- Improved internet connectivity checks.
- Added support for Secure DNS bypass.
- Addressed MSAL sign-in issues.
- The app package now includes the `com.microsoft.autoupdate2` application. You can optionally remove `com.microsoft.autoupdate2` from the Intune detection rules when deploying the app.
- Fixed an issue that prevented policies from being cleared during a cache reset.
- Fixed a crash during client restarts.
- Fixed a partial connection issue with the macOS 27 beta build.
- Fixed an issue that prevented the tunnel from being established when a device woke or was unlocked.

## Version 1.1.26030604

Released for download on June 05, 2026.

### Functional changes

- Optimized acquisition for Teams and OneDrive traffic.

### Other changes

- Fix for crash when disabling private access after cleaning the client's cache.
- Fix for an issue when sharing iPhone hotspot.

## Version 1.1.26030601

Released for download on April 16, 2026.

### Functional changes

- Optimizes Intelligent Local Access (ILA) detection by reevaluating the connection status to private networks on each network change.

### Other changes

- Accessibility improvements.
- Memory management improvements.
- Miscellaneous bug fixes and improvements.

## Version 1.1.25111702

Released for download on February 5, 2026.

### Functional changes

- Supports Intelligent Local Access (preview).
- Supports contacting Private DNS only when the Private Access channel is active.

### Other changes

- Memory management improvements.
- Miscellaneous bug fixes and improvements.

## Version 1.1.25090800

Released for download on November 24, 2025.

### Other changes

- Bug fix: Better recovery of the connection to the Global Secure Access cloud service when a device switches between networks.
- Bug fix: Mutual Transport Layer Security (mTLS) connections to the Global Secure Access cloud service use the correct certificate after renewal.
- Bug fix: Web page translation in Microsoft Edge browser is fully functional.
- Bug fix: DNS queries for service (SRV) records in public DNS servers are supported.
- Enhanced telemetry for better supportability and monitoring.
- Miscellaneous bug fixes and improvements.

## Version 1.1.25070402

Released for download on August 19, 2025.

### Other changes

- Bug fix: Fixes a compatibility issue with macOS 26.

Important

To maintain functionality, deploy version **1.1.25070402** of the client *before* upgrading to macOS 26.

- The installer now includes a stapled notarization ticket, so macOS can verify its integrity and avoid security warnings during offline installation.

## Version 1.1.25070401

Released for download on July 29, 2025.

### Functional changes

- First version in general availability.
- Bug fix: Provides better support for large forwarding profiles.
- Supports log collection with a script.
- Increases the client's log file size to allow for more comprehensive logging.

### Other changes

- Bug fix: Implements a workaround for Dynamic Host Configuration Protocol (DHCP) failures seen in macOS 15.4 and later because of a change in macOS.
- Bug fix: Avoids repeated, unnecessary certificate signing requests.
- Enhanced telemetry for better supportability and monitoring.
- Miscellaneous bug fixes and improvements.

### Known issues

- Client version **1.1.25070401** has a known compatibility issue with macOS 26 that causes the device to lose connectivity. To maintain compatibility with macOS 26, upgrade to and deploy client version **1.1.25070402** before upgrading to macOS 26.

## Version 1.1.25060400

Released for download on June 24, 2025.

### Important changes for deployment with Mobile Device Management (MDM)

- The distribution profile identifiers changed:
    - Previous: `com.microsoft.naas.globalsecure-df` → New: `com.microsoft.globalsecureaccess`
    - Previous: `com.microsoft.naas.globalsecure.tunnel-df` → New: `com.microsoft.globalsecureaccess.tunnel`
- Special upgrade instructions apply when moving from version **1.1.584.1** (or older) to version **1.1.25060400**(or newer):
    1. Exclude macOS devices you want to upgrade from MDM policies that distribute previous client versions to avoid side-by-side installations, which can break client behavior.
    2. Deploy MDM policies to automatically [allow system extensions](how-to-install-macos-client#allow-system-extensions-through-mobile-device-management-mdm) and [allow transparent app proxy](how-to-install-macos-client#allow-transparent-application-proxy-through-mdm).
    3. Follow the updated instructions for the new identifiers:
        - `com.microsoft.globalsecureaccess`
        - `com.microsoft.globalsecureaccess.tunnel`
    4. Create a new policy to install the new client version.
    5. Remove any old policies that allow system extensions and filtering app proxy with deprecated identifiers.
- Future versions keep the new distribution profile identifiers unless otherwise noted.
- You don't need the special upgrade procedure when upgrading from a version newer than **1.1.584.1** because those versions already use the new identifiers.

### Functional changes

- Support for mTLS connections to Global Secure Access.

Note

The mTLS connection rolls out gradually to customers through the cloud service. Customers continue to use the Transport Layer Security (TLS) connection until they receive mTLS.

- Telemetry collection is enabled.
- The new UI includes a link to Microsoft's privacy policy to comply with the telemetry collection policy.
- An uninstaller application is added for easy removal of the Global Secure Access client as an alternative to the uninstall script.
- Option to disable Private Access, letting users access private applications directly through the corporate network.
- Client disable-state doesn't persist after a restart; the client automatically re-enables after a restart.
- Support for Continuous Access Evaluation (CAE) in Global Secure Access client authentication.
- Accessibility improvements for the Advanced Diagnostics tool and main window.
- Bug fix: Canonical name (CNAME) records now resolve correctly (previously resolved as A records).
- Bug fix: Resolves connectivity issues when resuming from sleep.

### Other changes

- The client version format now uses the build date. Older versions might have higher numerical values than newer ones, but future versions increment numerically.
- Bug fix: Logging network trace is now disabled by default to optimize performance.
- Improvements and bug fixes for Advanced diagnostics.
- Miscellaneous bug fixes and improvements.

## Version 1.1.584

Released for download on November 18, 2024.

### Functional changes

- First public preview version.