---
layout: Conceptual
title: Secure hybrid access, protect legacy apps with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/secure-hybrid-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Find partner solutions to integrate your legacy on-premises, public cloud, or private cloud applications with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2023-01-17T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: not-enterprise-apps
locale: en-us
document_id: 639afd75-5ffa-3dc3-a256-19992958cdc9
document_version_independent_id: c269dd0f-607a-99a9-162b-b0ad5b186286
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/secure-hybrid-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/secure-hybrid-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/secure-hybrid-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4ede131a-2692-a023-cf03-16a446ae401a
---

# Secure hybrid access, protect legacy apps with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, learn to protect your on-premises and cloud legacy authentication applications by connecting them to Microsoft Entra ID.

- **Application Proxy**:

    - [Remote access to on-premises applications through Microsoft Entra application proxy](/en-us/entra/identity/app-proxy)
    - Protect users, apps, and data in the cloud and on-premises
    - [Use it to publish on-premises web applications externally](../app-proxy/overview-what-is-app-proxy)
- **Secure hybrid access through Microsoft Entra ID partner integrations**:

    - Pre-built solutions
    - [Apply Conditional Access policies per application](secure-hybrid-access-integrations#apply-conditional-access-policies)

In addition to Application Proxy, you can strengthen your security posture with [Microsoft Entra Conditional Access](../conditional-access/overview) and [Microsoft Entra ID Protection](../../id-protection/overview-identity-protection).

## Single sign-on and multifactor authentication

With Microsoft Entra ID as an identity provider (IdP), you can use modern authentication and authorization methods like [single sign-on (SSO)](what-is-single-sign-on) and [Microsoft Entra multifactor authentication](../authentication/concept-mfa-howitworks) to secure legacy, on-premises applications.

## Secure hybrid access with Application Proxy

Use Application Proxy to protect users, apps, and data in the cloud, and on premises. Use this tool for secure remote access to on-premises web applications. Users don’t need to use a virtual private network (VPN); they connect to applications from devices with SSO.

Learn more:

- [Remote access to on-premises applications through Microsoft Entra application proxy](/en-us/entra/identity/app-proxy)
- [Tutorial: Add an on-premises application for remote access through Application Proxy in Microsoft Entra ID](../app-proxy/application-proxy-add-on-premises-application)
- [How to configure SSO to an Application Proxy application](../app-proxy/how-to-configure-sso)
- [Using Microsoft Entra application proxy to publish on-premises apps for remote users](../app-proxy/overview-what-is-app-proxy)

### Application publishing and access management

Use Application Proxy remote access as a service to publish applications to users outside the corporate network. Help improve your cloud access management without requiring modification to your on-premises applications. Plan a [Microsoft Entra application proxy deployment](../app-proxy/conceptual-deployment-plan).

## Partner integrations for apps: on-premises and legacy authentication

Microsoft partners with various companies that deliver pre-built solutions for on-premises applications, and applications that use legacy authentication. The following diagram illustrates a user flow from sign-in to secure access to apps and data.

![Diagram of secure hybrid access integrations and Application Proxy providing user access.](media/secure-hybrid-access/secure-hybrid-access.png)

### Secure hybrid access through Microsoft Entra ID partner integrations

The following partners offer solutions to support [Conditional Access policies per application](secure-hybrid-access-integrations#apply-conditional-access-policies). Use the tables in the following sections to learn about the partners and Microsoft Entra integration documentation.

| Partner | Integration documentation |
| --- | --- |
| Akamai Technologies | [Tutorial: Microsoft Entra SSO integration with Akamai](../saas-apps/akamai-tutorial) |
| Citrix Systems, Inc. | [Tutorial: Microsoft Entra SSO integration with Citrix ADC SAML Connector for Microsoft Entra ID (Kerberos-based authentication)](../saas-apps/citrix-netscaler-tutorial) |
| Cloudflare, Inc. | [Tutorial: Configure Cloudflare with Microsoft Entra ID for secure hybrid access](cloudflare-integration) |
| Datawiza | [Tutorial: Configure Secure Hybrid Access with Microsoft Entra ID and Datawiza](datawiza-configure-sha) |
| F5, Inc. | [Integrate F5 BIG-IP with Microsoft Entra ID](f5-integration)[Tutorial: Configure F5 BIG-IP SSL-VPN for Microsoft Entra SSO](f5-passwordless-vpn) |
| Progress Software Corporation, Progress Kemp | [Tutorial: Microsoft Entra SSO integration with Kemp LoadMaster Microsoft Entra integration](../saas-apps/kemp-tutorial) |
| Perimeter 81 Ltd. | [Tutorial: Microsoft Entra SSO integration with Perimeter 81](../saas-apps/perimeter-81-tutorial) |
| Silverfort | [Tutorial: Configure Secure Hybrid Access with Microsoft Entra ID and Silverfort](silverfort-integration) |
| Strata Identity, Inc. | [Integrate Microsoft Entra SSO with Maverics Identity Orchestrator SAML Connector](../saas-apps/maverics-identity-orchestrator-saml-connector-tutorial) |

#### Partners with pre-built solutions and integration documentation

| Partner | Integration documentation |
| --- | --- |
| Amazon Web Service, Inc. | [Tutorial: Microsoft Entra SSO integration with AWS ClientVPN](../saas-apps/aws-clientvpn-tutorial) |
| Check Point Software Technologies Ltd. | [Tutorial: Microsoft Entra single SSO integration with Check Point Remote Secure Access VPN](../saas-apps/check-point-remote-access-vpn-tutorial) |
| Cisco Systems, Inc. | [Tutorial: Microsoft Entra SSO integration with Cisco Secure Firewall - Secure Client](../saas-apps/cisco-secure-firewall-secure-client) |
| Fortinet, Inc. | [Tutorial: Microsoft Entra SSO integration with FortiGate SSL VPN](../saas-apps/fortigate-ssl-vpn-tutorial) |
| Palo Alto Networks | [Tutorial: Microsoft Entra SSO integration with Palo Alto Networks Admin UI](../saas-apps/paloaltoadmin-tutorial) |
| Pulse Secure | [Tutorial: Microsoft Entra SSO integration with Pulse Connect Secure (PCS)](../saas-apps/pulse-secure-pcs-tutorial)[Tutorial: Microsoft Entra SSO integration with Pulse Secure Virtual Traffic Manager](../saas-apps/pulse-secure-virtual-traffic-manager-tutorial) |
| Zscaler, Inc. | [Tutorial: Integrate Zscaler Private Access with Microsoft Entra ID](../saas-apps/zscalerprivateaccess-tutorial) |