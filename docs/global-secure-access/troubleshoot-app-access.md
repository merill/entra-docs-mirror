---
layout: Conceptual
title: Troubleshoot application access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-app-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to troubleshoot application access problems with the Global Secure Access Windows client.
ms.topic: troubleshooting-general
ms.date: 2025-12-03T00:00:00.0000000Z
ms.reviewer: andresc, jricketts
locale: en-us
document_id: 8bc81662-c731-c176-7ab3-301a7e562394
document_version_independent_id: 8bc81662-c731-c176-7ab3-301a7e562394
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-app-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-app-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-app-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: ff6a6ce5-8f60-e408-de24-46e3a960c941
---

# Troubleshoot application access - Global Secure Access | Microsoft Learn

This article helps you identify and resolve application access problems with the Global Secure Access Windows client.

## Troubleshoot client connection

To check that the client successfully connects to all channels, double-click the tray icon. Reference [Troubleshoot the Global Secure Access client: Health check tab](troubleshoot-global-secure-access-client-diagnostics-health-check) for known issue troubleshooting guidance for the **Health check** tab in the Advanced diagnostics utility.

Review Global Secure Access Windows client [known limitations](how-to-install-windows-client#known-limitations).

## Does Global Secure Access acquire application traffic?

This section helps you understand whether Global Secure Access acquires the traffic that the application generates.

1. To troubleshoot client traffic, go to **Advanced diagnostics** &gt; **Traffic**.
2. Start the traffic collection.
3. Reproduce what you're trying to do.
4. Observe **Traffic** activity.
5. If you know the target IPs and ports your app should connect to, filter by them and remove unrelated traffic, which makes troubleshooting easier. In the following example screenshot, filter `Destination Port == 3389` helps to troubleshoot Remote Desktop Protocol (RDP) connections.

    [![Screenshot of Network traffic Destination port filter.](media/troubleshoot-app-access/network-traffic-destination-port.png)](media/troubleshoot-app-access/network-traffic-destination-port-expanded.png#lightbox)

In the previous example screenshot, the default filter `Action==Tunnel` results with a line (or flow) that indicates the Global Secure Access client is:

- Seeing the traffic.
- Evaluating the protocol, destination IP or FQDN, and port against the traffic forwarding rules.
- Determining that the traffic should tunnel to the Global Secure Access service. Otherwise, the **Connection Status** would say **Bypassed**.

If you don't know the destination IPs or ports, you can try filtering by process name. In the previous example, you can filter by process name `mstsc.exe`.

## Other traffic bypass problems

In **Traffic forwarding** &gt; **Microsoft traffic profile** and **Internet access profile**, you can configure bypass rules to defined destinations that Global Secure Access clients shouldn't handle. This scenario might cause the Global Secure Access client to not acquire and tunnel traffic.

[![Screenshot of Internet access policies Internet traffic profile.](media/troubleshoot-app-access/internet-access-policies-bypass.png)](media/troubleshoot-app-access/internet-access-policies-bypass-expanded.png#lightbox)

## App connectivity requirements

This section helps you understand how apps might require connectivity to destinations not included in existing app segments.

Applications might require connectivity to different services with multiple destination IPs or ports or that use User Datagram Protocol (UDP) or Transmission Control Protocol (TCP).

It's common to have applications that require connectivity to destinations not included in existing app segments. Follow these steps to determine if this scenario applies to you.

In the following example, the client successfully creates and tunnels an RDP connection. However, the user reports performance problems. To understand if traffic is being bypassed, you can remove the default `Action==Tunnel` filter, add a process name filter, and reproduce the problem. Then you can observe that `mstsc.exe` is trying to send traffic to the RDP server on 3389/UDP. The Global Secure Access client bypasses the traffic because it doesn't match a forwarding profile rule.

[![Screenshot of Network traffic Process name filter.](media/troubleshoot-app-access/network-traffic-process-name.png)](media/troubleshoot-app-access/network-traffic-process-name-expanded.png#lightbox)

In some cases, it's not as easy to spot missing traffic because the process that initiates the connection isn't the application process. A common example is authentication traffic.

Your application traffic might be correctly tunneled. If the app fails because of authentication failure, you might need to add filters to eliminate unrelated traffic from the collection. This approach might make it easier to spot what else is happening or what the Global Secure Access client bypassed.

For example, a user accesses a file share from a Windows 11 device. Observe the following conditions:

- Windows tries Server Message Block (SMB) over QUIC, which uses 443/UDP.
- `lsass.exe` (Local Security Authority process) initiates connections to domain controllers on port 88/TCP (Kerberos).
- In this case, the authentication traffic is being tunneled because the corresponding rules are created. If this case isn't true, Windows generally falls back to NTLM which doesn't require other ports but, depending on configuration, this case might not be true.
- We see a connection on 445/TCP, which is the SMB protocol used for file share access.

[![Screenshot of Network traffic filter for Kerberos.](media/troubleshoot-app-access/network-traffic-filter-kerberos.png)](media/troubleshoot-app-access/network-traffic-filter-kerberos-expanded.png#lightbox)

## Flows with zero sent or received bytes

Flows that show some sent bytes but zero received bytes might indicate a server or Private Connector problem. Use the Correlation Vector ID to investigate with [Traffic logs](how-to-view-traffic-logs). In Traffic logs, the Correlation Vector ID is called **Connection ID**.

In some cases, you might see traffic that the Global Secure Access client acquires but see no outbound packets. In the following example, **Bytes sent** is 0. This behavior might occur when a Windows Firewall rule drops or blocks specific traffic. In the previous example, a Windows Firewall rule was blocking RDP.

[![Screenshot of Network traffic Bytes sent.](media/troubleshoot-app-access/network-traffic-bytes-sent.png)](media/troubleshoot-app-access/network-traffic-bytes-sent-expanded.png#lightbox)

## How does DNS work with Global Secure Access?

The Global Secure Access client works with fully qualified domain names (FQDN) in two ways.

If you create rules (app segments) with FQDNs, the client intercepts DNS query responses sent to the DNS server defined on the device, usually with Dynamic Host Configuration Protocol (DHCP). If the query (for example, `fs.contoso.local`) matches a rule, irrespective of the result (for example, a user at home typically can't resolve corporate network names), Global Secure Access rewrites the query response to a dynamic synthetic IP. Then, if the destination protocol and port match a rule, the Global Secure Access cloud service for Internet traffic, or a private network connector for Microsoft Entra Private Access, resolves the name.

If you use private DNS, things get more interesting. For each configured private DNS suffix, the Global Secure Access client adds a Name Resolution Policy Table (NRPT) rule to direct those queries to a synthetic IP (usually `6.6.255.254`). The NRPT allows you to configure name resolution request routing to specified DNS servers for specified namespaces. It overrides the default behavior of sending these requests to the DNS server configured on your computer's network adapter.

Global Secure Access uses NRPT policies to direct all name resolution for private DNS suffixes to a specific server. A private network connector uses the DNS server configured on the server to tunnel and resolve these queries.

To check NRPT rules, run `Get-DnsClientNrptPolicy`. In the following example, Global Secure Access created two NRPT policies:

- One for a suffix configured on private DNS.
- One to send unqualified names (also known as *single label*) through the tunnel. The Global Secure Access client adds a DNS search suffix for `AppId.globalsecureaccess.local`.

[![Screenshot of Name Resolution Policy Table policy.](media/troubleshoot-app-access/nrpt-policies.png)](media/troubleshoot-app-access/nrpt-policies-expanded.png#lightbox)

After queries resolve, Global Secure Access continues with the IP/port/protocol evaluation to determine if it should acquire and tunnel the traffic.

To troubleshoot DNS resolution, use these options:

- The `Resolve-DnsName` PowerShell command follows NRPT rules.
- `NSLOOKUP` doesn't follow NRPT rules. To force queries with the tunnel, use `nslookup fs.contoso.local 6.6.255.254`.

For more advanced troubleshooting, use the DNS Client log provider. This method helps you understand the DNS servers used, queries sent while certain activity generates (for example, trying to open a file share), and responses.

- To enable the DNS Client log provider, run `wevtutil sl Microsoft-Windows-DNS-Client/Operational /enabled:true`. Remember to disable it after you finish troubleshooting.
- After you reproduce your problem, use PowerShell to filter and display the relevant logs. In the following example, logs are from the last three minutes, filtered by queries that contain `contoso.local`.

```powershell
    $StartDate = (Get-Date).AddMinutes(-3) ; Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-DNS-Client/Operational';StartTime=$Startdate} | where Message -Match contoso.local | Out-GridView
```

## Microsoft Entra Private Access resource access failure

Accessing resources through Private Access might fail for other reasons. Traffic logs can help you troubleshoot issues that might be unrelated to client-side problems. Here are some troubleshooting steps you can follow. Reference [Troubleshoot Global Secure Access client: Advanced Diagnostics](troubleshoot-global-secure-access-client-advanced-diagnostics).

- Capture traffic with the **Advanced Diagnostics** tool. Ensure that it acquires and tunnels the flows. Get and use the **Correlation vector ID** to look up Global Secure Access traffic logs on the Microsoft Entra admin center. Traffic logs show what connector handled the traffic and if errors occurred.
- If there are no errors on traffic logs pointing at problems communicating with private network connectors, obtain and analyze a network capture to see the actual conversations going through the tunnel.

## Apps that don't support concurrent sign-ins from multiple IPs

Some web apps initiate new network connections during the sign-in process. When multiple connectors exist in a connector group, these new sessions might be routed through a different connector than the one that handled the initial sign-in request. If the app doesn't support this behavior, the session breaks, resulting in a failed sign-in. These session disruptions can leave you unable to access certain web applications after signing in, or you might be unexpectedly signed out from a newly added application.

To prevent session disruption:

- Option 1: Pin the app to a connector group that contains only a single connector.
- Option 2: If feasible, temporarily stop the Microsoft Entra Private Access connector service on other connectors in the group during testing.

Note

After creating a new app definition, allow approximately 5–10 minutes for the configuration to propagate and appear on the client.

- Option 3: After confirming the application works through a single connector, enable session persistence. This consistently routes requests from the same user and device through the same connector during the session.See [Configure traffic routing for the app](how-to-configure-per-app-access#configure-traffic-routing-for-the-app).