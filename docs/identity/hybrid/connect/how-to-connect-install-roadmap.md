---
layout: Conceptual
title: Microsoft Entra Connect and Microsoft Entra Connect Health installation roadmap. - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-roadmap
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document provides an overview of the installation options and paths available for installing Microsoft Entra Connect and Connect Health.
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 601beac1-1bc3-5cfe-0653-4c31917a5503
document_version_independent_id: acd6ceee-f4b9-8b92-4b71-5e8de0ffcfde
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-install-roadmap.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-install-roadmap
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-install-roadmap.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b5f0a4e8-df60-e8e1-41ed-48435fdae359
---

# Microsoft Entra Connect and Microsoft Entra Connect Health installation roadmap. - Microsoft Entra ID | Microsoft Learn

## Install Microsoft Entra Connect

Important

Microsoft doesn't support modifying or operating Microsoft Entra Connect Sync outside of the actions that are formally documented. Any of these actions might result in an inconsistent or unsupported state of Microsoft Entra Connect Sync. As a result, Microsoft can't provide technical support for such deployments.

You can find the download for Microsoft Entra Connect on [Microsoft Download Center](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted).

| Solution | Scenario |
| --- | --- |
| Before you start - [Hardware and prerequisites](how-to-connect-install-prerequisites) | - Steps to complete before you start to install Microsoft Entra Connect. |
| [Express settings](how-to-connect-install-express) | - If you have a single forest AD, then this is the recommended option to use.<br>- User sign in with the same password using password synchronization. |
| [Customized settings](how-to-connect-install-custom) | - Used when you have multiple forests. Supports many on-premises [topologies](plan-connect-topologies).<br>- Customize your sign-in option, such as pass-through authentication, ADFS for federation or use a 3rd party identity provider.<br>- Customize synchronization features, such as filtering and writeback. |
| [Upgrade from DirSync](how-to-dirsync-upgrade-get-started) | - Used when you have an existing DirSync server already running. |
| [Upgrade from Azure AD Sync or Microsoft Entra Connect](how-to-upgrade-previous-version) | - There are several different methods depending on your preference. |

[After installation](how-to-connect-post-installation), you should verify it's working as expected and assign licenses to the users.

### Next steps to Install Microsoft Entra Connect

| Topic | Link |
| --- | --- |
| Download Microsoft Entra Connect | [Download Microsoft Entra Connect](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted) |
| Install using Express settings | [Express installation of Microsoft Entra Connect](how-to-connect-install-express) |
| Install using Customized settings | [Custom installation of Microsoft Entra Connect](how-to-connect-install-custom) |
| Upgrade from DirSync | [Upgrade from Azure AD Sync tool (DirSync)](how-to-dirsync-upgrade-get-started) |
| After installation | [Verify the installation and assign licenses](how-to-connect-post-installation) |

### Learn more about Install Microsoft Entra Connect

You also want to prepare for [operational](how-to-connect-sync-staging-server) concerns. You might want to have a stand-by server so you easily can fail over if there's a [disaster](how-to-connect-sync-staging-server#disaster-recovery). If you plan to make frequent configuration changes, you should plan for a [staging mode](how-to-connect-sync-staging-server) server.

| Topic | Link |
| --- | --- |
| Supported topologies | [Topologies for Microsoft Entra Connect](plan-connect-topologies) |
| Design concepts | [Microsoft Entra Connect design concepts](plan-connect-design-concepts) |
| Accounts used for installation | [More about Microsoft Entra Connect credentials and permissions](reference-connect-accounts-permissions) |
| Operational planning | [Microsoft Entra Connect Sync: Operational tasks and considerations](how-to-connect-sync-staging-server) |
| User sign-in options | [Microsoft Entra Connect User sign-in options](plan-connect-user-signin) |

## Configure sync features

Microsoft Entra Connect comes with several features you can optionally turn on or are enabled by default. Some features might sometimes require more configuration in certain scenarios and topologies.

[Filtering](how-to-connect-sync-configure-filtering) is used when you want to limit which objects are synchronized to Microsoft Entra ID. By default all users, contacts, groups, and Windows 10 computers are synchronized. You can change the filtering based on domains, OUs, or attributes.

[Password hash synchronization](how-to-connect-password-hash-synchronization) synchronizes the password hash in Active Directory to Microsoft Entra ID. The end-user can use the same password on-premises and in the cloud but only manage it in one location. Since it uses your on-premises Active Directory as the authority, you can also use your own password policy.

[Password writeback](../../authentication/tutorial-enable-sspr) allows your users to change and reset their passwords in the cloud and have your on-premises password policy applied.

[Device writeback](how-to-connect-device-writeback) allows a device registered in Microsoft Entra ID to be written back to on-premises Active Directory so it can be used for Conditional Access.

The [prevent accidental deletes](how-to-connect-sync-feature-prevent-accidental-deletes) feature is turned on by default and protects your cloud directory from numerous deletes at the same time. By default it allows 500 deletes per run. You can change this setting depending on your organization size.

[Automatic upgrade](how-to-connect-install-automatic-upgrade) is enabled by default for express settings installations and ensures your Microsoft Entra Connect is always up to date with the latest release.

### Next steps to configure sync features

| Topic | Link |
| --- | --- |
| Configure filtering | [Microsoft Entra Connect Sync: Configure filtering](how-to-connect-sync-configure-filtering) |
| Password hash synchronization | [Password hash synchronization](how-to-connect-password-hash-synchronization) |
| Pass-through Authentication | [Pass-through authentication](how-to-connect-pta) |
| Password writeback | [Getting started with password management](../../authentication/tutorial-enable-sspr) |
| Device writeback | [Enabling device writeback in Microsoft Entra Connect](how-to-connect-device-writeback) |
| Prevent accidental deletes | [Microsoft Entra Connect Sync: Prevent accidental deletes](how-to-connect-sync-feature-prevent-accidental-deletes) |
| Automatic upgrade | [Microsoft Entra Connect: Automatic upgrade](how-to-connect-install-automatic-upgrade) |

## Customize Microsoft Entra Connect Sync

Microsoft Entra Connect Sync comes with a default configuration that is intended to work for most customers and topologies. But there are always situations where the default configuration doesn't work and must be adjusted. It's supported to make changes as documented in this section and linked topics.

If you haven't worked with a synchronization topology before you want to start to understand the basics and the terms used as described in the [technical concepts](how-to-connect-sync-technical-concepts). Even if some things are similar, a lot has changed as well.

The [default configuration](concept-azure-ad-connect-sync-default-configuration) assumes there might be more than one forest in the configuration. In those topologies, a user object might be represented as a contact in another forest. The user might also have a linked mailbox in another resource forest. The behavior of the default configuration is described in [users and contacts](concept-azure-ad-connect-sync-user-and-contacts).

The configuration model in sync is called [declarative provisioning](concept-azure-ad-connect-sync-declarative-provisioning-expressions). The advanced attribute flows are using [functions](reference-connect-sync-functions-reference) to express attribute transformations. You can see and examine the entire configuration using tools which comes with Microsoft Entra Connect. If you need to make configuration changes, make sure you follow the [best practices](how-to-connect-sync-best-practices-changing-default-configuration) so it's easier to adopt new releases.

### Next steps to customize Microsoft Entra Connect Sync

| Topic | Link |
| --- | --- |
| All Microsoft Entra Connect Sync articles | [Microsoft Entra Connect Sync](how-to-connect-sync-whatis) |
| Technical concepts | [Microsoft Entra Connect Sync: Technical Concepts](how-to-connect-sync-technical-concepts) |
| Understanding the default configuration | [Microsoft Entra Connect Sync: Understanding the default configuration](concept-azure-ad-connect-sync-default-configuration) |
| Understanding users and contacts | [Microsoft Entra Connect Sync: Understanding Users and Contacts](concept-azure-ad-connect-sync-user-and-contacts) |
| Declarative provisioning | [Microsoft Entra Connect Sync: Understanding Declarative Provisioning Expressions](concept-azure-ad-connect-sync-declarative-provisioning-expressions) |
| Change the default configuration | [Best practices for changing the default configuration](how-to-connect-sync-best-practices-changing-default-configuration) |

## Configure federation features

Microsoft Entra Connect provides several features that simplify federating with Microsoft Entra ID using AD FS and managing your federation trust. Microsoft Entra Connect supports AD FS on Windows Server 2012R2 or later.

[Update TLS/SSL certificate of AD FS farm](how-to-connect-fed-ssl-update) even if you are not using Microsoft Entra Connect to manage your federation trust.

[Add an AD FS server](how-to-connect-fed-management#addadfsserver) to your farm to expand the farm as required.

[Repair the trust](how-to-connect-fed-management#repairthetrust) with Microsoft Entra ID in a few simple clicks.

ADFS can be configured to support [multiple domains](how-to-connect-install-multiple-domains). For example, you might have multiple top domains you need to use for federation.

If your ADFS server isn't configured to update certificates from Microsoft Entra ID automatically, or if you use a non-ADFS solution, then you'll be notified when you have to [update certificates](how-to-connect-fed-o365-certs).

### Next steps to configure federation features

| Topic | Link |
| --- | --- |
| All AD FS articles | [Microsoft Entra Connect and federation](how-to-connect-fed-whatis) |
| Configure ADFS with subdomains | [Multiple Domain Support for Federating with Microsoft Entra ID](how-to-connect-install-multiple-domains) |
| Manage AD FS farm | [AD FS management and customization with Microsoft Entra Connect](how-to-connect-fed-management) |
| Manually updating federation certificates | [Renewing Federation Certificates for Microsoft 365 and Microsoft Entra ID](how-to-connect-fed-o365-certs) |

## Get started with Microsoft Entra Connect Health

To get started with Microsoft Entra Connect Health, use the following steps:

1. [Get Microsoft Entra ID P1 or P2](../../../fundamentals/get-started-premium) or [start a trial](https://azure.microsoft.com/trial/get-started-active-directory/).
2. Download and install Microsoft Entra Connect Health Agents on your identity servers.
3. Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth) in the Microsoft Entra admin center.

Note

Before monitoring data appears in Microsoft Entra Connect Health, install the Microsoft Entra Connect Health agents on the targeted servers.

## Download and install Microsoft Entra Connect Health Agent

- Make sure that you [satisfy the prerequisites](how-to-connect-health-agent-install#prerequisites) for Microsoft Entra Connect Health.
- Get started using Microsoft Entra Connect Health for AD FS
    - [Download Microsoft Entra Connect Health Agent for AD FS.](https://www.microsoft.com/en-us/download/details.aspx?id=108777)
    - [See the installation instructions](how-to-connect-health-agent-install#install-the-agent-for-ad-fs).
- Get started using Microsoft Entra Connect Health for sync
    - [Download and install the latest version of Microsoft Entra Connect](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted). The Health Agent for sync is installed as part of the Microsoft Entra Connect installation (version 1.0.9125.0 or higher).
- Get started using Microsoft Entra Connect Health for AD DS
    - [Download Microsoft Entra Connect Health Agent for AD DS](https://www.microsoft.com/en-us/download/details.aspx?id=108777).
    - [See the installation instructions](how-to-connect-health-agent-install#install-the-agent-for-azure-ad-ds).

## Microsoft Entra Connect Health in the Microsoft Entra admin center

The [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth) experience provides a left menu for monitoring Microsoft Entra Connect Sync, AD FS, and AD DS. After you deploy the agents, the service automatically identifies the monitored service instances.

Note

For licensing information, see the [Microsoft Entra Connect Health FAQ](reference-connect-health-faq) or the [Microsoft Entra pricing page](https://aka.ms/aadpricing).

[![Screenshot of Microsoft Entra Connect Health navigation with callouts for service areas, Quick start resources, and configuration options.](media/how-to-connect-install-roadmap/connect-health-navigation.png)](media/how-to-connect-install-roadmap/connect-health-navigation.png#lightbox)

The menu includes the following options:

- **Quick start**: View what's new, download the agents and Microsoft Entra Connect, open documentation, or provide feedback.
- **Sync errors**: Review synchronization error categories and individual error details. For supported duplicate-attribute scenarios, you can start the guided **Fix Synchronization Error** experience.
- **Sync services**: View monitored Microsoft Entra Connect Sync service instances. Select a service to review its servers, alerts, synchronization errors, and settings. For details, see [Use Microsoft Entra Connect Health for Sync](how-to-connect-health-sync).
- **AD FS services**: View monitored AD FS farms. Select a service to review its servers, properties, alerts, performance monitoring, usage analytics, and security reports. For details, see [Use Microsoft Entra Connect Health with AD FS](how-to-connect-health-adfs).
- **AD DS services**: View monitored AD DS forests. Select a service to review its domain controllers, replication status, alerts, and performance monitoring. For details, see [Use Microsoft Entra Connect Health with AD DS](how-to-connect-health-adds).
- **Settings**: Configure tenant-level Microsoft Entra Connect Health settings.
- **Role based access control (IAM)**: Manage access to Microsoft Entra Connect Health data.
- **Troubleshoot** and **New support request**: Diagnose issues or contact Microsoft support.