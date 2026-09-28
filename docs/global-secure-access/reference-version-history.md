---
layout: Conceptual
title: Microsoft Entra private network connector version release notes - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-version-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: This article lists all releases of Microsoft Entra private network connector and describes new features and fixed issues.
ms.topic: reference
ms.date: 2026-06-08T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 550780b6-52e1-e767-2645-18a90aab74ec
document_version_independent_id: 550780b6-52e1-e767-2645-18a90aab74ec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-version-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-version-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-version-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9ec7307f-9654-e973-1620-c75edad40ada
---

# Microsoft Entra private network connector version release notes - Global Secure Access | Microsoft Learn

## Overview

This article lists the versions and features of the Microsoft Entra private network connector. The Microsoft Entra ID team regularly updates the private network connector with new features and functionality. Look into the release notes for information on whether the connector version will be pushed for automatic update or available for download and manual update only.

Important

Microsoft Entra application proxy and Microsoft Entra Private Access use the private network connector.

Make sure that auto updates are enabled for your connectors to get the latest features and bug fixes. Microsoft Support might ask you to install the latest connector version to resolve a problem.

Here's a list of related resources:

| Resource | Details |
| --- | --- |
| How to enable application proxy | Prerequisites for enabling application proxy and installing and registering a connector are described in this [tutorial](../identity/app-proxy/application-proxy-add-on-premises-application). |
| Understand Microsoft Entra private network connectors | Find out more about [connector management](concept-connectors) and how connectors [autoupgrade](concept-connectors#connector-updates). |
| Microsoft Entra private network connector Download | [Download the latest connector](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download). |

## Version 1.5.4892.0

### Release status

June 8, 2026: Released for download. This version is only available for install via the download page in the Microsoft Entra admin center.

### New features and improvements

- Diagnostics tool added to system tray: New interactive diagnostics experience that validates endpoint connectivity (including customer-configured outbound proxies), checks service health, and collects logs from Windows Event Viewer.
- Improved connector logging and observability: Connector logs available in Windows Event Viewer; Audit events include agent identity information; and a remote feature flag allows log verbosity control without a connector update.
- Improved DNS resolution reliability: Invalid DNS response records are now filtered out, preventing spurious resolution failures in certain network environments.
- Fixed WebSocket connection leaks that could cause port exhaustion. Connections to unresponsive backends are now properly closed with a configurable timeout instead of lingering indefinitely.
- Fixed an issue where the connector's control channel listener could fail to initialize when specific features were disabled, causing the connector to not start.

## Version 1.5.4594.0

### Release status

December 19, 2025: Released for download. This version is only available for install via the download page in the Microsoft Entra admin center.

### New features and improvements

- Enhanced private access sensor telemetry

## Version 1.5.4522.0

### Release status

October 10, 2025: Released for download. Note that Microsoft Entra ID occasionally provides automatic updates for all the connectors that you deploy. This version may perform auto-upgrade of your connector. As long as the private network connector updater service is running, your connectors may update with this connector release automatically. If you don’t see the connector updater service on your server, you need to reinstall your connector manually to get updates. You can install via the download page in the Microsoft Entra admin center.

### New features and improvements

- New UI for the Connector Diagnostics Tool to assist with troubleshooting setup issues
- Improvements related to connection timeout and intermittent failure logging and mitigation
- Optimizations for improved streaming bandwidth and performance
- Improved collection of private access sensor telemetry
- Bug fixes and other minor improvements

## Version 1.5.4364.0

### Release status

June 25, 2025: Released for download. Note that Microsoft Entra ID occasionally provides automatic updates for all the connectors that you deploy. This version may perform auto-upgrade of your connector. As long as the private network connector updater service is running, your connectors may update with this connector release automatically. If you don’t see the connector updater service on your server, you need to reinstall your connector manually to get updates. You can install via the download page in the Microsoft Entra admin center.

### New features and improvements

- Updated connector signaling in GSA Private Access, increasing overall stability and responsiveness.
- Bug fixes and minor improvements to enhance stability and performance.

## Version 1.5.4287.0

### Release status

May 28, 2025: Released for download. This version is only available for install via the download page in the Microsoft Entra admin center.

### New features and improvements

- The connector now supports routing outbound traffic to destinations in Microsoft Entra Private Access through a forward proxy, enhancing network control.
- The connector includes a new diagnostics tool to assist with troubleshooting setup issues.
- Bug fixes and minor improvements.

## Version 1.5.3925.0

### Release status

July 3, 2024: Released for download. This version is only available for install via the download page in the Microsoft Entra admin center.

### New features and improvements

- Bug fixes and minor improvements

## Version 1.5.3890.0

### Release status

May 29, 2024: Released for download. This version is only available for install via the download page in the Microsoft Entra admin center.

### New features and improvements

- General Availability of support for outbound proxy for Private Access flows.
- Memory issue fix for application proxy flows.
- Miscellaneous bugs and logging improvements.

## Version 1.5.3829.0

### Release status

April 2, 2024: Released for download. This version is only available for install via the download page in the Microsoft Entra admin center.

### Updated brand

The new name is now the Microsoft Entra private network connector. The updated brand emphasizes the connector as a common infrastructure for accessing any private network resource. The connector is used for both Microsoft Entra Private Access and Microsoft Entra application proxy. The new name appears in the user interface components.

### New features and improvements

- Support for User Datagram Protocol (UDP) and Private Domain Name System (DNS) features for Private Access flow. \*Requires the Early Access Preview.
- Support for outbound proxy in connector for Private Access flow. \*Requires the Early Access Preview.
- Improved resiliency and performance.
- Improved logging and metrics reporting.

Note

A reboot is required when you install or upgrade the connector.

\*Submit request for onboarding to the Early Access Preview [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR9iJt1_k-HZBpNjGBIMz6XZUNzNSRjc2UlozUDNHT1dDNzI0Q1gxWVc1Sy4u).

Refer to the table for updated paths.

| Category | Old name | New name |
| --- | --- | --- |
| Installer file | `AADApplicationProxyConnectorInstaller.exe` | `MicrosoftEntraPrivateNetworkConnectorInstaller.exe` |
| Install location | `C:\Program Files\Microsoft AAD App Proxy Connector` | `C:\Program Files\Microsoft Entra private network connector` |
|  | `C:\Program Files\Microsoft AAD App Proxy Connector\Modules\AppProxyPSModule` | `C:\Program Files\Microsoft Entra private network connector\Modules\MicrosoftEntraPrivateNetworkConnectorPSModule` |
|  | `C:\Program Files\Microsoft AAD App Proxy Connector Updater` | `C:\Program Files\Microsoft Entra private network connector Updater` |
|  | `C:\ProgramData\Microsoft\Microsoft AAD Application Proxy Connector` | `C:\ProgramData\Microsoft\Microsoft Entra private network connector` |
| Application | `ApplicationProxyConnectorService.exe` | `MicrosoftEntraPrivateNetworkConnectorService.exe` |
|  | `ApplicationProxyConnectorUpdaterService.exe` | `MicrosoftEntraPrivateNetworkConnectorUpdaterService.exe` |
| CONFIG file | `ApplicationProxyConnectorService.exe.config` | `MicrosoftEntraPrivateNetworkConnectorService.exe.config` |
|  | `ApplicationProxyConnectorUpdaterService.exe.config` | `MicrosoftEntraPrivateNetworkConnectorUpdaterService.exe.config` |
| PowerShell module | `AppProxyPSModule.psd1` | `MicrosoftEntraPrivateNetworkConnectorPSModule.psd1` |
| PowerShell command | `Register-AppProxyConnector` | `Register-MicrosoftEntraPrivateNetworkConnector` |
| Log file | `AadAppProxyConnector_{GUID}.log` | `MicrosoftEntraPrivateNetworkConnector_{GUID}.log` |
|  | `AadAppProxyConnectorUpdater_{GUID}.log` | `MicrosoftEntraPrivateNetworkConnectorUpdater_{GUID}.log` |
| Services | `Microsoft AAD Application Proxy Connector` | `Microsoft Entra private network connector` |
|  | `Microsoft AAD Application Proxy Connector Updater` | `Microsoft Entra private network connector updater` |
| Registries | `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft AAD App Proxy Connector` | `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Entra private network connector` |
|  | `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft AAD App Proxy Connector Updater` | `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Entra private network connector Updater` |
| Event logs | `Microsoft-AadApplicationProxy-Connector/Admin` | `Microsoft-Microsoft Entra private network-Connector/Admin` |
|  | `Microsoft-AadApplicationProxy-Updater/Admin` | `Microsoft-Microsoft Entra private network-Updater/Admin` |

Important

**.NET Framework**

You must have .NET version 4.7.2 or higher to install, or upgrade, application proxy version 1.5.3437.0 or later. Windows Server 2012 R2 and Windows Server 2016 do not have this by default. For more information, see [How to: Determine which .NET Framework versions are installed](/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed).

## Version 1.5.3437.0

### Release status

June 20, 2023: Released for download. This version is only available for install via the download page.

### New features and improvements

- Updated partner notices.

### Fixed issues

- Silent registration of connector with credentials. For more information, see [Create an unattended installation script for the Microsoft Entra private network connector](how-to-register-connector-powershell).
- Fixed dropping of `Secure` and `HttpOnly` attributes on the cookies passed by backend servers when there are trailing spaces in these attributes.
- Fixed services crash when back-end server of an application sets "Set-Cookie" header with empty value.

Important

**.NET Framework**

You must have .NET version 4.7.2 or higher to install, or upgrade, application proxy version 1.5.3437.0 or later. Windows Server 2012 R2 and Windows Server 2016 may not have this by default. For more information, see [How to: Determine which .NET Framework versions are installed](/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed).

## Version 1.5.2846.0

### Release status

March 22, 2022: Released for download. This version is only available for install via the download page.

### New features and improvements

- Increased the number of HTTP headers supported on HTTP requests from 41 to 60.
- Improved error handling of TLS failures between the connector and Azure services.
- Updated the default connection limit to 200 for connector traffic when going through outbound proxy. For more information about outbound proxy, see [Work with existing on-premises proxy servers](../identity/app-proxy/application-proxy-configure-connectors-with-proxy-servers#use-the-outbound-proxy-server).
- Deprecated the use of Active Directory Authentication Library (ADAL) and implemented Microsoft Authentication Library (MSAL) as part of the connector installation flow.

### Fixed issues

- Return original error code and response instead of a 400 Bad Request code for failing websocket connect attempts.

## Version 1.5.1975.0

### Release status

July 22, 2020: Released for download. This version is only available for install via the download page.

### New features and improvements

- Improved support for Azure Government cloud environments. For steps on how to properly install the connector for Azure Government cloud review the [prerequisites](../identity/hybrid/connect/reference-connect-government-cloud#allow-access-to-urls) and [installation steps](../identity/hybrid/connect/reference-connect-government-cloud#install-the-agent-for-the-azure-government-cloud).
- Support for using the Remote Desktop Services web client with application proxy. For more information, see [Publish Remote Desktop with Microsoft Entra application proxy](../identity/app-proxy/application-proxy-integrate-with-remote-desktop-services).
- Improved websocket extension negotiations.
- Support for optimized routing between connector groups and application proxy cloud services based on region. For more information, see [Optimize traffic flow with Microsoft Entra application proxy](../identity/app-proxy/application-proxy-network-topology).

### Fixed issues

- Fixed a websocket issue that forced lowercase strings.
- Fixed an issue that caused connectors to be occasionally unresponsive.

## Version 1.5.1626.0

### Release status

July 17, 2020: Released for download. This version is only available for install via the download page.

### Fixed issues

- Resolved memory leak issues present in previous version.
- Completed general improvements for websocket support.

## Version 1.5.1526.0

### Release status

April 07, 2020: Released for download. This version is only available for install via the download page.

### New features and improvements

- Connectors only use Transport Layer Security (TLS) 1.2 for all connections. For more information, see [connector prerequisites](../identity/app-proxy/application-proxy-add-on-premises-application#prerequisites).
- Improved signaling between the connector and Azure services. The signaling supports reliable sessions for Windows Communication Foundation (WCF) communication between the connector and Azure services and Domain Name System (DNS) caching improvements for WebSocket communications.
- Support for configuring a proxy between the connector and the backend application. For more information, see [Work with existing on-premises proxy servers](../identity/app-proxy/application-proxy-configure-connectors-with-proxy-servers).

### Fixed issues

- Removed falling back to port 8080 for communications from the connector to Azure services.
- Added debug traces for WebSocket communications.
- Resolved preserving the SameSite attribute when set on backend application cookies.

## Unsupported versions

If you're using a private network connector version 1.5.612.0 or earlier, immediately update to a newer version to ensure you have the latest fully supported features.

## Version 1.5.612.0 (Deprecated)

### Release status

September 20, 2018: Released for download.

### New features and improvements

- Added WebSocket support for the QlikSense application. For more information about how to integrate QlikSense with application proxy, see this [walkthrough](../identity/app-proxy/application-proxy-qlik).
- Improved the installation wizard to make it easier to configure an outbound proxy.
- Set TLS 1.2 as the default protocol for connectors.
- Added a new End-User License Agreement (EULA).

### Fixed issues

- A bug that caused memory leaks in the connector was fixed.
- Azure Service Bus version updated, which includes a bug fix for connector timeout issues.

## Version 1.5.402.0 (Deprecated)

### Release status

January 19, 2018: Released for download.

### Fixed issues

- Added support for custom domains that need domain translation in the cookie.

## Version 1.5.132.0 (Deprecated)

### Release status

May 25, 2017: Released for download.

### New features and improvements

Improved control over connectors' outbound connection limits.

## Version 1.5.36.0 (Deprecated)

### Release status

April 15, 2017: Released for download.

### New features and improvements

- Simplified onboarding and management with fewer required ports. Application proxy now requires opening only two standard outbound ports: 443 and 80. Application proxy continues to use only outbound connections, so you still don't need any components in a public facing network. For more information, see our [configuration documentation](../identity/app-proxy/application-proxy-add-on-premises-application).
- If supported by your external proxy or firewall, you can now open your network by DNS instead of IP range. Application proxy services require connections to `*.msappproxy.net` and `*.servicebus.windows.net` only.