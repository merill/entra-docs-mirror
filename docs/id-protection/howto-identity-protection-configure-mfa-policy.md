---
layout: Conceptual
title: Configure the MFA registration policy - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/howto-identity-protection-configure-mfa-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn how to configure the Microsoft Entra ID Protection multifactor authentication registration policy.
ms.topic: how-to
ms.date: 2025-08-06T00:00:00.0000000Z
ms.reviewer: etbasser
locale: en-us
document_id: ed580e9f-f99a-7e85-65f0-8a4304b9bf82
document_version_independent_id: bd7ab1c4-856b-0e1c-c9d7-d6a5ea494467
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/howto-identity-protection-configure-mfa-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/howto-identity-protection-configure-mfa-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/howto-identity-protection-configure-mfa-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 8978842c-ffb0-bc3c-5c2c-f763abc5018f
---

# Configure the MFA registration policy - Microsoft Entra ID Protection | Microsoft Learn

Microsoft helps you manage the deployment of multifactor authentication (MFA) by configuring the Microsoft Entra ID Protection policy to require MFA registration regardless of the modern authentication app you're signing in to. Multifactor authentication provides a means to verify who you are using more than just a username and password. It provides a second layer of security to user sign-ins. In order for users to be able to respond to MFA prompts, they must first register authentication methods, like the Microsoft Authenticator app.

We recommend that you require multifactor authentication for all user sign-ins. [Based on our studies](https://www.microsoft.com/security/security-insider/microsoft-digital-defense-report-2023), your account is more than 99% less likely to be compromised if you use MFA. Even if you don't require MFA all the time, this policy ensures your users are ready when MFA is needed.

For more information, see the article [Common Conditional Access policy: Require MFA for all users](../identity/conditional-access/policy-all-users-mfa-strength).

## Prerequisites

- The Microsoft Entra ID P2 or Microsoft Entra Suite license is required for full access to Microsoft Entra ID Protection features, including modifying the MFA registration policy.
    - For a detailed list of capabilities for each license tier, see [What is Microsoft Entra ID Protection](overview-identity-protection).
- The [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) role is the least privileged role required to **create or edit risk-based policies**.

## Policy configuration

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **ID Protection** &gt; **Dashboard** &gt; **Multifactor authentication registration policy**.
    1. Under **Assignments** &gt; **Users**.
        1. Under **Include**, select **All users** or **Select individuals and groups** if limiting your rollout.
        2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
3. Set **Policy enforcement** to **Enabled**.
4. Select **Save**.

## User experience

Microsoft Entra ID Protection prompts your users to register the next time they sign in interactively, and they have 14 days to complete registration. During this 14-day period, they can bypass registration if MFA isn't required as a condition, but at the end of the period, they must register before they can complete the sign-in process.

For an overview of the related user experience, see the following:

- [Sign-in experiences with Microsoft Entra ID Protection](concept-identity-protection-user-experience).