---
layout: Conceptual
title: Two-step verification Microsoft Entra multifactor authentication and ADFS - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/multi-factor-authentication-get-started-adfs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: This is the Microsoft Entra multifactor authentication page that describes how to get started with Microsoft Entra multifactor authentication and AD FS.
ms.topic: get-started
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: michmcla
locale: en-us
document_id: 886b8436-7403-cdf5-db0c-306a6adb2b45
document_version_independent_id: e6a00801-5a33-69d8-d9f7-a635ea2d6b5a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/multi-factor-authentication-get-started-adfs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/multi-factor-authentication-get-started-adfs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/multi-factor-authentication-get-started-adfs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: ae8c2b06-e2c7-1c97-4549-8ec44e1a5813
---

# Two-step verification Microsoft Entra multifactor authentication and ADFS - Microsoft Entra ID | Microsoft Learn

![Microsoft Entra multifactor authentication and ADFS getting started](media/multi-factor-authentication-get-started-adfs/adfs.png)

If your organization has federated your on-premises Active Directory with Microsoft Entra ID using AD FS, there are two options for using Microsoft Entra multifactor authentication.

- Secure cloud resources using Microsoft Entra multifactor authentication or Active Directory Federation Services
- Secure cloud and on-premises resources using Azure Multifactor Authentication Server

The following table summarizes the verification experience between securing resources with Microsoft Entra multifactor authentication and AD FS

| Verification Experience - Browser-based Apps | Verification Experience - Non-Browser-based Apps |
| --- | --- |
| Securing Microsoft Entra resources using Microsoft Entra multifactor authentication | - The first verification step is performed on-premises using AD FS.<br>- The second step is a phone-based method carried out using cloud authentication. |
| Securing Microsoft Entra resources using Active Directory Federation Services | - The first verification step is performed on-premises using AD FS.<br>- The second step is performed on-premises by honoring the claim. |

Caveats with app passwords for federated users:

- App passwords are verified using cloud authentication, so they bypass federation. Federation is only actively used when setting up an app password.
- On-premises Client Access Control settings aren't honored by app passwords.
- You lose on-premises authentication-logging capability for app passwords.
- Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.

For information on setting up either Microsoft Entra multifactor authentication or the Azure Multifactor Authentication Server with AD FS, see the following articles:

- [Secure cloud resources using Microsoft Entra multifactor authentication and AD FS](howto-mfa-adfs)
- [Secure cloud and on-premises resources using Azure Multifactor Authentication Server with Windows Server](howto-mfaserver-adfs-windows-server)
- [Secure cloud and on-premises resources using Azure Multifactor Authentication Server with AD FS 2.0](howto-mfaserver-adfs-2)