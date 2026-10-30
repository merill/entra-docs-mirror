---
layout: Conceptual
title: RADIUS authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-radius
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving RADIUS authentication with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 259fbf45-8ec4-d23e-9eb6-c4964bfa3547
document_version_independent_id: 3d404eb5-c07c-bbd0-104c-084095a175e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-radius.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-radius
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-radius.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: b31aa28d-6a4f-14d0-9420-b6a3813e9b01
---

# RADIUS authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Remote Authentication Dial-In User Service (RADIUS) is a network protocol that secures a network by enabling centralized authentication and authorization of dial-in users. Many applications still rely on the RADIUS protocol to authenticate users.

Microsoft Windows Server has a role called the Network Policy Server (NPS), which can act as a RADIUS server and support RADIUS authentication.

Microsoft Entra ID enables multifactor authentication with RADIUS-based systems. If a customer wants to apply Microsoft Entra multifactor authentication to any of the previously mentioned RADIUS workloads, they can install the Microsoft Entra multifactor authentication NPS extension on their Windows NPS server.

The Windows NPS server authenticates a user's credentials against Active Directory, and then sends the multifactor authentication request to Azure. The user then receives a challenge on their mobile authenticator. Once successful, the client application is allowed to connect to the service.

## Use when:

You need to add multifactor authentication to applications like

- a Virtual Private Network (VPN)
- WiFi access
- Remote Desktop Gateway (RDG)
- Virtual Desktop Infrastructure (VDI)
- Any others that depend on the RADIUS protocol to authenticate users into the service.

Note

Rather than relying on RADIUS and the Microsoft Entra multifactor authentication NPS extension to apply Microsoft Entra multifactor authentication to VPN workloads, we recommend that you upgrade your VPN's to Security Assertion Markup Language (SAML) and directly federate your VPN with Microsoft Entra ID. This gives your VPN the full breadth of Microsoft Entra ID Protection, including Conditional Access, multifactor authentication, device compliance, and Microsoft Entra ID Protection.

![architectural diagram](media/authentication-patterns/radius-auth.png)

## Components of the system

- **Client application (VPN client):** Sends authentication request to the RADIUS client.
- **RADIUS client:** Converts requests from client application and sends them to RADIUS server that has the NPS extension installed.
- **RADIUS server:** Connects with Active Directory to perform the primary authentication for the RADIUS request. Upon success, passes the request to Microsoft Entra multifactor authentication NPS extension.
- **NPS extension:** Triggers a request to Microsoft Entra multifactor authentication for a secondary authentication. If successful, NPS extension completes the authentication request by providing the RADIUS server with security tokens that include multifactor authentication claim, issued by Azure's Security Token Service.
- **Microsoft Entra multifactor authentication:** Communicates with Microsoft Entra ID to retrieve the user's details and performs a secondary authentication using a verification method configured by the user.

## Implement RADIUS with Microsoft Entra ID

- [Provide Microsoft Entra multifactor authentication capabilities using NPS](../identity/authentication/howto-mfa-nps-extension)
- [Configure the Microsoft Entra multifactor authentication NPS extension](../identity/authentication/howto-mfa-nps-extension-advanced)
- [VPN with Microsoft Entra multifactor authentication using the NPS extension](../identity/authentication/howto-mfa-nps-extension-vpn)