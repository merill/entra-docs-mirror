---
layout: FAQ
title: Microsoft Entra device management FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/faq
summary: ''
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Microsoft Entra device management FAQ.
ms.custom: has-azure-ad-ps-ref
ms.topic: faq
ms.date: 2024-11-25T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: fa632bd8-9300-c9fa-11fc-0c4be6862c6e
document_version_independent_id: d0d3cf71-5945-c202-d466-12c3da3fb473
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 79187b33-08a6-301e-4616-7586eda8d1c1
---

# Microsoft Entra device management FAQ - Microsoft Entra ID | Microsoft Learn

## General FAQ

### I registered the device recently. Why can't I see the device under my user info? Or why is the device owner marked as N/A for Microsoft Entra hybrid joined devices?

Windows 10 or newer devices that are Microsoft Entra hybrid joined don't show up under **USER devices**. Use the **All devices** view. You can also use a PowerShell [Get-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice) cmdlet.

Only the following devices are listed under **USER devices**:

- All personal devices that aren't Microsoft Entra hybrid joined.
- All non-Windows 10 or newer and Windows Server 2016 or later devices.
- All non-Windows devices.

### How do I know what the device registration state of the client is?

Go to **All devices**. Search for the device by using the device ID. Check the value under the join type column. Sometimes, the device might be reset or reimaged. So it's essential to also check the device registration state on the device:

- For Windows 10 or newer and Windows Server 2016 or later devices, run `dsregcmd.exe /status`.

For troubleshooting information, see these articles:

- [Troubleshooting devices using dsregcmd command](troubleshoot-device-dsregcmd)
- [Troubleshooting Microsoft Entra hybrid joined Windows 10 and Windows Server 2016 devices](troubleshoot-hybrid-join-windows-current)

### My org on-premises AD users are split into two or more different tenants in Microsoft Entra ID. Do I get Windows PRT for each tenant on client machine?

Windows clients fetch the PRT from Microsoft Entra ID if the user and the device belong to the same tenant. Users don't get a PRT for another tenant if the device isn't registered or the user isn't a member there. If the two tenants trust each other via B2B, you can always create cross tenant B2B access and trust device claims from your home tenant.

### I see the device record under the USER info and I see the state as registered. Am I set up correctly to use Conditional Access?

The device join state, shown by **deviceID**, must match the state on Microsoft Entra ID and meet any evaluation criteria for Conditional Access. For more information, see [Require managed devices for cloud app access with Conditional Access](../conditional-access/concept-conditional-access-grant).

### Why do my users see an error message saying "Your organization has deleted the device" or "Your organization has disabled the device" on their Windows 10/11 devices?

On Windows 10/11 devices joined or registered with Microsoft Entra ID, users are issued a [Primary refresh token (PRT)](concept-primary-refresh-token) which enables single sign-on. The validity of the PRT is based on the validity of the device itself. Users see this message if the device is either deleted or disabled in Microsoft Entra ID without initiating the action from the device itself. A device can be deleted or disabled in Microsoft Entra one of the following scenarios:

- User disables the device from the My Apps portal.
- An administrator (or user) deletes or disables the device.
- Microsoft Entra hybrid joined only: An administrator removes the devices OU out of sync scope resulting in the devices being deleted from Microsoft Entra ID.
- Microsoft Entra hybrid joined only: An administrator disables the computer account on premises, resulting in the device being disabled in Microsoft Entra ID.

### I disabled or deleted my device, but the local state on the device says it's registered. What should I do?

This operation is by design. In this case, the device doesn't have access to resources in the cloud. Administrators can perform this action for stale, lost, or stolen devices to prevent unauthorized access. If this action was performed unintentionally, you need to re-enable or re-register the device using the steps that follow:

- If the device was disabled in Microsoft Entra ID, an administrator with sufficient privileges can enable it in the Microsoft Entra admin center.

    Note

    If you're syncing devices using Microsoft Entra Connect, Microsoft Entra hybrid joined devices will be automatically re-enabled during the next sync cycle. So, if you need to disable a Microsoft Entra hybrid joined device, you need to disable it from your on-premises AD.
- If the device is deleted in Microsoft Entra ID, you need to re-register the device. To re-register, you must take a manual action on the device. See the following steps for instructions to re-register based on the device state.

    To re-register Microsoft Entra hybrid joined Windows 10/11 and Windows Server 2016/2019 devices, take the following steps:

    1. Open the command prompt as an administrator.
    2. Enter `dsregcmd.exe /debug /leave`.
    3. Sign out and sign in to trigger the scheduled task that registers the device again with Microsoft Entra ID.

    For Microsoft Entra joined devices Windows 10/11 devices, take the following steps:

    1. Open the command prompt as an administrator
    2. Enter `dsregcmd /forcerecovery` (You need to be an administrator to perform this action).
    3. Click "Sign in" in the dialog that opens up and continue with the sign in process.
    4. To complete the recovery, sign out and sign back in on the device.

    For Microsoft Entra registered Windows 10/11 devices, take the following steps:

    1. Go to **Settings** &gt; **Accounts** &gt; **Access Work or School**.
    2. Select the account and select **Disconnect**.
    3. Click on "+ Connect" and register the device again by going through the sign in process.

### Why do I see duplicate device entries?

- For Windows 10 or newer and Windows Server 2016 or later, repeated tries to unjoin and rejoin the same device might cause duplicate entries.
- Each Windows user who uses **Add Work or School Account** creates a new device record with the same device name.
- A Microsoft Entra joined machine that's wiped, reinstalled, and rejoined with the same name shows up as another record with the same device name.

### Does Windows 10/11 device registration in Microsoft Entra support TPMs in FIPS mode?

Windows 10/11 device registration is only supported for FIPS-compliant TPM 2.0 and not supported for TPM 1.2. If your devices have FIPS-compliant TPM 1.2, you must disable them before proceeding with Microsoft Entra join or Microsoft Entra hybrid join. Microsoft doesn't provide any tools for disabling FIPS mode for TPMs as it is dependent on the TPM manufacturer. Contact your hardware OEM for support.

### Why can a user still access resources from a device I disabled?

It takes up to an hour for a revoke to be applied from the time the Microsoft Entra device is marked as disabled.

Note

For enrolled devices, we recommend that you wipe the device to make sure users can't access the resources. For more information, see [What is device enrollment?](/en-us/mem/intune/user-help/use-managed-devices-to-get-work-done).

### I can't add more than three Microsoft Entra user accounts under the same user session on a Windows 10/11 device, why?

Microsoft Entra ID added support for multiple Microsoft Entra accounts starting in Windows 10 1803 release. However, Windows 10/11 restricts the number of Microsoft Entra accounts on a device to 3 to limit the size of token requests and enable reliable single sign-on (SSO). Once three accounts are added, users see an error for subsequent accounts. The additional problem information on the error screen provides the following message indicating the reason - "Add account operation is blocked because account limit is reached".

### What are the MS-Organization-Access certificates present on our Windows 10/11 devices?

The Microsoft Entra Device Registration Service issues the MS-Organization-Access certificates during the device registration process. These certificates are issued to all join types supported on Windows - Microsoft Entra joined, Microsoft Entra hybrid joined and Microsoft Entra registered devices. Once issued, they're used as part of the authentication process from the device to request a Primary Refresh Token (PRT). For Microsoft Entra joined and Microsoft Entra hybrid joined devices, this certificate is present in Local Computer\Personal\Certificates whereas for Microsoft Entra registered devices, certificate is present in Current User\Personal\Certificates. All MS-Organization-Access certificates have a default lifetime of 10 years. These certificates are deleted from the corresponding certificate store when the device is unregistered from Microsoft Entra ID. Any inadvertent deletion of this certificate leads to authentication failures for the user, and requiring re-registration of the device in such cases.

## Microsoft Entra join FAQ

### How do I unjoin a Microsoft Entra joined device locally on the device?

For pure Microsoft Entra joined devices, make sure you have an offline local administrator account or create one. You can't sign in with any Microsoft Entra user credentials. Next, go to **Settings** &gt; **Accounts** &gt; **Access Work or School**. Select your account and select **Disconnect**. Follow the prompts and provide the local administrator credentials when prompted. Reboot the device to finish the unjoin process.

### Can my users sign in to Microsoft Entra joined devices that are deleted or disabled in Microsoft Entra ID?

Yes. Windows has a cached username and password capability that allows users who signed in previously to access the desktop quickly even without network connectivity.

When a device is deleted or disabled in Microsoft Entra ID, it's not known to the Windows device. So users who signed in previously continue to access the desktop with the cached username and password. But as the device is deleted or disabled, users can't access any resources protected by device-based Conditional Access.

Users who didn't sign in previously can't access the device. There's no cached username and password enabled for them.

### Can a disabled or deleted user sign in to a Microsoft Entra joined device?

Yes, but only for a limited time. When a user is deleted or disabled in Microsoft Entra ID, it's not immediately known to the Windows device. So users who signed in previously can access the desktop with the cached username and password.

Typically, the device is aware of the user state in less than four hours. Then Windows blocks those users' access to the desktop. As the user is deleted or disabled in Microsoft Entra ID, all their tokens are revoked. So they can't access any resources.

Deleted or disabled users who didn't sign in previously can't access a device. There's no cached username and password enabled for them.

### Can a guest user sign in to a Microsoft Entra joined device?

No, currently, guest users can't sign in to a Microsoft Entra joined device.

### My users can't search printers from Microsoft Entra joined devices. How can I enable printing from those devices?

Organizations can choose to [deploy Windows Server Hybrid Cloud Print with Pre-Authentication](/en-us/universal-print/) or [Universal Print](/en-us/universal-print/fundamentals/universal-print-whatis) for their Microsoft Entra joined devices.

### How do I connect to a remote Microsoft Entra joined device?

See [Connect to remote Microsoft Entra joined PC](/en-us/windows/client-management/client-tools/connect-to-remote-aadj-pc).

### Why do my users see 'You can't get there from here'?

Did you configure Conditional Access policies to require a specific device state? If the device doesn't meet the criteria, users are blocked, and they see that message. Evaluate your Conditional Access policies. Make sure the device meets the criteria to avoid the message.

### Why do I get a 'username or password is incorrect' message for a device I just joined to Microsoft Entra ID?

Common reasons for this scenario are as follows:

- Your user credentials are no longer valid.
- Your computer can't communicate with Microsoft Entra ID. Check for any network connectivity issues.
- Federated sign-ins require your federation server to support WS-Trust endpoints that are enabled and accessible.
- You enabled pass-through authentication. So your temporary password needs to be changed when you sign in.

### How can users change their temporary or expired password on Microsoft Entra joined devices?

Currently, Microsoft Entra joined devices don't force users to change password on the lock screen. So, users with temporary or expired passwords will be forced to change passwords only when they access an application (that requires a Microsoft Entra token) after they log in to Windows.

### Why do I see the 'Oops… an error occurred!' dialog when I try to Microsoft Entra join my PC?

This error happens when you set up Microsoft Entra autoenrollment with Intune without proper license assigned. Make sure that the user who tries to Microsoft Entra join has the correct Intune license assigned. For more information, see [Set up enrollment for Windows devices](/en-us/mem/intune/enrollment/windows-enroll).

### Why did my attempt to Microsoft Entra join a PC fail, although I didn't get any error information?

A likely cause is that you signed in to the device by using the local built-in administrator account. Create a different local account before you use Microsoft Entra join to finish the setup.

### What is the P2P Server application and why is it registered in my tenant?

The P2P Server application is application registered by Microsoft Entra ID to enable Remote Desktop Protocol (RDP) connections to any Microsoft Entra joined or Microsoft Entra hybrid joined Windows devices in your tenant. This application creates a tenant wide certificate issued by Microsoft Entra's certificate authority and is used to issue RDP device and user certificates for RDP connectivity. To ensure this is the correct application, you can find the **Object ID** of the P2P Server application in the **Microsoft Entra admin center** &gt; **Applications** &gt; **Enterprise Applications**. Remove the default filter applied do you can see all applications. Compare this **Object ID** using the Microsoft Graph API to query for the details using [GET /servicePrincipals/{objectid}](/en-us/graph/api/serviceprincipal-get) and confirm that the servicePrincipalNames property is `urn:p2p_cert`.

### What are the MS-Organization-P2P-Access certificates present on our Windows 10/11 devices?

Microsoft Entra ID issues the MS-Organization-P2P-Access certificates to Microsoft Entra joined and Microsoft Entra hybrid joined devices. These certificates are used to enable trust between devices in the same tenant for remote desktop scenarios. One certificate is issued to the device and another is issued to the user. The device certificate is present in `Local Computer\Personal\Certificates` and is valid for one day. This certificate is renewed (by issuing a new certificate) if the device is still active in Microsoft Entra ID. The user certificate isn't persistent and is valid for one hour, it's issued on-demand when a user attempts a remote desktop session to another Microsoft Entra joined device. It isn't renewed on expiry. Both these certificates are issued using the MS-Organization-P2P-Access certificate present in the `Local Computer\AAD Token Issuer\Certificates`. Microsoft Entra ID issues this certificate during device registration.

### How can we disable cached logon/expire the cache logon of the user on Microsoft Entra joined devices?

It isn't possible to disable or expire previous cached logons on Microsoft Entra joined devices.

## Microsoft Entra hybrid join FAQ

### How do I unjoin a Microsoft Entra hybrid joined device locally on the device?

For Microsoft Entra hybrid joined devices, make sure to turn off automatic registration in AD using the [Controlled validation](hybrid-join-control) article. Then the scheduled task doesn't register the device again. Next, open a command prompt as an administrator and enter `dsregcmd.exe /debug /leave`. Or run this command as a script across several devices to unjoin in bulk.

### Where can I find troubleshooting information to diagnose Microsoft Entra hybrid join failures?

For troubleshooting information, see these articles:

- [Troubleshooting Microsoft Entra hybrid joined Windows 10 and Windows Server 2016 devices](troubleshoot-hybrid-join-windows-current)

### Why do I see a duplicate Microsoft Entra registered record for my Windows 10/11 Microsoft Entra hybrid joined device in the Microsoft Entra devices list?

When your users add their accounts to apps on a domain-joined device, they might be prompted with **Add account to Windows?** If they enter **Yes** on the prompt, the device registers with Microsoft Entra ID. The trust type is marked as Microsoft Entra registered. After you enable Microsoft Entra hybrid join in your organization, the device also gets Microsoft Entra hybrid joined. Then two device states show up for the same device.

In most cases, Microsoft Entra hybrid join takes precedence over the Microsoft Entra registered state, resulting in your device being considered Microsoft Entra hybrid joined for any authentication and Conditional Access evaluation. However, sometimes, this dual state can result in a nondeterministic evaluation of the device and cause access issues. We strongly recommend upgrading to Windows 10 version 1803 and above where we automatically clean up the Microsoft Entra registered state. Learn how to [avoid or clean up this dual state on the Windows 10 machine](hybrid-join-plan#review-things-you-should-know).

### Why do my users have issues on Windows 10 Microsoft Entra hybrid joined devices after changing their UPN?

UPN changes are supported with Windows 10 2004 update and also applicable to Windows 11. Users on devices with this update won't have any issues after changing their UPNs.

UPN changes on older versions of Windows 10 aren't fully supported with Microsoft Entra hybrid joined devices. While users can sign in to the device and access their on-premises applications, authentication with Microsoft Entra ID fails after a UPN change. As a result, users have SSO and Conditional Access issues on their devices. You need to unjoin the device from Microsoft Entra ID (run "dsregcmd /leave" with elevated privileges) and rejoin (happens automatically) to resolve the issue.

### Do Windows 10/11 Microsoft Entra hybrid joined devices require line of sight to the domain controller to get access to cloud resources?

No, except when the user's password is changed. After Windows 10/11 Microsoft Entra hybrid join is complete, and the user signs in at least once, the device doesn't require line of sight to the domain controller to access cloud resources. Windows 10/11 can get single sign-on to Microsoft Entra applications from anywhere with an internet connection, except when a password is changed. Users who sign in with Windows Hello for Business continue to get single sign-on to Microsoft Entra applications even after a password change, even if they don't have line of sight to their domain controller.

### What happens if a user changes their password and tries to sign in to their Windows 10/11 Microsoft Entra hybrid joined device outside the corporate network?

If a password is changed outside the corporate network (for example, by using Microsoft Entra SSPR), then the user sign-in with the new password fails. For Microsoft Entra hybrid joined devices, on-premises Active Directory is the primary authority. When a device doesn't have line of sight to a domain controller, it's unable to validate the new password. The user needs to establish a connection with the domain controller (either via VPN or being in the corporate network) before they're able to sign in to the device with their new password. Otherwise, they can only sign in with their old password because of cached sign-in capability in Windows. Microsoft Entra invalidates the old password during token requests. This invalidation process prevents single sign-on and fails any device-based Conditional Access policies until the user authenticates with their new password in an app or browser. This issue doesn't occur if you use Microsoft Entra joined devices.

## Microsoft Entra register FAQ

### How do I remove a Microsoft Entra registered state for a device locally?

- For Windows 10/11 Microsoft Entra registered devices, Go to **Settings** &gt; **Accounts** &gt; **Access Work or School**. Select your account and select **Disconnect**. Device registration is per user profile on Windows 10/11.
- For iOS and Android, you can use the Microsoft Authenticator application **Settings** &gt; **Device Registration** and select **Unregister device**.
- For macOS, you can use the Microsoft Intune Company Portal application to unenroll the device from management and remove any registration.

For Windows 10 version 2004 and older, this process can be automated with the [Workplace Join (WPJ) removal tool](https://download.microsoft.com/download/8/e/f/8ef13ae0-6aa8-48a2-8697-5b1711134730/WPJCleanUp.zip).

Note

This tool removes all SSO accounts on the device. After this operation, all applications will lose SSO state, and the device will be unenrolled from management tools (MDM) and unregistered from the cloud. The next time an application tries to sign in, users will be asked to add the account again.

### How can I block users from adding more work accounts (Microsoft Entra registered) on my corporate Windows 10/11 devices?

Enable the following registry to block your users from adding other work accounts to your corporate domain joined, Microsoft Entra joined, or Microsoft Entra hybrid joined Windows 10/11 devices. This policy can also be used to block domain joined machines from inadvertently getting Microsoft Entra registered with the same user account.

`HKLM\SOFTWARE\Policies\Microsoft\Windows\WorkplaceJoin, "BlockAADWorkplaceJoin"=dword:00000001`