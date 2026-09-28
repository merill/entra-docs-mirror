---
layout: Conceptual
title: Migrate from DirectAccess to Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-migrate-direct-access-to-private-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to migrate client devices from DirectAccess to Microsoft Entra Private Access with a phased approach that avoids tunnel conflicts and connectivity failures.
ms.topic: how-to
ms.date: 2026-03-27T00:00:00.0000000Z
ms.reviewer: buzaher
locale: en-us
document_id: f76a83e8-966e-328a-7155-56987ab1e7b6
document_version_independent_id: f76a83e8-966e-328a-7155-56987ab1e7b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-migrate-direct-access-to-private-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-migrate-direct-access-to-private-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-migrate-direct-access-to-private-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 71c90c76-f9fe-abdd-1dec-9397737a4962
---

# Migrate from DirectAccess to Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

DirectAccess provides remote connectivity to internal resources but relies on IPv6 transition technologies, requires domain-joined Windows Enterprise clients, and grants full network-level access once connected. However, these architectural constraints don't meet the needs of modern hybrid and cloud-first environments.

Microsoft Entra Private Access is a cloud-based, Zero Trust Network Access (ZTNA) solution that replaces legacy VPN and DirectAccess infrastructure. It uses the [Global Secure Access client](/en-us/entra/global-secure-access/concept-clients) and [private network connectors](/en-us/entra/global-secure-access/how-to-configure-connectors) to deliver conditional, per-app access to private resources without exposing your network to inbound connections. Migrating to Microsoft Entra Private Access reduces infrastructure complexity, strengthens your Zero Trust posture, and extends secure access to any managed or unmanaged device.

### Technical incompatibilities between DirectAccess and Private Access

DirectAccess and Microsoft Entra Private Access can't coexist on the same device. When both are active, you might experience the following problems:

- **Device tunnel conflict**: DirectAccess establishes a device tunnel at boot that takes precedence and prevents Private Access traffic from flowing.
- **NRPT rule conflicts**: Both solutions use Name Resolution Policy Table (NRPT) rules. Conflicting entries cause unpredictable DNS resolution behavior.
- **IPv6 transition technology interference**: The IP-HTTPS tunnel adapter that DirectAccess creates can interfere with Private Access network routing.

Important

To ensure a successful migration, you must **fully remove** DirectAccess from each device before you enable Private Access traffic forwarding.

## Prerequisites

Before you begin the migration, ensure the following requirements are met:

- Microsoft Entra Private Access is enabled in your tenant. Descope the pilot user from Private Access [user assignment](/en-us/entra/global-secure-access/how-to-manage-users-groups-assignment) for the initial setup.
- Private Access connectivity is configured by using [Quick Access](/en-us/entra/global-secure-access/how-to-configure-quick-access) or [per-app access](/en-us/entra/global-secure-access/how-to-configure-per-app-access).
- [Private DNS](/en-us/entra/global-secure-access/concept-private-name-resolution) and name resolution for internal resources is configured as required.

## Migration strategy

To avoid tunnel conflicts and partial connectivity failures, break the migration into four phases:

1. Deploy the Global Secure Access client (no impact)
2. Remove DirectAccess from pilot devices
3. Enable Private Access traffic forwarding for pilot users
4. Expand migration in controlled waves

## Phase 1: Deploy the Global Secure Access client

You can [deploy the Global Secure Access client](/en-us/entra/global-secure-access/how-to-install-windows-client) to your pilot device before removing DirectAccess.

- Deploy the Global Secure Access client by using a Mobile Device Management (MDM) solution, such as [Microsoft Intune](/en-us/intune/intune-service/apps/apps-win32-app-management).
- Don't assign the Private Access traffic forwarding profile yet. Instead, follow the steps in [How to assign users and groups to traffic forwarding profiles](/en-us/entra/global-secure-access/how-to-manage-users-groups-assignment#change-existing-user-and-group-assignments) to change the default **Assign to all users** setting to a new group.

### Expected behavior

| Indicator | Expected state |
| --- | --- |
| Global Secure Access client status | **Disabled by your organization** |
| DirectAccess | Continues to function normally |
| Private Access traffic | No traffic is forwarded |

Note

Phase 1 doesn't affect existing DirectAccess connectivity.

## Phase 2: Remove DirectAccess from pilot devices

Before you enable Private Access, you must **fully remove** DirectAccess. Partial removal leaves the DirectAccess device tunnel active and blocks Private Access traffic.

### Verify DirectAccess is active

Before you begin removal, verify that DirectAccess is currently active on the device. To verify, check the following indicators:

#### Network & internet status

Go to **Settings** &gt; **Network & internet** &gt; **DirectAccess**. The status shows **Workplace Connection: Connected**.

[![Screenshot that shows Windows Settings with the DirectAccess page displaying Workplace Connection status as Connected.](media/how-to-migrate-direct-access-to-private-access/direct-access-connection-status.png)](media/how-to-migrate-direct-access-to-private-access/direct-access-connection-status.png#lightbox)

#### IP-HTTPS tunnel adapter

In Command Prompt, run `ipconfig`. A **Tunnel adapter Microsoft IP-HTTPS Platform Interface** entry confirms that the DirectAccess IPv6 transition tunnel is active.

[![Screenshot that shows the command prompt with activity in the IP-HTTPS tunnel adapter.](media/how-to-migrate-direct-access-to-private-access/tunnel-adapter.png)](media/how-to-migrate-direct-access-to-private-access/tunnel-adapter.png#lightbox)

#### NRPT policies

Open PowerShell and run `Get-DnsClientNrptPolicy`. DirectAccess-related NRPT entries, such as `DirectAccess-NLS.*` namespaces, confirm that DirectAccess DNS policies are in place.

[![Screenshot that shows the PowerShell output of Get-DnsClientNrptPolicy with DirectAccess-related entries.](media/how-to-migrate-direct-access-to-private-access/get-client-policy.png)](media/how-to-migrate-direct-access-to-private-access/get-client-policy.png#lightbox)

### Remove DirectAccess from pilot devices

Complete the following steps on pilot devices only:

1. Remove the computer account from the DirectAccess security group.

    1. Open **Group Policy Management**.
    2. Locate the **DirectAccess Client Settings** Group Policy Object (GPO).
    3. Remove the pilot computer from the security filtering group (for example, `DirectAccess Computers`).

    [![Screenshot that shows the Group Policy Management console with the DirectAccess Client Settings GPO and its security filtering configuration.](media/how-to-migrate-direct-access-to-private-access/client-settings.png)](media/how-to-migrate-direct-access-to-private-access/client-settings.png#lightbox)
2. Ensure group membership changes replicate to all domain controllers.
3. On the client device, open PowerShell and run:

    ```powershell
    gpupdate /force
    shutdown /r /t 0
    ```
4. To fully clear the DirectAccess state, restart the client device twice.

### Validate DirectAccess removal

Important

Validate DirectAccess removal from the client **before** you proceed to Phase 3.

After the second restart, confirm the following conditions:

- No DirectAccess NRPT entries exist.

    - Run the following command and verify no DirectAccess-related entries are returned:

        ```powershell
        Get-DnsClientNrptPolicy
        ```
- No IP-HTTPS adapter exists.

    - Run `ipconfig` and verify that the **Tunnel adapter Microsoft IP-HTTPS Platform Interface** entry is gone.
- No DirectAccess UI state.

    - Go to **Settings** &gt; **Network & internet** and verify that the **DirectAccess** option no longer appears.

Tip

If DirectAccess client artifacts remain, restart the client device two more times and validate again. In some cases, you might need to restart several times to fully remove DirectAccess.

## Phase 3: Enable Private Access traffic forwarding

When you remove DirectAccess, enable Private Access for the pilot user.

1. Add your pilot user to the group that you assigned to the **Private Access traffic forwarding profile**. The Global Secure Access client can take 10-15 minutes to establish the Private Access tunnel.
2. Verify the Global Secure Access client shows **Connected** status in the system tray.

    [![Screenshot that shows the Global Secure Access client icon in the Windows system tray indicating a connected status.](media/how-to-migrate-direct-access-to-private-access/taskbar-client.png)](media/how-to-migrate-direct-access-to-private-access/taskbar-client.png#lightbox)

### Expected behavior

| Indicator | Expected state |
| --- | --- |
| Private resources | Reachable |
| Global Secure Access client status | **Connected** |
| Private Access diagnostics | Traffic appears in logs |
| DirectAccess | No longer involved in connectivity |

## Phase 4: Expand migration in controlled waves

Repeat **Phase 2** and **Phase 3** for more user and device groups.

- Don't remove DirectAccess globally until all devices are migrated.
- Validate each group before expanding to the next. This approach minimizes risk and prevents remote access outages.

Caution

Don't decommission DirectAccess server infrastructure until you confirm that all users can access required resources through Microsoft Entra Private Access.