---
layout: Conceptual
title: Introduction to Microsoft Global Secure Access Proof-of-Concept Guidance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/gsa-poc-guidance-intro
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: global-secure-access
manager: martinco
description: Learn how to deploy and test Microsoft Global Secure Access as a proof of concept with Microsoft Entra Internet Access, Microsoft Entra Private Access, and the Microsoft traffic profile.
ms.topic: concept-article
ms.date: 2025-01-22T00:00:00.0000000Z
locale: en-us
document_id: f35cbe92-e0ee-2fe9-4084-d11de4946172
document_version_independent_id: f35cbe92-e0ee-2fe9-4084-d11de4946172
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/gsa-poc-guidance-intro.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/gsa-poc-guidance-intro
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/gsa-poc-guidance-intro.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cebbf0e1-01a8-78e0-dcd7-e73fb1e203bd
---

# Introduction to Microsoft Global Secure Access Proof-of-Concept Guidance - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Global Secure Access with Microsoft Entra Internet Access, Microsoft Entra Private Access, and the Microsoft traffic profile.

Detailed guidance continues in these articles:

- [Configure Microsoft Entra Private Access](gsa-poc-private-access)
- [Configure Microsoft Entra Internet Access](gsa-poc-internet-access)

This guide assumes that you're running a PoC in a production environment. Running a PoC in a test environment might give you more flexibility.

Note

All PoC testing is dependent on traffic profile updates synchronizing to the client device. Synchronization can take up to 20 minutes to complete.

Follow the sections in this article to help ensure a successful PoC launch.

## Understand the products

Understanding the products and their core concepts is the first step toward running a successful PoC. Start with the resources in this section.

### Microsoft's Security Service Edge (SSE) solution

- [What is Microsoft's Security Service Edge (SSE) solution?](../global-secure-access/overview-what-is-global-secure-access#microsofts-security-service-edge-sse-solution)
- [Accelerate your Zero Trust journey with unified access controls](https://www.youtube.com/watch?v=_EGK57wwHfs) (video)

### Microsoft Entra Internet Access

- [Learn about Microsoft Entra Internet Access](../global-secure-access/concept-internet-access)
- [Identity-centric Microsoft Entra Internet Access protections](https://www.youtube.com/watch?v=-dKzwX5tRkg) (video)

### Microsoft Entra Private Access

- [Understand the Microsoft Entra private network connector](../global-secure-access/concept-connectors)
- [Replace VPNs for on-premises resources by using Microsoft Entra Private Access](https://www.youtube.com/watch?v=_dw2JVqA4E8) (video)

### Microsoft Global Secure Access

- [Global Secure Access licensing overview](../global-secure-access/overview-what-is-global-secure-access#licensing-overview)
- [Introduction to the Microsoft Global Secure Access deployment guide](gsa-deployment-guide-intro)

## Identify use cases

While you design your PoC, identify relevant use cases and plan for appropriate configuration and testing.

### Microsoft Entra Private Access use cases

Consider the following questions as you map out your Microsoft Entra Private Access use cases:

- **Are you using a VPN today? The best way to start is to test the VPN replacement scenario.** This scenario gives you the ability to publish all the same resources that users access through the VPN and help protect them by using Microsoft Entra ID. From that point onward, you can segment access.

    To define access to specific resources that only selected users should access, create enterprise apps. For example, only administrators should be able to remotely access servers. To understand the recommended configuration, review the [VPN replacement](gsa-poc-private-access#replace-vpn) scenario.
- **What device types do you plan to test? Users' day-to-day work devices or separate test devices?** If you plan to use work devices, consider testing the [VPN replacement](gsa-poc-private-access#replace-vpn) scenario so that you can use Microsoft Entra Private Access for all your daily work.

    If you decide to [publish only certain resources by using Microsoft Entra Private Access](gsa-poc-private-access#provide-access-to-specific-apps), consider how users authenticate to those resources and if you require [single sign-on (SSO) with Active Directory](gsa-poc-private-access#use-kerberos-sso-to-active-directory-resources). You also might need to switch to using your VPN to access other resources that you need during your day.

### Microsoft Entra Internet Access use cases

You can test several Microsoft Entra Internet Access and Microsoft Entra Internet Access for Microsoft Services scenarios in your PoC. Consider testing coexistence with other solutions, as the [Learn about Security Service Edge (SSE) coexistence with Microsoft and Cisco](../global-secure-access/how-to-cisco-coexistence) article describes.

- **Do you need to block or allow certain fully qualified domain names (FQDNs) or web categories from access by all users when they're using a managed device?** If you plan to block or allow most of your user base's access to specific FQDNs or web categories, consider testing the [Create a baseline policy that applies to all internet access traffic routed through the service](gsa-poc-internet-access#create-a-baseline-profile-that-applies-to-all-internet-traffic-routed-through-the-service) use case. You can create and apply the baseline policy to all users without needing to create Conditional Access policies. If necessary, you can override it for subsets of users.
- **Do you need to block certain groups from accessing websites based on category or FQDN?** If you need to prevent specific groups of users from accessing FQDNs or web categories, consider testing the [Block a group from accessing websites based on category](gsa-poc-internet-access#block-a-group-from-accessing-websites-based-on-category) and [Block a group from accessing websites based on FQDN](gsa-poc-internet-access#block-a-group-from-accessing-websites-based-on-fqdn) use cases.
- **Do you need to override broad block or allow policies for certain users or specific circumstances?** If you want to allow specific users or groups to access a blocked website, consider testing the [Allow a user to access a blocked website](gsa-poc-internet-access#allow-a-user-to-access-a-blocked-website) use case.
- **Do you need to manage or control access to your Microsoft data?** You can use the Microsoft traffic profile to enable Global Secure Access to acquire and route SharePoint Online, Exchange Online, and other Microsoft traffic through the Global Secure Access cloud services. Test this scenario with the [Enable and manage the Microsoft traffic forwarding profile](../global-secure-access/how-to-manage-microsoft-profile) use case.
- **Do you need to control whether your users can use your organization's managed devices to sign in to other Entra ID tenants?** Consider testing [Universal Tenant Restrictions](../global-secure-access/how-to-universal-tenant-restrictions).

## Scope and define success criteria

Use the [PoC kickoff deck](https://download.microsoft.com/download/4/7/9/4793b9f2-35fe-4513-9c7e-31482a003bbc/GSA_POC_kickoff.pptx) to plan your PoC. Walk through the high-level requirements to identify key stakeholders to include in the project. Then decide on in-scope scenarios and agree on a timeline.

## Meet prerequisites

Ensure that you meet these prerequisites for your PoC:

- A Microsoft Entra ID test tenant.
- A user with the Global Secure Access Administrator, Application Administrator, and Conditional Access Administrator roles. Refer to [Microsoft Global Secure Access built-in roles](../global-secure-access/reference-role-based-permissions).
- At least one Microsoft Entra ID test user account.
- At least one client device for user testing. To test remote access, make sure that this device has only Microsoft Entra Internet Access and can't connect directly to your private network.

    - Windows 11 devices must be either Microsoft Entra ID joined or hybrid joined to your test tenant.
    - For Android and iOS devices, install the Microsoft Defender app and register it in your test tenant.
- The appropriate paid or trial licenses:

    - [Global Secure Access licensing overview](../global-secure-access/overview-what-is-global-secure-access#licensing-overview)
    - [Microsoft Entra Suite trial licenses](https://aka.ms/EntraSuiteTrial)
    - [Microsoft Entra Internet Access trial licenses](https://aka.ms/InternetAccessTrial)
    - [Microsoft Entra Private Access trial licenses](https://aka.ms/PrivateAccessTrial)

To test Microsoft Entra Private Access scenarios, ensure that you meet these prerequisites:

- Deploy at least one Windows Server 2019 or 2022 machine with your private or on-premises resources. This server must have a line of sight to the resources that you want to make available through Microsoft Entra Private Access. It should be able to access [Microsoft URLs](../global-secure-access/how-to-configure-connectors#allow-access-to-urls).
- To test VPN replacement, you need the IP ranges and FQDNs that are used for full access to your corporate network.
- To test per-app Zero Trust network access by using Microsoft Entra Private Access, identify one or more test applications. You need the IP addresses or FQDNs, protocols, and ports that clients use when they access each test application.

To test Microsoft traffic scenarios, you need Microsoft 365 products such as SharePoint Online or Exchange Online.

## Configure the product for use cases

After you meet the prerequisites, use the following sections as steps to configure your test environment.

### 1. Enable the product in your tenant

Enable each product's traffic profile for Global Secure Access to acquire and tunnel traffic for that product area. Assign users and groups to the profile so that the Global Secure Access client for those users acquires and routes traffic to Global Secure Access. The following articles define the required [roles](../global-secure-access/reference-role-based-permissions#role-based-permissions) for those tasks:

- [Enable and manage the Microsoft profile](../global-secure-access/how-to-manage-microsoft-profile)
- [Manage the Private Access profile](../global-secure-access/how-to-manage-private-access-profile)
- [Manage the Internet Access profile](../global-secure-access/how-to-manage-internet-access-profile)
- [Assign users and groups to traffic forwarding profiles](../global-secure-access/how-to-manage-users-groups-assignment)

### 2. Install the Global Secure Access client

Install the Global Secure Access client on each client device that connects to Global Secure Access services. Ensure that your test devices meet prerequisites. Review [Known limitations for Global Secure Access](../global-secure-access/reference-current-known-limitations).

- Install the [Global Secure Access client for Windows](../global-secure-access/how-to-install-windows-client).
- Install the [Global Secure Access client for macOS](../global-secure-access/how-to-install-macos-client).
- Install the [Global Secure Access client for Android](../global-secure-access/how-to-install-android-client).
- Install the [Global Secure Access client for iOS (preview)](../global-secure-access/how-to-install-ios-client).

To deploy the client to multiple devices, use Intune or another mobile device management solution.

### 3. Configure Microsoft Entra Private Access

For detailed steps, see the [Configure Microsoft Entra Private Access](gsa-poc-private-access) article.

### 4. Configure Microsoft Entra Internet Access

For detailed steps, see the [Configure Microsoft Entra Internet Access](gsa-poc-internet-access) article.

## Troubleshoot

If you have problems with your PoC, these articles can help you with troubleshooting, logging, and monitoring:

- [Global Secure Access FAQ](../global-secure-access/resource-faq)
- [Troubleshoot problems installing the Microsoft Entra private network connector](../global-secure-access/troubleshoot-connectors)
- [Troubleshoot the Global Secure Access client: Diagnostics](../global-secure-access/troubleshoot-global-secure-access-client-advanced-diagnostics)
- [Troubleshoot the Global Secure Access client: Health check tab](../global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check)
- [Troubleshoot a Distributed File System issue with Global Secure Access](../global-secure-access/troubleshoot-distributed-file-system)
- [Global Secure Access logs and monitoring](../global-secure-access/concept-global-secure-access-logs-monitoring)
- [How to use workbooks with Global Secure Access](../global-secure-access/how-to-use-workbooks)