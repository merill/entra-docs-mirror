---
layout: Conceptual
title: Install the Global Secure Access Client for Android - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-android-client
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: The Global Secure Access client helps secure network traffic at the user device. This article describes how to download and install the Android client.
ms.topic: how-to
ms.date: 2026-02-21T00:00:00.0000000Z
ms.reviewer: cagautham
ms.custom: sfi-image-nochange
locale: en-us
document_id: f85eb9f8-ef23-346f-a379-ef98d373f4d2
document_version_independent_id: f85eb9f8-ef23-346f-a379-ef98d373f4d2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-install-android-client.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-install-android-client
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-install-android-client.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: edf80820-4388-7f03-783b-35e0795f9e18
---

# Install the Global Secure Access Client for Android - Global Secure Access | Microsoft Learn

This article describes how to deploy the Global Secure Access client to Android devices by using Microsoft Intune and Microsoft Defender for Endpoint on Android. The Android client is built into the Defender for Endpoint Android app, which streamlines how users connect to Global Secure Access. The Global Secure Access Android client makes it easier for your users to connect to the resources that they need without having to manually configure VPN settings on their devices.

## Prerequisites

- The product requires licensing. For details, see the licensing section of [What is Global Secure Access?](overview-what-is-global-secure-access). If necessary, [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).
- Enable at least one Global Secure Access [traffic forwarding profile](concept-traffic-forwarding).
- You need device installation permissions to install the client.
- Android devices need to run Android 11.0 or later.
- Android devices need to be Microsoft Entra registered devices:

    - Devices that your organization doesn't manage need to have the Microsoft Authenticator app installed.
    - Devices not managed through Intune need to have the Company Portal app installed.
    - Device enrollment is required to enforce Intune device compliance policies.
- To enable a Kerberos single sign-on (SSO) experience, install and configure a non-Microsoft SSO client.

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Supported scenarios

The Global Secure Access client for Android supports deployment in these Android Enterprise scenarios:

- Corporate-owned, fully managed user devices
- Corporate-owned devices with a work profile
- Personal devices with a work profile

### Non-Microsoft mobile device management

The Global Secure Access client also supports non-Microsoft mobile device management (MDM) scenarios. These scenarios, known as *Global Secure Access only mode*, require enabling a traffic forwarding profile and configuring the app based on the vendor documentation.

When you're configuring through a non-Microsoft MDM solution, use the following key/value pairs in the managed app configuration:

| Configuration key | Value | Details |
| --- | --- | --- |
| `Global Secure Access` | `1`–`3` | Required. Controls whether Global Secure Access is enabled in the Defender app. For detailed value descriptions, see the table later in this article. |
| `GlobalSecureAccessPrivateChannel` | `0`–`3` | Optional. Controls the Private Access channel. For detailed value descriptions, see the table later in this article. |

## Deploy Microsoft Defender for Endpoint on Android

To deploy Microsoft Defender for Endpoint on Android, create an MDM profile and configure Global Secure Access:

1. In the [Microsoft Intune admin center](https://intune.microsoft.com/#home), go to **Apps** &gt; **Android** &gt; **Manage Apps** &gt; **Configuration**.
2. Select **+ Create**, and then select **Managed devices**. The **Create app configuration policy** form opens.
3. On the **Basics** tab:

    1. Enter a **Name** value.
    2. Set **Platform** to **Android Enterprise**.
    3. Set **Profile Type** to **Fully Managed, Dedicated, and Corporate-Owned Work Profile Only**.
    4. Set **Targeted app** to **Microsoft Defender**.

    [![Screenshot of the Basics tab in the pane for creating an app configuration policy.](media/how-to-install-android-client/create-policy-basics.png)](media/how-to-install-android-client/create-policy-basics-expanded.png#lightbox)
4. Select **Next**.
5. On the **Settings** tab:

    1. Set **Configuration settings format** to **Use configuration designer**.
    2. Select the **+ Add** button.
    3. In the search box, type **global** and select the Global Secure Access configuration keys listed in the following table.
    4. Set the appropriate values for each configuration key according to the following table.

    Note

    The Android configuration keys differ from the iOS client keys. On Android, use `Global Secure Access` and `GlobalSecureAccessPrivateChannel` as shown here. Don't use the iOS key names (`EnableGSA`, `EnableGSAPrivateChannel`).

    The `GlobalSecureAccessPA` configuration key is no longer supported.

    | Configuration key | Value | Details |
    | --- | --- | --- |
    | `Global Secure Access` | No value | Global Secure Access defaults to value 1 behavior. |
    |  | `0` | Global Secure Access isn't enabled and the tile isn't visible. |
    |  | `1` | The tile is visible and defaults to `false` (disabled state). The user can enable or disable Global Secure Access by using the toggle in the app. |
    |  | `2` | The tile is visible and defaults to `true` (enabled state). The user can override Global Secure Access. The user can enable or disable Global Secure Access by using the toggle in the app. |
    |  | `3` | The tile is visible and defaults to `true` (enabled state). The user *can't* disable Global Secure Access. |
    | `GlobalSecureAccessPrivateChannel` | No value | Global Secure Access defaults to value `2` behavior. |
    |  | `0` | Private Access isn't enabled and the toggle option isn't visible to the user. |
    |  | `1` | The Private Access toggle is visible and defaults to the disabled state. The user can enable or disable Private Access. |
    |  | `2` | The Private Access toggle is visible and defaults to the enabled state. The user can enable or disable Private Access. |
    |  | `3` | The Private Access toggle is visible but unavailable, and it defaults to the enabled state. The user *can't* disable Private Access. |

    [![Screenshot of the Settings tab in the pane for creating an app configuration policy.](media/how-to-install-android-client/create-policy-settings.png)](media/how-to-install-android-client/create-policy-settings-expanded.png#lightbox)
6. Select **Next**.
7. On the **Scope tags** tab, configure scope tags as needed and then select **Next**.
8. On the **Assignments** tab, select **+ Add groups** to assign the configuration policy and enable Global Secure Access.

    [![Screenshot of the Assignments tab in the pane for creating an app configuration policy.](media/how-to-install-android-client/create-policy-assignments.png)](media/how-to-install-android-client/create-policy-assignments-expanded.png#lightbox)

    Tip

    To enable the policy for all but a few specific users, select **Add all devices** in the **Included groups** section. Then, add the users or groups to exclude in the **Excluded groups** section.
9. Select **Next**.
10. Review the configuration summary, and then select **Create**.

## Confirm Global Secure Access appears in the Defender app

Because the Android client is integrated with Defender for Endpoint, it's helpful to understand the user experience. The client appears in the Defender dashboard after you onboard to Global Secure Access. Onboarding happens by enabling a traffic forwarding profile.

![Screenshot of the Global Secure Access tile on the dashboard of the Defender app.](media/how-to-install-android-client/defender-endpoint-dashboard.png)

*The client is disabled by default when it's deployed to user devices.* Users need to enable the client from the Defender app. To enable the client, tap the toggle.

![Screenshot of the Global Secure Access client in a disabled state.](media/how-to-install-android-client/defender-global-secure-access-disabled.png)

To view client details, tap the tile on the dashboard. When the client is enabled and working properly, the dashboard displays an "Enabled" message. It also shows the date and time when the client connected to Global Secure Access.

![Screenshot of the Global Secure Access client in an enabled state.](media/how-to-install-android-client/defender-global-secure-access-enabled.png)

If the client can't connect, a toggle appears to disable the service. Users can return later to enable the client.

![Screenshot of a Global Secure Access client that's unable to connect.](media/how-to-install-android-client/defender-global-secure-access-unable.png)

## Troubleshooting

If the Global Secure Access tile doesn't appear after you onboard the tenant to the service, restart the Defender app.

When you try to access a Private Access application, the connection might time out after a successful interactive sign-in. Reload the application by refreshing the web browser.