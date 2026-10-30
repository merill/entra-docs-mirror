---
layout: Conceptual
title: Microsoft Entra Connect and federation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-fed-whatis
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This page is the central location for all documentation regarding AD FS operations that use Microsoft Entra Connect.
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 3940481f-f5b9-ed46-0a87-bcdb3929566b
document_version_independent_id: dba7a49b-3653-3ac1-e87e-c1240c6eaca7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-fed-whatis.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-fed-whatis
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-fed-whatis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d635d5c9-2ff3-9113-77ce-e686e0f2c9c4
---

# Microsoft Entra Connect and federation - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect lets you configure federation with on-premises Active Directory Federation Services (AD FS) and Microsoft Entra ID. With federation sign-in, you can enable users to sign in to Microsoft Entra ID-based services with their on-premises passwords--and, while on the corporate network, without having to enter their passwords again. By using the federation option with AD FS, you can deploy a new installation of AD FS, or you can specify an existing installation in a Windows Server 2012 R2 farm.

This topic is the home for information on federation-related functionalities for Microsoft Entra Connect. It lists links to all related topics. For links to Microsoft Entra Connect, see [Integrating your on-premises identities with Microsoft Entra ID](../whatis-hybrid-identity).

## Microsoft Entra Connect: federation topics

| Topic | What it covers and when to read it |
| --- | --- |
| **Microsoft Entra Connect user sign-in options** |  |
| [Understand user sign-in options](plan-connect-user-signin) | Learn about various user sign-in options and how they affect the Azure sign-in user experience. |
| **Install AD FS by using Microsoft Entra Connect** |  |
| [Prerequisites](how-to-connect-install-custom#ad-fs-configuration-prerequisites) | See the prerequisites for a successful AD FS installation via Microsoft Entra Connect. |
| [Configure an AD FS farm](how-to-connect-install-custom#configuring-federation-with-ad-fs) | Install a new AD FS farm by using Microsoft Entra Connect. |
| [Federate with Microsoft Entra ID using alternate login ID](how-to-connect-fed-management#alternateid) | Configure federation using alternate login ID |
| **Modify the AD FS configuration** |  |
| [Repair the trust](how-to-connect-fed-management#repairthetrust) | Repair the current trust between on-premises AD FS and Microsoft 365/Azure. |
| [Add a new AD FS server](how-to-connect-fed-management#addadfsserver) | Expand an AD FS farm with an additional AD FS server after initial installation. |
| [Add a new AD FS WAP server](how-to-connect-fed-management#addwapserver) | Expand an AD FS farm with an additional Web Application Proxy (WAP) server after initial installation. |
| [Add a new federated domain](how-to-connect-fed-management#addfeddomain) | Add another domain to be federated with Microsoft Entra ID. |
| [Update the TLS/SSL certificate](how-to-connect-fed-ssl-update) | Update the TLS/SSL certificate for an AD FS farm. |
| [Renew federation certificates for Microsoft 365 and Microsoft Entra ID](how-to-connect-fed-o365-certs) | Renew your O365 certificate with Microsoft Entra ID. |
| **Other federation configuration** |  |
| [Federate multiple instances of Microsoft Entra ID with single instance of AD FS](how-to-connect-fed-single-adfs-multitenant-federation) | Federate multiple Microsoft Entra ID with single AD FS farm |
| [Add a custom company logo/illustration](how-to-connect-fed-management#customlogo) | Modify the sign-in experience by specifying the custom logo that is shown on the AD FS sign-in page. |
| [Add a sign-in description](how-to-connect-fed-management#addsignindescription) | Change the sign-in description on the AD FS sign-in page. |
| [Modify AD FS claim rules](how-to-connect-fed-management#modclaims) | Modify or add claim rules in AD FS that correspond to Microsoft Entra Connect Sync configuration. |