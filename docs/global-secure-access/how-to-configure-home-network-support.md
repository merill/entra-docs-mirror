---
layout: Conceptual
title: Configure home network support for Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-home-network-support
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure home network support so users can access local resources while Microsoft Entra Private Access remains enabled.
ms.topic: how-to
ms.date: 2026-10-13T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 5e8aef2a-b5df-550e-f4e8-367894b19302
document_version_independent_id: 5e8aef2a-b5df-550e-f4e8-367894b19302
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-home-network-support.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-home-network-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-home-network-support.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: 8aa3c225-53ac-936a-119b-ae948cea57b0
---

# Configure home network support for Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

Home network support in Microsoft Entra Private Access helps users connect to resources on their directly connected local network while Private Access remains enabled. For example, users can connect to a home printer, router, wireless display adapter, or locally hosted virtual machine without disconnecting the Global Secure Access client.

This capability is useful when a Private Access application segment overlaps the user's local subnet. An organization might configure a broad private IP range, such as `10.0.0.0/8` or `192.168.0.0/16`, while a user's home network uses an address within the same range. Without home network support, the Global Secure Access client can acquire traffic intended for the local resource and route it through Private Access, breaking local access.

When **Prefer Local Network** is enabled, the client identifies the directly connected local subnet and sends matching traffic directly to the local network.

Note

Home network support is currently in preview. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here. For more information, see the [Microsoft Entra preview terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

Before you begin, make sure you have:

- A Microsoft Entra Private Access or Microsoft Entra Suite license.
- A configured and enabled Private Access traffic forwarding profile.
- A supported Global Secure Access client with Private Access connected.
- The [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role to manage traffic forwarding profiles.

## How home network support works

The Global Secure Access client uses the IP address and subnet mask assigned to a network adapter to calculate the directly connected local subnet.

For example, if an adapter has the address `192.168.4.69/22`, the calculated local subnet is `192.168.4.0/22`. When **Prefer Local Network** is enabled, traffic to a destination in that subnet remains on the local network instead of being acquired by Private Access.

Home network support affects Private Access traffic only. It doesn't bypass Microsoft traffic or internet traffic forwarding policies.

## Enable home network support

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as a Global Secure Access Administrator.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Switch to the new v2 experience, if you haven't already.
4. Open the Private Access traffic forwarding profile that applies to the target users.
5. Enable the **Allow local subnet bypass** setting.
6. Save the profile.

![Screenshot of the Private Access traffic forwarding profile Basics page with Allow local subnet bypass enabled.](media/how-to-configure-home-network-support/allow-local-subnet-bypass.png)

After the updated profile reaches the client, the user can manage the local network preference from the Global Secure Access client.

## Enable Prefer Local Network on the client

1. Open the Global Secure Access client.
2. Select **Settings**.
3. Turn on **Prefer Local Network**.
4. Connect to the local resource again.

![Screenshot of Global Secure Access client Settings with Prefer Local Network turned on.](media/how-to-configure-home-network-support/prefer-local-network.png)

The preference remains in effect as the device changes networks. The client calculates the applicable local subnet for the current network connection.

## Understand routing behavior

When **Prefer Local Network** is enabled, routing is evaluated in the following order:

1. Intelligent Local Access, when the configured corporate network detection and application conditions are met.
2. Home network support for a destination in an eligible directly connected local subnet.
3. Normal Private Access traffic acquisition and tunneling.

Intelligent Local Access takes precedence so that its authentication requirements can be applied.

### Overlapping corporate and local destinations

A local resource and a corporate private application can use the same IP address or subnet. When **Prefer Local Network** is enabled, a matching destination uses the local path. The corporate resource in the overlapping range isn't reachable through Private Access from that network.

To reach the corporate resource, the user can temporarily turn off **Prefer Local Network**. The client then applies the organization's Private Access forwarding rules.

Caution

Enable this capability only for users who need access to local resources. Where possible, avoid configuring corporate applications with address ranges that are likely to overlap users' directly connected home subnets.

## Verify local network routing

Use **Advanced diagnostics** in the Global Secure Access client to verify the routing decision:

1. Open the Global Secure Access client.
2. Select **Troubleshooting** &gt; **Advanced diagnostics**.
3. In **Forwarding Profile**, verify that the expected Private Access profile was received.
4. Open the network traffic view and start collecting traffic.
5. Connect to the local resource.
6. Filter the results by the destination IP address.
7. Verify that the action indicates local bypass.

For more information, see [Global Secure Access client advanced diagnostics](troubleshoot-global-secure-access-client-advanced-diagnostics).

## Troubleshoot home network access

### The local resource is still unreachable

- Confirm that **Prefer Local Network** is available and enabled in the client.
- Confirm that the destination is in the device's directly connected subnet.
- Confirm that the destination uses an RFC 1918 IPv4 address.
- In **Advanced diagnostics**, verify that the expected traffic forwarding profile reached the client.
- Collect traffic while reproducing the issue and review the action for the destination IP address.
- Verify that the local device and operating-system firewall allow the connection.

### A corporate private application is unreachable

The corporate application's address might overlap the local subnet. Turn off **Prefer Local Network** and try the connection again. If the connection succeeds, the local preference was taking precedence over Private Access for that destination.

Consider publishing the corporate application by FQDN with a more specific application segment or changing the addressing plan to avoid the overlap.

### Prefer Local Network isn't displayed

- Verify that the device runs a supported Global Secure Access client version.
- Verify that the administrator enabled home network support for the user's Private Access traffic forwarding profile.
- Verify that the user is assigned to the expected profile.
- Refresh the client configuration or restart the client after the profile change.

## Limitations

- Home network support applies only to directly connected local subnets. It doesn't provide a general bypass for routed networks behind the local gateway.
- Only IPv4 private ranges defined by RFC 1918 are supported. IPv6 local subnets aren't supported.
- Mobile clients aren't supported.