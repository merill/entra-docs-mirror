---
layout: Conceptual
title: 'Troubleshoot the Windows Global Secure Access client: Health check - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Troubleshoot the Global Secure Access client using the Health check tab in the Advanced diagnostics utility.
ms.topic: troubleshooting
ms.date: 2026-02-24T00:00:00.0000000Z
ms.reviewer: lirazbarak
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8bf5bcdb-7797-918c-2ba9-20f9e6e43101
document_version_independent_id: 8bf5bcdb-7797-918c-2ba9-20f9e6e43101
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 925f56de-8ba1-edaf-fd16-f040fafa3444
---

# Troubleshoot the Windows Global Secure Access client: Health check - Global Secure Access | Microsoft Learn

This article provides troubleshooting guidance for the Global Secure Access Windows client using the **Health check** tab in the Advanced diagnostics utility.

## Introduction

The Advanced diagnostics Health check runs tests to verify that the Global Secure Access client works correctly and that its components are running.

## Run the health check

To run a health check for the Global Secure Access client:

1. Right-click the Global Secure Access client system tray icon and select **Advanced Diagnostics**.
2. The User Account Control dialog box opens. Select **Yes** to allow the client application to make changes to your device.
3. In the **Global Secure Access Client - Advanced diagnostics** dialog box, select the **Health check** tab. Switching tabs runs the health check.

### Resolution process

Most of the Health check tests depend on one another. If tests fail:

1. Resolve the first failed test in the list.
2. Select **Refresh** to view the updated test status.
3. Repeat until you resolve all failed tests. ![Screenshot of the Global Secure Access Health check tab with the Refresh button highlighted.](media/troubleshoot-global-secure-access-client-diagnostics-health-check/troubleshoot-health-check-refresh.png)

### Check the Event Viewer

As part of the troubleshooting process, it can be useful to check the Event Viewer for the Global Secure Access client. The log contains valuable events regarding errors and their cause.

1. Navigate to **Control Panel** &gt; **System and Security** &gt; **Windows Tools**.
2. Launch **Event Viewer**.
3. Navigate to **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **Global Secure Access Client**.
    1. To view client logs, select **Operational**.
    2. To view driver logs, select **Kernel**.

## Health check tests

The following checks verify the health of the Global Secure Access client.

### Device is Microsoft Entra joined

The Windows client authenticates the user and the device to Global Secure Access services. The device authentication, based on a device token, requires that the device is either Microsoft Entra joined or Microsoft Entra hybrid joined. Microsoft Entra registered devices aren't currently supported. To check the status of your device, enter the following command in the Command Prompt: `dsregcmd.exe /status`. ![Screenshot of the Command Prompt with the Device State, AzureAdJoined : Yes, highlighted.](media/troubleshoot-global-secure-access-client-diagnostics-health-check/troubleshoot-health-entra-joined.png)

### Entra user signed in to Windows

This check verifies that the user currently signed in to Windows is a Microsoft Entra user. The Global Secure Access client requires the Windows sign-in user to be a Microsoft Entra user, not a local-only account.

If this test fails:

1. Verify the user signed in to the device with a Microsoft Entra account or a Microsoft Entra hybrid identity.
2. Check that the Windows sign-in session uses Microsoft Entra credentials (not a local account).
3. Run `dsregcmd.exe /status` and verify the **SSO State** section shows `AzureAdPrt : YES`.

### Can connect to the internet

This check indicates whether the device is connected to the internet. The Global Secure Access client requires an internet connection. This test is based on the [Network Connectivity Status Indicator (NCSI)](/en-us/windows-server/networking/ncsi/ncsi-overview) feature.

### Tunneling service running

The Global Secure Access Tunneling service must be running.

1. To verify that this service is running, enter the following command in the Command Prompt:`sc query GlobalSecureAccessTunnelingService`
2. If the Global Secure Access Tunneling service isn't running, start it from the `services.msc`.
3. If the service fails to start, look for errors in the Event Viewer.

### Engine service running

The Global Secure Access Engine service must be running.

1. To verify that this service is running, enter the following command in the Command Prompt:`sc query GlobalSecureAccessEngineService`
2. If the Global Secure Access Engine Service isn't running, start it from the `services.msc`.
3. If the service fails to start, look for errors in the Event Viewer.

### Policy Retriever service running

The Global Secure Access Policy Retriever service must be running.

1. To verify that this service is running, enter the following command in the Command Prompt:`sc query GlobalSecureAccessPolicyRetrieverService`
2. If the Global Secure Access Policy Retriever service isn't running, start it from the `services.msc`.
3. If the service fails to start, look for errors in the Event Viewer.

### Driver running

The Global Secure Access driver must be running. To verify that this service is running, enter the following command in the Command Prompt:`sc query GlobalSecureAccessDriver`

If the driver isn't running:

1. Open the Event Viewer and search the Global Secure Access client log for **event 304**.
2. If the driver isn't running, reboot the machine.
3. Run the `sc query GlobalSecureAccessDriver` command again.
4. If the issue remains unresolved, reinstall the Global Secure Access client.

### Client tray application running

The GlobalSecureAccessClient.exe process runs the client UX in the system tray. If you can't see the Global Secure Access icon in the system tray, you can run it from the following path:`C:\Program Files\Global Secure Access Client\GlobalSecureAccessClient.exe`

### Forwarding profile registry exists

This test verifies that the following registry key exists:`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Global Secure Access Client\ForwardingProfile`

If the registry key doesn't exist, try to force forwarding policy retrieval:

1. Delete the `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Global Secure Access Client\ForwardingProfileTimestamp` registry key, if it exists.
2. Restart the service, `Global Secure Access Policy Retriever Service`.
3. Check if the two registry keys are created.
4. If not, look for errors in the Event Viewer.

### Forwarding profile matches expected schema

This test verifies that the forwarding profile in the registry has a valid format that the client can read.

If this test fails, make sure you're using the most updated forwarding profile of your tenant by following these steps:

1. Delete the following registry keys:
    - `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Global Secure Access Client\ForwardingProfile`
    - `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Global Secure Access Client\ForwardingProfileTimestamp`
2. Restart the service, `Global Secure Access Policy Retriever Service`.
3. Restart the Global Secure Access client.
4. Run the health check again.
5. If the previous steps don't solve the problem, upgrade the Global Secure Access client to the latest version.
6. If the problem still exists, contact Microsoft Support.

### Break-glass mode disabled

Break-glass mode prevents the Global Secure Access client from tunneling network traffic to the Global Secure Access cloud service. In break-glass mode, all traffic profiles in the Global Secure Access portal are unchecked and the Global Secure Access client isn't expected to tunnel any traffic.

To set the client to acquire traffic and tunnel that traffic to the Global Secure Access service:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Navigate to Global Secure **Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Enable at least one of the traffic profiles that match your organization's needs.

The Global Secure Access client should receive the updated forwarding profile within one hour after you make changes in the portal.

### Diagnostic URLs in forwarding profile

For each channel activated in the forwarding profile, this test checks that the configuration contains a URL to probe the service's health. To view the health status, select the system tray icon. On the Connections tab, view the **Status**.

If this test fails, it's usually because of an internal problem with Global Secure Access. Contact Microsoft Support.

### Authentication certificate exists

This test verifies that a certificate exists on the device for the Mutual Transport Layer Security (mTLS) connection to the Global Secure Access cloud service.

Tip

This test doesn't appear if you don't enable mTLS for your tenant.

If this test fails, enroll in a new certificate by completing the following steps:

1. Launch the Microsoft Management console by entering the following command in the Command Prompt: `certlm.msc`.
2. In the **certlm** window, navigate to **Personal** &gt; **Certificates**.
3. Delete the certificate that ends with **gsa.client**, if it exists. ![Screenshot of the list of certificates with the gsa.client certificate highlighted.](media/troubleshoot-global-secure-access-client-diagnostics-health-check/troubleshoot-health-check-certificates-registry-key.png)
4. Delete the following registry key:`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Global Secure Access Client\CertCommonName`
5. Restart the Global Secure Access Engine Service in the services MMC.
6. Refresh the certificates MMC to verify that a new certificate was created.*Provisioning a new certificate might take a few minutes.*
7. Check the Global Secure Access client event log for errors.
8. Run the Health check tests again.

### Authentication certificate is valid

This test verifies that the authentication certificate used for the mTLS connection to the Global Secure Access cloud service is valid.

Tip

This test doesn't appear if you don't enable mTLS for your tenant.

If this test fails, enroll in a new certificate by completing the following steps:

1. Launch the Microsoft Management console by entering the following command in the Command Prompt: `certlm.msc`.
2. In the **certlm** window, navigate to **Personal** &gt; **Certificates**.
3. Delete the certificate that ends with **gsa.client**. ![Screenshot of the list of certificates with the gsa.client certificate highlighted.](media/troubleshoot-global-secure-access-client-diagnostics-health-check/troubleshoot-health-check-certificates-registry-key.png)
4. Delete the following registry key:`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Global Secure Access Client\CertCommonName`
5. Restart the Global Secure Access Engine Service in the services MMC.
6. Refresh the certificates MMC to verify that a new certificate was created.*Provisioning a new certificate might take a few minutes.*
7. Check the Global Secure Access client event log for errors.
8. Run the Health check tests again.

### DNS over HTTPS not supported

For the Global Secure Access client to acquire network traffic by a fully qualified domain name (FQDN) destination (instead of an IP destination), the client needs to read the DNS requests the device sends to the DNS server. This requirement means that if the forwarding profile contains FQDN rules, you must disable DNS over HTTPS.

#### Secure DNS disabled in OS

To disable DNS over HTTPS in Windows, see [Secure DNS Client over HTTPS (DoH)](/en-us/windows-server/networking/dns/doh-client-support#configure-the-dns-client-to-support-doh.md).

Important

You must disable DNS over HTTPS to successfully run the Global Secure Access client Health check.

#### Secure DNS disabled in browsers (Microsoft Edge, Chrome, Firefox)

Check that Secure DNS is disabled for each of the following browsers:

##### Secure DNS disabled in Microsoft Edge

To disable DNS over HTTPS in Microsoft Edge:

1. Launch Microsoft Edge.
2. Open the **Settings and more** menu and select **Settings**.
3. Select **Privacy, search, and services**.
4. In the **Security** section, set the **Use secure DNS to specify how to lookup the network address for websites** toggle to off.

##### Secure DNS disabled in Chrome

To disable DNS over HTTPS in Google Chrome:

1. Open Chrome.
2. Select **Customize and control Google Chrome** and then select **Settings**.
3. Select **Privacy and security**.
4. Select **Security**.
5. In the **Advanced** section, set the **Use secure DNS** toggle to **off**.

##### Secure DNS disabled in Firefox

To disable DNS over HTTPS in Mozilla Firefox:

1. Open Firefox.
2. Select the **Open application menu** button and then select **Settings**.
3. Select **Privacy & Security**.
4. In the **DNS over HTTPS** section, select **Off**.

### DNS responsive

This test checks whether the DNS server configured in Windows returns a DNS response.

If this test fails:

1. Pause the Global Secure Access client.
2. Check if the DNS server configured in Windows is reachable. For example, try resolving `microsoft.com` by using the `nslookup` tool.
3. Verify that no firewalls block traffic to the DNS server.
4. Configure an alternate DNS server and test again.
5. Resume the Global Secure Access client.

### Magic IP received

This check verifies that the client can acquire traffic from a fully qualified domain name (FQDN).

If the test fails:

1. Restart the client and test again.
2. Restart Windows. This step might be necessary in rare cases to delete volatile cache.

### Cached token

This test verifies that the client successfully authenticates to Microsoft Entra.

If the cached token test fails:

1. Verify that the services and the driver are running.
2. Verify that the system tray icon is visible.
3. If the sign-in notification appears, select **Sign in**.
4. If the sign-in notification doesn't appear, check if it's in the Notification Center and select **Sign in**.
5. Sign in with a user that is a member of the same Microsoft Entra tenant that the device is joined to.
6. Verify the network connection.
7. Hover over the system tray icon and verify that the client *isn't* disabled by your organization.
8. Restart the client and wait for a few seconds.
9. Look for errors in the Event Viewer.

### IPv4 preferred

Global Secure Access doesn't yet support traffic acquisition for destinations with IPv6 addresses. Configure the client to prefer IPv4 over IPv6 if:

1. The forwarding profile is set to acquire traffic by IPv4 (as opposed to by FQDN).
2. The FQDN resolved to this IP also resolves to an IPv6 address.

To configure the client to prefer IPv4 over IPv6, set the following registry key:`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\ Name: DisabledComponents Type: REG_DWORD Value: 0x20 (Hex)`

Important

Changes to this registry value require a computer restart. For more information, see [Guidance for configuring IPv6 in Windows for advanced users](/en-us/troubleshoot/windows-server/networking/configure-ipv6-in-windows).

### Edge hostname resolved by DNS

This test checks all active traffic types: **Microsoft 365**, **Private Access**, and **Internet Access**. If this test fails, the DNS can't resolve the hostnames of the Global Secure Access cloud service, and therefore the service isn't reachable. This failed test could be due to an internet connectivity problem or a DNS server that doesn't resolve public internet hostnames.

To verify that the hostname resolution works correctly:

1. Pause the client.
2. Run the PowerShell command: `Resolve-DnsName -Name <edge's FQDN>`
3. If the hostname resolution fails, try running: `Resolve-DnsName -Name microsoft.com`
4. Verify that the DNS servers are configured for this machine: `ipconfig /all`
5. If the previous steps don't resolve the issue, consider setting another public DNS server.

### Edge is reachable

This test checks all active traffic types: **Microsoft 365**, **Private Access**, and **Internet Access**. If this test fails, the device doesn't have a network connection to the Global Secure Access cloud service.

If the test fails:

1. Verify that the device has an internet connection.
2. Verify that the firewall or proxy doesn't block the connection to the edge.
3. Make sure IPv4 is active on the device. Currently the edge works only with an IPv4 address.
4. Stop the client and retry `Test-NetConnection -ComputerName <edge's fqdn> -Port 443`.
5. Try the PowerShell command from another device connected to the internet from a public network.

### Proxy disabled

This test checks whether the proxy is configured on the device. If a device uses a proxy for outgoing traffic to the internet, you must exclude the destination IPs and FQDNs that the client acquires with a Proxy Auto-Configuration (PAC) file or with the Web Proxy Auto-Discovery (WPAD) protocol.

#### Change the PAC file

Add the IPs and FQDNs to be tunneled to Global Secure Access edge as exclusions in the PAC file, so that HTTP requests for these destinations don't redirect to the proxy. These IPs and FQDNs are also set to tunnel to Global Secure Access in the forwarding profile. To show the client's health status properly, add the FQDN used for health probing to the exclusions list: `.edgediagnostic.globalsecureaccess.microsoft.com`.

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

#### Global Secure Access client and outbound proxies

Important

If the Global Secure Access client is behind an outbound proxy, configure PAC file exclusions to bypass the proxy for Global Secure Access traffic.

### No Hyper-V external virtual switch detected

Hyper-V support:

1. External virtual switch: The Global Secure Access Windows client doesn't currently support host machines that have a Hyper-V external virtual switch. However, you can install the client on the virtual machines to tunnel traffic to Global Secure Access.
2. Internal virtual switch: You can install the Global Secure Access Windows client on host and guest machines. The client tunnels only the network traffic of the machine it's installed on. In other words, a client installed on a host machine doesn't tunnel the network traffic of the guest machines.

The Global Secure Access Windows client supports Azure Virtual Machines.

The Global Secure Access Windows client supports Azure Virtual Desktop (AVD).

Note

AVD multisesion isn't supported.

### Tunneling succeeded

This test checks each active traffic profile in the forwarding profile (**Microsoft 365**, **Private Access**, and **Internet Access**) to verify that connections to the health service of the corresponding channel are tunneled successfully.

If this test fails:

1. Check the Event Viewer for errors.
2. Restart the client and try again.

### Global Secure Access processes healthy (last 24 h)

If this test fails, it means that at least one process of the client crashed in the last 24 hours.

If all other tests pass, the client should be currently functioning. However, it can be helpful to investigate the process dump file to increase future stability and to better understand why the process crashed.

To investigate the process dump file when a process crashes:

1. Configure user mode dumps:
    - Add the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps`
    - Add a `REG_SZ DumpFolder` registry value and set its data to the **existing** DumpFolder where you want to save the dump file.
2. Reproduce the issue to create a new dump file in the selected DumpFolder.
3. Open a ticket for Microsoft Support and attach the dump file and the steps to reproduce the issue.
4. Review the Event Viewer logs and filter for crash events (Filter current logs: Event ID = 1000). ![Screenshot of the Event Viewer showing a filtered log list.](media/troubleshoot-global-secure-access-client-diagnostics-health-check/troubleshoot-health-check-filtered-logs.png)
5. Save the filtered log as a file and attach the log file to the support ticket.

### QUIC not supported for Internet Access

Since QUIC isn't yet supported for Internet Access, traffic to ports 80 UDP and 443 UDP can't be tunneled.

Tip

QUIC is currently supported in Private Access and Microsoft 365 workloads.

Administrators can disable QUIC protocol triggering clients to fall back to HTTPS over TCP, which is fully supported in Internet Access.

### Disable QUIC in Microsoft Edge

To disable QUIC in Microsoft Edge:

1. Open Microsoft Edge.
2. Paste `edge://flags/#enable-quic` in the address bar.
3. Set the **Experimental QUIC protocol** drop-down to **Disabled**.

### Disable QUIC in Chrome

To disable QUIC in Google Chrome:

1. Open Google Chrome.
2. Paste `chrome://flags/#enable-quic` in the address bar.
3. Set the **Experimental QUIC protocol** drop-down to **Disabled**.

### Disable QUIC in Mozilla Firefox

To disable QUIC in Mozilla Firefox:

1. Open Firefox.
2. Paste `about:config` in the address bar.
3. In the **Search preference name field**, paste `network.http.http3.enable`.
4. Toggle the **network.http.http3.enable** option to **false**.