---
layout: Conceptual
title: Use Windows Local Administrator Password Solution (LAPS) with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/howto-manage-local-admin-passwords
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Manage your device's local administrator password with Microsoft Entra LAPS.
ms.topic: how-to
ms.date: 2024-01-16T00:00:00.0000000Z
ms.reviewer: joflore, sandeo
ms.custom: references_regions
locale: en-us
document_id: 8b3c7a42-50dd-c476-58b9-e7fbab8b432d
document_version_independent_id: 6a251807-c5f8-4014-f242-e3526435a997
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/howto-manage-local-admin-passwords.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/howto-manage-local-admin-passwords
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/howto-manage-local-admin-passwords.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f8295326-8068-9c5c-18c2-0e764393e37d
---

# Use Windows Local Administrator Password Solution (LAPS) with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Every Windows device comes with a built-in local administrator account that you must secure and protect to mitigate any Pass-the-Hash (PtH) and lateral traversal attacks. Many customers have been using our standalone, on-premises [Local Administrator Password Solution (LAPS)](https://www.microsoft.com/download/details.aspx?id=46899) product for local administrator password management of their domain joined Windows machines. With Microsoft Entra support for Windows LAPS, we're providing a consistent experience for both Microsoft Entra joined and Microsoft Entra hybrid joined devices.

Microsoft Entra support for LAPS includes the following capabilities:

- **Enabling Windows LAPS with Microsoft Entra ID** - Enable a tenant wide policy and a client-side policy to back up local administrator password to Microsoft Entra ID.
- **Local administrator password management** - Configure client-side policies to set account name, password age, length, complexity, manual password reset and so on.
- **Recovering local administrator password** - Use API/Portal experiences for local administrator password recovery.
- **Enumerating all Windows LAPS enabled devices** - Use API/Portal experiences to enumerate all Windows devices in Microsoft Entra ID enabled with Windows LAPS.
- **Authorization of local administrator password recovery** - Use role-based access control (RBAC) policies with custom roles and administrative units.
- **Auditing local administrator password update and recovery** - Use audit logs API/Portal experiences to monitor password update and recovery events.
- **Conditional Access policies for local administrator password recovery** - Configure Conditional Access policies on directory roles that have the authorization of password recovery.

Note

Windows LAPS with Microsoft Entra ID is not supported for Windows devices that are [Microsoft Entra registered](concept-device-registration).

Local Administrator Password Solution isn't supported on non-Windows platforms.

To learn about Windows LAPS in more detail, start with the following articles in the Windows documentation:

- [What is Windows LAPS?](/en-us/windows-server/identity/laps/laps-scenarios-azure-active-directory) – Introduction to Windows LAPS and the Windows LAPS documentation set.
- [Windows LAPS CSP](/en-us/windows/client-management/mdm/laps-csp) – View the full details for LAPS settings and options. Intune policy for LAPS uses these settings to configure the LAPS CSP on devices.
- [Microsoft Intune support for Windows LAPS](/en-us/mem/intune/protect/windows-laps-overview)
- [Windows LAPS architecture](/en-us/windows-server/identity/laps/laps-concepts-overview#windows-laps-architecture)

## Requirements

### Supported Azure regions and Windows distributions

This feature is now available in the following Azure clouds:

- Azure Global
- Azure Government
- Microsoft Azure operated by 21Vianet

### Operating system updates

This feature is now available on the following Windows OS platforms with the specified update or later installed:

- [Windows 11 22H2 - April 11, 2023 Update](https://support.microsoft.com/help/5025239)
- [Windows 11 21H2 - April 11, 2023 Update](https://support.microsoft.com/help/5025224)
- [Windows 10 20H2, 21H2 and 22H2 - April 11, 2023 Update](https://support.microsoft.com/help/5025221)
- [Windows Server 2022 - April 11, 2023 Update](https://support.microsoft.com/help/5025230)
- [Windows Server 2019 - 11 2023 11, 2023 11 2023 Update](https://support.microsoft.com/help/5025229)

### Join types

LAPS is supported on Microsoft Entra joined or Microsoft Entra hybrid joined devices only. Microsoft Entra registered devices aren't supported.

### License requirements

LAPS is available to all customers with Microsoft Entra ID Free or higher licenses. Other related features like administrative units, custom roles, Conditional Access, and Intune have other licensing requirements.

### Required roles or permission

Other than the built-in Microsoft Entra roles like [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator) and [Intune Administrator](../role-based-access-control/permissions-reference#intune-administrator) that are granted *device.LocalCredentials.Read.All*, you can use [Microsoft Entra custom roles](../role-based-access-control/custom-create) or administrative units to authorize local administrator password recovery. For example:

- Custom roles must be assigned the *microsoft.directory/deviceLocalCredentials/password/read* permission to authorize local administrator password recovery. You can [create a custom role](../role-based-access-control/custom-create) and grant permissions using the [Microsoft Entra admin center](https://entra.microsoft.com), Microsoft Graph API, or PowerShell. Once you create a custom role, you can assign it to users.
- You can also create a Microsoft Entra ID [administrative unit](../role-based-access-control/administrative-units), add devices, and assign the Cloud Device Administrator role scoped to the administrative unit to authorize local administrator password recovery.

## Enabling Windows LAPS with Microsoft Entra ID

To enable Windows LAPS with Microsoft Entra ID, you must take actions in Microsoft Entra ID and the devices you wish to manage. We recommend organizations [manage Windows LAPS using Microsoft Intune](/en-us/mem/intune/protect/windows-laps-policy). If your devices are Microsoft Entra joined but not using or don't support Microsoft Intune, you can deploy Windows LAPS for Microsoft Entra ID manually. For more information, see the article [Configure Windows LAPS policy settings](/en-us/windows-server/identity/laps/laps-management-policy-settings).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator).
2. Browse to **Entra ID** &gt; **Devices** &gt; **Overview** &gt; **Device settings**
3. Select **Yes** for the **Enable Local Administrator Password Solution (LAPS)** setting, then select **Save**. You might also use the Microsoft Graph API [Update deviceRegistrationPolicy](/en-us/graph/api/deviceregistrationpolicy-update?view=graph-rest-beta&amp;preserve-view=true) to complete this task.
4. Configure a client-side policy and set the **BackUpDirectory** to be Microsoft Entra ID.

    - If you're using Microsoft Intune to manage client side policies, see [Manage Windows LAPS using Microsoft Intune](/en-us/mem/intune/protect/windows-laps-policy)
    - If you're using Group Policy Objects (GPOs) to manage client side policies, see [Windows LAPS Group Policy](/en-us/windows-server/identity/laps/laps-management-policy-settings#windows-laps-group-policy)

## Recovering local administrator password and password metadata

To view the local administrator password for a Windows device joined to Microsoft Entra ID, you must be granted the *microsoft.directory/deviceLocalCredentials/password/read* action.

To view the local administrator password metadata for a Windows device joined to Microsoft Entra ID, you must be granted the *microsoft.directory/deviceLocalCredentials/standard/read* action.

The following built-in roles are granted these actions by default:

| Built-in role | microsoft.directory/deviceLocalCredentials/standard/read and microsoft.directory/deviceLocalCredentials/password/read | microsoft.directory/deviceLocalCredentials/standard/read |
| --- | --- | --- |
| [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator) | Yes | Yes |
| [Intune Service Administrator](../role-based-access-control/permissions-reference#intune-administrator) | Yes | Yes |
| [Helpdesk Administrator](../role-based-access-control/permissions-reference#helpdesk-administrator) | No | Yes |
| [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) | No | Yes |
| [Security Reader](../role-based-access-control/permissions-reference#security-reader) | No | Yes |

Any roles not listed are granted neither action.

You can also use Microsoft Graph API [Get deviceLocalCredentialInfo](/en-us/graph/api/devicelocalcredentialinfo-get?view=graph-rest-beta&amp;preserve-view=true) to recover local administrative password. If you use the Microsoft Graph API, the password returned is in Base64 encoded value that you need to decode before using it.

## List all Windows LAPS enable devices

To list all Windows LAPS enabled devices, you can browse to **Entra ID** &gt; **Devices** &gt; **Overview** &gt; **Local administrator password recovery** or use the Microsoft Graph API.

## Auditing local administrator password update and recovery

To view audit events, you can browse to **Entra ID** &gt; **Devices** &gt; **Overview** &gt; **Audit logs**, then use the **Activity** filter and search for **Update device local administrator password** or **Recover device local administrator password** to view the audit events.

## Conditional Access policies for local administrator password recovery

Conditional Access policies can be scoped to the built-in roles to protect access to recover local administrator passwords. You can find an example of a policy that requires multifactor authentication in the article, [Common Conditional Access policy: Require MFA for administrators](../conditional-access/policy-old-require-mfa-admin).

Note

Other role types including administrative unit-scoped roles and custom roles aren't supported

## Frequently asked questions

### Is Windows LAPS with Microsoft Entra management configuration supported using Group Policy Objects (GPOs)?

Yes, for [Microsoft Entra hybrid joined](concept-hybrid-join) devices only. See see [Windows LAPS Group Policy](/en-us/windows-server/identity/laps/laps-management-policy-settings#windows-laps-group-policy).

### Is Windows LAPS with Microsoft Entra management configuration supported using MDM?

Yes, for [Microsoft Entra join](concept-directory-join)/[Microsoft Entra hybrid join](concept-hybrid-join) ([co-managed](/en-us/mem/configmgr/comanage/overview)) devices. Customers can use [Microsoft Intune](/en-us/mem/intune/protect/windows-laps-overview) or any other third-party mobile device management (MDM) of their choice.

### What happens when a device is deleted in Microsoft Entra ID?

When a device is deleted in Microsoft Entra ID, the LAPS credential that was tied to that device is lost, and the password that is stored in Microsoft Entra ID is lost. Unless you have a custom workflow to retrieve LAPS passwords and store them externally, there's no method in Microsoft Entra ID to recover the LAPS managed password for a deleted device.

### What roles are needed to recover LAPS passwords?

The following built-in roles Microsoft Entra roles have permission to recover LAPS passwords: Cloud Device Administrator and Intune Administrator.

### What roles are needed to read LAPS metadata?

The following built-in roles are supported to view metadata about LAPS including the device name, last password rotation, and next password rotation: Cloud Device Administrator, Intune Administrator, Helpdesk Administrator, Security Reader and Security Administrator.

### Are custom roles supported?

Yes. If you have Microsoft Entra ID P1 or P2, you can create a custom role with the following RBAC permissions:

- To read LAPS metadata: *microsoft.directory/deviceLocalCredentials/standard/read*
- To read LAPS passwords: *microsoft.directory/deviceLocalCredentials/password/read*

### What happens when the local administrator account specified by policy is changed?

Because Windows LAPS can only manage one local admin account on a device at a time, the original account is no longer managed by LAPS policy. If policy has the device back up that account, the new account is backed up and details about the previous account are no longer available from within the Intune admin center or from the Directory specified to store the account information.