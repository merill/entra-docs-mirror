---
layout: Conceptual
title: Source IP anchoring with Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/source-ip-anchoring
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure Microsoft Entra Private Access to tunnel specific application traffic through a private network for application's network-based access control policy.
ms.reviewer: jebley, jricketts
ms.subservice: entra-internet-access
ms.topic: how-to
ms.date: 2026-02-21T00:00:00.0000000Z
locale: en-us
document_id: 13205baf-cb33-20c8-4cf6-f975387ee1d7
document_version_independent_id: 13205baf-cb33-20c8-4cf6-f975387ee1d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/source-ip-anchoring.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/source-ip-anchoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/source-ip-anchoring.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 371cd5d5-6541-5d4d-4f0a-4c87d8ea4f49
---

# Source IP anchoring with Global Secure Access - Global Secure Access | Microsoft Learn

Organizations with Software-as-a-Service (SaaS) or Line-of-Business (LOB) applications might enforce specific network locations before allowing access. One approach is to use Microsoft Entra Private Access to route specific web application traffic with a privately controlled network. This approach allows you to enforce specific egress IPs that only your organization uses. This article describes how to configure Microsoft Entra Private Access to tunnel specific application traffic through a private network to satisfy an application's network-based access control policy.

Tip

**Source IP anchoring** and **source IP restoration** are different features. Source IP anchoring (this article) routes application traffic through your private network connector so that a SaaS app sees your known egress IP address. [Source IP restoration](how-to-source-ip-restoration) preserves the user's original public IP address in Microsoft Entra sign-in logs when traffic flows through Global Secure Access. Choose the feature that matches your scenario.

## Configure source IP anchoring to route traffic from a dedicated IP address

To enable application enforcement of a dedicated network, configure an enterprise application with Microsoft Entra Private Access. An example where this configuration might be necessary is when the application allows access with local credentials which are not tied to your identity provider.

This solution acquires application traffic and routes it from the client device. It routes through Microsoft's Secure Service Edge then to a private network with a private network connector. From the private network, the traffic can access the application with internet or any other available private connection. The application sees the traffic as originating from the allowed egress IP address indicating that access is coming from the dedicated network that satisfies its own network access controls.

The following architectural diagram illustrates an example configuration.

[![Diagram of an example architectural configuration.](media/source-ip-anchoring/architectural-diagram-example-inline.png)](media/source-ip-anchoring/architectural-diagram-example-expanded.png#lightbox)

In the example configuration, the application only allows connections that originate from 15.4.23.54, which is the egress IP address of customer's on-premises network. When a user attempts to access the application, the Global Secure Access client acquires and tunnels the traffic through Microsoft's Secure Service Edge where authorization control enforcement (such as Conditional Access) can occur. The traffic tunnels to the on-premises network using the Private Network Connector. Finally, the traffic uses the internet to connect to the web application. The application sees the connection originating from 15.4.23.54 and allows access.

Note

Configuring source IP anchoring is necessary when a SaaS app enforces its own network-based controls. If your requirement is limited to location enforcement from the identity provider, [compliant network check](how-to-compliant-network) is sufficient. Compliant network check enforces network-based access controls at the authentication layer and avoids the need to hairpin traffic through your private network. Global Secure Access binds traffic to your tenant ID to ensure that other organizations using Global Secure Access can't satisfy your Conditional Access policies.

## Prerequisites

Before you get started with configuring source IP anchoring, make sure your environment is ready and compliant.

- You have a SaaS application that enforces its own network-based access control policy.
- Your license includes Microsoft Entra Suite or Microsoft Entra Private Access.
- You enabled the Microsoft Entra Private Access forwarding profile.
- You have the latest version of the [Global Secure Access client](concept-clients).

## Deploy private network connectors

When you meet the prerequisites, perform the following steps to deploy private network connectors:

1. [Install a private network connector](how-to-configure-connectors) in a private network that has outbound connectivity to the destination web application. A good option is to host the connector in an Azure Virtual Network where you control the outbound egress IP. We recommend that you install two or more connectors for resiliency and high availability.
2. Provide the public IP address of the connectors to the SaaS app so that your users can connect to the app.

## Configure source IP anchoring

After you install and configure the private network connectors, perform the following steps to create an enterprise application:

1. Navigate to `entra.microsoft.com`.
2. Select **Global Secure Access** &gt; **Applications &gt; Enterprise applications.**
3. Select **New application**.
4. Enter a name for the application.
5. Select the **Connector Group** that acquires and routes the traffic.
6. Select **Add application segment**.
7. Complete the following fields:

    1. **Destination type** -- Select **Fully qualified domain name**.
    2. **Fully qualified domain name** -- Enter the fully qualified domain name of the web application.
    3. **Ports** -- If the application uses HTTP, enter **80**. If the application uses HTTPS, enter **443**. You might also enter both ports.
    4. **Protocol** -- Select **TCP**.

        ![Screenshot of Create application segment dialog.](media/source-ip-anchoring/create-application-segment.png)
8. Select **Apply**.
9. Select **Save**.
10. Navigate back to **Enterprise applications**. Select the application that you created.
11. Select **Users and groups**.
12. Select **Add user/group**.
13. Select **Users and groups** &gt; **None Selected**.
14. Search for and select the users and groups that you want to assign to this application. Select **Select**.
15. Select **Assign**.

## Validate the configuration

After you configure an enterprise application for the web application, perform the following steps to validate that it's working properly.

1. In the Windows Global Secure Access client, open **Advanced Diagnostics**.
2. Select **Forwarding profile**.
3. Expand **Private access rules**. Validate that the web application's fully qualified domain name (FQDN) is in the list.

    ![ Screenshot of Global Secure Access - Advanced diagnostics - Rules.](media/source-ip-anchoring/advanced-diagnostics-rules.png)
4. Select **Traffic**.
5. Select **Start collecting**.
6. In a browser, navigate to the web application.
7. Return to **Advanced Diagnostics**.
8. Select **Stop collecting.**
9. Validate these settings:

    1. The web application appears under **Destination FQDN**.
    2. The **Channel** field is **Private Access**.
    3. The **Action** field is **Tunnel**.

        [![Screenshot of Global Secure Access - Advanced diagnostics - Network traffic.](media/source-ip-anchoring/advanced-diagnostics-network-traffic-inline.png)](media/source-ip-anchoring/advanced-diagnostics-network-traffic-expanded.png#lightbox)
10. Check the application's logs (not in Microsoft Entra ID). Validate that the application sees the sign-in from an IP address that matches an egress IP of your private network.

## Troubleshooting

Ensure that you disabled QUIC, IPv6, and encrypted DNS. You can find details in our [troubleshooting guide for the Global Secure Access client](troubleshoot-global-secure-access-client-diagnostics-health-check).