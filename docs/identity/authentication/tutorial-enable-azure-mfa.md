---
layout: Conceptual
title: Enable Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-azure-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: In this tutorial, you learn how to enable Microsoft Entra multifactor authentication for a group of users and test the secondary factor prompt during a sign-in event.
ms.topic: tutorial
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: jupetter
locale: en-us
document_id: 80005683-d3e5-aab5-2642-677a2ef96203
document_version_independent_id: 6abac9a6-5472-62c3-5eae-fa39ecccd12e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/tutorial-enable-azure-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/tutorial-enable-azure-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/tutorial-enable-azure-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7fc30126-fd4d-7315-3128-4c059dc0c177
---

# Enable Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn

Multifactor authentication is a process in which a user is prompted for additional forms of identification during a sign-in event. For example, the prompt could be to enter a code on their cellphone or to provide a fingerprint scan. When you require a second form of identification, security is increased because this additional factor isn't easy for an attacker to obtain or duplicate.

Microsoft Entra multifactor authentication and Conditional Access policies give you the flexibility to require MFA from users for specific sign-in events.

Important

This tutorial shows an administrator how to enable Microsoft Entra multifactor authentication. To step through the multifactor authentication as a user, see [Sign in to your work or school account using your two-step verification method](https://support.microsoft.com/account-billing/sign-in-to-your-work-or-school-account-using-your-two-step-verification-method-c7293464-ef5e-4705-a24b-c4a3ec0d6cf9).

If your IT team hasn't enabled the ability to use Microsoft Entra multifactor authentication, or if you have problems during sign-in, reach out to your Help desk for additional assistance.

In this tutorial you learn how to:

- Create a Conditional Access policy to enable Microsoft Entra multifactor authentication for a group of users.
- Configure the policy conditions that prompt for MFA.
- Test configuring and using multifactor authentication as a user.

## Prerequisites

To complete this tutorial, you need the following resources and privileges:

- A working Microsoft Entra tenant with Microsoft Entra ID P1 or trial licenses enabled.

    - If you need to, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An account with at least the [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) role. Some MFA settings can also be managed by an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
- A non-administrator account with a password that you know. For this tutorial, we created such an account, named *testuser*. In this tutorial, you test the end-user experience of configuring and using Microsoft Entra multifactor authentication.

    - If you need information about creating a user account, see [Add or delete users using Microsoft Entra ID](../../fundamentals/how-to-create-delete-users).
- A group that the non-administrator user is a member of. For this tutorial, we created such a group, named *MFA-Test-Group*. In this tutorial, you enable Microsoft Entra multifactor authentication for this group.

    - If you need more information about creating a group, see [Create a basic group and add members using Microsoft Entra ID](/en-us/entra/fundamentals/how-to-manage-groups).

## Create a Conditional Access policy

The recommended way to enable and use Microsoft Entra multifactor authentication is with Conditional Access policies. Conditional Access lets you create and define policies that react to sign-in events and that request additional actions before a user is granted access to an application or service.

[![Overview diagram of how Conditional Access works to secure the sign-in process](media/tutorial-enable-azure-mfa/conditional-access-overview.png)](media/tutorial-enable-azure-mfa/conditional-access-overview.png#lightbox)

Conditional Access policies can be applied to specific users, groups, and apps. The goal is to protect your organization while also providing the right levels of access to the users who need it.

In this tutorial, we create a basic Conditional Access policy to prompt for MFA when a user signs in. In a later tutorial in this series, we configure Microsoft Entra multifactor authentication by using a risk-based Conditional Access policy.

First, create a Conditional Access policy and assign your test group of users as follows:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; Overview , select **+ Create new policy**.

![A screenshot of the Conditional Access page, where you select 'New policy' and then select 'Create new policy'.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-menu-new-policy.png)

1. Enter a name for the policy, such as *MFA Pilot*.
2. Under **Assignments**, select the current value under **Users or workload identities**.

    ![A screenshot of the Conditional Access page, where you select the current value under 'Users or workload identities'.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-menu-users.png)
3. Under **What does this policy apply to?**, verify that **Users and groups** is selected.
4. Under **Include**, choose **Select users and groups**, and then select **Users and groups**.

    ![A screenshot of the page for creating a new policy, where you select options to specify users and groups.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-menu-select-users-groups.png)

    Since no one is assigned yet, the list of users and groups (shown in the next step) opens automatically.
5. Browse for and select your Microsoft Entra group, such as *MFA-Test-Group*, then choose **Select**.

    ![A screenshot of the list of users and groups, with results filtered by the letters M F A, and 'MFA-Test-Group' selected.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-select-mfa-test-group.png)

We've selected the group to apply the policy to. In the next section, we configure the conditions under which to apply the policy.

## Configure the conditions for multifactor authentication

Now that the Conditional Access policy is created and a test group of users is assigned, define the cloud apps or actions that trigger the policy. These cloud apps or actions are the scenarios that you decide require additional processing, such as prompting for multifactor authentication. For example, you could decide that access to a financial application or use of management tools require an additional prompt for authentication.

### Configure which apps require multifactor authentication

For this tutorial, configure the Conditional Access policy to require multifactor authentication when a user signs in.

1. Select the current value under **Cloud apps or actions**, and then under **Select what this policy applies to**, verify that **Cloud apps** is selected.
2. Under **Include**, choose **Select resources**.

    Since no apps are yet selected, the list of apps (shown in the next step) opens automatically.

    Tip

    You can choose to apply the Conditional Access policy to **All resources (formerly 'All cloud apps')** or **Select resources**. To provide flexibility, you can also exclude certain apps from the policy.
3. Browse the list of available sign-in events that can be used. For this tutorial, select **Windows Azure Service Management API** so that the policy applies to sign-in events. Then choose **Select**.

    ![A screenshot of the Conditional Access page, where you select the app, Windows Azure Service Management API, to which the new policy will apply.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-menu-select-apps.png)

### Configure multifactor authentication for access

Next, we configure access controls. Access controls let you define the requirements for a user to be granted access. They might be required to use an approved client app or a device that's hybrid-joined to Microsoft Entra ID.

In this tutorial, configure the access controls to require multifactor authentication during a sign-in event.

1. Under **Access controls**, select the current value under **Grant**, and then select **Grant access**.

    ![A screenshot of the Conditional Access page, where you select 'Grant' and then select 'Grant access'.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-menu-grant-access.png)
2. Select **Require multifactor authentication**, and then choose **Select**.

    ![A screenshot of the options for granting access, where you select 'Require multi-factor authentication'.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-select-require-mfa.png)

### Activate the policy

Conditional Access policies can be set to **Report-only** if you want to see how the configuration would affect users, or **Off** if you don't want to the use policy right now. Because a test group of users is targeted for this tutorial, let's enable the policy, and then test Microsoft Entra multifactor authentication.

1. Under **Enable policy**, select **On**.

    ![A screenshot of the control that's near the bottom of the web page where you specify whether the policy is enabled.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-conditional-access-enable-policy-on.png)
2. To apply the Conditional Access policy, select **Create**.

## Test Microsoft Entra multifactor authentication

Let's see your Conditional Access policy and Microsoft Entra multifactor authentication in action.

First, sign in to a resource that doesn't require MFA:

1. Open a new browser window in InPrivate or incognito mode and browse to https://account.activedirectory.windowsazure.com.

    Using a private mode for your browser prevents any existing credentials from affecting this sign-in event.
2. Sign in with your non-administrator test user, such as *testuser*. Be sure to include `@` and the domain name for the user account.

    If this is the first instance of signing in with this account, you're prompted to change the password. However, there's no prompt for you to configure or use multifactor authentication.
3. Close the browser window.

You configured the Conditional Access policy to require additional authentication for sign in. Because of that configuration, you're prompted to use Microsoft Entra multifactor authentication or to configure a method if you haven't yet done so. Test this new requirement by signing in to the Microsoft Entra admin center:

1. Open a new browser window in InPrivate or incognito mode and sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Sign in with your non-administrator test user, such as *testuser*. Be sure to include `@` and the domain name for the user account.

    You're required to register for and use Microsoft Entra multifactor authentication.

    ![A prompt that says 'More information required.' This is a prompt to configure a method of multi-factor authentication for this user.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-browser-prompt-more-info.png)
3. Select **Next** to begin the process.

    You can choose to configure an authentication phone, an office phone, or a mobile app for authentication. *Authentication phone* supports text messages and phone calls, *office phone* supports calls to numbers that have an extension, and *mobile app* supports using a mobile app to receive notifications for authentication or to generate authentication codes.

    ![A prompt that says, 'Additional security verification.' This is a prompt to configure a method of multi-factor authentication for this user. You can choose as the method an authentication phone, an office phone, or a mobile app.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-additional-security-verification-mobile-app.png)
4. Complete the instructions on the screen to configure the method of multifactor authentication that you've selected.
5. Close the browser window, and sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) again to test the authentication method that you configured. For example, if you configured a mobile app for authentication, you should see a prompt like the following.

    ![To sign in, follow the prompts in your browser and then the prompt on the device that you registered for multifactor authentication.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-browser-prompt.png)
6. Close the browser window.

## Clean up resources

If you no longer want to use the Conditional Access policy that you configured as part of this tutorial, delete the policy by using the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Policies** &gt; **Conditional Access**, and then select the policy that you created, such as **MFA Pilot**.
3. select **Delete**, and then confirm that you want to delete the policy.

    ![To delete the Conditional Access policy that you've opened, select Delete which is located under the name of the policy.](media/tutorial-enable-azure-mfa/tutorial-enable-azure-mfa-delete-policy.png)