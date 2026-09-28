---
layout: Conceptual
title: Install the Global Secure Access Client for macOS - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-macos-client
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: The Global Secure Access client helps secure network traffic at the user device. This article describes how to download and install the macOS client.
ms.topic: how-to
ms.date: 2026-08-21T00:00:00.0000000Z
ms.reviewer: lirazbarak
ms.custom: sfi-image-nochange, msecd-doc-authoring-1024
locale: en-us
document_id: 3ab84be9-c912-e2f5-b1b9-24edcd37d6ed
document_version_independent_id: 3ab84be9-c912-e2f5-b1b9-24edcd37d6ed
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-install-macos-client.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-install-macos-client
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-install-macos-client.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: f102e68d-cabe-3e7c-b121-25d3e44ffdab
---

# Install the Global Secure Access Client for macOS - Global Secure Access | Microsoft Learn

The Global Secure Access client, an essential component of Global Secure Access, helps organizations manage and secure network traffic on user devices. The client's main role is to route traffic that needs to be secured by Global Secure Access to the cloud service. All other traffic goes directly to the network. The [forwarding profiles](concept-traffic-forwarding) that you configure in the portal determine which traffic the Global Secure Access client routes to the cloud service.

This article describes how to download and install the Global Secure Access client for macOS.

## Prerequisites

- A Mac device with an Intel, M1, M2, M3, or M4 processor running macOS version 14 or later.
- A device registered to a Microsoft Entra tenant through the Company Portal app.
- A Microsoft Entra tenant onboarded to Global Secure Access.
- An internet connection.
- For a single sign-on (SSO) experience based on the user signed in to the Company Portal app, deployment of the [Microsoft Enterprise SSO plug-in for Apple devices](../identity-platform/apple-sso-plugin).

## Download the client

You can download the most current version of the Global Secure Access client from the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Client download**.
3. Select the **macOS** tab.
4. Select **Download Client**.

![Screenshot of the pane for client downloads. The Download Client button is highlighted.](media/how-to-install-macos-client/macos-client-download-screen.png)

## Install the client

### Automated installation

Use the following command for silent installation. *Substitute your file path according to the download location of the .pkg file.*

`sudo installer -pkg ~/Downloads/GlobalSecureAccessClient.pkg -target / -verboseR`

The client uses system extensions and a transparent application proxy that you need to approve during the installation. For a silent deployment without prompting the user to allow these components, deploy a policy to automatically approve the components by using mobile device management (MDM).

### Deploy by using Microsoft Intune

To deploy the Global Secure Access client's .pkg file through Microsoft Intune as a managed app:

Important

Beginning with version **1.1.26060207**, the app package includes the `com.microsoft.autoupdate2` application to support future use cases. If `com.microsoft.autoupdate2` is already installed, including it in the Intune detection rules might cause a conflict. You can optionally remove `com.microsoft.autoupdate2` from the detection rules when deploying the app.

1. Download the `GlobalSecureAccessClient.pkg` file from the Microsoft Entra admin center.
2. In the [Microsoft Intune admin center](https://intune.microsoft.com), select **Apps** &gt; **All Apps** &gt; **Create**.
3. In the **Select app type** pane, under **Other** app types, select **macOS app (PKG)**. Then choose **Select**.
4. On the **App package file** tab, select **Select app package file**. Browse to the `GlobalSecureAccessClient.pkg` file, and then select **OK**.
5. On the **App information** tab, fill in the required details and then select **Next**.
6. On the **Requirements** tab, set the minimum operating system to **macOS 14.0** and then select **Next**.
7. On the **Detection rules** tab, review the **Included apps** list to verify that the Global Secure Access client app is detected correctly. Optionally, remove the `com.microsoft.autoupdate2` app from the list. Then select **Next**.
8. On the **Assignments** tab, assign the app to the appropriate device or user groups. Then select **Next**.
9. Review the configuration, and then select **Create**.

### Allow system extensions through mobile device management

Important

Previous versions of these instructions referenced the deprecated **Extensions** profile type. If your organization previously deployed system extensions by using the **Extensions** profile, migrate to the **Allowed System Extensions** setting in **Settings catalog** as described in the following steps.

The following instructions are for [Microsoft Intune](/en-us/mem/intune/apps/apps-win32-app-management). You can adapt them for different MDM solutions.

1. In the Microsoft Intune admin center, select **Devices** &gt; **Manage devices** &gt; **Configuration** &gt; **Policies** &gt; **Create** &gt; **New policy**.
2. Create a profile with **Platform** set to **macOS** and **Profile type** set to **Settings catalog**. Then select **Create**.

    ![Screenshot of the form for creating a profile, with the platform and profile type highlighted.](media/how-to-install-macos-client/macos-client-create-profile.png)
3. On the **Basics** tab, enter a name for the new profile, and then select **Next**.
4. On the **Configuration settings** tab, select **+ Add settings**.
5. In **Settings picker**, expand the **System Configuration** category and select **System Extensions**.
6. In the **System Extensions** subcategory, select **Allowed System Extensions**.

    ![Screenshot of the settings picker with the category and subcategory selections highlighted.](media/how-to-install-macos-client/macos-settings-picker.png)
7. Close **Settings picker**.
8. In the **Allowed System Extensions** list, select **+ Edit instance**.
9. In the **Configure instance** dialog, configure the **System Extensions** payload settings with the following entries:

    | Bundle identifier | Team identifier |
    | --- | --- |
    | `com.microsoft.globalsecureaccess.tunnel` | `UBF8T346G9` |
    | `com.microsoft.globalsecureaccess` | `UBF8T346G9` |
10. Select **Save** &gt; **Next**.
11. On the **Scope tags** tab, add tags as appropriate.
12. On the **Assignments** tab, assign the profile to a group of macOS devices or users.
13. On the **Review + create** tab, review the configuration and then select **Create**.

### Allow a transparent application proxy through MDM

The following instructions are for [Microsoft Intune](/en-us/mem/intune/apps/apps-win32-app-management). You can adapt them for different MDM solutions.

1. In the Microsoft Intune admin center, select **Devices** &gt; **Manage devices** &gt; **Configuration** &gt; **Policies** &gt; **Create** &gt; **New policy**.
2. Create a profile for the macOS platform based on a template of type **Custom**, and then select **Create**.

    ![Screenshot of the form for creating a profile with the platform, profile type, and template type highlighted.](media/how-to-install-macos-client/macos-client-create-profile-custom.png)
3. On the **Basics** tab, enter a **Name** value for the profile.
4. On the **Configuration settings** tab, enter a **Custom configuration profile name** value.
5. Keep **Deployment channel** set to **Device channel**.
6. Upload an .xml file that contains the following data:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
      <dict>
        <key>PayloadUUID</key>
        <string>87cbb424-6af7-4748-9d43-f1c5dda7a0a6</string>
        <key>PayloadType</key>
        <string>Configuration</string>
        <key>PayloadOrganization</key>
        <string>Microsoft Corporation</string>
        <key>PayloadIdentifier</key>
        <string>com.microsoft.globalsecureaccess</string>
        <key>PayloadDisplayName</key>
        <string>Global Secure Access Proxy Configuration</string>
        <key>PayloadDescription</key>
        <string>Add Global Secure Access Proxy Configuration</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadEnabled</key>
        <true/>
        <key>PayloadRemovalDisallowed</key>
        <true/>
        <key>PayloadScope</key>
        <string>System</string>
        <key>PayloadContent</key>
        <array>
          <dict>
            <key>PayloadUUID</key>
            <string>04e13063-2bb8-4b72-b1ed-45290f91af68</string>
            <key>PayloadType</key>
            <string>com.apple.vpn.managed</string>
            <key>PayloadOrganization</key>
            <string>Microsoft Corporation</string>
            <key>PayloadIdentifier</key>
            <string>com.microsoft.globalsecureaccess</string>
            <key>PayloadDisplayName</key>
            <string>Global Secure Access Proxy Configuration</string>
            <key>PayloadDescription</key>
            <string/>
            <key>PayloadVersion</key>
            <integer>1</integer>
            <key>TransparentProxy</key>
            <dict>
              <key>AuthenticationMethod</key>
              <string>Password</string>
              <key>Order</key>
              <integer>1</integer>
              <key>ProviderBundleIdentifier</key>
              <string>com.microsoft.globalsecureaccess.tunnel</string>
              <key>ProviderDesignatedRequirement</key>
              <string>identifier "com.microsoft.globalsecureaccess.tunnel" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = UBF8T346G9</string>
              <key>ProviderType</key>
              <string>app-proxy</string>
              <key>RemoteAddress</key>
              <string>100.64.0.0</string>
            </dict>
            <key>UserDefinedName</key>
            <string>Global Secure Access Proxy Configuration</string>
            <key>VPNSubType</key>
            <string>com.microsoft.globalsecureaccess</string>
            <key>VPNType</key>
            <string>TransparentProxy</string>
          </dict>
        </array>
      </dict>
    </plist>
    ```
7. Complete the creation of the profile by assigning users and devices according to your needs.

### Manually install the client

1. Run the `GlobalSecureAccessClient.pkg` setup file. The **Install** wizard starts. Follow the prompts.
2. In the **Introduction** step, select **Continue**.
3. In the **License** step, select **Continue**, and then select **Agree** to accept the license agreement.

    ![Screenshot of the License step of the Install wizard, showing the software license agreement dialog.](media/how-to-install-macos-client/macos-install-license-agreement.png)
4. In the **Installation** step, select **Install**.
5. In the **Summary** step, when the installation is complete, select **Close**.
6. Allow the Global Secure Access system extension:

    1. In the **System Extension Blocked** dialog, select **Open System Settings**.

        ![Screenshot of the System Extension Blocked dialog with Open System Settings highlighted.](media/how-to-install-macos-client/macos-client-open-system-settings.png)
    2. Allow the Global Secure Access client's system extension by selecting **Allow**.

        ![Screenshot of the system settings, open to the options for privacy and security, showing a blocked application message with the Allow button highlighted.](media/how-to-install-macos-client/macos-allow-blocked-application.png)
    3. In the **Privacy & Security** dialog, enter your username and password to validate the approval of the system extension. Then select **Modify Settings**.

        ![Screenshot of the Privacy &amp; Security dialog requesting sign-in credentials, with the Modify Settings button highlighted.](media/how-to-install-macos-client/macos-client-credentials.png)
    4. Complete the process by selecting **Allow** to enable the Global Secure Access client to add proxy configurations.

        ![Screenshot of the dialog that says the Global Secure Access client would like to add proxy configurations, with the Allow button highlighted.](media/how-to-install-macos-client/macos-add-proxy.png)
7. After the installation is complete, you might be prompted to sign in to Microsoft Entra.

    Note

    If the [Microsoft Enterprise SSO plug-in for Apple devices](../identity-platform/apple-sso-plugin) is deployed, the default behavior is to use SSO with the credentials entered in the Company Portal app.
8. Verify that the **Global Secure Access - Connected** icon appears in the system tray. It indicates a successful connection to Global Secure Access.

    ![Screenshot of the system tray with the icon for connectivity to Global Secure Access highlighted.](media/how-to-install-macos-client/macos-client-system-tray-icon-connected.png)

## Upgrade the client

The client installer supports upgrades. You can use the installation wizard to install a new version on a device that's currently running a previous client version.

For a silent upgrade, run the following command. *Substitute your file path according to the download location of the .pkg file.*

`sudo installer -pkg ~/Downloads/GlobalSecureAccessClient.pkg -target / -verboseR`

## Uninstall the client

To manually uninstall the Global Secure Access client, use either of the following methods:

- Run the **Uninstall Global Secure Access Client** application.
- Run the following command: `sudo /Applications/GlobalSecureAccessClient/Global\ Secure\ Access\ Client.app/Contents/Resources/install_scripts/uninstall`.

If you're using an MDM solution, uninstall the client with the MDM solution.

## Client actions

To view the available client menu actions, right-click the Global Secure Access icon in the system tray.

![Screenshot that shows the list of Global Secure Access client actions.](media/how-to-install-macos-client/macos-client-actions.png)

| Action | Description |
| --- | --- |
| **Disable** | Disables the client until you enable it again. When you disable the client, you're prompted to enter a business justification and reenter your sign-in credentials. The business justification is logged. |
| **Enable** | Enables the client. |
| **Pause** | Pauses the client for 10 minutes, until you resume the client, or until the device is restarted. When you pause the client, you're prompted to enter a business justification and reenter your sign-in credentials. The business justification is logged. |
| **Resume** | Resumes the paused client. |
| **Restart** | Restarts the client. |
| **Collect Logs** | Collects client logs and archives them in a .zip file to share with Microsoft Support for investigation. |
| **Settings** | Opens the **Settings and Advanced diagnostics** tool. |
| **About** | Shows information about the product's version. |

### Client statuses in the system tray

| Icon | Message | Description |
| --- | --- | --- |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-initializing.png) | Global Secure Access Client | The client is initializing and checking its connection to Global Secure Access. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-connected.png) | Global Secure Access Client - Connected | The client is connected to Global Secure Access. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-disabled.png) | Global Secure Access Client - Disabled | The client is disabled because services are offline or you disabled the client. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-disconnected.png) | Global Secure Access Client - Disconnected | The client failed to connect to Global Secure Access. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-warning.png) | Global Secure Access Client - Some channels are unreachable | The client is partially connected to Global Secure Access. That is, the connection to at least one channel failed: Microsoft Entra, Microsoft 365, Private Access, Internet Access. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-warning.png) | Global Secure Access Client - Disabled by your organization | Your organization disabled the client. That is, all traffic forwarding profiles are disabled. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-warning.png) | Global Secure Access - Private Access is disabled | You disabled Private Access on this device. |
| ![](media/how-to-install-macos-client/global-secure-access-client-icon-warning.png) | Global Secure Access - could not connect to the Internet | The client couldn't detect an internet connection. The device is either connected to a network that doesn't have an internet connection or connected to a network that requires captive portal sign-in. |

## Settings and troubleshooting

In the **Settings** window, you can set configurations and perform some advanced actions. The **Settings** window has two tabs.

### Settings tab

| Option | Description |
| --- | --- |
| **Telemetry full diagnostics** | Sends full diagnostic data to Microsoft for application improvement. |
| **Enable Verbose Logging** | Enables verbose logging and network capture to be collected when you're exporting the logs to a .zip file. |

![Screenshot of the macOS Settings tab.](media/how-to-install-macos-client/macos-client-settings-toggles.png)

### Troubleshooting tab

| Action | Description |
| --- | --- |
| **Get Latest Policy** | Downloads and applies the latest forwarding profile for your organization. |
| **Clear cached data** | Deletes the client's internal cached data related to authentication, forwarding profile, FQDNs, and IPs. |
| **Export Logs** | Exports client-related logs and configuration files to a .zip file. |
| **Advanced Diagnostics Tool** | Opens an advanced tool to monitor and troubleshoot the client's behavior. |

![Screenshot of the macOS Troubleshooting tab.](media/how-to-install-macos-client/macos-client-troubleshooting-toggles.png)

### Hide or unhide menu buttons in the system tray

The administrator can show or hide specific buttons on the icon menu in the client's system tray by deploying the values in the following table.

| Value | Type | Data | Default behavior | Description |
| --- | --- | --- | --- | --- |
| `HideDisablePrivateAccessButton` | Boolean | `false` = shown `true` = hidden | Hidden | Set this value to show or hide the **Disable Private Access** button. This option is for a scenario when the device is directly connected to the corporate network and the user prefers to access private applications directly through the network instead of through Global Secure Access. |
| `HideDisableButton` | Boolean | `false` = shown `true` = hidden | Shown | Set this value to show or hide the **Disable** action. When the action is visible, the user can disable the Global Secure Access client. The client stays disabled until the user enables it again or restarts the device. |
| `HidePauseButton` | Boolean | `false` = shown `true` = hidden | Shown | Set this value to show or hide the **Pause** action. When the action is visible, the user can pause the Global Secure Access client. The client pauses for 10 minutes or until the user enables it again. |
| `HideQuitButton` | Boolean | `false` = shown `true` = hidden | Hidden | Set this value to show or hide the **Quit** action. When the action is visible, the user can quit the Global Secure Access client, which closes the client application. To open it again, run the Global Secure Access application from Finder. |

You can also configure the icon menu in the client's system tray by using Microsoft Intune:

1. Follow the instructions to [create the profile](/en-us/intune/intune-service/configuration/preference-file-settings-macos#create-the-profile).
2. For **Preference domain name**, enter `com.microsoft.globalsecureaccess`.
3. For **Property list file**, upload an XML file similar to the following sample. Revise the XML to match your preferences.

    ```xml
    <key>HidePauseButton</key>
    <false/>
    <key>HideDisableButton</key>
    <false/>
    <key>HideQuitButton</key>
    <true/>
    <key>HideDisablePrivateAccessButton</key>
    <true/>
    ```

![Screenshot of the configuration step in the Microsoft Intune admin center, showing sample XML code.](media/how-to-install-macos-client/intune-xml-sample.png)

## Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).