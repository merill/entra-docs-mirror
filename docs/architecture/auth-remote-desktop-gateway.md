---
layout: Conceptual
title: Remote Desktop Gateway Services with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-remote-desktop-gateway
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving Remote Desktop Gateway Services with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-03-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 505559fa-bd88-4f58-690e-4c3e6fd37365
document_version_independent_id: 30b3d170-d9cc-59ca-42a8-6995e306af11
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-remote-desktop-gateway.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-remote-desktop-gateway
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-remote-desktop-gateway.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ddab3cd8-636f-4a91-896e-1c23f399a6bd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f409bb5d-e203-40c5-9d95-0ee717231beb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b87be1f8-e855-63bb-fc2f-4f577d904a70
---

# Remote Desktop Gateway Services with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

A standard Remote Desktop Services (RDS) deployment includes various [Remote Desktop role services](/en-us/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture) running on Windows Server. The RDS deployment with Microsoft Entra application proxy has a permanent outbound connection from the server that is running the connector service. Other deployments leave open inbound connections through a load balancer.

This authentication pattern allows you to offer more types of applications by publishing on-premises applications through Remote Desktop Services. It reduces the attack surface of their deployment by using Microsoft Entra application proxy.

## When to use Remote Desktop Gateway Services

Use Remote Desktop Gateway Services when you need to provide remote access and protect your Remote Desktop Services deployment with pre-authentication.

![architectural diagram](media/authentication-patterns/rdp-auth.png)

## System components

- **User:** Accesses RDS served by Application Proxy.
- **Web browser:** The component that the user interacts with to access the external URL of the application.
- **Microsoft Entra ID:** Authenticates the user.
- **Application Proxy service:** Acts as reverse proxy to forward request from the user to RDS. Application Proxy can also enforce any Conditional Access policies.
- **Remote Desktop Services:** Acts as a platform for individual virtualized applications, providing secure mobile and remote desktop access. It provides end users with the ability to run their applications and desktops from the cloud.

## Implement Remote Desktop Gateway services with Microsoft Entra ID

Explore the following resources to learn more about implementing Remote Desktop Gateway services with Microsoft Entra ID.

- [Publish Remote Desktop with Microsoft Entra application proxy](../identity/app-proxy/application-proxy-integrate-with-remote-desktop-services) describes how Remote Desktop Service and Microsoft Entra application proxy work together to improve productivity of workers who are away from the corporate network.
- The [Tutorial - Add an on-premises app - Application Proxy in Microsoft Entra ID](../identity/app-proxy/application-proxy-add-on-premises-application) helps you to prepare your environment for use with Application Proxy.