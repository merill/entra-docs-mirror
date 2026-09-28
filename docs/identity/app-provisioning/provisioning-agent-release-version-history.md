---
layout: Conceptual
title: Microsoft Entra Connect Provisioning Agent - Version release history - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/provisioning-agent-release-version-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This article lists all releases of Microsoft Entra Connect Provisioning Agent and describes new features and fixed issues.
ms.topic: reference
ms.date: 2026-04-14T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
locale: en-us
document_id: 2dda8f8c-500e-3c63-9133-0a7f3b8b118d
document_version_independent_id: 26a9b4bc-5e0f-d8b9-b284-827665fa24e5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/provisioning-agent-release-version-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/provisioning-agent-release-version-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/provisioning-agent-release-version-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 57534474-56e0-3bce-6237-849d604306c2
---

# Microsoft Entra Connect Provisioning Agent - Version release history - Microsoft Entra ID | Microsoft Learn

This article lists the versions and features of Microsoft Entra provisioning agent releases. The Microsoft Entra team regularly updates the Provisioning Agent with new features and functionality.

Note

All new Provisioning Agent releases are made available for download through the Microsoft Entra admin center and only specific releases are pushed for auto upgrade.

Note

Microsoft Entra provisioning agent follows the [Modern Lifecycle Policy](/en-us/lifecycle/policies/modern). Changes for products and services under the Modern Lifecycle Policy may be more frequent and require customers to be alert for forthcoming modifications to their product or service.

Products governed by the Modern Policy follow a [continuous support and servicing model](/en-us/lifecycle/overview/product-end-of-support-overview). Customers must take the latest update to remain supported.

For products and services governed by the Modern Lifecycle Policy, Microsoft's policy is to provide a minimum 30 days' notification when customers are required to take action in order to avoid significant degradation to the normal use of the product or service.

## Download link

From the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted), select **Cloud Sync**, and go to **Agents** to download the **Provisioning Agent**.

Get notified about when to revisit this page for updates by copying and pasting this URL: `https://aka.ms/cloudsyncrss` into your ![RSS feed reader icon](../../includes/media/cloud-sync-version-history/feed-icon-16-x-16.png) feed reader.

## 1.1.2505.0

**Release date:** September 21, 2026

### New features and improvements

- Added download functionality support for Azure China Cloud.
- Simplified Provisioning Agent configuration by eliminating the requirement for Domain Admin credentials when customers provide a gMSA and select custom gMSA permissions. This enhancement supports hybrid cloud synchronization scenarios and aligns with the gMSA PowerShell cmdlets experience.
- Streamlined the AADCloudSyncTools PowerShell module by removing the Repair-AADCloudSyncToolsAccount cmdlet, aligning the module with the updated Provisioning Agent configuration experience.

### Fixes

- Improved cloud environment discovery for Azure Government tenants that use domain suffixes.
- Resolved formatting inconsistencies affecting security groups during initial synchronization.
- Fixed an issue that could result in unresolved cross-domain directory references causing object-level quarantine errors in AD2AADProvisioning jobs.
- Fixed domain controller affinity paging issues when processing nested organizational units and containers.

### Security hardening

- Implemented additional security hardening improvements to further strengthen the reliability and protection of hybrid identity synchronization deployments.

## 1.1.2334.0

April 14, 2026: released for download

May 5, 2026: released for auto upgrade

### New or changed functionality

- [Account discovery](https://aka.ms/accountDiscoveryDocumentation) is now supported for on-premises applications using ECMA connectors.
- The `Add-AADCloudSyncADDomain` PowerShell cmdlet no longer sets additional Active Directory permissions on custom group Managed Service Accounts (gMSAs). Administrators are now responsible for ensuring that the custom gMSA has the right permissions, documented in [gMSA PowerShell cmdlets](../hybrid/cloud-sync/how-to-gmsa-cmdlets).

### Fixed issues

- Fixed an issue where the Provisioning Agent service could fail to shut down cleanly, affecting restarts and upgrades.

## 1.1.2108.0

December 4, 2025: released for download only

### Fixed Issues

Fixed the known issue that causes failure when writing back passwords using Microsoft Entra provisioning agent in AzureUSGovernment cloud with version 1.1.2102.0.

## 1.1.2102.0

Sept 22, 2025: released for download only

### Fixed issues

- Improved reliability of agent install and upgrade by preventing service timeouts
- Streamlined how to enable Windows Credential Manager during agent installation
- Added a check for the Hybrid Administrator role prerequisite, and activate the role for eligible authenticated users
- Simplified how to choose your provisioning scenario
- Configured installation for the current cloud environment by default
- Faster enumeration for large groups by preventing service timeouts
- Improved how admins can view their domain controller priority list
- Added UserAccountControl as a System for Cross-domain Identity Management (SCIM) property
- Added a configurable password length for newly created users. The default password length for newly created users is 256. Admins can set an integer value between 127 and 256 for newly created users by creating a registry entry with REG\_DWORD data type at:

    `HKLM\Software\Microsoft\Azure AD Connect Agents\Azure AD Connect Provisioning Agent\UserPasswordLength`

### Known issues

- If you are an AzueUSGovernment customer and have enabled writing back passwords with Microsoft Entra provisioning agent, the operation may fail. Please upgrade the agent to version 1.1.2108.0 to address this issue.

## 1.1.1586.0

May 13, 2024: released for download only

### Fixed issues

- Miscellaneous supportability improvements.
- Improved handling of Active Directory Provider initialization issues.
- Fixed a bug with removing attributes.
- Improved group writeback error handling.

## 1.1.1373.0

January 19, 2024: released for download and auto upgrade

### Fixed issues

Fixed an issue with case-sensitive comparison of domain names and enhanced the error handling.

## 1.1.1370.0

Release date: October 16, 2023

### New or changed functionality

- Added Public Preview feature: [Group provisioning to Active Directory](../hybrid/cloud-sync/govern-on-premises-groups)
- Rebranded the agent for Microsoft Entra

## 1.1.1365.0

September 8, 2023: released for download only

### New or changed functionality

- Added support for Applications Kerberos Key synchronization to Provisioning Agent
- Added support for Web Service, Windows PowerShell, and custom ECMA2 connectors
- **Query attribute** of ECMA2Host is no longer in use and removed from the ECMA2 Configuration wizard
- Update AADCloudSyncTools module with function to disable DirSyncConfiguration Accidental Deletion Prevention

### Fixed issues

- Fixed an issue with jobs going into quarantine if an OR name attribute value points to a nonexistent object
- Fixed an issue that caused customizations to AADConnectProvisioningAgent.exe.config to reset when the agent is updated
- Fixed provisioning agent incorrect creds if NTLM traffic is set to 'Deny-All'
- Fixed incorrect file path to trace log
- Fixed an issue that caused Provisioning Agent installer crashing from duplicate schema objects
- Update Windows Server Version check as per documented prerequisites
- Fixed for install page links visibility in 'high contrast black' mode
- Fixed case sensitive comparison and add logging for UPN / role ID checks
- Accessibility fixes for ECMA2 Configuration wizard

## 1.1.1107.0

December 16, 2022: released for download only

### New or changed functionality

- Added support for [on-premises application provisioning](/en-us/azure/active-directory/app-provisioning/on-premises-application-provisioning-architecture) (SCIM, SQL, LDAP)

## 1.1.977.0

September 23, 2022: released for download only

### New or changed functionality

- Added support for [cloud sync Self Service Password Reset](../authentication/tutorial-enable-cloud-sync-sspr-writeback) General Availability.
- Added support for password writeback in disconnected forests.

### Fixed issues

- Fixed various bug fixes to support SSPR with cloud sync

## 1.1.972.0

August 8, 2022: released for download only

### New or changed functionality

- Added a new cmdlet to enable and disable writeback of passwords. For more information about this cmdlet and its use, see [Enable password writeback in Microsoft Entra Connect cloud sync](../authentication/tutorial-enable-cloud-sync-sspr-writeback#enable-password-writeback-in-sspr).
- More info is now returned from 'Get-AADCloudSyncDomains' cmdlet
- Updated new cmdlets of CloudSync PowerShell module in the unattended agent install script.
- Added support for the installation of the provisioning agent using the commandline.
- Added support for EX and RX environments.

### Fixed issues

- Remove the app.config file on upgrade of the agent. After the Newtonsoft.Json upgrade, AADConnectProvisioningAgent.exe.config isn't updated after install, which results in a failure of sync.
- Fixed an issue with DC affinity after an OU is renamed.
- Fixed several issues in the PowerShell module.
- Fixed a memory leak due to not disposing HTTP client.
- Fixed a bug in the code for granting the "logon as a service" right to the GMSA.
- Refined the permissions on the GMSA for CloudHR.
- Cloud sync agent is now uninstalled, when the bundle is uninstalled.
- Fixed a bug that prevents deletion of the Service Principal if not all Jobs are deleted.
- Fixed an issue with updating of the password of a user with "User must change password at next logon."
- Fixed an issue with the agent GMSA folder permissions.
- Fixed an issue where group membership updates aren't always correct.

## 1.1.818.0

April 18, 2022: released for download only

New features and improvements

- Fixed bug where granting logon as a service right to a gMSA would fail.
- Updated the agent to honor the preferred Domain Controller list that is configured in the agent to also be used for the Self Service Password Reset feature.

## 1.1.587.0

November 2, 2021: released for download only

New features and improvements

- Added a cmdlet to configure Password Writeback

## 1.1.584.0

August 20, 2021: released for download only

### Fixed issues

- Fixed a bug where, when a domain is renamed, Password Hash Sync would fail with an error indicating "a specified cast is not valid" in the Event log. This error is a regression from earlier builds.

## 1.1.582.0

August 8, 2021: released for download only

Note

This is a security update release of Azure AD Connect. This release addresses a vulnerability as documented in [this CVE](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-36949). For more information about this vulnerability, see the CVE.

## 1.1.359.0

### New features and improvements

- GMSA Cmdlets to set/reset permission

### Fixed issues

- Fixed GMSA folder permissions (originally, the issue resulted in bootstrap issues)
- Fixed the handling of multiple changes to a single value reference attribute (for example, manager)
- Fixed the failure in Initial Enumeration, plus enhanced tracing of the failure
- Optimized group membership updates to a Scoping Group. With this update, customers now can sync a group of up to 50 K members using group scoping filter
- Added support to retrieve a single object by DN with Scoping used by Provisioning On Demand to obey Scoping logic

## 1.1.354.0

January 20, 2021: released for download only

### New features and improvements

- Improvement to GMSA experience including support for pre-custom created GMSA Account
- Added support for GMSA setup with [PowerShell cmdlets](../hybrid/cloud-sync/how-to-gmsa-cmdlets)
- Added support for [CLI](../hybrid/cloud-sync/how-to-install-pshell) agent install (silent installation)
- Added more diagnostics for agent source quarantine issues
- Reduced memory usage of OU scoping filters, running PHS only for in-scope users, handling of nested objects in OU when using OU scoping etc.

### Fixed issues

- Prevent quarantine when scoping group is out of scope
- PHS job now only operates for in-scope users, when scoping filters are configured
- Agent would sometimes stop responding during upgrade
- Initial Sync for objects in nested OUs when using OU scoping
- Make the Repair-AADCloudSyncToolsAccount more robust
- Reduce large memory usage of OU scoping filters
- Admin role check fails if the role members contain a security group
- Fixed GMSA folder permission issue, which prevents Agent Cert renewal

## 1.1.281.0

### Release status

November 23, 2020: released for download only

### New features and improvements

- Added support for [gMSA](../hybrid/cloud-sync/how-to-prerequisites#group-managed-service-accounts)
- Added support for groups up to size less than 1500 members during incremental or delta sync cycle. This change is applicable when using group scoping filter
- Added support for large groups with member size up to 15 K
- Added Initial sync improvements
- Added advanced verbose logging
- Added a new [AADCloudSyncTools PowerShell module](../hybrid/cloud-sync/reference-powershell)
- Fixed limitations to allow agent to be installed in non-English server
- Added support for PHS filtering only for objects in scope (Originally, we were syncing password hashes for all objects)
- Fixed a memory leak issue in the agent
- Added improvements in provisioning logs
- Added support for configuring [LDAP connection timeout](../hybrid/cloud-sync/how-to-manage-registry-options#configure-ldap-connection-timeout)
- Added support for configuring [referral chasing](../hybrid/cloud-sync/how-to-manage-registry-options#configure-referral-chasing)

## 1.1.96.0

### Release status

December 4, 2019: released for download only

### New features and improvements

- Added support for [Azure AD Connect cloud sync](../hybrid/cloud-sync/what-is-cloud-sync) to synchronize user, contact and group data from on-premises Active Directory to Azure AD

## 1.1.67.0

### Release status

September 9, 2019: Released for auto update

### New features and improvements

- Added ability to configure more tracing and logging for debugging Provisioning Agent issues
- Added ability to fetch only those Azure AD attributes that are configured in the mapping to improve performance of sync

### Fixed issues

- Fixed a bug wherein the agent went into an unresponsive state if there were issues with Azure AD connection failures
- Fixed a bug that caused issues when binary data was read from Azure Active Directory
- Fixed a bug wherein the agent failed to renew trust with the cloud hybrid identity service

## 1.1.30.0

### Release status

January 23, 2019: Released for download

### New features and improvements

- Revamped the Provisioning Agent and connector architecture for better performance, stability, and reliability
- Simplified the Provisioning Agent configuration using UI-driven installation wizard