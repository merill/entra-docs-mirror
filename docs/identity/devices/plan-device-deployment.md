---
layout: Conceptual
title: Plan your Microsoft Entra device deployment - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/plan-device-deployment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: martinco
description: Choose the Microsoft Entra device integration strategies that meet your organizational needs.
ms.topic: how-to
ms.date: 2024-11-25T00:00:00.0000000Z
ms.reviewer: sandeo, gasinh
locale: en-us
document_id: a61e732b-598f-0f74-ec52-8167b4ffacf0
document_version_independent_id: 4e853408-bc43-d9d3-dcf6-12b475499898
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/plan-device-deployment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/plan-device-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/plan-device-deployment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6fad278c-155a-9ab9-112f-e9f9f93f56e6
---

# Plan your Microsoft Entra device deployment - Microsoft Entra ID | Microsoft Learn

This article helps you evaluate the methods to integrate your device with Microsoft Entra ID, choose the implementation plan, and provides key links to supported device management tools.

The landscape of your user's devices is constantly expanding. Organizations might provide desktops, laptops, phones, tablets, and other devices. Your users might bring their own array of devices, and access information from varied locations. In this environment, your job as an administrator is to keep your organizational resources secure across all devices.

Microsoft Entra ID enables your organization to meet these goals with device identity management. You can now get your devices in Microsoft Entra ID and control them from a central location in the [Microsoft Entra admin center](https://entra.microsoft.com). This process gives you a unified experience, enhanced security, and reduces the time needed to configure a new device.

There are multiple methods to integrate your devices into Microsoft Entra ID. These methods can work separately or together based on the operating system and your requirements:

- You can [register devices](concept-device-registration) with Microsoft Entra ID.
- [Join devices](concept-directory-join) to Microsoft Entra ID (cloud-only).
- [Microsoft Entra hybrid join](concept-hybrid-join) devices to your on-premises Active Directory domain and Microsoft Entra ID.

## Learn

Before you begin, make sure that you're familiar with the [device identity management overview](overview).

### Benefits

The key benefits of giving your devices a Microsoft Entra identity:

- Increase productivity – Users can do [seamless sign-on (SSO)](device-sso-to-on-premises-resources) to your on-premises and cloud resources, enabling productivity wherever they are.
- Increase security – Apply [Conditional Access policies](../conditional-access/overview) to resources based on the identity of the device or user. Joining a device to Microsoft Entra ID is a prerequisite for increasing your security with a [Passwordless](../authentication/concept-authentication-passkeys-fido2) strategy.
- Improve user experience – Provide your users with easy access to your organization’s cloud-based resources from both personal and corporate devices. Administrators can enable [Enterprise State Roaming](enterprise-state-roaming-enable) for a unified experience across all Windows devices.
- Simplify deployment and management – Simplify the process of bringing devices to Microsoft Entra ID with [Windows Autopilot](/en-us/windows/deployment/windows-autopilot/windows-10-autopilot), [bulk provisioning](/en-us/mem/intune/enrollment/windows-bulk-enroll), or [self-service: Out of Box Experience (OOBE)](https://support.microsoft.com/account-billing/join-your-work-device-to-your-work-or-school-network-ef4d6adb-5095-4e51-829e-5457430f3973). Manage devices with Mobile Device Management (MDM) tools like [Microsoft Intune](/en-us/mem/intune/fundamentals/what-is-intune), and their identities in the [Microsoft Entra admin center](https://entra.microsoft.com).

## Plan the deployment project

Consider your organizational needs while you determine the strategy for this deployment in your environment.

### Engage the right stakeholders

When technology projects fail, they typically do because of mismatched expectations on impact, outcomes, and responsibilities. To avoid these pitfalls, [ensure that you're engaging the right stakeholders,](../../architecture/deployment-plans) and that stakeholder roles in the project are well understood.

For this plan, add the following stakeholders to your list:

| Role | Description |
| --- | --- |
| Device administrator | A representative from the device team that can verify that the plan meets the device requirements of your organization. |
| Network administrator | A representative from the network team that can make sure to meet network requirements. |
| Device management team | Team that manages inventory of devices. |
| OS-specific admin teams | Teams that support and manage specific OS versions. For example, there might be a Mac or iOS focused team. |

### Plan communications

Communication is critical to the success of any new service. Proactively communicate with your users how their experience changes, when it changes, and how to gain support if they experience issues.

### Plan a pilot

We recommend that the initial configuration of your integration method is in a test environment, or with a small group of test devices. See [Best practices for a pilot](../../architecture/deployment-plans).

You might want to do a [targeted deployment of Microsoft Entra hybrid join](hybrid-join-control) before enabling it across the entire organization.

Warning

Organizations should include a sample of users from varying roles and profiles in their pilot group. A targeted rollout will help identify any issues your plan may not have addressed before you enable for the entire organization.

### Network Requirements for Device Registration with Microsoft Entra

The following sites must be exempted if using TLS interception or network proxy filtering to ensure registration works as intended:

- `enterpriseregistration.windows.net`
- `certauth.enterpriseregistration.windows.net`
- `enterpriseregistration.partner.microsoftonline.cn` (\*\*)
- `certauth.enterpriseregistration.partner.microsoftonline.cn`(\*\*)
- `enterpriseregistration.microsoftonline.us`(\*\*)
- `certauth.enterpriseregistration.microsoftonline.us`(\*\*)

( \*\* ) You only need to allow sovereign cloud domains if you rely on those in your environment.

Note

Failure to exempt these endpoints may result in failure of device registration flows.

## Choose your integration methods

Your organization can use multiple device integration methods in a single Microsoft Entra tenant. The goal is to choose one or more methods suitable to get your devices securely managed in Microsoft Entra ID. There are many parameters that drive this decision including ownership, device types, primary audience, and your organization’s infrastructure.

The following information can help you decide which integration methods to use.

### Decision tree for devices integration

Use this tree to determine options for organization-owned devices.

Note

Personal or bring-your-own device (BYOD) scenarios are not pictured in this diagram. They always result in Microsoft Entra registration.

![Decision tree](media/plan-device-deployment/flowchart.png)

### Comparison matrix

iOS and Android devices are only Microsoft Entra registered. The following table presents high-level considerations for Windows client devices. Use it as an overview, then explore the different integration methods in detail.

| Consideration | Microsoft Entra registered | Microsoft Entra joined | Microsoft Entra hybrid joined |
| --- | --- | --- | --- |
| **Client operating systems** |  |  |  |
| Windows 11 or Windows 10 devices | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Linux Desktop - Ubuntu 20.04/22.04/24.04, RHEL 8/9 | ![Checkmark for these values.](media/plan-device-deployment/check.png) |  |  |
| **Sign in options** |  |  |  |
| End-user local credentials | ![Checkmark for these values.](media/plan-device-deployment/check.png) |  |  |
| Password | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Device PIN | ![Checkmark for these values.](media/plan-device-deployment/check.png) |  |  |
| Windows Hello | ![Checkmark for these values.](media/plan-device-deployment/check.png) |  |  |
| Windows Hello for Business |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| FIDO 2.0 security keys |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Microsoft Authenticator App (passwordless) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| **Key capabilities** |  |  |  |
| SSO to cloud resources | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| SSO to on-premises resources |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Conditional Access  (Require devices be marked as compliant)  (Must be managed by MDM) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Conditional Access (Require Microsoft Entra hybrid joined devices) |  |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Self-service password reset from the Windows login screen |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| Windows Hello PIN reset |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |

## Microsoft Entra Registration

Registered devices are often managed with [Microsoft Intune](/en-us/mem/intune/fundamentals/deployment-guide-enrollment). Devices are enrolled in Intune in several ways, depending on the operating system.

Microsoft Entra registered devices provide support for Bring Your Own Devices (BYOD) and corporate owned devices to SSO to cloud resources. Access to resources is based on the Microsoft Entra [Conditional Access policies](../conditional-access/concept-conditional-access-grant) applied to the device and the user.

### Registering devices

Registered devices are often managed with [Microsoft Intune](/en-us/mem/intune/fundamentals/deployment-guide-enrollment). Devices are enrolled in Intune in several ways, depending on the operating system.

Users install the Company portal app to register BYOD and corporate owned mobile devices.

- [iOS](/en-us/mem/intune/user-help/sign-in-to-the-company-portal)
- [Android](/en-us/mem/intune/user-help/enroll-device-android-company-portal)
- [Windows 10 or newer](/en-us/mem/intune/user-help/enroll-windows-10-device)
- [macOS](/en-us/mem/intune/user-help/enroll-your-device-in-intune-macos-cp)
- [Linux Desktop](/en-us/mem/intune/user-help/enroll-device-linux)

If registering your devices is the best option for your organization, see the following resources:

- This overview of [Microsoft Entra registered devices](concept-device-registration).
- This end-user documentation on [Register your personal device on your organization’s network](https://support.microsoft.com/account-billing/register-your-personal-device-on-your-work-or-school-network-8803dd61-a613-45e3-ae6c-bd1ab25bf8a8).

## Microsoft Entra join

Microsoft Entra join enables you to transition towards a cloud-first model with Windows. It provides a great foundation if you're planning to modernize your device management and reduce device-related IT costs. Microsoft Entra join works with Windows 10 or newer devices only. Consider it as the first choice for new devices.

[Microsoft Entra joined devices can SSO to on-premises resources](device-sso-to-on-premises-resources) when they are on the organization's network, can authenticate to on-premises servers like file, print, and other applications.

If this option is best for your organization, see the following resources:

- This overview of [Microsoft Entra joined devices](concept-directory-join).
- Familiarize yourself with the [Microsoft Entra join implementation plan](device-join-plan).

### Provisioning Microsoft Entra joined devices

To provision devices to Microsoft Entra join, you have the following approaches:

- Self-Service: [Windows 10 first-run experience](device-join-out-of-box)

If you have either Windows 10 Professional or Windows 10 Enterprise installed on a device, the experience defaults to the setup process for company-owned devices.

- [Windows Out of Box Experience (OOBE) or from Windows Settings](https://support.microsoft.com/account-billing/join-your-work-device-to-your-work-or-school-network-ef4d6adb-5095-4e51-829e-5457430f3973)
- [Windows Autopilot](/en-us/windows/deployment/windows-autopilot/windows-autopilot)
- [Bulk Enrollment](/en-us/mem/intune/enrollment/windows-bulk-enroll)

Choose your deployment procedure after careful [comparison of these approaches](device-join-plan).

You might determine that Microsoft Entra join is the best solution for a device in a different state. The following table shows how to change the state of a device.

| Current device state | Desired device state | How-to |
| --- | --- | --- |
| On-premises domain joined | Microsoft Entra joined | Unjoin the device from on-premises domain before joining to Microsoft Entra ID. |
| Microsoft Entra hybrid joined | Microsoft Entra joined | Unjoin the device from on-premises domain and from Microsoft Entra ID before joining to Microsoft Entra ID. |
| Microsoft Entra registered | Microsoft Entra joined | Unregister the device before joining to Microsoft Entra ID. |

## Microsoft Entra hybrid join

If you have an on-premises Active Directory environment and want to join your existing domain-joined computers to Microsoft Entra ID, you can accomplish this task with Microsoft Entra hybrid join. It supports a [broad range of Windows devices](hybrid-join-plan).

Most organizations already have domain joined devices and manage them via Group Policy or System Center Configuration Manager (SCCM). In that case, we recommend configuring Microsoft Entra hybrid join to start getting benefits while using existing investments.

If Microsoft Entra hybrid join is the best option for your organization, see the following resources:

- This overview of [Microsoft Entra hybrid joined devices](concept-hybrid-join).
- Familiarize yourself with the [Microsoft Entra hybrid join implementation](hybrid-join-plan) plan.

### Provisioning Microsoft Entra hybrid join to your devices

[Review your identity infrastructure](hybrid-join-plan). Microsoft Entra Connect provides you with a wizard to configure Microsoft Entra hybrid join for:

- [Managed domains](how-to-hybrid-join#managed-domains)
- [Federated domains](how-to-hybrid-join#federated-domains)

If installing the required version of Microsoft Entra Connect isn't an option for you, see [how to manually configure Microsoft Entra hybrid join](hybrid-join-manual).

Note

The on-premises domain-joined Windows 10 or newer device attempts to auto-join to Microsoft Entra ID to become Microsoft Entra hybrid joined by default. This will only succeed if you have set up the right environment.

You might determine that Microsoft Entra hybrid join is the best solution for a device in a different state. The following table shows how to change the state of a device.

| Current device state | Desired device state | How-to |
| --- | --- | --- |
| On-premises domain joined | Microsoft Entra hybrid joined | Use Microsoft Entra Connect or AD FS to join to Azure. |
| On-premises workgroup joined or new | Microsoft Entra hybrid joined | Supported with [Windows Autopilot](/en-us/windows/deployment/windows-autopilot/windows-autopilot). Otherwise device needs to be on-premises domain joined before Microsoft Entra hybrid join. |
| Microsoft Entra joined | Microsoft Entra hybrid joined | Unjoin from Microsoft Entra ID, which puts it in the on-premises workgroup or new state. |
| Microsoft Entra registered | Microsoft Entra hybrid joined | Depends on Windows version. [See these considerations](hybrid-join-plan). |

## Manage your devices

Once you've registered or joined your devices to Microsoft Entra ID, use the [Microsoft Entra admin center](https://entra.microsoft.com) as a central place to manage your device identities. The Microsoft Entra devices page enables you to:

- [Configure your device settings](manage-device-identities#configure-device-settings).
- You need to be a local administrator to manage Windows devices. [Microsoft Entra ID updates this membership for Microsoft Entra joined devices](assign-local-admin), automatically adding users with the device manager role as administrators to all joined devices.

Make sure that you keep the environment clean by [managing stale devices](manage-stale-devices), and focus your resources on managing current devices.

- [Review device-related audit logs](manage-device-identities#audit-logs)

### Supported device management tools

Administrators can secure and further control registered and joined devices using other device management tools. These tools provide you with a way to enforce configurations like requiring storage to be encrypted, password complexity, software installations, and software updates.

Review supported and unsupported platforms for integrated devices:

| Device management tools | Microsoft Entra registered | Microsoft Entra joined | Microsoft Entra hybrid joined |
| --- | --- | --- | --- |
| [Mobile Device Management (MDM)](/en-us/windows/client-management/azure-active-directory-integration-with-mdm)Example: Microsoft Intune | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| [Co-management with Microsoft Intune and Microsoft Configuration Manager](/en-us/mem/configmgr/comanage/overview)(Windows 10 or newer) |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) | ![Checkmark for these values.](media/plan-device-deployment/check.png) |
| [Group policy](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831791%28v=ws.11%29)(Windows only) |  |  | ![Checkmark for these values.](media/plan-device-deployment/check.png) |

We recommend that you consider [Microsoft Intune Mobile Application management (MAM)](/en-us/mem/intune/apps/app-management) with or without device management for registered iOS or Android devices.

Administrators can also [deploy virtual desktop infrastructure (VDI) platforms](howto-device-identity-virtual-desktop-infrastructure) hosting Windows operating systems in their organizations to streamline management and reduce costs through consolidation and centralization of resources.