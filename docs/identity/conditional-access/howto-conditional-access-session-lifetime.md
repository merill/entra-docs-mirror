---
layout: Conceptual
title: Configure adaptive session lifetime policies - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/howto-conditional-access-session-lifetime
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to configure adaptive session lifetime policies in Microsoft Entra to manage sign-in frequency and browser session persistence effectively.
ms.topic: how-to
ms.date: 2026-04-02T00:00:00.0000000Z
ms.reviewer: inbarc, sreyanthmora
ms.custom:
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:09/02/2025
- ai-gen-description
locale: en-us
document_id: 9561a367-20d8-62e9-57e5-694bab4c0878
document_version_independent_id: a7c757e0-052b-fc42-70c5-030081baa573
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/howto-conditional-access-session-lifetime.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/howto-conditional-access-session-lifetime
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/howto-conditional-access-session-lifetime.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 92052d93-8132-5f7e-1bf6-478884fb623c
---

# Configure adaptive session lifetime policies - Microsoft Entra ID | Microsoft Learn

## Overview

Warning

If you're using the [configurable token lifetime](../../identity-platform/configurable-token-lifetimes) feature, we don't support creating two different policies for the same user or app combination: one with this feature and another with the configurable token lifetime feature. Microsoft retired the configurable token lifetime feature for refresh and session token lifetimes on January 30, 2021, and replaced it with the Conditional Access authentication session management feature.

Before enabling Sign-in Frequency, make sure other reauthentication settings are disabled in your tenant. If "Remember MFA on trusted devices" is enabled, disable it before using Sign-in Frequency, as using these two settings together might prompt users unexpectedly. To learn more about reauthentication prompts and session lifetime, see the article, [Optimize reauthentication prompts and understand session lifetime for Microsoft Entra multifactor authentication](../authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).

## Policy deployment

To ensure your policy works as expected, test it before rolling it out into production. Use a test tenant to verify that your new policy works as intended. For more information, see the article [Plan a Conditional Access deployment](plan-conditional-access).

### Policy 1: Sign-in frequency control

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for naming policies.
5. Choose all required conditions for customer’s environment, including the target cloud apps.

    Note

    It's recommended to set equal authentication prompt frequency for key Microsoft 365 apps such as Exchange Online and SharePoint Online for best user experience.
6. Under **Access controls** &gt; **Session**.

    1. Select **Sign-in frequency**.
        1. Choose **Periodic reauthentication** and enter a value of hours or days or select **Every time**.

> 
> ![Screenshot showing a Conditional Access policy configured for sign-in frequency.](media/howto-conditional-access-session-lifetime/conditional-access-policy-session-sign-in-frequency.png)
7. Save your policy.

### Policy 2: Persistent browser session

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Choose all required conditions.

    Note

    This control requires selecting "All Cloud Apps" as a condition. Browser session persistence is controlled by authentication session token. All tabs in a browser session share a single session token and therefore they all must share persistence state.
6. Under **Access controls** &gt; **Session**.

    1. Select **Persistent browser session**.

        Note

        Persistent browser session configuration in Microsoft Entra Conditional Access overrides the "Stay signed in?" setting in the company branding pane for the same user if both policies are configured.
    2. Select a value from dropdown.
7. Save your policy.

Note

Session lifetime settings, including sign-in frequency and persistent browser sessions, determine how often users must reauthenticate and whether sessions persist across browser restarts. Shorter lifetimes enhance security for high-risk apps, while longer ones improve convenience for trusted or managed devices.

### Policy 3: Sign-in frequency control every time risky user

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
    1. Select **Require authentication strength**, then select the built-in **Multifactor authentication** authentication strength from the list.
    2. Select **Require password change**.
    3. Select **Select**.
9. Under **Session**.
    1. Select **Sign-in frequency**.
    2. Ensure **Every time** is selected.
    3. Select **Select**.
10. Confirm your settings and set **Enable policy** to **Report-only**.
11. Select **Create** to enable your policy.

After confirming your settings using [report-only mode](howto-conditional-access-insights-reporting), move the **Enable policy** toggle from **Report-only** to **On**.

### Validation

Use the [What If tool](what-if-tool) to simulate a sign-in to the target application and other conditions based on your policy configuration. The authentication session management controls show up in the result of the tool.

## Prompt tolerance

The system accounts for five minutes of clock skew when **every time** is selected in policy, so users aren’t prompted more often than once every five minutes. If the user completes MFA in the last 5 minutes and encounters another Conditional Access policy that requires reauthentication, we don't prompt the user. Prompting users too often for reauthentication can affect their productivity and increase the risk of users approving MFA requests they didn’t initiate. Use "Sign-in frequency – every time" only when there are specific business needs.

## Known issues

- If you configure sign-in frequency for mobile devices: Authentication after each sign-in frequency interval might be slow and can take 30 seconds on average. This issue might also occur across various apps simultaneously.
- On iOS devices: If an app configures certificates as the first authentication factor and has both sign-in frequency and [Intune mobile application management policies](/en-us/mem/intune/apps/app-lifecycle) applied, users are blocked from signing in to the app when the policy triggers.
- Microsoft Entra Private Access doesn't support setting sign-in frequency to every time.