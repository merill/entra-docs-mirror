---
layout: Conceptual
title: 'Tutorial: Add Shared Device Mode support to an Android device - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-android-device-shared-mode
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this tutorial, learn how to add Shared Device Mode support to an Android device using the Microsoft Authenticator App or Intune
manager: dougeby
ms.date: 2024-08-30T00:00:00.0000000Z
ms.subservice: workforce
ms.reviewer: akgoel
ms.topic: tutorial
locale: en-us
document_id: c3dd31c1-bf9f-f7b5-9f84-417d5fe956c2
document_version_independent_id: c3dd31c1-bf9f-f7b5-9f84-417d5fe956c2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-android-device-shared-mode.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-android-device-shared-mode
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-android-device-shared-mode.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 351a6111-0009-d74c-88ae-55e6ee1e1a66
---

# Tutorial: Add Shared Device Mode support to an Android device - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to add shared device mode support to an Android device with the Microsoft Authenticator App or a Mobile Device Management (MDM) tool like Microsoft Intune. Employees sign in once for single sign-on (SSO) to all SDM-supported apps and sign out to make the device ready for the next user with no access to previous data.

In this tutorial, you:

- Zero-touch set up via Microsoft Intune
- Supported third-party MDMs for zero-touch setup
- Manual setup with the Microsoft Authenticator app

## Prerequisites

- An Azure account with an active subscription. If you don't have one, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An Android device running Android OS version 8.0 or later. Ensure the device is wiped either by a factory reset or uninstalling all Microsoft and other SDM-enabled app.
- [Microsoft Authenticator app](https://play.google.com/store/apps/details/Microsoft_Authenticator?id=com.azure.authenticator&amp;hl=en_NZ) latest version installed on the device.
- For setup via MDM, the device should be managed by an MDM that supports shared device mode such as Microsoft Intune.

## Zero-touch setup via Intune

Microsoft Intune supports zero-touch provisioning for devices in Microsoft Entra shared device mode (SDM), which means that the device can be set up and enrolled in Intune with minimal interaction from the frontline worker.

To set up device in shared device mode when using Microsoft Intune as the MDM, first step is to enroll the shared device into Intune and install Authenticator app with SDM enabled. For more information on how to set up the SDM using Microsoft Intune, see [Set up Intune enrollment for Android Enterprise dedicated devices](/en-us/mem/intune/enrollment/android-kiosk-enroll)

Once enrolled, switch on the device to initiate standard Android device setup, which automatically triggers device registration with Microsoft Entra ID and get it ready for use.

## Supported third-party MDMs for zero-touch setup

The following third-party Mobile Device Management (MDM) tools support Microsoft Entra shared device mode

- [VMware Workspace ONE](https://docs.omnissa.com/bundle/UEMSharedDevicesVSaaS/page/UEMSharedDeviceConditionalAccess.html) - VMware supports Conditional Access capabilities but currently doesn’t support global sign-in and global sign-out with shared device mode.
- [SOTI MobiControl](https://soti.net/resources/blog/2023/soti-mobicontrol-supports-microsoft-shared-device-mode/)

Note

If your MDM doesn’t support setting the device in shared device mode, reach out to your MDM provider to request support for this feature. Additionally, you can manually put devices in shared device mode for testing if your MDM doesn’t support shared device mode.

## Manual setup with the Microsoft Authenticator app

To complete manual setup using the Microsoft Authenticator app, you require a cloud device administrator account. Follow these steps to complete the setup process:

1. Launch the Authenticator App and navigate to main account page where you can see the **Add Account** option, as shown:

    ![Screenshot of the Microsoft Authenticator app add account option.](media/tutorial-v2-shared-device-mode/authenticator-add-account.png)
2. Go to the **Settings** pane using the right-hand menu bar. Select **Device Registration** under **Work & School accounts**.

    ![Screenshot of the Microsoft Authenticator app settings.](media/tutorial-v2-shared-device-mode/authenticator-settings.png)
3. When you select **Device Registration**, you're asked to authorize access to device contacts. This is due to Android's account integration on the device. Choose **Allow**.

    ![Screenshot of the Microsoft Authenticator app allow access confirmation window.](media/tutorial-v2-shared-device-mode/authenticator-allow-screen.png)
4. Enter your organizational email under **Or register as a shared device**. Then select the **Register as shared device** button, and enter their credentials.

    ![Screenshot of the Microsoft Authenticator Device registration window in app.](media/tutorial-v2-shared-device-mode/register-device.png)

    ![Screenshot of the Microsoft sign-in page.](media/tutorial-v2-shared-device-mode/sign-in.png)
5. The device is now in shared mode.

    ![Screenshot of the Microsoft Authenticator app showing shared device mode enabled.](media/tutorial-v2-shared-device-mode/shared-device-mode-screen.png)

Any sign-in and sign-out instances on the device are global, and apply to all apps that are integrated with MSAL and Microsoft Authenticator on the device. You can now deploy applications to the device that use shared-device mode features.

## View the shared device

Once you set up a device in shared-mode, it becomes known to your organization and is tracked in your organizational tenant. You can view your shared devices by looking at the **Join Type**.

![Screenshot of Microsoft Entra window showing a shared device that's registered via zero-touch.](media/tutorial-v2-shared-device-mode/shared-device-mode-via-zero-touch-setup.png)