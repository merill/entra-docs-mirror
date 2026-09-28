---
layout: Conceptual
title: Introduction to Microsoft Entra Connect V2 - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-azure-ad-connect-v2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn about the next version of Microsoft Entra Connect.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.collection: has-adal-ref
locale: en-us
document_id: 2fdc3de4-b7f1-e7e2-45e1-c7b8f28f3838
document_version_independent_id: f1d4639b-322e-c7dd-2002-bf61e72e8a14
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/whatis-azure-ad-connect-v2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/whatis-azure-ad-connect-v2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/whatis-azure-ad-connect-v2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b2de5ba8-f8e2-218c-c9ed-5983c92d4962
---

# Introduction to Microsoft Entra Connect V2 - Microsoft Entra ID | Microsoft Learn

Azure AD Connect V1 was released several years ago. Since this time, several of the components used have been scheduled for deprecation and updated to newer versions. Attempting to update all of these components individually would take time and planning.

To address this issue, we've bundled as many of these newer components into a new single release, so you only have to update once. This release is Microsoft Entra Connect V2. This release is a new version of the same software used to accomplish your hybrid identity goals, built using the latest foundational components.

Note

Azure AD Connect V1 is retired as of August 31, 2022 and is no longer supported. Azure AD Connect V1 installations may **stop working unexpectedly**. If you're still using Azure AD Connect V1, you need to upgrade or consider moving to Microsoft Entra Cloud Sync.

## Consider moving to Microsoft Entra Cloud Sync

Microsoft Entra Cloud Sync is the new sync client that works from the cloud and allows customers to set up and manage their sync preferences online. We recommend that you use Cloud Sync because we are introducing new features that improve the sync experiences through Cloud Sync. You can avoid future migrations by choosing Cloud Sync if that's the right option for you. Use the [supported sync scenarios comparison](../common-scenarios) to see if Cloud Sync is the right sync client for you.

View the following video to understand how Cloud sync provides value to your business.

For more information, see [What is cloud sync?](/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync)

## What are the major changes?

### SQL Server 2019 LocalDB

The previous versions of Microsoft Entra Connect shipped with a SQL Server 2012 LocalDB. V2.0 ships with a SQL Server 2019 LocalDB, which promises enhanced stability and performance and has several security-related bug fixes. SQL Server 2012 ended extended support in July 2022. For more information, see [Microsoft SQL 2019](https://www.microsoft.com/sql-server/sql-server-2019).

### MSAL authentication library

The previous versions of Microsoft Entra Connect shipped with the ADAL authentication library. This library is deprecated as of December 2022. The V2 release ships with the newer MSAL library. For more information, see [Overview of the MSAL library](../../../identity-platform/msal-overview).

### Visual C++ Redist 14

SQL Server 2019 requires the Visual C++ Redist 14 runtime, so we're updating the C++ runtime library to use this version. This Redistributable is installed with the Microsoft Entra Connect V2 package, so you don't have to take any action for the C++ runtime update.

### TLS 1.2

Important

Version 2.3.20.0 is a security update. With this update, Microsoft Entra Connect requires TLS 1.2. Ensure that you have TLS 1.2 enabled before updating to this version.

All versions of [Windows Server support TLS 1.2](/en-us/windows-server/security/tls/tls-ssl-schannel-ssp-overview). If TLS 1.2 is not enabled on your server, you need to enable this before you can deploy Microsoft Entra Connect V2.0.

For a PowerShell script to check whether TLS 1.2 is enabled, see [PowerShell script to check TLS](reference-connect-tls-enforcement#powershell-script-to-check-tls-12)

For more information about TLS 1.2, see [Microsoft Security Advisory 2960358](/en-us/security-updates/SecurityAdvisories/2015/2960358). For more information on enabling TLS 1.2, see [how to enable TLS 1.2](reference-connect-tls-enforcement)

TLS1.0 and TLS 1.1 are protocols that are deemed unsafe. Microsoft is deprecating them. This release of Microsoft Entra Connect only supports TLS 1.2. All versions of Windows Server that are supported for Microsoft Entra Connect V2 already default to TLS 1.2. If your server doesn't support TLS 1.2 you'll need to enable this before you can deploy Microsoft Entra Connect V2. For more information, see [TLS 1.2 enforcement for Microsoft Entra Connect](reference-connect-tls-enforcement).

### All binaries signed with SHA2

We noticed that some components had SHA1 signed binaries. We no longer support SHA1 for downloadable binaries and we upgraded all binaries to SHA2 signing. The digital signatures are used to ensure that the updates come directly from Microsoft and weren't tampered with during delivery. Because of weaknesses in the SHA-1 algorithm and to align to industry standards, we've changed the signing of Windows updates to use the more secure SHA-2 algorithm." 

There's no action needed from your side.

### Windows Server 2012 and Windows Server 2012 R2 are no longer supported

SQL Server 2019 requires Windows Server 2016 or newer as a server operating system. Since Microsoft Entra Connect v2 contains SQL Server 2019 components, we no longer can support older Windows Server versions.

You can't install this version on an older Windows Server version. We suggest you upgrade your Microsoft Entra Connect server to Windows Server 2019, which is the most recent version of the Windows Server operating system.

This [article](/en-us/windows-server/get-started/install-upgrade-migrate) describes the upgrade from older Windows Server versions to Windows Server 2019.

### PowerShell 5.0

This release of Microsoft Entra Connect contains several cmdlets that require PowerShell 5.0, so this requirement is a new prerequisite for Microsoft Entra Connect.

More details about PowerShell prerequisites can be found [here](/en-us/powershell/scripting/windows-powershell/install/windows-powershell-system-requirements#windows-powershell-50).

Note

PowerShell 5 is already part of Windows Server 2016 so you probably don't have to take action as long as you're on a recent Window Server version.

## What else do I need to know?

**Why is this upgrade important for me?** Several of the components in your current Microsoft Entra Connect server installations will no longer be supported. If you're using unsupported products, it is harder for our support team to provide you with the support experience your organization requires. So we recommend all customers to upgrade to this newer version as soon as they can.

This upgrade is especially important since we've had to update our prerequisites for Microsoft Entra Connect and you may need additional time to plan and update your servers to the newer versions of these prerequisites

**Is there any new functionality I need to know about?** No – the V2.0 release doesn't contain any new functionality. This release only contains updates of some of the foundational components on Microsoft Entra Connect.

**Can I upgrade from any previous version to V2?** Yes – upgrades from any previous version of Microsoft Entra Connect to Microsoft Entra Connect V2 is supported. Follow the guidance in [this article](how-to-upgrade-previous-version) to determine what is the best upgrade strategy for you. Before upgrading, you should consider moving to Microsoft Entra Cloud Sync.

**Can I export the configuration of my current server and import it in Microsoft Entra Connect V2?** Yes, you can do that, and it's a great way to migrate to Microsoft Entra Connect V2 – especially if you're also upgrading to a new operating system version. You can read more about the Import/export configuration feature and how you can use it in this [article](how-to-connect-import-export-config).

**I have enabled auto upgrade for Microsoft Entra Connect – will I get this new version automatically?** Yes - your Microsoft Entra Connect server is upgraded to the latest release if you enabled the auto-upgrade feature. However, we can only upgrade your server if you're using Windows Server 2016 or newer and you enabled TLS 1.2.

**I am not ready to upgrade yet – how much time do I have?** You should upgrade to Microsoft Entra Connect V2 as soon as you can. **All Azure AD Connect V1 versions are retired on 31 August, 2022.** For now, we'll continue to support older versions of Microsoft Entra Connect. However, it may prove difficult to provide a good support experience if some of the components in Microsoft Entra Connect have dropped out of support. This upgrade is particularly important for ADAL and TLS1.0/1.1 as these services might stop working unexpectedly after they're deprecated.

**I use an external SQL database and don't use SQL 2012 LocalDb – do I still have to upgrade?** Yes, you still need to upgrade to remain in a supported state even if you don't use SQL Server 2012, due to the TLS1.0/1.1 and ADAL deprecation. Note that SQL Server 2012 can still be used as an external SQL database with Microsoft Entra Connect V2. The SQL 2019 drivers in Microsoft Entra Connect V2 are compatible with SQL Server 2012.

**After the upgrade of my Microsoft Entra Connect instance to V2, will the SQL 2012 components automatically get uninstalled?** No, the upgrade to SQL 2019 doesn't remove any SQL 2012 components from your server. If you no longer need these components, then you should follow [the SQL Server uninstallation instructions](/en-us/sql/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup).

**What happens if I don't upgrade?** Until one of the components that are being retired are actually deprecated, you won't see any impact. Microsoft Entra Connect keeps on working.

Support for TLS 1.0/1.1 is deprecated in 2022, and you need to make sure you aren't using these protocols by that date as your service may stop working unexpectedly. You can manually configure your server for TLS 1.2 though, and that doesn't require an update of Microsoft Entra Connect to V2.

Microsoft Entra Connect Health may stop working after March 2023. We'll auto upgrade all Health agents to a new version before that, but we can't auto upgrade if you're running Azure AD Connect V1 due to compatibility issues with V versions.

After December 2022, ADAL is planned to go out of support. When ADAL goes out of support, authentication may stop working unexpectedly, and this blocks the Microsoft Entra Connect server from working properly. We strongly advise you to upgrade to Microsoft Entra Connect V2 before December 2022. You can't upgrade to a supported authentication library with your current Microsoft Entra Connect version.

**After upgrading to V2 the ADSync PowerShell cmdlets don't work?** This is a known issue. Restart your PowerShell session after installing or upgrading to V2 and then reimport the module. Use the following instructions to import the module.

1. Open Windows PowerShell with administrative privileges.
2. Type or copy and paste the following code:

    ```powershell
    Import-module -Name "C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync"
    ```

## License requirements for using Microsoft Entra Connect V2

Using this feature is free and included in your Azure subscription.

## License requirements for using Microsoft Entra Connect Health

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).