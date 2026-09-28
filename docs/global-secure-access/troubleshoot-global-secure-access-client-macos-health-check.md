---
layout: Conceptual
title: 'Troubleshoot the macOS Global Secure Access client: Health check - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-macos-health-check
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Troubleshoot the macOS Global Secure Access client using the Health check tab in the Advanced diagnostics utility.
ms.topic: troubleshooting
ms.date: 2026-01-16T00:00:00.0000000Z
ms.reviewer: LuisPFlores
ms.custom: sfi-image-nochange
locale: en-us
document_id: f9dc5c93-05d1-cf8f-73c4-26494640b4f8
document_version_independent_id: f9dc5c93-05d1-cf8f-73c4-26494640b4f8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-global-secure-access-client-macos-health-check.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-global-secure-access-client-macos-health-check
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-global-secure-access-client-macos-health-check.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 00e596a3-74c1-70cf-2bcb-860c6333c855
---

# Troubleshoot the macOS Global Secure Access client: Health check - Global Secure Access | Microsoft Learn

This article provides troubleshooting guidance for the macOS Global Secure Access client using the **Health check** tab in the Advanced diagnostics utility.

## Introduction

The Advanced diagnostics Health check runs tests to verify that the macOS Global Secure Access client works correctly and that its components are running.

## Run the health check

To run a health check for the macOS Global Secure Access client:

1. Select **Global Secure Access** in the menu bar and select **Settings**.![Screen shot of the system tray menu with the Settings option highlighted.](media/troubleshoot-global-secure-access-client-macos-health-check/system-tray-settings.png)
2. Select the **Troubleshooting** tab.
3. In the **Advanced Diagnostics tool** section, select **Run tool**.
4. In the **Advanced Diagnostics** window, select the **Health Check** tab. Switching tabs runs the health check.

### Resolution process

Most of the Health check tests depend on one another. If tests fail:

1. Resolve the first failed test in the list.
2. Select **Refresh** to view the updated test status.
3. Repeat until you resolve all failed tests.[![Screen shot of the macOS Global Secure Access client, open to the Health check tab, with example health check results listed.](media/troubleshoot-global-secure-access-client-macos-health-check/macos-health-check-results.png)](media/troubleshoot-global-secure-access-client-macos-health-check/macos-health-check-results.png#lightbox)

## Health check tests

The following checks verify the health of the Global Secure Access client.

### Notifications enabled

The **Notifications enabled** test checks if the macOS Global Secure Access client notifications are enabled. If the test isn't enabled, open System Settings and allow the notifications. [![Screen shot of the Global Secure Access notifications settings, with all notifications enabled.](media/troubleshoot-global-secure-access-client-macos-health-check/allow-notifications.png)](media/troubleshoot-global-secure-access-client-macos-health-check/allow-notifications.png#lightbox)

### System extension

This test checks if the client's system extension is installed and active. If this test fails, try one of the following solutions:

- Check for the option to **Allow Network Extension**:

    1. Select **Global Secure Access** in the menu bar.
    2. If the option is available, select **Allow Network Extension** to enable the system extension.![Screenshot of the system tray menu with the Allow Network Extension option highlighted.](media/troubleshoot-global-secure-access-client-macos-health-check/allow-network-extension.png)
- Allow the system extension in **Privacy & Security** settings:

    1. Open **System Settings**.
    2. Select **Privacy & Security**.
    3. Scroll down to the **Security** section.
    4. If there's a message about the Global Secure Access system extension being blocked, select **Allow** to enable the system extension.[![Screenshot of the Privacy &amp; Security settings with the Allow button highlighted.](media/troubleshoot-global-secure-access-client-macos-health-check/privacy-security.png)](media/troubleshoot-global-secure-access-client-macos-health-check/privacy-security.png#lightbox)
- Use a Terminal command to check if the system extension is running and enabled:

    1. Open **Terminal**.
    2. Run the following command: `systemextensionsctl list | grep -E '.*com.microsoft.naas.globalsecure.tunnel-df.*Global Secure Access'`
    3. The Terminal command enables the system extension, with the output:

    ```bash
    Virtual-Machine ~ % systemextensionsctl list | grep -E '.*com.microsoft.naas.*Global.*Secure.*Access.*Network.*Extension.*activated.*enabled'
    UBF8T346G9    com.microsoft.naas.globalsecure.tunnel-df (1.1.432/1.1.432)    Global Secure Access Network Extension    [activated enabled]
    ```

### Transparent proxy service

This test checks if the Transparent Proxy service is running. If the test fails, enable the Transparent Proxy service:

1. Open **System Settings**.
2. Select **Network**.
3. Select **Filters & Proxies**.
4. Verify that the Global Secure Access Transparent Proxy **Status** is **Enabled**. If not, switch it to **Enabled**.[![Screen shot of the Filters &amp; Proxies settings with the Transparent Proxy status set to Enabled.](media/troubleshoot-global-secure-access-client-macos-health-check/filters-proxies.png)](media/troubleshoot-global-secure-access-client-macos-health-check/filters-proxies.png#lightbox)
5. If you can't enable the Transparent Proxy through **System Settings**, check the log file.

### UI - System extension bridge (IPC)

This test checks if the System Extension Bridge is active. If the test fails, disable and re-enable the Global Secure Access client.

### Connected active interface

This test shows the active interface used for traffic. To see all the active interfaces, enter the following command in Terminal: `ifconfig`.

This info comes from the path `State:/Network/Global/IPv4`.

```bash
  scutil <<< "show State:/Network/Global/IPv4"
```

### Tunnel interface (L3)

This test shows the name of the tunnel interface the client uses. A failed test indicates that the tunnel interface wasn't created successfully. To fix the issue:

1. Disable and re-enable client from the system tray.
2. Verify the following output in the tunnel log file:

```bash
"l3Interface" : {
"name" : "_interface-name",
"status" : "Yes"
},
```

### DNS server IP

This test shows the IP of the preferred DNS server configured at the operating system level. You must configure a DNS server that can resolve internet hostnames. An empty value means that no DNS server is configured.

### Is DNS encrypted

To allow the macOS Global Secure Access client to capture network traffic by fully qualified domain name (FQDN) instead of IP address, the client must read DNS requests sent to the DNS server.

Examples of secure DNS servers:

- Google DNS: 8.8.8.8, 8.8.4.4
- Cloudflare DNS: 1.1.1.1, 1.0.0.1
- OpenDNS: 208.67.222.222, 208.67.220.220

If the forwarding profile includes FQDN rules, disable DNS over HTTPS. To check whether secure DNS is enabled, run the following command:

```bash
    scutil --dns | grep 'nameserver\[[0-9]*\]'
```

For example:

```bash
$ scutil --dns | grep 'nameserver\[[0-9]*\]'   
  nameserver[0] : 10.50.50.50   
  nameserver[1] : 10.50.10.50   
  nameserver[0] : 10.50.50.50   
  nameserver[1] : 10.50.10.50   
```

To check if a specific port is closed, use the `nc` (netcat) command:

```bash
$ nc -zv 10.50.50.50 853
nc: connectx to 10.50.50.50 port 853 (tcp) failed: Connection refused
```

If the connection is closed, the DNS isn't encrypted. If any connection succeeds, the DNS server uses encryption.

### Authentication succeeded

This test checks for a successful Global Secure Access authentication. A failed authentication results in an error or a prompt for an interactive sign-in. If the test fails:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Go to **Entra ID** &gt; **Devices** &gt; **Overview**.
3. Verify that the device is registered and that you're signed in to the Microsoft Entra tenant. For more information, see [Manage device identities using the Microsoft Entra admin center](../identity/devices/manage-device-identities).
4. Select **Audit logs**.
5. Check the log file: **com.microsoft.naas.globalsecure-df xx.xx.xx.xx.log**

### Forwarding profile cached in a file

This test checks that a forwarding profile exists in the file system. If the test fails, complete the following steps:

1. Select the Global Secure Access system tray icon.
2. Select **Settings**.
3. On the **Troubleshooting** tab, select **Clear cache**.
4. Sign in again. The client retrieves an updated forwarding profile from the Global Secure Access service.
5. Run the test again. If the test fails:
    1. Check the tunnel log file for errors.
    2. Check the following path for the policy .plist file: `/private/var/root/Library/Preferences/com.microsoft.naas.globalsecure.tunnel-df.plist`

### Break-glass mode disabled

Break-glass mode prevents the Global Secure Access client from tunneling network traffic to the Global Secure Access cloud service. In break-glass mode, all traffic profiles in the Global Secure Access portal are unchecked and the Global Secure Access client isn't expected to tunnel any traffic.

If you want the client to acquire traffic and send it to the Global Secure Access service:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Navigate to Global Secure **Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Enable at least one of the traffic profiles that match your organization's needs.

The Global Secure Access client typically receives the updated forwarding profile within one hour after making changes in the portal.

### Proxy Configured

This test checks whether the proxy is configured on the device. If a device uses a proxy for outgoing traffic to the internet, you must exclude the destination IPs and FQDNs that the client acquires by using a Proxy Auto-Configuration (PAC) file or by using the Web Proxy Auto-Discovery (WPAD) protocol.

#### Change the PAC file

Add the IPs and FQDNs to tunnel to Global Secure Access edge as exclusions in the PAC file, so that HTTP requests for these destinations don't redirect to the proxy. These IPs and FQDNs are also set to tunnel to Global Secure Access in the forwarding profile. To show the client's health status properly, add the FQDN used for health probing to the exclusions list: `.edgediagnostic.globalsecureaccess.microsoft.com`.

Example PAC file containing exclusions:

```javascript
function FindProxyForURL(url, host) {  
        if (isPlainHostName(host) ||   
            dnsDomainIs(host, ".edgediagnostic.globalsecureaccess.microsoft.com") || //tunneled
            dnsDomainIs(host, ".contoso.com") || //tunneled 
            dnsDomainIs(host, ".fabrikam.com")) // tunneled 
           return "DIRECT";                    // For tunneled destinations, use "DIRECT" connection (and not the proxy)
        else                                   // for all other destinations 
           return "PROXY 10.1.0.10:8080";  // route the traffic to the proxy.
}
```

### Internet reachable

This test checks whether the internet is reachable when the client is running. Run one of the following commands in Terminal:

```bash
curl http://www.msftconnecttest.com/connecttest.txt
```

Important

Make sure the following URLs are accessible and not blocked by the firewall and VPN providers. http://www.msftconnecttest.com/connecttest.txthttp://captive.apple.com/hotspot-detect.htmlhttp://connectivitycheck.gstatic.com/generate_204

### Diagnostic URLs present

For each channel activated in the forwarding profile, this test checks that the configuration contains a URL to probe the service's health. To view the health status, select the system tray icon. On the **Connections** tab, view the **Status**.

If this test fails, it's usually because of an internal problem with Global Secure Access. Contact Microsoft Support.

### Diagnostics URLs monitoring status

This test verifies whether the diagnostics URLs monitoring is working. If the test fails, disable and re-enable the client.

### Magic-IP received for EDS

This test validates if magic IP is received for EDS URLs. If the test fails, complete the following steps:

1. Verify that the DNS server is responsive. For example, try resolving "microsoft.com" using the `nslookup` tool.
2. Make sure the DNS server set on the macOS device doesn't support Secure DNS.

### Edges are reachable

This test verifies whether the device is connected to the internet:

```bash
nc -vz 9d39e890-4c9e-433b-9b7a-625f7e26d855.m365.client.globalsecureaccess.microsoft.com 443
```

### Tunneling succeeded

This test validates if tunneling succeeded for all EDS URLs. If this test fails:

1. Verify that all other health check tests passed.
2. Verify that tunneling is working on other devices.
3. Check the log file.
4. Restart the client.
5. If the test still fails, contact Microsoft Support.