---
layout: Conceptual
title: Hybrid Identity required ports and protocols - Azure - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-ports
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This page is a technical reference page for ports that are required to be open for Microsoft Entra Connect
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.tgt_pltfrm: na
ms.topic: reference
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 8a8936f3-3cd7-a365-81f2-33b9ee505a7b
document_version_independent_id: 6488ea50-f1d7-8240-3669-41591c56d862
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-ports.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-ports
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-ports.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8ccfd69a-7aee-3f11-5a17-d9cf182f33eb
---

# Hybrid Identity required ports and protocols - Azure - Microsoft Entra ID | Microsoft Learn

The following document is a technical reference on the required ports and protocols for implementing a hybrid identity solution. Use the following illustration and refer to the corresponding table.

![What is Microsoft Entra Connect](media/reference-connect-ports/required3.png)

## Table 1 - Microsoft Entra Connect and On-premises AD

This table describes the ports and protocols that are required for communication between the Microsoft Entra Connect server and on-premises AD.

| Protocol | Ports | Description |
| --- | --- | --- |
| DNS | 53 (TCP/UDP) | DNS lookups on the destination forest. |
| Kerberos | 88 (TCP/UDP) | Kerberos authentication to the AD forest. |
| MS-RPC | 135 (TCP) | Used during the initial configuration of the Microsoft Entra Connect wizard when it binds to the AD forest, and also during Password synchronization. |
| LDAP | 389 (TCP/UDP) | Used for data import from AD. Data is encrypted with Kerberos Sign & Seal. |
| SMB | 445 (TCP) | Used by Seamless SSO to create a computer account in the AD forest and during password writeback. For more information, see [Change a user account's password](/en-us/openspecs/windows_protocols/ms-adod/d211aaba-d188-4836-8007-8c62f7c9402d). |
| LDAP/SSL | 636 (TCP/UDP) | Used for data import from AD. The data transfer is signed and encrypted. Only used if you are using TLS. |
| RPC | 49152- 65535 (Random high RPC Port) (TCP) | Used during the initial configuration of Microsoft Entra Connect when it binds to the AD forests, and during Password synchronization. If the dynamic port has been changed, you need to open that port. See [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017), and [KB224196](https://support.microsoft.com/kb/224196) for more information. |
| WinRM | 5985 (TCP) | Only used if you are installing AD FS with gMSA by Microsoft Entra Connect Wizard |
| AD DS Web Services | 9389 (TCP) | Only used if you are installing AD FS with gMSA by Microsoft Entra Connect Wizard |
| Global Catalog | 3268 (TCP) | Used by Seamless SSO to query the global catalog in the forest before creating a computer account in the domain. |

## Table 2 - Microsoft Entra Connect and Microsoft Entra ID

This table describes the ports and protocols that are required for communication between the Microsoft Entra Connect server and Microsoft Entra ID.

| Protocol | Ports | Description |
| --- | --- | --- |
| HTTP | 80 (TCP) | Used to download CRLs (Certificate Revocation Lists) to verify TLS/SSL certificates. |
| HTTPS | 443 (TCP) | Used to synchronize with Microsoft Entra ID. |

For a list of URLs and IP addresses you need to open in your firewall, see [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) and [Troubleshooting Microsoft Entra Connect connectivity](tshoot-connect-connectivity#connectivity-issues-in-the-installation-wizard).

## Table 3 - Microsoft Entra Connect and AD FS Federation Servers/WAP

This table describes the ports and protocols that are required for communication between the Microsoft Entra Connect server and AD FS Federation/WAP servers.

| Protocol | Ports | Description |
| --- | --- | --- |
| HTTP | 80 (TCP) | Used to download CRLs (Certificate Revocation Lists) to verify TLS/SSL certificates. |
| HTTPS | 443 (TCP) | Used to synchronize with Microsoft Entra ID. |
| WinRM | 5985 | WinRM Listener |

## Table 4 - WAP and Federation Servers

This table describes the ports and protocols that are required for communication between the Federation servers and WAP servers.

| Protocol | Ports | Description |
| --- | --- | --- |
| HTTPS | 443 (TCP) | Used for authentication. |

## Table 5 - WAP and Users

This table describes the ports and protocols that are required for communication between users and the WAP servers.

| Protocol | Ports | Description |
| --- | --- | --- |
| HTTPS | 443 (TCP) | Used for device authentication. |
| TCP | 49443 (TCP) | Used for certificate authentication. |

## Table 6a & 6b - Pass-through Authentication with Single Sign On (SSO) and Password Hash Sync with Single Sign On (SSO)

The following tables describes the ports and protocols that are required for communication between the Microsoft Entra Connect and Microsoft Entra ID.

### Table 6a - Pass-through Authentication with SSO

| Protocol | Ports | Description |
| --- | --- | --- |
| HTTP | 80 (TCP) | Used to download CRLs (Certificate Revocation Lists) to verify TLS/SSL certificates. Also needed for the connector auto-update capability to function properly. |
| HTTPS | 443 (TCP) | Used to enable and disable the feature, register connectors, download connector updates, and handle all user sign-in requests. |

In addition, Microsoft Entra Connect needs to be able to make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).

### Table 6b - Password Hash Sync with SSO

| Protocol | Ports | Description |
| --- | --- | --- |
| HTTPS | 443 (TCP) | Used to enable SSO registration (required only for the SSO registration process). |

In addition, Microsoft Entra Connect needs to be able to make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653). Again, this is only required for the SSO registration process.

## Table 7a & 7b - Microsoft Entra Connect Health agent for (AD FS/Sync) and Microsoft Entra ID

The following tables describe the endpoints, ports, and protocols that are required for communication between Microsoft Entra Connect Health agents and Microsoft Entra ID

### Table 7a - Ports and Protocols for Microsoft Entra Connect Health agent for (AD FS/Sync) and Microsoft Entra ID

This table describes the following outbound ports and protocols that are required for communication between the Microsoft Entra Connect Health agents and Microsoft Entra ID.

| Protocol | Ports | Description |
| --- | --- | --- |
| Azure Service Bus | 5671 (TCP) | Used to send health information to Microsoft Entra ID. (recommended but not required in latest versions) |
| HTTPS | 443 (TCP) | Used to send health information to Microsoft Entra ID. (failback) |

If 5671 is blocked, the agent falls back to 443, but using 5671 is recommended. This endpoint isn't required in the latest version of the agent. The latest Microsoft Entra Connect Health agent versions only require port 443.

### 7b - Endpoints for Microsoft Entra Connect Health agent for (AD FS/Sync) and Microsoft Entra ID

For a list of endpoints, see [the Prerequisites section for the Microsoft Entra Connect Health agent](how-to-connect-health-agent-install#prerequisites).