---
layout: Conceptual
title: 'Tutorial: Configure Intelligent Local Access - Microsoft Entra Private Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-private-access-intelligent-local-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure Intelligent Local Access (ILA) in Microsoft Entra Private Access to optimize traffic flow when users are on the corporate network.
ms.topic: tutorial
ms.date: 2026-03-11T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 516f793e-eebf-3b4c-fec0-00c9c55c09a6
document_version_independent_id: 516f793e-eebf-3b4c-fec0-00c9c55c09a6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-private-access-intelligent-local-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-private-access-intelligent-local-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-private-access-intelligent-local-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2e4ea89b-a8aa-dfd0-7e23-1605c1792588
---

# Tutorial: Configure Intelligent Local Access - Microsoft Entra Private Access | Microsoft Learn

Intelligent Local Access (ILA) is a feature in Microsoft Entra Private Access that optimizes traffic flow when users are on the corporate network. When the Global Secure Access client detects that the user is inside the corporate network using DNS probes, traffic to specified Private Access applications can bypass the cloud backend and connect directly. This reduces latency and improves user experience while maintaining a consistent security posture.

In this tutorial, you learn how to:

- Create a Private Network with Intelligent Local Access configuration
- Link the Private Network to a target application
- Verify ILA flow on the client

## Key concepts

Tip

ILA is a **path optimization** capability, not a separate access model.

- Off corporate network: traffic follows standard Private Access tunnel path.
- On corporate network (probe match): configured app traffic can take a local/bypassed route.

Detection is based on DNS probe logic (server + FQDN + expected resolution result). When the probe result matches your configured corporate network signature, the client knows local reachability is available and can avoid unnecessary cloud traversal for targeted resources.

Even if the user is on the corporate network and ILA takes effect, Conditional Access policies for Private Access applications will still apply. This gives you a dual benefit: Zero Trust access continuity for remote users and improved performance for in-office users.

### Step 1: Create a Private Network with ILA configuration

To enable Intelligent Local Access, you need to create a Private Network that defines how the Global Secure Access client identifies it is on the corporate network.

1. From the Microsoft Entra admin center, browse to **Global Secure Access &gt; Connect &gt; Private networks**.
2. Select **Add Private network**.
3. In the **Add Private network**panel, configure the following:
    - **Name**: Enter a friendly name for the network (e.g., `Contoso Corporate Network`)
    - **DNS Servers**: Enter the DNS server address used for DNS resolution on the corporate network. This should be an IPv4 address, such as `10.10.2.1`, that identifies a DNS server on the network.
    - **Fully qualified domain name (FQDN)**: Enter the FQDN that needs to be resolved to identify the corporate network
    - **Resolved to IP address type**: Select the appropriate type based on your network configuration, such as **IP address**
    - **Resolved to IP address value**: Enter the appropriate value to which the DNS query will resolve
4. Under **Target Resource**, select **Select applications**.
5. Select an application you want to configure for Intelligent Local Access.
6. Select **Create**.

Note

The Global Secure Access client uses DNS probes to determine if the client is inside the corporate network. When the DNS query for the specified FQDN resolves to an IP address within the configured range, the client knows it's on the corporate network and can enable local bypass for the specified applications.

Tip

You can create multiple Private Networks with different target resources to control which applications use Intelligent Local Access on which networks based on your organization's requirements.

### Step 2: Verify ILA flow on the client

To verify that Intelligent Local Access is working correctly, use the **Advanced Diagnostics** tool in the **Global Secure Access** client.

1. On the client device, right-click the **Global Secure Access** icon in the system tray and select **Advanced diagnostics**.
2. Select the **Traffic** tab, then select **Start Collecting**.
3. In the filter options, add a filter for **Destination IP/FQDN** and enter the FQDN of the resource you want to test.

    Note

    Remove the default filter for `Action == Tunnel` to see all traffic including bypassed traffic.
4. Access the Private Access application you configured with ILA.
5. Review the network traffic results and verify the following:

    - **Connection Status**: Should show as **Bypassed**
    - **Action**: Should show as **Local**

    ![Screenshot showing network traffic capture with Intelligent Local Access bypassed traffic.](media/tutorial-private-access-intelligent-local-access/intelligent-local-access-traffic-capture.png)

Note

You can also review Windows Event Logs by opening **Event Viewer** and navigating to **Application and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **Global Secure Access Client** &gt; **Operational**. You can then search for Event ID's 217 and 218, which are triggered when the GSA client detects that it is now on or off the corporate network.

To fully understand ILA behavior, you can test from both locations:

| Location | Expected behavior |
| --- | --- |
| **On corporate network** | Traffic is bypassed locally (Action: `Local`) |
| **Off corporate network (remote)** | Traffic goes through the tunnel (Action: `Tunnel`) |

Note

The DNS probe used by Intelligent Local Access always bypasses GSA tunneling even if the DNS probe matches a suffix configured in Private DNS. This ensures that when the user is off the corporate network, the DNS probe will fail to resolve to the expected IP range, and traffic will be tunneled as normal.

## Troubleshooting

If ILA isn't working as expected:

1. **Verify DNS configuration**: Ensure the DNS record is correctly configured on the private network.
2. **Check IP resolution**: Verify from the client that the FQDN resolves to an IP address within the configured range when on the private network. For example, when on the private network, run `nslookup -v your.domain.com 10.0.100.10` (pointing to your DNS server's IP) then verify it resolves to the expected values.
3. **Review client logs**: Use the **Advanced Diagnostics** tool to review connection attempts and identify any issues.
4. **Confirm target resource assignment**: Verify that the correct Quick Access or enterprise application is linked to the Private Network.

## What you learned

In this exercise, you accomplished the following:

- **Defined corporate network detection signals** - You configured DNS-based indicators used by the client to determine when it is on or off the private network.
- **Scoped ILA to specific target resources** - You controlled which apps can bypass tunnel routing when on the private network.
- **Validated behavior in diagnostics** - You confirmed expected `Local` vs `Tunnel` actions by network location.

ILA improves user experience and reduces unnecessary tunnel usage without requiring users to change how they access applications.