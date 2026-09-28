---
layout: Conceptual
title: Risk policies - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/howto-identity-protection-configure-risk-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Enable and configure risk policies in Microsoft Entra ID Protection.
ms.topic: how-to
ms.date: 2025-10-30T00:00:00.0000000Z
ms.reviewer: cokoopma
locale: en-us
document_id: 75919910-c2c4-b678-44c0-62ed63fe8a1a
document_version_independent_id: c82be269-3182-f9f5-2d88-c95b258f969e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/howto-identity-protection-configure-risk-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/howto-identity-protection-configure-risk-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/howto-identity-protection-configure-risk-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f38a88a8-4a2a-1e1b-5c9c-ba9156b382f0
---

# Risk policies - Microsoft Entra ID Protection | Microsoft Learn

There are two types of [risk policies](concept-identity-protection-policies) in Microsoft Entra Conditional Access you can set up. You can use these policies to automate the response to risks allowing users to self-remediate when risk is detected:

- User risk policy
- Sign-in risk policy

Warning

Don't combine sign-in risk and user risk conditions in the same Conditional Access policy. Create separate policies for each risk condition.

![Screenshot of a Conditional Access policy showing risk as conditions.](media/howto-identity-protection-configure-risk-policies/sign-in-risk-conditions.png)

## Prerequisites

- The Microsoft Entra ID P2 or Microsoft Entra Suite license is required for full access to Microsoft Entra ID Protection features.
    - For a detailed list of capabilities for each license tier, see [What is Microsoft Entra ID Protection](overview-identity-protection).
- The [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role is the least privileged role required to **create or edit Conditional Access policies**.

## Choosing acceptable risk levels

Organizations must decide the level of risk they want to require access control on, while balancing security posture and user productivity.

Choosing to apply access control on a **High** risk level reduces the number of times a policy is triggered and minimizes friction for users. However, it excludes **Low** and **Medium** risks from the policy, which might not block an attacker from exploiting a compromised identity. Selecting **Medium** and/or **Low** risk levels usually introduces more user interrupts.

Configured trusted [network locations](../identity/conditional-access/concept-assignment-network#trusted-locations) are used by Microsoft Entra ID Protection in some risk detections to reduce false positives.

### Risk remediation

Organizations can choose to block access when risk is detected. Blocking sometimes stops legitimate users from doing what they need to. A better solution is to configure user and sign-in risk-based Conditional Access policies that [allow users to self-remediate](howto-identity-protection-remediate-unblock#end-user-self-remediation).

Warning

Users must register for Microsoft Entra multifactor authentication before they face a situation requiring remediation. For hybrid users that are synced from on-premises, password writeback must be enabled. Users not registered are blocked and require administrator intervention.

Password change (I know my password and want to change it to something new) outside of the risky user policy remediation flow doesn't meet the requirement for secure password change.

### Microsoft recommendations

Microsoft recommends the following risk policy configurations to protect your organization:

### User risk policy

Organizations should select **Require risk remediation** when user risk level is **High**. For passwordless users, Microsoft Entra revokes the user's sessions so they must reauthenticate. For users with passwords, they're prompted to complete a secure password change after a successful Microsoft Entra multifactor authentication.

When **Require risk remediation** is selected, two settings are automatically applied:

- **Require authentication strength** is automatically selected as a grant control.
- **Sign-in frequency - Every time** is automatically applied as a session control.

### Sign-in risk policy

Require Microsoft Entra multifactor authentication when sign-in risk level is **Medium** or **High**. This configuration allows users to prove it's them by using one of their registered authentication methods, remediating the sign-in risk.

We also recommend including the [sign-in frequency session control](../identity/conditional-access/concept-session-lifetime#require-reauthentication-every-time) to require reauthentication for risky sign-ins. A successful "strong authentication" usually via multifactor authentication or passwordless authentication, is the only way to self-remediate sign-in risk, regardless of the risk level.

## Enable policies

Organizations can choose to deploy risk-based policies in Conditional Access using the following steps or use [Conditional Access templates](../identity/conditional-access/concept-conditional-access-policy-common).

Before organizations enable these policies, they should take action to [investigate](howto-identity-protection-investigate-risk) and [remediate](howto-identity-protection-remediate-unblock) any active risks.

### Policy exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../identity/managed-identities-azure-resources/overview).

### User risk policy in Conditional Access

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. Under **Target resources** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **User risk**, set **Configure** to **Yes**.
    1. Under **Configure user risk levels needed for policy to be enforced**, select **High**. [This guidance is based on Microsoft recommendations and might be different for each organization](howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels)
    2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require risk remediation**. The **Require authentication strength** grant control is automatically selected. Choose the strength appropriate for your organization.
    2. Select **Select**.
9. Under **Session**, **Sign-in frequency - Every time** is automatically applied as a session control and is mandatory.
10. Confirm your settings and set **Enable policy** to **Report-only**.
11. Select **Create** to create your policy.

After confirming your settings using [policy impact or report-only mode](../identity/conditional-access/concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

### Sign-in risk policy in Conditional Access

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. Under **Cloud apps or actions** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**.
    1. Under **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**. [This guidance is based on Microsoft recommendations and might be different for each organization](howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels)
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

After confirming your settings using [policy impact or report-only mode](../identity/conditional-access/concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

### Passwordless scenarios

For organizations that adopt [passwordless authentication methods](/en-us/entra/identity/authentication/howto-authentication-passwordless-deployment) make the following changes:

#### Update your passwordless sign-in risk policy

1. Under **Users**:
    1. **Include**, select **Users and groups** and target your passwordless users.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
2. Under **Cloud apps or actions** &gt; **Include**, select **All resources** (formerly 'All cloud apps').
3. Under **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**.
    1. Under **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**. For more information on risk levels, see [Choosing acceptable risk levels](howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels).
    2. Select **Done**.
4. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the built-in **Passwordless MFA** or **Phishing-resistant MFA** based on which method the targeted users have.
    2. Select **Select**.
5. Under **Session**:
    1. Select **Sign-in frequency**.
    2. Ensure **Every time** is selected.
    3. Select **Select**.

## Migrate risk policies to Conditional Access

If you have legacy risk policies enabled in Microsoft Entra ID Protection, you should plan to migrate them to Conditional Access:

Warning

The legacy risk policies configured in Microsoft Entra ID Protection will be retired on **October 1, 2026**.

### Migrate to Conditional Access

1. **Create equivalent**user risk-based and sign-in risk-based policies in Conditional Access in report-only mode. You can create a policy with the previous steps or using [Conditional Access templates](../identity/conditional-access/concept-conditional-access-policy-common)based on Microsoft's recommendations and your organizational requirements.
    1. After administrators confirm the settings using [report-only mode](../identity/conditional-access/howto-conditional-access-insights-reporting), they can move the **Enable policy** toggle from **Report-only** to **On**.
2. **Disable**the old risk policies in ID Protection.
    1. Browse to **ID Protection** &gt; **Dashboard** &gt; Select the **User risk** or **Sign-in risk** policy.
    2. Set **Enforce policy** to **Disabled**.
3. Create other risk policies if needed in [Conditional Access](../identity/conditional-access/concept-conditional-access-policy-common).

#### Help and support for migrating risk policies

If you need help migrating your risk policies to Conditional Access, please submit a support request in the Microsoft Entra admin center.

1. Go to **New support request** in the Microsoft Entra admin center.
2. Describe your issue: **Migrate legacy ID Protection policy**.
3. Select **Microsoft Entra Sign-in and Multifactor Authentication** &gt; **Next**.
4. Select **Configuring new or existing policy settings** &gt; **Next**.
5. Close the solution page.
6. Select **Create a support request**.
7. Use the following selections to get your request to the right team:
    1. Issue type: **Technical**.
    2. Service type: **Microsoft Entra Sign-in and Multifactor Authentication**.
    3. Summary: **Migrate legacy ID Protection policy**.
    4. Problem type: **Identity Protection**.
    5. Problem subtype: **Configure risk policies**.
8. Select **Next** and navigate to the **Additional details** tab to fill out your details.
9. Fill out the required details and submit your request.