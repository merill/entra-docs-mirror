---
layout: Conceptual
title: Password protection agent release history - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-agent-versions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Documents version release and behavior change history
ms.topic: release-notes
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: jsimmons
locale: en-us
document_id: 1f20b22c-e31c-67df-cea1-9a39bcbe6788
document_version_independent_id: 158dbe00-1ca1-085c-be81-01a7cadfd082
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-password-ban-bad-on-premises-agent-versions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-password-ban-bad-on-premises-agent-versions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-password-ban-bad-on-premises-agent-versions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 24b72159-e0d4-2606-67de-847edd42c5d6
---

# Password protection agent release history - Microsoft Entra ID | Microsoft Learn

To download the most recent version, see [Microsoft Entra Password Protection for Windows Server Active Directory](https://www.microsoft.com/download/details.aspx?id=57071).

## 1.2.177.1

Release date: March 28, 2022

- Fixed software version being incorrect

## 1.2.177.0

Release date: March 14, 2022

- Minor bugfixes
- Fixed issue with Microsoft Entra Connect Agent Updater not being updated

## 1.2.176.0

Release date: June 4, 2021

- Minor bugfixes to issues which prevented the proxy and DC agents from running successfully in certain environments.

## 1.2.172.0

Release date: February 22, 2021

It has been almost two years since the GA versions of the on-premises Microsoft Entra Password Protection agents were released. A new update is now available - see change descriptions below. Thank you to everyone who has given us feedback on the product.

- The DC agent and Proxy agent software both now require .NET 4.7.2 to be installed.
    - If .NET 4.7.2 is not already installed, download and run the installer found at [The .NET Framework 4.7.2 offline installer for Windows](https://support.microsoft.com/topic/microsoft-net-framework-4-7-2-offline-installer-for-windows-05a72734-2127-a15d-50cf-daf56d5faec2).
- The AzureADPasswordProtection PowerShell module is now also installed by the DC agent software.
- Two new health-related PowerShell cmdlets have been added: Test-AzureADPasswordProtectionDCAgent and Test-AzureADPasswordProtectionProxy.
- The AzureADPasswordProtection DC Agent password filter dll will now load and run on machines where lsass.exe is configured to run in PPL mode.
- Bug fix to password algorithm that allowed banned passwords fewer than five characters in length to be incorrectly accepted.
    - This bug is only applicable if your on-premises AD minimum password length policy was configured to allow fewer than five character passwords in the first place.
- Other minor bug fixes.

The new installers will automatically upgrade older versions of the software. If you have installed both the DC agent and the Proxy software on a single machine (only recommended for test environments), you must upgrade both at the same time.

It is supported to run older and newer versions of the DC agent and proxy software within a domain or forest, although we recommend upgrading all agents to the latest version as a best practice. Any ordering of agent upgrades is supported - new DC agents can communicate through older Proxy agents, and older DC agents can communicate through newer Proxy agents.

## 1.2.125.0

Release date: March 2, 2019

- Fix minor typo errors in event log messages
- Update EULA agreement to final General Availability version

Note

Build 1.2.125.0 is the General Availability build. Thank you again to everyone has provided feedback on the product!

## 1.2.116.0

Release date: March 3, 2019

- The Get-AzureADPasswordProtectionProxy and Get-AzureADPasswordProtectionDCAgent cmdlets now report software version and the current Azure tenant with the following limitations:
    - Software version and Azure tenant data are only available for DC agents and proxies running version 1.2.116.0 or later.
    - Azure tenant data may not be reported until a re-registration (or renewal) of the proxy or forest has occurred.
- The Proxy service now requires that .NET 4.7 is installed.
    - If .NET 4.7 is not already installed, download and run the installer found at [The .NET Framework 4.7 offline installer for Windows](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows).
    - On Server Core systems, it may be necessary to pass the /q flag to the .NET 4.7 installer to get it to succeed.
- The Proxy service now supports automatic upgrade. Automatic upgrade uses the Microsoft Entra Connect Agent Updater service, which is installed side by side with the Proxy service. Automatic upgrade is on by default.
- Automatic upgrade can be enabled or disabled using the Set-AzureADPasswordProtectionProxyConfiguration cmdlet. The current setting can be queried using the Get-AzureADPasswordProtectionProxyConfiguration cmdlet.
- The service binary for the DC agent service has been renamed to AzureADPasswordProtectionDCAgent.exe.
- The service binary for the Proxy service has been renamed to AzureADPasswordProtectionProxy.exe. Firewall rules may need to be modified accordingly if a third-party firewall is in-use.
    - NOTE: if an http proxy config file was being used in a previous Proxy install, it will need to be renamed (from *proxyservice.exe.config* to *AzureADPasswordProtectionProxy.exe.config*) after this upgrade.
- All time-limited functionality checks have been removed from the DC agent.
- Minor bugs fixes and logging improvements.

## 1.2.65.0

Release date: February 1, 2019

Changes:

- DC agent and proxy service are now supported on Server Core. Minimum OS requirements are unchanged from before: Windows Server 2012 for DC agents, and Windows Server 2012 R2 for proxies.
- The Register-AzureADPasswordProtectionProxy and Register-AzureADPasswordProtectionForest cmdlets now support device-code-based Azure authentication modes.
- The Get-AzureADPasswordProtectionDCAgent cmdlet will ignore mangled and/or invalid service connection points. This change fixes the bug where domain controllers would sometimes show up multiple times in the output.
- The Get-AzureADPasswordProtectionSummaryReport cmdlet will ignore mangled and/or invalid service connection points. This change fixes the bug where domain controllers would sometimes show up multiple times in the output.
- The Proxy PowerShell module is now registered from %ProgramFiles%\WindowsPowerShell\Modules. The machine's PSModulePath environment variable is no longer modified.
- A new Get-AzureADPasswordProtectionProxy cmdlet has been added to aid in discovering registered proxies in a forest or domain.
- The DC agent uses a new folder in the sysvol share for replicating password policies and other files.

    Old folder location:

    `\\<domain>\sysvol\<domain fqdn>\Policies\{4A9AB66B-4365-4C2A-996C-58ED9927332D}`

    New folder location:

    `\\<domain>\sysvol\<domain fqdn>\AzureADPasswordProtection`

    (This change was made to avoid false-positive "orphaned GPO" warnings.)

    Note

    No migration or sharing of data will be done between the old folder and the new folder. Older DC agent versions will continue to use the old location until upgraded to this version or later. Once all DC agents are running version 1.2.65.0 or later, the old sysvol folder may be manually deleted.
- The DC agent and proxy service will now detect and delete mangled copies of their respective service connection points.
- Each DC agent will periodically delete mangled and stale service connection points in its domain, for both DC agent and proxy service connection points. Both DC agent and proxy service connection points are considered stale if its heartbeat timestamp is older than seven days.
- The DC agent will now renew the forest certificate as needed.
- The Proxy service will now renew the proxy certificate as needed.
- Updates to password validation algorithm: the global banned password list and customer-specific banned password list (if configured) are combined prior to password validations. A given password may now be rejected (fail or audit-only) if it contains tokens from both the global and customer-specific list. The event log documentation has been updated to reflect this; see [Monitor Microsoft Entra Password Protection](howto-password-ban-bad-on-premises-monitor).
- Performance and robustness fixes
- Improved logging

Warning

Time-limited functionality: the DC agent service in this release (1.2.65.0) will stop processing password validation requests as of September 1st 2019. DC agent services in prior releases (see list below) will stop processing as of July 1st 2019. The DC agent service in all versions will log 10021 events to the Admin event log in the two months leading up these deadlines. All time-limit restrictions will be removed in the upcoming GA release. The Proxy agent service is not time-limited in any version but should still be upgraded to the latest version in order to take advantage of all subsequent bug fixes and other improvements.

## 1.2.25.0

Release date: November 1, 2018

Fixes:

- DC agent and proxy service should no longer fail due to certificate trust failures.
- DC agent and proxy service have fixes for FIPS-compliant machines.
- Proxy service will now work properly in a TLS 1.2-only networking environment.
- Minor performance and robustness fixes
- Improved logging

Changes:

- The minimum required OS level for the Proxy service is now Windows Server 2012 R2. The minimum required OS level for the DC agent service remains at Windows Server 2012.
- The Proxy service now requires .NET version 4.6.2.
- The password validation algorithm uses an expanded character normalization table. This change may result in passwords being rejected that were accepted in prior versions.

## 1.2.10.0

Release date: August 17, 2018

Fixes:

- Register-AzureADPasswordProtectionProxy and Register-AzureADPasswordProtectionForest now support multi-factor authentication
- Register-AzureADPasswordProtectionProxy requires a WS2012 or later domain controller in the domain to avoid encryption errors.
- DC agent service is more reliable about requesting a new password policy from Azure on startup.
- DC agent service will request a new password policy from Azure every hour if necessary, but will now do so on a randomly selected start time.
- DC agent service will no longer cause an indefinite delay in new DC advertisement when installed on a server prior to its promotion as a replica.
- DC agent service will now honor the “Enable password protection on Windows Server Active Directory” configuration setting
- Both DC agent and proxy installers will now support in-place upgrade when upgrading to future versions.

Warning

In-place upgrade from version 1.1.10.3 is not supported and will result in an installation error. To upgrade to version 1.2.10 or later, you must first completely uninstall the DC agent and proxy service software, then install the new version from scratch. Re-registration of the Microsoft Entra password protection Proxy service is required. It is not required to re-register the forest.

Note

In-place upgrades of the DC agent software will require a reboot.

- DC agent and proxy service now support running on a server configured to only use FIPS-compliant algorithms.
- Minor performance and robustness fixes
- Improved logging

## 1.1.10.3

Release date: June 15, 2018

Initial public preview release