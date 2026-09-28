---
layout: Conceptual
title: Device identity and desktop virtualization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/howto-device-identity-virtual-desktop-infrastructure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to manage Microsoft Entra device identities in virtual desktop infrastructure (VDI) environments to prevent stale devices and tenant quota consumption.
ms.topic: concept-article
ms.date: 2026-06-04T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
ms.reviewer: sandeo
locale: en-us
document_id: 0e8f55d4-539c-7835-010b-34026860f699
document_version_independent_id: 4f8db376-bed9-6fd2-2e65-ac11c0952540
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/howto-device-identity-virtual-desktop-infrastructure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/howto-device-identity-virtual-desktop-infrastructure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/howto-device-identity-virtual-desktop-infrastructure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7814ca69-56be-4667-8a46-86327796c328
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f15dfcd0-2664-48ba-bb88-f1f86eadbfd1
platformId: e80a6eac-bdc4-e504-217a-53b4b7beec15
---

# Device identity and desktop virtualization - Microsoft Entra ID | Microsoft Learn

Administrators commonly deploy virtual desktop infrastructure (VDI) platforms that host Windows operating systems in their organizations. VDI helps to:

- Streamline management.
- Reduce costs through consolidation and centralization of resources.
- Deliver end-user mobility and the freedom to access virtual desktops anytime, from anywhere, on any device.

There are two versions of virtual desktops. These names refer to the user session and profile experience, not the lifecycle of the underlying virtual machine (VM).

| Virtual desktop type | Description | Effect on tenant quota |
| --- | --- | --- |
| Persistent | Uses a unique desktop image for each user or pool of users. These desktops can be customized and saved for future use. | Devices register once and remain in the directory. Stale devices accumulate only if VMs are periodically reset without cleanup. |
| Non-persistent | Uses a collection of desktops that users access on an as-needed basis. These desktops revert to their original state after a VM shutdown, restart, or OS reset. | Each reset can trigger a new device registration, which rapidly increases stale device records and consumes tenant quota. |

Persistent versions use a unique desktop image for each user or a pool of users. These unique desktops can be customized and saved for future use.

Session host VMs in both pooled and personal host pools are standard Azure virtual machines and are persistent by default. Azure Virtual Desktop doesn't automatically delete, reset, or recreate these VMs unless customers explicitly implement automation or third‑party tooling, which can result in non‑persistent behavior at the device or identity level.

Non-persistent versions use a collection of desktops that users can access on an as needed basis. These non-persistent desktops are reverted to their original state when a virtual machine goes through a shutdown/restart/OS reset process.

Important

Stale devices increase your tenant quota usage consumption. To avoid consumption increase from stale devices when you deploy non-persistent VDI environments, see Non-persistent-vdi.

Some scenarios require unique device names in the directory. This can be achieved by proper management of stale devices, or you can guarantee device name uniqueness by using some pattern in device naming.

This article provides guidance for managing device identities in VDI environments. For more information about device identity, see the article [What is a device identity](overview).

## Supported scenarios

Before configuring device identities in Microsoft Entra ID for your VDI environment, familiarize yourself with the supported scenarios. The following table illustrates which provisioning scenarios are supported. Provisioning in this context implies that an administrator can configure device identities at scale without requiring any end-user interaction.

**Windows current** devices represent Windows 10 or newer, Windows Server 2016 v1803 or higher, and Windows Server 2019 or higher.

| Device identity type | Identity infrastructure | Windows devices | VDI platform version | Supported |
| --- | --- | --- | --- | --- |
| Microsoft Entra hybrid joined | Federated^1^ | Windows current | Persistent | Yes |
|  |  | Windows current | Non-persistent | Yes^2^ |
|  | Managed^3^ | Windows current | Persistent | Yes |
|  |  | Windows current | Non-persistent | Limited^4^ |
| Microsoft Entra joined | Federated | Windows current | Persistent | Limited |
|  |  |  | Non-persistent | No |
|  | Managed | Windows current | Persistent | Limited^5^ |
|  |  |  | Non-persistent | No |
| Microsoft Entra registered | Federated/Managed | Windows current | Persistent/Non-persistent | Not Applicable |

Important

When deploying a VDI farm (persistent or non-persistent), customers should take into consideration [Entra device operation throttling limits](/en-us/graph/throttling-limits#identity-and-access-device-operation-service-limits). Microsoft recommends device registration requests to be staged at the rate of 500 requests per every 2 minutes and 30 seconds interval. Failure to stage such requests can lead to throttling errors resulting in device registration failures and longer delays for device registration to succeed.

^1^ A **Federated** identity infrastructure environment represents an environment with an identity provider (IdP) such as AD FS or other non-Microsoft IdP. In a federated identity infrastructure environment, computers follow the [federated device registration flow](device-registration-how-it-works#microsoft-entra-joined-in-federated-environments) based on the [Microsoft Windows Server Active Directory Service Connection Point (SCP) settings](hybrid-join-manual#configure-a-service-connection-point).

^2^**Non-Persistence support for Windows current** requires other consideration as documented in the guidance section. This scenario requires Windows 10 1803 or newer, Windows Server 2019, or Windows Server (Semi-annual channel) starting with version 1803.

^3^ A **Managed** identity infrastructure environment represents an environment with Microsoft Entra ID as the identity provider deployed with either [password hash sync (PHS)](../hybrid/connect/whatis-phs) or [pass-through authentication (PTA)](../hybrid/connect/how-to-connect-pta) with [seamless single sign-on](../hybrid/connect/how-to-connect-sso).

^4^**Non-Persistence support for Windows current** in a Managed identity infrastructure environment is only available with following vendors:

- [Omnissa Horizon 8 on-premises customer managed](https://docs.omnissa.com/bundle/Horizon8InstallUpgrade/page/SupportforAzureActiveDirectory.html) and [Horizon Cloud Service managed environments](https://docs.omnissa.com/bundle/UsingManagingHorizonCloud/page/CreateaPool.html). For any support related queries, contact [Omnissa support](https://kb.omnissa.com/s/article/6000005) directly.
- Citrix [on-premises customer managed](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure/machine-identities/hybrid-azure-active-directory-joined) and [Cloud service managed](https://docs.citrix.com/en-us/citrix-daas/install-configure/machine-identities/hybrid-azure-active-directory-joined). For any support related queries, contact [Citrix support](https://www.citrix.com/support/) directly.

^5^**Microsoft Entra join support** is available with [Azure Virtual Desktop](/en-us/azure/virtual-desktop/), [Windows 365](https://www.microsoft.com/windows-365), and [Amazon WorkSpaces](https://docs.aws.amazon.com/workspaces/latest/adminguide/launch-workspaces-tutorials.html#launch-entra-id). For any support related queries with Amazon WorkSpaces and Microsoft Entra integration, contact [Amazon support](https://aws.amazon.com/contact-us/) directly.

## Microsoft's guidance

Administrators should reference the following articles, based on their identity infrastructure, to learn how to configure Microsoft Entra hybrid join.

- [Configure Microsoft Entra hybrid join for federated environment](how-to-hybrid-join)
- [Configure Microsoft Entra hybrid join for managed environment](how-to-hybrid-join)

### Non-persistent VDI

When you deploy non-persistent VDI, Microsoft recommends the following guidance. Failure to follow these steps results in your directory accumulating stale Microsoft Entra hybrid joined devices from your non-persistent VDI platform.

- If you're relying on the System Preparation Tool (sysprep.exe) and if you're using a pre-Windows 10 1809 image for installation, make sure that image isn't from a device that is already registered with Microsoft Entra ID as Microsoft Entra hybrid joined.
- If you're relying on a Virtual Machine (VM) snapshot to create more VMs, make sure that snapshot isn't from a VM that is already registered with Microsoft Entra ID as Microsoft Entra hybrid join.
- Active Directory Federation Services (AD FS) supports instant join for non-persistent VDI and Microsoft Entra hybrid join.
- Create and use a prefix for the display name (for example, NPVDI-) of the computer that indicates the desktop as non-persistent VDI-based.
- For Windows devices in a Federated environment (for example, AD FS):
    - Implement **dsregcmd /join** as part of VM boot sequence/order and before user signs in.
    - **DO NOT** execute dsregcmd /leave as part of VM shutdown/restart process.
- Define and implement process for [managing stale devices](manage-stale-devices).
    - Once you have a strategy to identify your non-persistent Microsoft Entra hybrid joined devices (such as using computer display name prefix), you should be more aggressive on the cleanup of these devices to ensure your directory doesn't get consumed with lots of stale devices.
    - For non-persistent VDI deployments, you should delete devices that have **ApproximateLastLogonTimestamp** of older than 15 days.

Note

When using non-persistent VDI, if you want to prevent adding a work or school account ensure the following registry key is set: `HKLM\SOFTWARE\Policies\Microsoft\Windows\WorkplaceJoin: "BlockAADWorkplaceJoin"=dword:00000001`

Ensure you're running Windows 10, version 1803 or higher.

Roaming any data under the path `%localappdata%` is not supported. If you choose to move content under `%localappdata%`, make sure that the content of the following folders and registry keys **never** leaves the device under any condition. For example, profile migration tools must skip the following folders and keys:

- `%localappdata%\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy`
- `%localappdata%\Packages\Microsoft.Windows.CloudExperienceHost_cw5n1h2txyewy`
- `%localappdata%\Packages\<any app package>\AC\TokenBroker`
- `%localappdata%\Microsoft\TokenBroker`
- `%localappdata%\Microsoft\OneAuth`
- `%localappdata%\Microsoft\IdentityCache`
- `HKEY_CURRENT_USER\SOFTWARE\Microsoft\IdentityCRL`
- `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\AAD`
- `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\WorkplaceJoin`
- `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\TokenBroker`

Roaming of the work account's device certificate is not supported. The certificate, issued by "MS-Organization-Access", is stored in the Personal (MY) certificate store of the current user and on the local machine.

### Persistent VDI

When you deploy persistent VDI, Microsoft recommends the following guidance. Failure to follow these steps results in deployment and authentication issues.

- If you're relying on the System Preparation Tool (sysprep.exe) and if you're using a pre-Windows 10 1809 image for installation, make sure that image isn't from a device that is already registered with Microsoft Entra ID as Microsoft Entra hybrid joined.
- If you're relying on a Virtual Machine (VM) snapshot to create more VMs, make sure that snapshot isn't from a VM that is already registered with Microsoft Entra ID as Microsoft Entra hybrid join.

We recommend you implement a process for [managing stale devices](manage-stale-devices). This process ensures your directory doesn't accumulate stale devices if you periodically reset your VMs.