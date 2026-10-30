---
layout: Conceptual
title: Conditional Access - Require app protection policy for Windows - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-windows-app-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a Conditional Access policy to require app protection policy for Windows.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth, jogro
ms.custom: sfi-image-nochange
locale: en-us
document_id: 611bdafa-13de-8363-0033-4aaa6bef190b
document_version_independent_id: db63f68d-c962-84c4-6e2d-88061e37f284
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-windows-app-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-windows-app-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-windows-app-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d66c7634-a785-9f8a-56ed-0988f7cb1ac8
---

# Conditional Access - Require app protection policy for Windows - Microsoft Entra ID | Microsoft Learn

## Overview

App protection policies apply [mobile application management (MAM)](/en-us/mem/intune/apps/app-management#mobile-application-management-mam-basics) to specific applications on a device. These policies let you secure data within an application for scenarios like bring your own device (BYOD).

::![Screenshot of a browser requiring the user to sign in to their Microsoft Edge profile to access an application.](media/policy-all-users-windows-app-protection/browser-sign-in-with-edge-profile.png)

## Prerequisites

- Policy can be applied to the Microsoft Edge browser on devices running Windows 11 and Windows 10 version 20H2 and higher with KB5031445.
- Set up an app protection policy targeting Windows devices. For details, see [Configured app protection policy targeting Windows devices](/en-us/mem/intune/apps/app-protection-policy-settings-windows).
- Sovereign clouds aren't supported.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Create a Conditional Access policy

Start with [Report-only mode](howto-conditional-access-insights-reporting) so admins can check how the policy affects existing users. When admins are sure the policy works as intended, they can switch to **On** or stage the deployment by adding specific groups and excluding others.

### Require app protection policy for Windows devices

Follow these steps to create a Conditional Access policy that requires an app protection policy when using a Windows device to use the Office 365 apps group in Conditional Access. Also set up and assign the app protection policy to users in Microsoft Intune. For details about creating the app protection policy, see [App protection policy settings for Windows](/en-us/mem/intune/apps/app-protection-policy-settings-windows). This policy includes multiple controls that let devices either use app protection policies for mobile application management (MAM) or be managed and compliant with mobile device management (MDM) policies.

Tip

App protection policies (MAM) support unmanaged devices:

- If a device is already managed through mobile device management (MDM), Intune MAM enrollment is blocked, and app protection policy settings don't apply.
- If a device becomes managed after MAM enrollment, app protection policy settings don't apply.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **Office 365**.
7. Under **Conditions**:
    1. **Device platforms** set **Configure** to **Yes**.
        1. Under **Include**, **Select device platforms**.
        2. Choose **Windows** only.
        3. Select **Done**.
    2. **Client apps** set **Configure** to **Yes**.
        1. Select **Browser** only.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require app protection policy** and **Require device to be marked as compliant**.
    2. **For multiple controls**, select **Require one of the selected controls**
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

Note

If you set to **Require all the selected controls** or just use the **Require app protection policy** control alone, you need to make sure that you only target unmanaged devices or that the devices are not MDM managed. Otherwise, the policy will block access to all applications since it cannot assess whether the application is compliant as per policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Tip

Organizations should also deploy a policy that [blocks access from unsupported or unknown device platforms](policy-all-users-device-unknown-unsupported) along with this policy.

## Sign in to Windows devices

When users attempt to sign in to a site that is protected by an app protection policy for the first time, they're prompted: To access your service, app, or website, you might need to sign in to Microsoft Edge using `username@domain.com` or register your device with `organization` if you're already signed in.

Selecting **Switch Edge profile** opens a window listing their Work or school account along with an option to **Sign in to sync data**.

![Screenshot showing the popup in Microsoft Edge asking user to sign in.](media/policy-all-users-windows-app-protection/browser-sign-in-continue-with-work-or-school-account.png)

This process opens a window offering to allow Windows to remember your account and automatically sign you in to your apps, websites, and services. Select **Yes** to sign in and enroll your device in mobile application management.

![Screenshot showing the stay signed in to all your apps window for MAM enrollment.](media/policy-all-users-windows-app-protection/stay-signed-in-to-all-your-apps.png)

After selecting **Yes**, you might see a progress window while policy is applied. After a few moments, you should see a window saying **You're all set**, app protection policies are applied.

If your organization shows the following MDM enrollment option, select **No**. Selecting **Yes** enrolls your device in mobile device management (MDM), not mobile application management (MAM).

![Screenshot showing the MDM enrollment window.](media/policy-all-users-windows-app-protection/mdm-enrollment.png)

Tip

Now in preview, a new property to [disable the device management UX screen](/en-us/intune/intune-service/enrollment/windows-enroll) during this flow can be applied that will not display the option to MDM enroll to end users. This can reduce accidental MDM enrollments that block MAM enrollments.

## Troubleshooting

### Common issues

In some circumstances, after getting the "you're all set" page you might still be prompted to sign in with your work account. This prompt might happen when:

- Your profile is added to Microsoft Edge, but MAM enrollment is still being processed.
- Your profile is added to Microsoft Edge, but you selected "this app only" on the heads up page.
- You enrolled into MAM but your enrollment expired or you aren't compliant with your organization's requirements.

To resolve these possible scenarios:

- Wait a few minutes and try again in a new tab.
- Contact your administrator to check that Microsoft Intune MAM policies are applying to your account correctly.

### Existing account

There's a known issue where there's a preexisting, unregistered account, like `user@contoso.com` in Microsoft Edge, or if a user signs in without registering using the Heads Up Page, then the account isn't properly enrolled in MAM. This configuration blocks the user from being properly enrolled in MAM.