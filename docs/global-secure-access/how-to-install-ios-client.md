---
layout: Conceptual
title: Install the Global Secure Access Client for iOS - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-ios-client
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: The Global Secure Access client helps secure network traffic at the user device. This article describes how to download and install the iOS client.
ms.topic: how-to
ms.date: 2025-10-13T00:00:00.0000000Z
ms.reviewer: cagautham
ms.custom: sfi-image-nochange
locale: en-us
document_id: c9ddf414-4f0b-6876-487d-e562cecf8f8b
document_version_independent_id: c9ddf414-4f0b-6876-487d-e562cecf8f8b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-install-ios-client.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-install-ios-client
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-install-ios-client.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 1c59e821-870c-47fc-4f52-65fee14671d9
---

# Install the Global Secure Access Client for iOS - Global Secure Access | Microsoft Learn

This article explains how to set up and deploy the Global Secure Access client app on iOS and iPadOS devices. For simplicity, this article refers to both iOS and iPadOS as *iOS*.

The Global Secure Access client is deployed through Microsoft Defender for Endpoint on iOS. The Global Secure Access client on iOS uses a VPN that isn't a regular VPN. Instead, it's a local/self-looping VPN.

Caution

Running non-Microsoft endpoint protection products alongside Defender for Endpoint on iOS is likely to cause performance problems and unpredictable system errors.

## Prerequisites

- To use the Global Secure Access iOS client, configure the iOS endpoint device as a Microsoft Entra registered device.
- To enable Global Secure Access for your tenant, refer to the [licensing requirements](overview-what-is-global-secure-access#licensing-overview). If necessary, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).
- Onboard the tenant to Global Secure Access, and configure one or more traffic forwarding profiles. For more information, see [Access the Global Secure Access area of the Microsoft Entra admin center](quickstart-access-admin-center).
- To enable a Kerberos single sign-on (SSO) experience, create and deploy a profile for the iOS [SSO app extension](/en-us/intune/intune-service/configuration/ios-device-features-settings#single-sign-on-app-extension).

## Requirements

### Network requirements

For Microsoft Defender for Endpoint on iOS to function when it's connected to a network, you must configure the firewall/proxy to [enable access to Microsoft Defender for Endpoint service URLs](/en-us/defender-endpoint/configure-environment#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server). Microsoft Defender for Endpoint on iOS is available in the [Apple App Store](https://apps.apple.com/us/app/microsoft-defender-security/id1526737990).

Note

Microsoft Defender for Endpoint on iOS isn't supported on userless or shared devices.

### System requirements

The iOS device (phone or tablet) must meet the following requirements:

- The device runs iOS 16.0 or newer.
- The device has the Microsoft Authenticator app or the Intune Company Portal app.
- If the device is supervised, it must be enrolled to apply Intune device compliance policies.

## Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Installation steps

### Deploy on Device Administrator enrolled devices with Microsoft Intune

1. In the [Microsoft Intune admin center](https://intune.microsoft.com/#home), go to **Apps** &gt; **iOS/iPadOS** &gt; **Add** &gt; **iOS store app**. Then choose **Select**.

    ![Screenshot of the Microsoft Intune admin center with the steps to add an iOS store app highlighted.](media/how-to-install-ios-client/ios-client-add-ios-store-app.png)
2. On the **Add app** page, select **Search the App Store** and enter **Microsoft Defender** on the search bar.
3. In the search results, select **Microsoft Defender** and then choose **Select**.
4. Select **iOS 16.0** as the minimum operating system. Review the rest of the information about the app, and then select **Next**.
5. In the **Assignments** section, go to the **Required** section and select **Add group**.

    ![Screenshot of the Add App page with the option for adding a group highlighted.](media/how-to-install-ios-client/ios-client-add-group.png)
6. Choose the user groups to target with the Defender for Endpoint on iOS app.

    Note

    Selected user groups should consist of Microsoft Intune enrolled users.
7. Choose **Select**, and then select **Next**.
8. In the **Review + Create** section, verify that all the entered information is correct and then select **Create**. After a few moments, the Defender for Endpoint app is created successfully, and a notification appears at the upper-right corner of the page.
9. On the app information page, in the **Monitor** section, select **Device install status** to verify that the device installation finished successfully.

    ![Screenshot that shows a list of installed devices on the pane for device installation status.](media/how-to-install-ios-client/ios-client-device-install-status.png)

### Create a VPN profile and configure Global Secure Access for Microsoft Defender for Endpoint

1. In the [Microsoft Intune admin center](https://intune.microsoft.com/#home), go to **Devices** &gt; **Configuration** &gt; **Create** &gt; **New Policy**.
2. Set **Platform** to **iOS/iPadOS**, **Profile type** to **Templates**, and **Template name** to **VPN**.
3. Select **Create**.
4. Enter a name for the profile, and then select **Next**.
5. Set **Connection type** to **Custom VPN**.
6. In the **Base VPN** section, enter the following information:

    - **Connection name**: **Microsoft Defender for Endpoint**
    - **VPN server address**: **127.0.0.1**
    - **Authentication method**: **Username and password**
    - **Split tunneling**: **Disable**
    - **VPN identifier**: **com.microsoft.scmx**
7. In the boxes for key/value pairs:

    - Add the `EnableGSA` key and set the appropriate value from the following table:

        | Key | Value | Details |
        | --- | --- | --- |
        | `EnableGSA` | No value | Global Secure Access defaults to value 1 behavior. |
        |  | `0` | Global Secure Access isn't enabled and the tile isn't visible. |
        |  | `1` | Global Secure Access tile is visible and defaults to a disabled state. The user can enable or disable the tile by using the toggle. |
        |  | `2` | Global Secure Access tile is visible and defaults to an enabled state. The user can enable or disable the tile by using the toggle from the app. |
        |  | `3` | Global Secure Access tile is visible and defaults to an enabled state. The user *can't* disable Global Secure Access. |
    - Add the `SilentOnboard` key and set the value to `True`.
    - Add more key/value pairs as required (optional). If you add the `EnableGSAPrivateChannel` key, select one of the following values:

        | Key | Value | Details |
        | --- | --- | --- |
        | `EnableGSAPrivateChannel` | No value | Use the `EnableGSA` configured option. |
        |  | `0` | Private Access isn't enabled and the toggle option isn't visible to the user. |
        |  | `1` | The Private Access toggle is visible and defaults to a disabled state. The user can enable or disable it. |
        |  | `2` | The Private Access toggle is visible and defaults to an enabled state. The user can enable or disable it. |
        |  | `3` | The Private Access toggle is visible but unavailable, and it defaults to an enabled state. The user *can't* disable Private Access. |
8. For **Type of automatic VPN**, select **On-demand VPN**.
9. For **On-demand rules**, select **Add** and then:

    - Set **I want to do the following** to **Connect VPN**.
    - Set **I want to restrict** to **All domains**.

    ![Screenshot of example setup parameters in VPN configuration settings.](media/how-to-install-ios-client/ios-client-set-up-vpn.png)
10. To prevent users from disabling the VPN, set **Block users from disabling automatic VPN** to **Yes**. By default, this setting isn't configured, and users can disable the VPN only in the settings.
11. Select **Next** and assign the profile to targeted users.
12. In the **Review + Create** section, verify that all the information is correct and then select **Create**.

After the configuration is complete and synced with the device, the following actions take place on the targeted iOS devices:

- Microsoft Defender for Endpoint is deployed and silently onboarded.
- The device is listed in the Defender for Endpoint portal.
- A provisional notification is sent to the user device.
- Global Secure Access and other Microsoft Defender for Endpoint-configured features are activated.

## Confirm Global Secure Access appears in the Defender app

Because the Global Secure Access client for iOS is integrated with Microsoft Defender for Endpoint, it's helpful to understand the user experience. The client appears in the Defender dashboard after you onboard to Global Secure Access.

![Screenshot of the Microsoft Defender dashboard for iOS.](media/how-to-install-ios-client/ios-defender-dashboard-1.png)

You can enable or disable the Global Secure Access client for iOS by setting the `EnableGSA` key in the VPN profile. Users can enable or disable individual services or the client itself based on the configuration settings, by using the appropriate toggles.

![Screenshot of the Global Secure Access client on iOS that shows both the Active and Not Connected status screens.](media/how-to-install-ios-client/ios-client-enabled-disabled-1.png)

## Troubleshooting

If the Global Secure Access tile doesn't appear in the Defender app after you onboard the tenant, reopen the Defender app.

If access to the Private Access application shows a connection timeout error after a successful interactive sign-in, reload the application (or refresh the web browser).