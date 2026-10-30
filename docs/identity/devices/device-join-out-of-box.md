---
layout: Conceptual
title: Join Windows 11 Devices to Microsoft Entra ID During OOBE - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/device-join-out-of-box
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Discover how to set up Microsoft Entra join on a Windows 11 device during OOBE, ensuring seamless integration with your organization's directory.
ms.topic: tutorial
ms.date: 2026-01-08T00:00:00.0000000Z
ms.reviewer: 
locale: en-us
document_id: 7a7a5351-21c0-946d-fdc0-5e1943aa0a01
document_version_independent_id: acf0eb8d-109f-c3b4-b862-adb61ae8fdc7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/device-join-out-of-box.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/device-join-out-of-box
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/device-join-out-of-box.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ec6774-09b8-473e-a17e-b17b518bbad7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ade36b61-c646-4bd8-87ee-f3a843461962
platformId: d20820dc-c927-c69a-b704-238bb1baebd2
---

# Join Windows 11 Devices to Microsoft Entra ID During OOBE - Microsoft Entra ID | Microsoft Learn

This tutorial shows you how to join a new Windows 11 device to Microsoft Entra ID during the out-of-box experience (OOBE). When you join a device during OOBE, the device becomes part of your organization's directory and can be managed according to their policies.

This functionality pairs well with mobile device management platforms like [Microsoft Intune](/en-us/mem/intune/fundamentals/what-is-intune) and tools like [Windows Autopilot](/en-us/mem/autopilot/windows-autopilot) to ensure devices are configured according to your standards.

## Prerequisites

To Microsoft Entra join a Windows device, the device registration service must be configured to enable you to register devices. For more information about prerequisites, see the article [How to: Plan your Microsoft Entra join implementation](device-join-plan).

Tip

Windows Home Editions do not support Microsoft Entra join. These editions can still access many of the benefits by using [Microsoft Entra registration](concept-device-registration).

For information about how to complete Microsoft Entra registration on a Windows device, see the support article [Register your personal device on your work or school network](https://support.microsoft.com/account-billing/register-your-personal-device-on-your-work-or-school-network-8803dd61-a613-45e3-ae6c-bd1ab25bf8a8).

## Join a new Windows 11 device to Microsoft Entra ID

Your device might restart several times as part of the setup process. Your device must be connected to the Internet to complete Microsoft Entra join.

1. Turn on your new device and start the setup process. Follow the prompts to set up your device.
2. When prompted **How would you like to set up this device?**, select **Set up for work or school**. ![Screenshot of Windows 11 out-of-box experience showing the option to set up for work or school.](media/device-join-out-of-box/windows-11-first-run-experience-work-or-school.png)
3. On the **Let's set things up for your work or school** page, provide the credentials that your organization provided. These credentials might include a username and password, or a method like a [passkey](/en-us/entra/identity/authentication/how-to-authentication-synced-passkeys). Your users should be able to use the credential that they have to sign in to Microsoft Entra ID, including [passkeys](/en-us/entra/identity/authentication/how-to-authentication-synced-passkeys), as shown in the following animation.

    ![Animation of how to sign in to Windows 11 out of box by using a passkey.](media/device-join-out-of-box/passkey-sign-in.gif)
4. Continue to follow the prompts to set up your device.
5. Microsoft Entra ID checks if an enrollment in mobile device management is required and starts the process.

    1. Windows registers the device in the organization's directory and enrolls it in mobile device management, if applicable.
6. If you sign in with a managed user account, Windows takes you to the desktop through the automatic sign-in process. Federated users are directed to the Windows sign-in screen to enter your credentials. ![Screenshot of Windows 11 at the desktop after first run experience Microsoft Entra joined.](media/device-join-out-of-box/windows-11-first-run-experience-complete-automatic-sign-in-desktop.png)

For more information about the out-of-box experience, see the support article [Join your work device to your work or school network](https://support.microsoft.com/account-billing/join-your-work-device-to-your-work-or-school-network-ef4d6adb-5095-4e51-829e-5457430f3973).

## Verification

To verify whether a device is joined to your Microsoft Entra ID, review the **Access work or school** dialog on your Windows device found in **Settings** &gt; **Accounts**. The dialog should indicate that you're connected to Microsoft Entra ID, and provides information about areas managed by your IT staff.

![Screenshot of Windows 11 Settings app showing current connection.](media/device-join-out-of-box/windows-11-access-work-or-school.png)