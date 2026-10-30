---
layout: Conceptual
title: Risk-based user sign-in protection in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-risk-based-sspr-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: In this tutorial, you learn how to enable Microsoft Entra ID Protection to protect users when risky sign-in behavior is detected on their account.
ms.topic: tutorial
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
ms.custom: sfi-image-nochange
locale: en-us
document_id: acf3eec1-54ad-4dad-0925-58d4bbf2f020
document_version_independent_id: 3b2e0da9-0693-881c-b974-b4080f207bf3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/tutorial-risk-based-sspr-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/tutorial-risk-based-sspr-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/tutorial-risk-based-sspr-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: adc8cb59-6fe8-c506-288e-7f4dc1fe0cda
---

# Risk-based user sign-in protection in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

To protect your users, you can configure risk-based Microsoft Entra Conditional Access policies that automatically respond to risky behaviors. These policies can automatically block a sign-in attempt or require extra action, such as require a secure password change or prompting for Microsoft Entra multifactor authentication. These policies work with existing Microsoft Entra Conditional Access policies as an extra layer of protection for your organization. Users might never trigger a risky behavior in one of these policies, but your organization is protected if an attempt to compromise your security is made.

Important

This tutorial shows an administrator how to enable risk-based multifactor authentication (MFA).

If your IT team hasn't enabled the ability to use Microsoft Entra multifactor authentication or you have problems during sign-in, reach out to your helpdesk for additional assistance.

In this tutorial, you learn how to:

- Understand the available policies
- Enable Microsoft Entra multifactor authentication registration
- Enable risk-based password changes
- Enable risk-based multifactor authentication
- Test risk-based policies for user sign-in attempts

## Prerequisites

To complete this tutorial, you need the following resources and privileges:

- A working Microsoft Entra tenant with at least a Microsoft Entra ID P2 or trial license enabled.
    - If needed, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An account with Security Administrator privileges.
- Microsoft Entra ID configured for self-service password reset and Microsoft Entra multifactor authentication
    - If needed, [complete the tutorial to enable Microsoft Entra SSPR](tutorial-enable-sspr).
    - If needed, [complete the tutorial to enable Microsoft Entra multifactor authentication](tutorial-enable-azure-mfa).

## Overview of Microsoft Entra ID Protection

Each day, Microsoft collects and analyses trillions of anonymized signals as part of user sign-in attempts. These signals help build patterns of good user sign-in behavior, and identify potential risky sign-in attempts. Microsoft Entra ID Protection can review user sign-in attempts and take extra action if there's suspicious behavior:

Some of the following actions might trigger Microsoft Entra ID Protection risk detection:

- Users with leaked credentials.
- Sign-ins from anonymous IP addresses.
- Impossible travel to atypical locations.
- Sign-ins from infected devices.
- Sign-ins from IP addresses with suspicious activity.
- Sign-ins from unfamiliar locations.

This article guides you through enabling three policies to protect users and automate the response to suspicious activity.

- Multifactor authentication registration policy
    - Makes sure users are registered for Microsoft Entra multifactor authentication. If a sign-in risk policy prompts for MFA, the user must already be registered for Microsoft Entra multifactor authentication.
- User risk policy
    - Identifies and automates response to user accounts that might have compromised credentials. Can prompt the user to create a new password.
- Sign in risk policy
    - Identifies and automates response to suspicious sign-in attempts. Can prompt the user to provide extra forms of verification using Microsoft Entra multifactor authentication.

When you enable a risk-based policy, you can also choose the threshold for risk level - *low*, *medium*, or *high*. This flexibility lets you decide how aggressive you want to be in enforcing any controls for suspicious sign-in events. Microsoft recommends the following policy configurations.

For more information about Microsoft Entra ID Protection, see [What is Microsoft Entra ID Protection?](../../id-protection/overview-identity-protection)

## Enable multifactor authentication registration policy

Microsoft Entra ID Protection includes a default policy that can help get users registered for Microsoft Entra multifactor authentication. If you use other policies to protect sign-in events, you would need users to have already registered for MFA. When you enable this policy, it doesn't require users to perform MFA at each sign-in event. The policy only checks the registration status for a user and asks them to preregister if needed.

It's recommended to enable this registration policy for users that use multifactor authentication. To enable this policy, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **ID Protection** &gt; **Dashboard** &gt; **Multifactor authentication registration policy**.
3. By default, the policy applies to *All users*. If desired, select **Assignments**, then choose the users or groups to apply the policy on.
4. Under *Controls*, select **Access**. Make sure the option for *Require Microsoft Entra multifactor authentication registration* is checked, then choose **Select**.
5. Set **Enforce Policy** to *On*, then select **Save**.

[![Screenshot of how to require users to register for MFA.](media/tutorial-risk-based-sspr-mfa/enable-mfa-registration.png)](media/tutorial-risk-based-sspr-mfa/enable-mfa-registration.png#lightbox)

## Enable user risk policy for password change

Microsoft works with researchers, law enforcement, various security teams at Microsoft, and other trusted sources to find username and password pairs. When one of these pairs matches an account in your environment, a risk-based password change can be requested. This policy and action requires the user update their password before they can sign in to make sure any previously exposed credentials no longer work.

To enable this policy, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. Under **Target resources** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **User risk**, set **Configure** to **Yes**.
    1. Under **Configure user risk levels needed for policy to be enforced**, select **High**. [This guidance is based on Microsoft recommendations and might be different for each organization](../../id-protection/howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels)
    2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require risk remediation**. The **Require authentication strength** grant control is automatically selected. Choose the strength appropriate for your organization.
    2. Select **Select**.
9. Under **Session**, **Sign-in frequency - Every time** is automatically applied as a session control and is mandatory.
10. Confirm your settings and set **Enable policy** to **Report-only**.
11. Select **Create** to create your policy.

After confirming your settings using [policy impact or report-only mode](../conditional-access/concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## Enable sign-in risk policy for MFA

Most users have a normal behavior that can be tracked. When they fall outside of this norm, it could be risky to allow them to successfully sign in. Instead, you might want to block that user, or ask them to perform a multifactor authentication. If the user successfully completes the MFA challenge, you can consider it a valid sign-in attempt and grant access to the application or service.

To enable this policy, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. Under **Cloud apps or actions** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**.
    1. Under **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**. [This guidance is based on Microsoft recommendations and might be different for each organization](../../id-protection/howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels)
    2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the built-in **Multifactor authentication** authentication strength from the list.
    2. Select **Select**.
9. Under **Session**.
    1. Select **Sign-in frequency**.
    2. Ensure **Every time** is selected.
    3. Select **Select**.
10. Confirm your settings and set **Enable policy** to **Report-only**.
11. Select **Create** to create to enable your policy.

After confirming your settings using [policy impact or report-only mode](../conditional-access/concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

### Passwordless scenarios

For organizations that adopt [passwordless authentication methods](/en-us/entra/identity/authentication/howto-authentication-passwordless-deployment) make the following changes:

#### Update your passwordless sign-in risk policy

1. Under **Users**:
    1. **Include**, select **Users and groups** and target your passwordless users.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
2. Under **Cloud apps or actions** &gt; **Include**, select **All resources** (formerly 'All cloud apps').
3. Under **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**.
    1. Under **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**. For more information on risk levels, see [Choosing acceptable risk levels](../../id-protection/howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels).
    2. Select **Done**.
4. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the built-in **Passwordless MFA** or **Phishing-resistant MFA** based on which method the targeted users have.
    2. Select **Select**.
5. Under **Session**:
    1. Select **Sign-in frequency**.
    2. Ensure **Every time** is selected.
    3. Select **Select**.

## Test risky sign events

Most user sign-in events don't trigger the risk-based policies configured in the previous steps. A user might never see a prompt for MFA or to reset their password. If their credentials remain secure and their behavior consistent, their sign-in events would be successful.

To test the Microsoft Entra ID Protection policies created in the previous steps, you need a way to simulate risky behavior or potential attacks. The steps to do these tests vary based on the Microsoft Entra ID Protection policy you want to validate. For more information on scenarios and steps, see [Simulate risk detections in Microsoft Entra ID Protection](../../id-protection/howto-identity-protection-simulate-risk).

## Clean up resources

If you complete your testing and no longer want to have the risk-based policies enabled, return to each policy you want to disable and set **Enable policy** to *Off* or delete them.