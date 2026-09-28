---
layout: Conceptual
title: Configure Workday Mobile Application for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/workday-mobile-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and Workday Mobile Application.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fc88e998-f267-60d8-7f32-137564b72a82
document_version_independent_id: 6cdd9828-2bf7-4e49-4fa6-4399adb581ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/workday-mobile-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/workday-mobile-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/workday-mobile-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4e691972-5c0c-1f56-d528-436caba6694d
---

# Configure Workday Mobile Application for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you’ll learn how to integrate Microsoft Entra ID, Conditional Access, and Intune with Workday Mobile Application. When you integrate Workday Mobile Application with Microsoft, you can:

- Ensure that devices are compliant with your policies prior to sign-in.
- Add controls to Workday Mobile Application to ensure that users are securely accessing corporate data.
- Control in Microsoft Entra ID who has access to Workday.
- Enable your users to be automatically signed in to Workday with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started:

- Integrate Workday with Microsoft Entra ID.
- Read [Microsoft Entra single sign-on (SSO) integration with Workday](workday-tutorial).

## Scenario description

In this article, you configure and test Microsoft Entra Conditional Access policies and Intune with Workday Mobile Application.

For enabling single sign-on (SSO), you can configure Workday Federated application with Microsoft Entra ID. For more information, see [Microsoft Entra single sign-on (SSO) integration with Workday](workday-tutorial).

Note

Workday doesn't support the app protection policies of Intune. You must use mobile device management to use Conditional Access.

## Ensure users have access to Workday Mobile Application

Configure Workday to allow access to their mobile apps. You need to configure the following policies for Workday Mobile:

1. Access the domain security policies for functional area report.
2. Select the appropriate security policy:
    - Mobile Usage - Android
    - Mobile Usage - iPad
    - Mobile Usage - iPhone
3. Select **Edit Permissions**.
4. Select the **View or Modify** check box to grant the security groups access to the report or task securable items.
5. Select the **Get or Put** check box to grant the security groups access to integration and report or task securable actions.

Activate pending security policy changes by running **Activate Pending Security Policy Changes**.

## Open Workday sign-in page in Workday Mobile Browser

To apply Conditional Access to Workday Mobile Application, you must open the app in an external browser. In **Edit Tenant Setup - Security**, select **Enable Mobile Browser SSO for Native Apps**. This requires a browser approved by Intune to be installed on the device for iOS, and in the work profile for Android.

![Screenshot of Workday Mobile Browser sign-in.](media/workday-tutorial/mobile-browser.png)

## Set up Conditional Access policy

This policy only affects signing in on an iOS or Android device. If you want to extend it to all platforms, select **Any Device**. This policy requires the device to be compliant with the policy, and verifies this via Intune. Because Android has work profiles, this blocks any users from signing into Workday, unless they're signing in through their work profile and have installed the app through the Intune company portal. There's one additional step for iOS to make sure that the same situation applies.

Workday supports the following access controls:

- Require multifactor authentication
- Require device to be marked as compliant

Workday App doesn't support the following:

- Require approved client app
- Require app protection policy (preview)

To set up Workday as a managed device, perform the following steps:

![Screenshot of Managed Devices Only and Cloud apps or actions.](media/workday-tutorial/managed-devices-only.png)

1. Select **Home** &gt; **Microsoft Intune** &gt; **Conditional Access-Policies**. Then select **Managed Devices Only**.
2. In **Managed Devices Only**, under **Name**, select **Managed Devices Only** and then select **Cloud apps or actions**.
3. In **Cloud apps or actions**:

    1. Switch **Select what this policy applies to** to **Cloud apps**.
    2. In **Include**, choose **Select resources**.
    3. From the **Select** list, choose **Workday**.
    4. Select **Done**.
4. Switch **Enable policy** to **On**.
5. Select **Save**.

For **Grant** access, perform the following steps:

1. Select **Home** &gt; **Microsoft Intune** &gt; **Conditional Access-Policies**. Then select **Managed Devices Only**.
2. In the **Managed Devices Only**, under **Name**, select **Managed Devices Only**. Under **Access controls**, select **Grant**.
3. In **Grant**:

    1. Select the controls to be enforced as **Grant access**.
    2. Select **Require device to be marked as compliant**.
    3. Select **Require one of the selected controls**.
    4. Choose **Select**.
4. Switch **Enable policy** to **On**.
5. Select **Save**.

## Set up device compliance policy

To ensure that iOS devices are only able to sign in through Workday managed by mobile device management, you must block the App Store app by adding **com.workday.workdayapp** to the list of restricted apps. This ensures that only devices that have Workday installed through the company portal can access Workday. For the browser, devices are only able to access Workday if the device is managed by Intune and is using a managed browser.

![Screenshot of iOS device compliance policy.](media/workday-tutorial/ios-policy.png)

## Set up Intune app configuration policies

| Scenario | Key value pairs |
| --- | --- |
| Automatically populate the Tenant and Web Address fields for:● Workday on Android when you enable Android for work profiles.● Workday on iPad and iPhone. | Use these values to configure your Tenant: ● Configuration Key = `UserGroupCode`● Value Type = String ● Configuration Value = Your tenant name. Example: `gms`Use these values to configure your Web Address:● Configuration Key = `AppServiceHost`● Value Type = String● Configuration Value = The base URL for your tenant. Example: `https://www.myworkday.com` |
| Disable these actions for Workday on iPad and iPhone:● Cut, Copy, and Paste● Print | Set the value (Boolean) to `False` on these keys to disable the functionality:● `AllowCutCopyPaste`● `AllowPrint` |
| Disable screenshots for Workday on Android. | Set the value (Boolean) to `False` on the `AllowScreenshots` key to disable functionality. |
| Disable suggested updates for your users. | Set the value (Boolean) to `False` on the `AllowSuggestedUpdates` key to disable functionality. |
| Customize the app store URL to direct mobile users to the app store of your choice. | Use these values to change the app store URL:● Configuration Key = `AppUpdateURL`● Value Type = String ● Configuration Value = App store URL |

## iOS configuration policies

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for **Intune** or select the widget from the list.
3. Go to **Client Apps** &gt; **Apps** &gt; **App Configuration Policies**. Then select **+ Add** &gt; **Managed Devices**.
4. Enter a name.
5. Under **Platform**, choose **iOS/iPadOS**.
6. Under **Associated App**, choose the Workday for iOS app that you added.
7. Select **Configuration Settings**. Under **Configuration settings format**, select **Enter XML Data**.
8. Here's an example XML file. Add the configurations you want to apply. Replace `STRING_VALUE` with the string you want to use. Replace `<true /> or <false />` with `<true />` or `<false />`. If you don't add a configuration, this example functions like it's set to `True`.

    ```
    <dict>
    <key>UserGroupCode</key>
    <string>STRING_VALUE</string>
    <key>AppServiceHost</key>
    <string>STRING_VALUE</string>
    <key>AllowCutCopyPaste</key>
    <true /> or <false />
    <key>AllowPrint</key>
    <true /> or <false />
    <key>AllowSuggestedUpdates</key>
    <true /> or <false />
    <key>AppUpdateURL</key>
    <string>STRING_VALUE</string>
    </dict>
    
    ```
9. Select **Add**.
10. Refresh the page, and select the newly created policy.
11. Select **Assignments**, and choose who you want the app to apply to.
12. Select **Save**.

## Android configuration policies

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for **Intune** or select the widget from the list.
3. Go to **Client Apps** &gt; **Apps** &gt; **App Configuration Policies**. Then select **+ Add** &gt; **Managed Devices**.
4. Enter a name.
5. Under **Platform**, choose **Android**.
6. Under **Associated App**, choose the Workday for Android app that you added.
7. Select **Configuration Settings**. Under **Configuration settings format**, select **Enter JSON Data**.