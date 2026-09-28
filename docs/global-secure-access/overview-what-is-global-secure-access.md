---
layout: Conceptual
title: What is Global Secure Access? - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/overview-what-is-global-secure-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how Microsoft's Security Service Edge (SSE) solution, Global Secure Access, provides network access control and visibility to users and devices inside and outside a traditional office.
ms.topic: overview
ms.date: 2026-04-15T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: c948212f-57d1-a5ee-2fb3-880d8a88fbda
document_version_independent_id: a3cda05e-679f-1677-cf3a-2210624ac566
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/overview-what-is-global-secure-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/overview-what-is-global-secure-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/overview-what-is-global-secure-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2235a9f5-ccc7-8c6c-2793-3f39ff161f8d
---

# What is Global Secure Access? - Global Secure Access | Microsoft Learn

## Overview

The way people work changed. Instead of working in traditional offices, people now work from nearly anywhere. As applications and data move to the cloud, the modern workforce needs an identity-aware, cloud-delivered network perimeter. This new network security category is called Security Service Edge (SSE).

Microsoft Entra Internet Access and Microsoft Entra Private Access comprise Microsoft's Security Service Edge (SSE) solution. Global Secure Access is the unifying term used for both Microsoft Entra Internet Access and Microsoft Entra Private Access. Global Secure Access is the unified location in the Microsoft Entra admin center. Global Secure Access is built upon the core principles of Zero Trust to use least privilege, verify explicitly, and assume breach.

![Diagram of the Global Secure Access solution, illustrating how identities and remote networks can connect to Microsoft, private, and public resources through the service.](media/overview-what-is-global-secure-access/global-secure-access-diagram.png)

## Microsoft's Security Service Edge (SSE) solution

Microsoft Entra Internet Access and Microsoft Entra Private Access - coupled with Microsoft Defender for Cloud Apps, Microsoft's SaaS-security focused Cloud Access Security Broker (CASB) - are uniquely built as a solution that converges network, identity, and endpoint access controls so you can secure access to any app or resource, from anywhere. With the addition of these Global Secure Access products, Microsoft Entra ID simplifies access policy management and enables access orchestration for employees, business partners, and digital workloads. You can continuously monitor and adjust user access in real time if permissions or risk level changes.

The Global Secure Access features streamline the roll-out and management of the access control capabilities with a unified portal. These features are delivered from Microsoft's Wide Area Network, spanning 70 regions and 190+ network edge locations. This private network, which is one of the largest in the world, enables organizations to optimally connect users and devices to public and private resources seamlessly and securely. For a list of the current points of presence, see [Global Secure Access points of presence article](reference-points-of-presence).

## Microsoft Entra Internet Access

Microsoft Entra Internet Access protects access to internet and SaaS apps with an identity-based Secure Web Gateway (SWG), blocking threats, unsafe content, and malicious traffic.

### Key features

- Acquire network traffic by using the user aware internet traffic forwarding profile, either from the desktop client or from a remote network, such as a branch location.
- Detailed network traffic logs for internet traffic (including enforced policy details). Dashboards such as relationship maps between users, devices and endpoints, cross tenant access, and top network destination in use.
- Use rich context awareness (user, device, location, risk, and compliance policy) while applying network security policies through integration with Conditional Access. Protect user access to the public internet while using Microsoft's cloud-delivered, identity-aware SWG solution.
- Enable web content filtering to regulate access to internet destinations based on their web-content categories and/or FQDN-domain names.
- Apply universal Conditional Access policies for all internet destinations, even if not federated with Microsoft Entra ID, through integration with Conditional Access session controls.

## Microsoft Entra Internet Access for Microsoft Services

Microsoft Entra Internet Access for Microsoft services enhances Microsoft Entra ID capabilities with direct connectivity to supported Microsoft services, improving security, performance, and resilience.

### Key features

- Connect to Microsoft services directly by using the prepopulated Microsoft traffic forwarding profile, either from the desktop client or from a remote network, such as a branch location.
- Simplify Conditional Access policy configurations by requiring Compliant Network check for any Microsoft Entra ID integrated application with Microsoft Entra ID Conditional Access.
- Apply Universal Tenant Restrictions to reduce the risk of data exfiltration to unauthorized foreign tenants or personal accounts.
- Increase the accuracy of threat detections with source IP restoration for the Microsoft Entra ID sign in logs.
- Access detailed network traffic logs for Microsoft traffic, including enforced policy details. View dashboards that show relationship maps between users, devices and endpoints, cross tenant access, and top network destinations in use.

## Microsoft Entra Private Access

Microsoft Entra Private Access provides your users - whether in an office or working remotely - secured access to your private, corporate resources. Microsoft Entra Private Access builds on the capabilities of Microsoft Entra application proxy and extends access to any private resource, port, and protocol.

Remote users connect to private apps across hybrid and multicloud environments, private networks, and data centers from any device and network without requiring a VPN. The service offers per-app adaptive access based on Conditional Access policies, for more granular security than a VPN.

### Key features

- Zero Trust-based access to a range of IP addresses and/or Fully Qualified Domain Names (FQDNs) without requiring a legacy VPN. This feature is known as Quick Access.
- Per-app access for Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) applications.
- Modernize legacy app authentication with deep Conditional Access integration.
- Provide a seamless end-user experience by acquiring network traffic from the desktop client and deploying side-by-side with your existing non-Microsoft SSE solutions.

## Licensing overview

Microsoft Entra Internet Access, Microsoft Entra Internet Access for Microsoft services, and Microsoft Entra Private Access are now generally available.

- Microsoft Entra Internet Access capabilities are included in the Microsoft Entra Suite license and standalone. Microsoft Entra Internet Access helps you secure access to all internet and SaaS applications.
- Microsoft Entra Private Access capabilities are included in the Microsoft Entra Suite license and standalone. Microsoft Entra Private Access elevates network security with a Zero Trust Network Access (ZTNA) solution.
- Microsoft Entra Internet Access for Microsoft services capabilities are included in a Microsoft Entra ID P1 or Microsoft Entra ID P2 license. Microsoft Entra Internet Access for Microsoft services enhances Microsoft Entra ID capabilities with direct connectivity to supported Microsoft services, improving security, performance, and resilience.

To use Microsoft Entra Private Access and Microsoft Entra Internet Access, users need a Microsoft Entra ID P1 or Microsoft Entra ID P2 license.

Most Global Secure Access services operate on a per-user license model unless otherwise stated. For more information about licensing costs and the Microsoft Entra Suite, see [Microsoft Entra Plans & Pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing). For more information about purchasing individual licenses, see the Microsoft Entra Suite standalone products tab of the licensing page. For information about guest user licensing, see [Global Secure Access licensing for guest users](reference-licensing-guest-users).

### Feature comparison table

| Feature | Entra P1/P2 License - Microsoft traffic profile | Internet Access License¹ - Internet Access profile | Private Access License¹ - Private Access profile |
| --- | --- | --- | --- |
| [Windows client](how-to-install-windows-client) | ✅ | ✅ | ✅ |
| [macOS client](how-to-install-macos-client) | ✅ | ✅ | ✅ |
| Mobile client ([iOS](how-to-install-ios-client), [Android](how-to-install-android-client)) | ✅ | ✅ | ✅ |
| [Traffic logs (Preview)](how-to-view-traffic-logs) | ✅ | ✅ | ✅ |
| [Remote network (branch connectivity)](concept-remote-network-connectivity) | ✅ | ✅ |  |
| [Direct Microsoft services connectivity](how-to-manage-microsoft-profile) | ✅ |  |  |
| [Universal Tenant Restrictions](how-to-universal-tenant-restrictions) | ✅ |  |  |
| [Compliant network check](how-to-compliant-network) | ✅ |  |  |
| [Source IP restoration](how-to-source-ip-restoration) | ✅ |  |  |
| [Microsoft 365 Enriched logs](how-to-view-enriched-logs) | ✅ |  |  |
| [Universal Conditional Access (CA)](concept-universal-conditional-access) | ✅ | ✅ |  |
| [Context-aware network security](concept-internet-access) |  | ✅ |  |
| [Web category filtering](how-to-configure-web-content-filtering) |  | ✅ |  |
| [Fully qualified domain name (FQDN) filtering](how-to-configure-web-content-filtering) |  | ✅ |  |
| [TLS inspection](tutorial-internet-access-tls-inspection) |  | ✅ |  |
| [Threat intelligence](how-to-configure-threat-intelligence) |  | ✅ |  |
| [Prompt injection protection](how-to-ai-prompt-injection-protection) |  | ✅ |  |
| [Data Loss Prevention](how-to-network-content-filtering) |  | ✅ |  |
| [Universal Continuous Access Evaluation (CAE)](concept-universal-continuous-access-evaluation) | ✅ | ✅ | ✅ |
| [VPN replacement with an identity-centric ZTNA](tutorial-private-access-vpn-replacement) |  |  | ✅ |
| [Quick Access](how-to-configure-quick-access) |  |  | ✅ |
| [Per-app access (TCP/UDP)](how-to-configure-per-app-access) |  |  | ✅ |
| [App Discovery](how-to-application-discovery) |  |  | ✅ |
| [Shadow AI discovery](concept-shadow-ai-discovery) |  | ✅ |  |
| [Private Domain Name System (DNS)](concept-private-name-resolution) |  |  | ✅ |
| [Single sign-on across all private apps](how-to-configure-kerberos-sso) |  |  | ✅ |
| [Marketplace availability (Preview)](how-to-configure-connectors) |  |  | ✅ |
| [Private network connector multicloud support (Preview)](how-to-configure-connectors) |  |  | ✅ |
| [Network controls for agents²](how-to-secure-web-ai-gateway-agents) |  | ✅ |  |

¹ Included in [Microsoft Entra Suite](../fundamentals/try-microsoft-entra-suite#what-is-the-microsoft-entra-suite).

² Network controls for agents requires a [Microsoft Agent 365](/en-us/microsoft-agent-365/overview) license.

**Remote Network licensing**

The remote network (branch connectivity) feature is included in both the Microsoft Entra ID P1 license for Microsoft traffic, and the Microsoft Entra Internet Access license for Internet Traffic (coming soon). You must have a combined total of at least 50 licenses from Microsoft Entra ID P1 and Microsoft Entra Internet Access to enable remote network connectivity. For details on how much bandwidth is allocated, see [Understand remote network connectivity](concept-remote-network-connectivity#what-is-the-bandwidth-allocation-for-each-tenant). For more information about remote networks, see [How to create a remote network with Global Secure Access](how-to-create-remote-networks).