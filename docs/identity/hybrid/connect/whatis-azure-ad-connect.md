---
layout: Conceptual
title: What is Microsoft Entra Connect and Connect Health. - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-azure-ad-connect
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn about the tools used to synchronize and monitor your on-premises environment with Microsoft Entra ID.
ms.topic: overview
ms.date: 2026-09-10T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 86ed5438-9076-fa6f-d42a-e9bef29beb6e
document_version_independent_id: f6490079-8f4a-f621-623b-d500b52abef8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/whatis-azure-ad-connect.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/whatis-azure-ad-connect
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/whatis-azure-ad-connect.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 75f6d7f4-9c1e-ea7c-a48a-55d49e41b78a
---

# What is Microsoft Entra Connect and Connect Health. - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect is an on-premises Microsoft application designed to meet and accomplish your hybrid identity goals. If you're evaluating how to best meet your goals, you should also consider the cloud-managed solution [Microsoft Entra Cloud Sync](/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync).

Important

Azure AD Connect V1 has been retired as of August 31, 2022 and is no longer supported. Azure AD Connect V1 installations may **stop working unexpectedly**. If you are still using an Azure AD Connect V1 you need to upgrade to Microsoft Entra Connect V2 immediately.

## Consider moving to Microsoft Entra Cloud Sync

Microsoft Entra Cloud Sync is the future of synchronization for Microsoft. It replaces Microsoft Entra Connect.

Before moving to Microsoft Entra Connect V2.0, you should consider moving to cloud sync. You can see if cloud sync is right for you, by accessing the [Check sync tool](https://aka.ms/M365Wizard) from the portal or via the link provided.

For more information, see [What is cloud sync?](/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync)

## Microsoft Entra Connect features

- [Password hash synchronization](whatis-phs) - A sign-in method that synchronizes a hash of a users on-premises AD password with Microsoft Entra ID.
- [Pass-through authentication](how-to-connect-pta) - A sign-in method that allows users to use the same password on-premises and in the cloud, but doesn't require the additional infrastructure of a federated environment.
- [Federation integration](how-to-connect-fed-whatis) - Federation is an optional part of Microsoft Entra Connect and can be used to configure a hybrid environment using an on-premises AD FS infrastructure. It also provides AD FS management capabilities such as certificate renewal and additional AD FS server deployments.
- [Synchronization](how-to-connect-sync-whatis) - Responsible for creating users, groups, and other objects. And, making sure identity information for your on-premises users and groups is matching the cloud. This synchronization also includes password hashes.
- [Health Monitoring](whatis-azure-ad-connect#what-is-azure-ad-connect-health) - Microsoft Entra Connect Health can provide robust monitoring and provide a central location in the [Microsoft Entra admin center](https://entra.microsoft.com) to view this activity.

![What is Microsoft Entra Connect](../media/whatis-hybrid-identity/arch.png)

Important

Microsoft Entra Connect Health for Sync requires Microsoft Entra Connect Sync V2. If you are still using Azure AD Connect V1 you must upgrade to the latest version. Azure AD Connect V1 is retired on August 31, 2022. Microsoft Entra Connect Health for Sync will no longer work with Azure AD Connect V1 in December 2022.

## What is Microsoft Entra Connect Health?

Microsoft Entra Connect Health provides monitoring for your on-premises identity infrastructure. It helps you maintain a reliable connection to Microsoft 365 and Microsoft Online Services by making health data for your key identity components available in one place.

Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth) in the Microsoft Entra admin center to view alerts, performance monitoring, usage analytics, synchronization errors, and service information. Use the left menu to move between Microsoft Entra Connect Sync, AD FS, and AD DS monitoring experiences.

![What is Microsoft Entra Connect Health](media/whatis-hybrid-identity-health/aadconnecthealth2.png)

## Why use Microsoft Entra Connect?

Integrating your on-premises directories with Microsoft Entra ID makes your users more productive by providing a common identity for accessing both cloud and on-premises resources. Users and organizations can take advantage of:

- Users can use a single identity to access on-premises applications and cloud services such as Microsoft 365.
- Single tool to provide an easy deployment experience for synchronization and sign-in.
- Provides the newest capabilities for your scenarios. Microsoft Entra Connect replaces older versions of identity integration tools such as DirSync and Azure AD Sync. For more information, see [Hybrid Identity directory integration tools comparison](../).

## Why use Microsoft Entra Connect Health?

When authenticating with Microsoft Entra ID, your users are more productive because there's a common identity to access both cloud and on-premises resources. Ensuring the environment is reliable, so that users can access these resources, becomes a challenge. Microsoft Entra Connect Health helps monitor and gain insights into your on-premises identity infrastructure thus ensuring the reliability of this environment. It's as simple as installing an agent on each of your on-premises identity servers.

Microsoft Entra Connect Health for AD FS supports AD FS on Windows Server 2012 R2, Windows Server 2016, Windows Server 2019, Windows Server 2022, and Windows Server 2025. It also supports monitoring the web application proxy servers that provide authentication support for extranet access. With an easy and quick installation of the Health Agent, Microsoft Entra Connect Health for AD FS provides you with a set of key capabilities.

Key benefits and best practices:

| Key Benefits | Best Practices |
| --- | --- |
| Enhanced security | [Extranet lockout trends](how-to-connect-health-adfs#usage-analytics-for-ad-fs)[Failed sign-ins report](how-to-connect-health-adfs-risky-ip)[In privacy compliant](reference-connect-health-user-privacy) |
| Get alerted on [all critical ADFS system issues](how-to-connect-health-alert-catalog#alerts-for-active-directory-federation-services) | Server configuration and availability[Performance and connectivity](how-to-connect-health-adfs#performance-monitoring-for-ad-fs)Regular maintenance |
| Easy to deploy and manage | [Quick agent installation](how-to-connect-health-agent-install#install-the-agent-for-ad-fs)Agent auto upgrade to the latestData available in portal within minutes |
| Rich [usage metrics](how-to-connect-health-adfs#usage-analytics-for-ad-fs) | Top applications usageNetwork locations and TCP connectionToken requests per server |
| Great user experience | Dashboard fashion from [Microsoft Entra admin center](https://entra.microsoft.com)[Alerts through emails](how-to-connect-health-adfs#alerts-for-ad-fs) |

## License requirements for using Microsoft Entra Connect

Using this feature is free and included in your Azure subscription.

## License requirements for using Microsoft Entra Connect Health

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).