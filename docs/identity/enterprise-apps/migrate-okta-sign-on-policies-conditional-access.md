---
layout: Conceptual
title: Tutorial to migrate Okta sign-on policies to Microsoft Entra Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-okta-sign-on-policies-conditional-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Learn how to migrate Okta sign-on policies to Microsoft Entra Conditional Access.
ms.topic: tutorial
ms.date: 2023-01-13T00:00:00.0000000Z
ms.reviewer: gasinh
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 5967ed62-56cb-8fa4-7c1c-cfe655d91a23
document_version_independent_id: a49e257a-8596-3f73-78b3-04289e96d728
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-okta-sign-on-policies-conditional-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-okta-sign-on-policies-conditional-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-okta-sign-on-policies-conditional-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 8f526f28-4cc5-454b-a5d6-92cd2dbe8a25
---

# Tutorial to migrate Okta sign-on policies to Microsoft Entra Conditional Access - Microsoft Entra ID | Microsoft Learn

In this tutorial, learn to migrate an organization from global or application-level sign-on policies in Okta Conditional Access in Microsoft Entra ID. Conditional Access policies secure user access in Microsoft Entra ID and connected applications.

Learn more: [What is Conditional Access?](../conditional-access/overview)

This tutorial assumes you have:

- Office 365 tenant federated to Okta for sign-in and multifactor authentication
- Microsoft Entra Connect server, or Microsoft Entra Connect cloud provisioning agents configured for user provisioning to Microsoft Entra ID

## Prerequisites

See the following two sections for licensing and credentials prerequisites.

### Licensing

There are licensing requirements if you switch from Okta sign-on to Conditional Access. The process requires a Microsoft Entra ID P1 license to enable registration for Microsoft Entra multifactor authentication.

Learn more: [Assign or remove licenses in the Microsoft Entra admin center](../../fundamentals/licensing)

### Enterprise Administrator credentials

To configure the service connection point (SCP) record, ensure you have Enterprise Administrator credentials in the on-premises forest.

## Evaluate Okta sign-on policies for transition

Locate and evaluate Okta sign-on policies to determine what will be transitioned to Microsoft Entra ID.

1. In Okta go to **Security** &gt; **Authentication** &gt; **Sign On**.

    ![Screenshot of Global MFA Sign On Policy entries on the Authentication page.](media/migrate-okta-sign-on-policies-conditional-access/global-sign-on-policies.png)
2. Go to **Applications**.
3. From the submenu, select **Applications**
4. From the **Active apps list**, select the Microsoft Office 365 connected instance.

    ![Screenshot of settings under Sign On, for Microsoft Office 365.](media/migrate-okta-sign-on-policies-conditional-access/global-sign-on-policies-enforce-mfa.png)
5. Select **Sign On**.
6. Scroll to the bottom of the page.

The Microsoft Office 365 application sign-on policy has four rules:

- **Enforce MFA for mobile sessions** - requires MFA from modern authentication or browser sessions on iOS or Android
- **Allow trusted Windows devices** - prevents unnecessary verification or factor prompts for trusted Okta devices
- **Require MFA from untrusted Windows devices** - requires MFA from modern authentication or browser sessions on untrusted Windows devices
- **Block legacy authentication** - prevents legacy authentication clients from connecting to the service

The following screenshot is conditions and actions for the four rules, on the Sign On Policy screen.

![Screenshot of conditions and actions for the four rules, on the Sign On Policy screen.](media/migrate-okta-sign-on-policies-conditional-access/sign-on-rules.png)

## Configure Conditional Access policies

Configure Conditional Access policies to match Okta conditions. However, in some scenarios, you might need more setup:

- Okta network locations to named locations in Microsoft Entra ID
    - [Using the location condition in a Conditional Access policy](../conditional-access/concept-assignment-network)
- Okta device trust to device-based Conditional Access (two options to evaluate user devices):
    - See the following section, **Microsoft Entra hybrid join configuration** to synchronize Windows devices, such as Windows 10, Windows Server 2016 and 2019, to Microsoft Entra ID
    - See the following section, **Configure device compliance**
    - See, Use Microsoft Entra hybrid join, a feature in Microsoft Entra Connect server that synchronizes Windows devices, such as Windows 10, Windows Server 2016, and Windows Server 2019, to Microsoft Entra ID
    - See, Enroll the device in Microsoft Intune and assign a compliance policy

### Microsoft Entra hybrid join configuration

To enable Microsoft Entra hybrid join on your Microsoft Entra Connect server, run the configuration wizard. After configuration, enroll devices.

Note

Microsoft Entra hybrid join isn't supported with the Microsoft Entra Connect cloud provisioning agents.

1. [Configure Microsoft Entra hybrid join](../devices/how-to-hybrid-join).
2. On the **SCP configuration** page, select the **Authentication Service** dropdown.

    ![Screenshot of the Authentication Service dropdown on the Microsoft Entra Connect dialog.](media/migrate-okta-sign-on-policies-conditional-access/scp-configuration.png)
3. Select an Okta federation provider URL.
4. Select **Add**.
5. Enter your on-premises Enterprise Administrator credentials
6. Select **Next**.

    Tip

    If you blocked legacy authentication on Windows clients in the global or app-level sign-on policy, make a rule that enables the Microsoft Entra hybrid join process to finish. Allow the legacy authentication stack for Windows clients. To enable custom client strings on app policies, contact the [Okta Help Center](https://support.okta.com/help/).

### Configure device compliance

Microsoft Entra hybrid join is a replacement for Okta device trust on Windows. Conditional Access policies recognize compliance for devices enrolled in Microsoft Intune.

#### Device compliance policy

- [Use compliance policies to set rules for devices you manage with Intune](/en-us/mem/intune/protect/device-compliance-get-started)
- [Create a compliance policy in Microsoft Intune](/en-us/mem/intune/protect/create-compliance-policy)

#### Windows 10/11, iOS, iPadOS, and Android enrollment

If you deployed Microsoft Entra hybrid join, you can deploy another group policy to complete auto-enrollment of these devices in Intune.

- [Enrollment in Microsoft Intune](/en-us/mem/intune/)
- [Quickstart: Set up automatic enrollment for Windows 10/11 devices](/en-us/mem/intune/enrollment/quickstart-setup-auto-enrollment)
- [Enroll Android devices](/en-us/mem/intune/fundamentals/deployment-guide-enrollment-android)
- [Enroll iOS/iPadOS devices in Intune](/en-us/mem/intune/fundamentals/deployment-guide-enrollment-ios-ipados)

## Configure Microsoft Entra multifactor authentication tenant settings

Before you convert to Conditional Access, confirm the base MFA tenant settings for your organization.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **Per-user MFA** on the top menu of the **Users** pane.
4. The legacy Microsoft Entra multifactor authentication portal appears. Or select [Microsoft Entra multifactor authentication portal](https://aka.ms/mfaportal).

    ![Screenshot of the multifactor authentication screen.](media/migrate-okta-sign-on-policies-conditional-access/legacy-portal.png)
5. Confirm there are no users enabled for legacy MFA: On the **Multifactor authentication** menu, on **Multifactor authentication status**, select **Enabled** and **Enforced**. If the tenant has users in the following views, disable them in the legacy menu.

    ![Screenshot of the multifactor authentication screen with the search feature highlighted.](media/migrate-okta-sign-on-policies-conditional-access/disable-user-portal.png)
6. Ensure the **Enforced** field is empty.
7. Select the **Service settings** option.
8. Change the **App passwords** selection to **Do not allow users to create app passwords to sign in to non-browser apps**.

    ![Screenshot of the multifactor authentication screen with service settings highlighted.](media/migrate-okta-sign-on-policies-conditional-access/app-password-selection.png)
9. Clear the checkboxes for **Skip multifactor authentication for requests from federated users on my intranet** and **Allow users to remember multifactor authentication on devices they trust (between one to 365 days)**.
10. Select **Save**.

    ![Screenshot of cleared checkboxes on the Require Trusted Devices for Access screen.](media/migrate-okta-sign-on-policies-conditional-access/uncheck-fields-legacy-portal.png)

    Note

    See [Optimize reauthentication prompts and understand session lifetime for Microsoft Entra multifactor authentication](../authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).

## Build a Conditional Access policy

To configure Conditional Access policies, see [Best practices for deploying and designing Conditional Access](../conditional-access/plan-conditional-access#conditional-access-policy-components).

After you configure the prerequisites and established base settings, you can build Conditional Access policy. Policy can be targeted to an application, a test group of users, or both.

Before you get started:

- [Understand Conditional Access policy components](../conditional-access/plan-conditional-access)
- [Building a Conditional Access policy](../conditional-access/concept-conditional-access-policies)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. To learn how to create a policy in Microsoft Entra ID. See, [Common Conditional Access policy: Require MFA for all users](../conditional-access/policy-all-users-mfa-strength).
4. Create a device trust-based Conditional Access rule.

    ![Screenshot of entries for Require Trusted Devices for Access, under Conditional Access.](media/migrate-okta-sign-on-policies-conditional-access/test-user.png)

    ![Screenshot of the Keep you account secure dialog with the success message.](media/migrate-okta-sign-on-policies-conditional-access/success-test-user.png)
5. After you configure the location-based policy and device trust policy, [Block legacy authentication with Microsoft Entra ID with Conditional Access](../conditional-access/policy-block-legacy-authentication).

With these three Conditional Access policies, the original Okta sign-on policies experience is replicated in Microsoft Entra ID.

## Enroll pilot members in MFA

Users register for MFA methods.

For individual registration, users go to [Microsoft Sign-in pane](https://aka.ms/mfasetup).

To manage registration, users go to [Microsoft My Sign-Ins | Security Info](https://aka.ms/mysecurityinfo).

Learn more: [Enable combined security information registration in Microsoft Entra ID](../authentication/howto-registration-mfa-sspr-combined).

Note

If users registered, they're redirected to the **My Security** page, after they satisfy MFA.

## Enable Conditional Access policies

1. To test, change the created policies to **Enabled test user login**.

    ![Screenshot of policies on the Conditional Access, Policies screen.](media/migrate-okta-sign-on-policies-conditional-access/enable-test-user.png)
2. On the Office 365 **Sign-In** pane, the test user John Smith is prompted to sign in with Okta MFA and Microsoft Entra multifactor authentication.
3. Complete the MFA verification through Okta.

    ![Screenshot of MFA verification through Okta.](media/migrate-okta-sign-on-policies-conditional-access/mfa-verification-through-okta.png)
4. The user is prompted for Conditional Access.
5. Ensure the policies are configured to be triggered for MFA.

    ![Screenshot of MFA verification through Okta prompted for Conditional Access.](media/migrate-okta-sign-on-policies-conditional-access/mfa-verification-through-okta-prompted-ca.png)

## Add organization members to Conditional Access policies

After you conduct testing on pilot members, add the remaining organization members to Conditional Access policies, after registration.

To avoid double-prompting between Microsoft Entra multifactor authentication and Okta MFA, opt out from Okta MFA: modify sign-on policies.

1. Go to the Okta admin console
2. Select **Security** &gt; **Authentication**
3. Go to **Sign-on Policy**.

    Note

    Set global policies to **Inactive** if all applications from Okta are protected by application sign-on policies.
4. Set the **Enforce MFA** policy to **Inactive**. You can assign the policy to a new group that doesn't include the Microsoft Entra users.

    ![Screenshot of Global MFA Sign On Policy as Inactive.](media/migrate-okta-sign-on-policies-conditional-access/mfa-policy-inactive.png)
5. On the application-level sign-on policy pane, select the **Disable Rule** option.
6. Select **Inactive**. You can assign the policy to a new group that doesn't include the Microsoft Entra users.
7. Ensure there's at least one application-level sign-on policy enabled for the application that allows access without MFA.

    ![Screenshot of application access without MFA.](media/migrate-okta-sign-on-policies-conditional-access/application-access-without-mfa.png)
8. Users are prompted for Conditional Access the next time they sign in.