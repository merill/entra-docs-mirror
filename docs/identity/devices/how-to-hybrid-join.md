---
layout: Conceptual
title: Configure Microsoft Entra hybrid join - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/how-to-hybrid-join
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to configure Microsoft Entra hybrid join.
ms.topic: how-to
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: 4c959c98-c6ce-7a6e-d4d6-2a2118d63138
document_version_independent_id: ad40c382-f00b-dd28-b2b5-d889ac265ba5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/how-to-hybrid-join.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/how-to-hybrid-join
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/how-to-hybrid-join.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 00cac3d1-5295-bb03-96fb-b2fa42ead519
---

# Configure Microsoft Entra hybrid join - Microsoft Entra ID | Microsoft Learn

Bringing your devices to Microsoft Entra ID maximizes user productivity through single sign-on (SSO) across your cloud and on-premises resources. You can secure access to your resources with [Conditional Access](../conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa) at the same time.

## Prerequisites

- [Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594)version 1.1.819.0 or later.
    - Don't exclude the default device attributes from your Microsoft Entra Connect Sync configuration. To learn more about default device attributes synced to Microsoft Entra ID, see [Attributes synchronized by Microsoft Entra Connect](../hybrid/connect/reference-connect-sync-attributes-synchronized#windows-10).
    - If the computer objects of the devices you want to be Microsoft Entra hybrid joined belong to specific organizational units (OUs), configure the correct OUs to sync in Microsoft Entra Connect. To learn more about how to sync computer objects by using Microsoft Entra Connect, see [Organizational unit–based filtering](../hybrid/connect/how-to-connect-sync-configure-filtering#organizational-unitbased-filtering).
- [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator) credentials for your Microsoft Entra tenant.
- Enterprise administrator credentials for each of the on-premises Active Directory Domain Services forests.
- (**For federated domains**) At least Windows Server 2012 R2 with Active Directory Federation Services installed.
- Users can register their devices with Microsoft Entra ID. More information about this setting can be found under the heading **Configure device settings**, in the article, [Configure device settings](manage-device-identities#configure-device-settings).

### Network connectivity requirements

Microsoft Entra hybrid join requires devices to have access to the following Microsoft resources from inside your organization's network:

- `https://enterpriseregistration.windows.net`
- `https://login.microsoftonline.com`
- `https://device.login.microsoftonline.com`
- `https://autologon.microsoftazuread-sso.com` (If you use or plan to use seamless SSO)
- Your organization's Security Token Service (STS) (**For federated domains**)

Warning

If your organization uses proxy servers that intercept SSL traffic for scenarios like data loss prevention or Microsoft Entra tenant restrictions, ensure that traffic to `https://device.login.microsoftonline.com` and `https://enterpriseregistration.windows.net` are excluded from TLS break-and-inspect. Failure to exclude these URLs might cause interference with client certificate authentication, cause issues with device registration, and device-based Conditional Access.

If your organization requires access to the internet via an outbound proxy, you can use [Web Proxy Auto-Discovery (WPAD)](/en-us/previous-versions/tn-archive/cc995261%28v=technet.10%29) to enable Windows 10 or newer computers for device registration with Microsoft Entra ID. To address issues configuring and managing WPAD, see [Troubleshooting Automatic Detection](/en-us/previous-versions/tn-archive/cc302643%28v=technet.10%29).

If you don't use WPAD, you can configure WinHTTP proxy settings on your computer with a Group Policy Object (GPO) beginning with Windows 10 1709. For more information, see [WinHTTP Proxy Settings deployed by GPO](/en-us/archive/blogs/netgeeks/winhttp-proxy-settings-deployed-by-gpo).

Note

If you configure proxy settings on your computer by using WinHTTP settings, any computers that can't connect to the configured proxy will fail to connect to the internet.

If your organization requires access to the internet via an authenticated outbound proxy, make sure that your Windows 10 or newer computers can successfully authenticate to the outbound proxy. Because Windows 10 or newer computers run device registration by using machine context, configure outbound proxy authentication by using machine context. Follow up with your outbound proxy provider on the configuration requirements.

Verify devices can access the required Microsoft resources under the system account by using the [Test Device Registration Connectivity](/en-us/samples/azure-samples/testdeviceregconnectivity/testdeviceregconnectivity/) script.

## Managed domains

We think most organizations deploy Microsoft Entra hybrid join with managed domains. Managed domains use [password hash sync (PHS)](../hybrid/connect/whatis-phs) or [pass-through authentication (PTA)](../hybrid/connect/how-to-connect-pta) with [seamless single sign-on](../hybrid/connect/how-to-connect-sso). Managed domain scenarios don't require configuring a federation server.

Configure Microsoft Entra hybrid join by using Microsoft Entra Connect for a managed domain:

1. Open Microsoft Entra Connect, and then select **Configure**.
2. In **Additional tasks**, select **Configure device options**, and then select **Next**.
3. In **Overview**, select **Next**.
4. In **Connect to Microsoft Entra ID**, enter the credentials of a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator) for your Microsoft Entra tenant.
5. In **Device options**, select **Configure Microsoft Entra hybrid join**, and then select **Next**.
6. In **Device operating systems**, select the operating systems that devices in your Active Directory environment use, and then select **Next**.
7. In **SCP configuration**, for each forest where you want Microsoft Entra Connect to configure a service connection point (SCP), complete the following steps, and then select **Next**.

    1. Select the **Forest**.
    2. Select an **Authentication Service**.
    3. Select **Add** to enter the enterprise administrator credentials.

    ![A screenshot showing Microsoft Entra Connect and options to for SCP configuration in a managed domain.](media/how-to-hybrid-join/azure-ad-connect-scp-configuration-managed.png)
8. In **Ready to configure**, select **Configure**.
9. In **Configuration complete**, select **Exit**.

## Federated domains

A federated environment should have an identity provider that supports the following requirements. If you have a federated environment using Active Directory Federation Services (AD FS), then the below requirements are already supported.

- **WS-Trust protocol:**This protocol is required to authenticate the Microsoft Entra hybrid joined devices with Microsoft Entra ID. When you're using AD FS, you need to enable the following WS-Trust endpoints:
    - `/adfs/services/trust/2005/windowstransport`
    - `/adfs/services/trust/13/windowstransport`
    - `/adfs/services/trust/2005/usernamemixed`
    - `/adfs/services/trust/13/usernamemixed`
    - `/adfs/services/trust/2005/certificatemixed`
    - `/adfs/services/trust/13/certificatemixed`

Warning

Both **adfs/services/trust/2005/windowstransport** and **adfs/services/trust/13/windowstransport** should be enabled as intranet facing endpoints only and must NOT be exposed as extranet facing endpoints through the Web Application Proxy. To learn more on how to disable WS-Trust Windows endpoints, see [Disable WS-Trust Windows endpoints on the proxy](/en-us/windows-server/identity/ad-fs/deployment/best-practices-securing-ad-fs#disable-ws-trust-windows-endpoints-on-the-proxy-ie-from-extranet). You can see what endpoints are enabled through the AD FS management console under **Service** &gt; **Endpoints**.

Configure Microsoft Entra hybrid join by using Microsoft Entra Connect for a federated environment:

1. Open Microsoft Entra Connect, and then select **Configure**.
2. On the **Additional tasks** page, select **Configure device options**, and then select **Next**.
3. On the **Overview** page, select **Next**.
4. On the **Connect to Microsoft Entra ID** page, enter the credentials of a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator) for your Microsoft Entra tenant, and then select **Next**.
5. On the **Device options** page, select **Configure Microsoft Entra hybrid join**, and then select **Next**.
6. On the **SCP** page, complete the following steps, and then select **Next**:

    1. Select the forest.
    2. Select the authentication service. You must select **AD FS server** unless your organization has exclusively Windows 10 or newer clients and you configure computer/device sync, or your organization uses seamless SSO.
    3. Select **Add** to enter the enterprise administrator credentials.

    ![A screenshot showing Microsoft Entra Connect and options to for SCP configuration in a federated domain.](media/how-to-hybrid-join/azure-ad-connect-scp-configuration-federated.png)
7. On the **Device operating systems** page, select the operating systems that the devices in your Active Directory environment use, and then select **Next**.
8. On the **Federation configuration** page, enter the credentials of your AD FS administrator, and then select **Next**.
9. On the **Ready to configure** page, select **Configure**.
10. On the **Configuration complete** page, select **Exit**.

### Federation caveats

With Windows 10 1803 or newer, if instantaneous Microsoft Entra hybrid join for a federated environment using federation service fails, we rely on Microsoft Entra Connect to sync the computer object in Microsoft Entra ID to complete the device registration for Microsoft Entra hybrid join.

## Other scenarios

Organizations can test Microsoft Entra hybrid join on a subset of their environment before a full rollout. The steps to complete a targeted deployment can be found in the article [Microsoft Entra hybrid join targeted deployment](hybrid-join-control). Organizations should include a sample of users from varying roles and profiles in this pilot group. A targeted rollout helps identify any issues your plan might not address before you enable for the entire organization.

Some organizations might not be able to use Microsoft Entra Connect to configure AD FS. The steps to configure the claims manually can be found in the article [Configure Microsoft Entra hybrid join manually](hybrid-join-manual).

### US Government cloud (inclusive of GCCHigh and DoD)

For organizations in [Azure Government](https://azure.microsoft.com/global-infrastructure/government/), Microsoft Entra hybrid join requires devices to have access to the following Microsoft resources from inside your organization's network:

- `https://enterpriseregistration.windows.net`**and**`https://enterpriseregistration.microsoftonline.us`
- `https://login.microsoftonline.us`
- `https://device.login.microsoftonline.us`
- `https://autologon.microsoft.us` (If you use or plan to use seamless SSO)

## Troubleshoot Microsoft Entra hybrid join

If you experience issues with completing Microsoft Entra hybrid join for domain-joined Windows devices, see:

- [Troubleshooting devices using dsregcmd command](troubleshoot-device-dsregcmd)
- [Troubleshoot Microsoft Entra hybrid join for Windows current devices](troubleshoot-hybrid-join-windows-current)
- [Troubleshoot Microsoft Entra hybrid join for Windows downlevel devices](troubleshoot-hybrid-join-windows-legacy)
- [Troubleshoot pending device state](/en-us/troubleshoot/azure/active-directory/pending-devices)