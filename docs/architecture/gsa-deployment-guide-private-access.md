---
layout: Conceptual
title: Microsoft Global Secure Access Deployment Guide for Microsoft Entra Private Access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/gsa-deployment-guide-private-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: global-secure-access
manager: martinco
description: Learn how to deploy Microsoft Global Secure Access for Microsoft Entra Private Access
customer intent: As a Microsoft Partner, I want to deploy Microsoft Entra Private Access as a Proof of Concept in my production or test environment.
ms.topic: how-to
ms.date: 2025-01-06T00:00:00.0000000Z
locale: en-us
document_id: dce380f4-32fb-2bb7-f6d7-71f544933cbc
document_version_independent_id: dce380f4-32fb-2bb7-f6d7-71f544933cbc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/gsa-deployment-guide-private-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/gsa-deployment-guide-private-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/gsa-deployment-guide-private-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d018a634-fcad-740c-b5f8-e95944dc46e6
---

# Microsoft Global Secure Access Deployment Guide for Microsoft Entra Private Access - Microsoft Entra | Microsoft Learn

[Microsoft Global Secure Access](../global-secure-access/overview-what-is-global-secure-access) converges network, identity, and endpoint access controls for secure access to any app or resource from any location, device, or identity. It enables and orchestrates access policy management for corporate employees. You can continuously monitor and adjust, in real time, user access to your private apps, Software-as-a-Service (SaaS) apps, and Microsoft endpoints. Continuous monitoring and adjusting helps you to appropriately respond to permission and risk level changes as they occur.

Microsoft Entra Private Access enables you to replace your corporate VPN. It provides your enterprise users with macro- and micro-segmented access to corporate applications that you control with Conditional Access policies. It helps you to:

- Provide Zero Trust point-to-point access to private applications with all ports and protocols. This approach prevents bad actors from lateral movement or port scans on your corporate network.
- Require multifactor authentication when users connect to private applications.
- Tunnel data over Microsoft's vast global private wide area network to maximize secure network communications.

The guidance in this article helps you to test and deploy [Microsoft Entra Private Access](../global-secure-access/concept-private-access) in your production environment as you enter your deployment execution phase. [Microsoft Global Secure Access deployment guide introduction](gsa-deployment-guide-intro) provides guidance on how to initiate, plan, execute, monitor, and close your Global Secure Access deployment project.

## Identify and plan for key use cases

VPN replacement is the primary scenario for Microsoft Entra Private Access. You might have other use cases within this scenario for your deployment. For example, you might need to:

- Apply Conditional Access policies to control users and groups before they connect to private applications.
- Configure multifactor authentication as a requirement to connect to any private app.
- Enable a phased deployment that approaches Zero Trust over time for your Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) -based applications.
- Use fully qualified domain name (FQDN) to connect to virtual networks that overlap or duplicate IP address ranges to configure access to ephemeral environments.
- Privileged Identify Management (PIM) to configure destination segmentation for privileged access.

After you understand the capabilities you require in your use cases, create an inventory to associate your users and groups with these capabilities. Plan to use Quick Access functionality to duplicate your VPN functionality initially so that you can test connectivity and remove your VPN. Then use Application Discovery to identify the application segments your users connect to so that you can then secure connectivity to specific IP addresses, FQDNs, and ports.

## Test and deploy Microsoft Entra Private Access

At this point, you completed the initiate and plan stages of your Secure Access Service Edge (SASE) deployment project. You understand what you need to implement for whom. You defined the users to enable in each wave. You have a schedule for each wave's deployment. You have met [licensing requirements](../global-secure-access/overview-what-is-global-secure-access#licensing-overview). You're ready to enable Microsoft Entra Private Access.

1. Create end user communications to set expectations and provide an escalation path.
2. Create a roll-back plan that defines the circumstances and procedures for when you remove Global Secure Access client from a user device or disable the traffic forwarding profile.
3. [Create a Microsoft Entra group](../fundamentals/how-to-manage-groups) that includes your pilot users.
4. Enable the [Microsoft Entra Private Access traffic forwarding profile](../global-secure-access/how-to-manage-private-access-profile) and assign your pilot group. [Assign users and groups to traffic forwarding profiles](../global-secure-access/how-to-manage-users-groups-assignment).
5. Provision servers or virtual machines that have line of sight access to your applications to function as connectors, providing outbound connectivity to applications for your users. Consider load balancing scenarios and capacity requirements for acceptable performance. [Configure connectors for Microsoft Entra Private Access](../global-secure-access/how-to-configure-connectors) on each connector machine.
6. If you have an inventory of enterprise applications, [configure per-app access using Global Secure Access applications](../global-secure-access/how-to-configure-per-app-access). If not, [configure Quick Access for Global Secure Access](../global-secure-access/how-to-configure-quick-access).
7. Communicate expectations to your pilot group.
8. Deploy the [Global Secure Access client for Windows](../global-secure-access/how-to-install-windows-client) on devices for your pilot group to test.
9. Create [Conditional Access policies](../global-secure-access/how-to-configure-per-app-access#assign-conditional-access-policies) per your security requirements to apply to your pilot group when these users connect to your published Global Secure Access Enterprise applications.
10. Have your pilot users test your configuration.
11. If needed, update your configuration and retest. If needed, initiate roll-back plan.
12. As needed, iterate changes to your end user communications and deployment plan.

## Configure per-app access

To maximize the value of your Microsoft Entra Private Access deployment, you should transition from Quick Access to per-app access. You can use [Application Discovery](../global-secure-access/how-to-application-discovery) feature to quickly create Global Secure Access applications from app segments your users access. You can also use [Global Secure Access Enterprise applications](../global-secure-access/how-to-configure-per-app-access) to do create them manually, or you can use [PowerShell](gsa-poc-private-access#use-powershell-to-manage-microsoft-entra-private-access) to automate creation.

1. Create the application and scope it to either all users assigned to Quick Access (recommended) or all users that need to access the specific application.
2. Add at least one app segment to the application. You don't need to add all app segments at the same time. You might prefer to add them slowly so that you can validate traffic flow for each segment.
3. Notice that traffic to these app segments no longer appears in Quick Access. Use Quick Access to identify app segments that you need to configure as Global Secure Access applications.
4. Continue to create Global Secure Access applications until no app segments appear in Quick Access.
5. Disable Quick Access.

After your pilot is complete, you should have a repeatable process and understand how to proceed with each wave of users in your production deployment.

1. Identify the groups that contain your wave of users.
2. Notify your support team of the scheduled wave and its included users.
3. Send planned and prepared end user communications.
4. Assign the groups to the Microsoft Entra Private Access traffic forwarding profile.
5. Deploy the Global Secure Access Client on devices for the wave's users.
6. If needed, deploy more private network connectors and create more Global Secure Access Enterprise applications.
7. If needed, create Conditional Access policies to apply to the wave's users when they connect to these applications.
8. Update your configuration. Test again to address issues, If needed, initiate roll-back plan.
9. As needed, iterate changes to your end user communications and deployment plan.