---
layout: Conceptual
title: Microsoft Entra ID Protection risk-based access policies - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/concept-identity-protection-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Identifying risk-based Conditional Access policies
ms.topic: concept-article
ms.date: 2026-05-15T00:00:00.0000000Z
ms.reviewer: ebasseri
ms.custom: sfi-image-nochange
locale: en-us
document_id: 196f4c49-ee5c-dc51-774a-05f42b72d425
document_version_independent_id: 29d381d5-68b1-6198-f3ee-c78d9cc9e629
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/concept-identity-protection-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/concept-identity-protection-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/concept-identity-protection-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 556e2af0-c51c-3740-76df-e7d50ebfeb33
---

# Microsoft Entra ID Protection risk-based access policies - Microsoft Entra ID Protection | Microsoft Learn

Risk-based access control policies can be applied to protect organizations when a sign-in or user is detected to be at risk.

![Diagram that shows a conceptual risk-based Conditional Access policy.](media/concept-identity-protection-policies/risk-based-conditional-access-diagram.png)

Microsoft Entra Conditional Access offers two user-specific risk conditions powered by Microsoft Entra ID Protection signals: **[Sign-in risk](../identity/conditional-access/concept-conditional-access-conditions#sign-in-risk)** and **[User risk](../identity/conditional-access/concept-conditional-access-conditions#user-risk)**. Organizations can create risk-based Conditional Access policies by configuring these two risk conditions and choosing an access control method. During each sign-in, ID Protection sends the detected risk levels to Conditional Access, and the risk-based policies apply if the policy conditions are satisfied.

You might require multifactor authentication when the sign-in risk level is medium or high. Users are only prompted at that level.

![Diagram that shows a conceptual risk-based Conditional Access policy with self-remediation.](media/concept-identity-protection-policies/risk-based-conditional-access-policy-example.png)

The previous example also demonstrates a main benefit of a risk-based policy: **automatic risk remediation**. When a user successfully completes the required access control, like a secure password change, their risk is remediated. That sign-in session and user account are no longer at risk, and no action is needed from the administrator.

Allowing users to self-remediate using this process significantly reduces the risk investigation and remediation burden on administrators while protecting your organization from security compromises. More information about risk remediation can be found in the article, [Remediate risks and unblock users](howto-identity-protection-remediate-unblock).

Note

[Microsoft Entra ID P2](https://www.microsoft.com/security/business/microsoft-entra-pricing) is required to use risk-based access policies.

## User risk-based Conditional Access policy

ID Protection analyzes signals about user accounts and calculates a risk score based on the probability that the user is compromised. If a user has risky user sign-in behavior, or their credentials were leaked, ID Protection uses these signals to calculate the user risk level. Administrators can configure risk-based Conditional Access policies to enforce access controls based on user risk, including requirements such as:

1. Require risk remediation: ID Protection manages the appropriate remediation flow for all authentication methods.
2. Require password change: ID Protection blocks access until user completes a secure password change.
3. Block access: ID Protection blocks the user until risk is addressed.

Policies requiring either #1 or #2 forces end users to remediate their user risk and unblock themselves.

## Require risk remediation control

This control uses adaptive risk remediation to let you author a Conditional Access risk policy that accommodates all authentication methods, including password-based and passwordless. This means that when you select "Require risk remediation" in your policy's grant controls, Microsoft Entra ID Protection manages the appropriate remediation flow based on the threat observed and the user's authentication method. For detailed steps on how to enable adaptive risk remediation, see [Configure risk policies](howto-identity-protection-configure-risk-policies#microsoft-recommendations).

- **Password authentication**: Risky user has an active risk detection, such as a leaked credential, password spray, or session history involving a compromised password. The user is prompted to perform a secure password change and when completed, their previous sessions are revoked.
- **Passwordless authentication**: Risky user has an active risk detection, but it doesn't involve a compromised password. Possible risk detections include anomalous token, impossible travel, or unfamiliar sign-in properties. The user's sessions are revoked and they're prompted to sign in again.
- **Attacker-added device**: Risky user is flagged by Microsoft's threat intelligence as having a device added by an attacker. The Entra device object is disabled, blocking new token issuance. The user's sessions are revoked, and they're prompted to sign-in again.

#### Special considerations

- **Require Risk Remediation** remediates user risk, not sign-in risk.
- If a user is assigned to multiple policies, precedence applies: **Require risk remediation** overrides **Require password change**, and **Block** overrides all others. To avoid conflicts, assign each user to only one of these policies at a time.
- **Require authentication strength** and **Sign-in frequency - Every time** are automatically applied to the policy to ensure that after session revocation, end users are immediately prompted to reauthenticate with the specified authentication strength.
- **Require risk remediation** is not supported for external and guest users because Microsoft Entra ID doesn't support session revocation for those users.
- During risk remediation, Microsoft Entra ID uses a dedicated, secure flow to perform actions such as session revocation. To ensure remediation is not blocked, this flow is allowed to proceed without being impacted by other Conditional Access policies.
    - `AppId`: Public cloud = `93625bc8-bfe2-437a-97e0-3d0060024faa`, Azure for US Government = `00001111-aaaa-2222-bbbb-3333cccc4444`
    - `ResourceId`: `00000003-0000-0000-c000-000000000000`

## Sign-in risk-based Conditional Access policy

During each sign-in, ID Protection analyzes hundreds of signals in real-time and calculates a sign-in risk level that represents the probability that the given authentication request isn't authorized. This risk level then gets sent to Conditional Access, where the organization's configured policies are evaluated. Administrators can configure sign-in risk-based Conditional Access policies to enforce access controls based on sign-in risk, including requirements such as:

- Block access
- Allow access
- Require multifactor authentication
- Require reauthentication (Sign-in frequency)

If risks are detected on a sign-in, users can perform the required access control such as multifactor authentication to self-remediate and close the risky sign-in event to prevent unnecessary noise for administrators.

![Screenshot of a sign-in risk-based Conditional Access policy.](media/concept-identity-protection-policies/sign-in-risk-policy.png)

Note

Users must have registered an authentication method that can satisfy Microsoft Entra multifactor authentication before triggering a sign-in risk policy.

## Migrate ID Protection risk policies to Conditional Access

If you have the legacy **user risk policy** or **sign-in risk policy** enabled in ID Protection (formerly Identity Protection), [migrate them to Conditional Access](howto-identity-protection-configure-risk-policies#migrate-risk-policies-to-conditional-access).

Warning

The legacy risk policies configured in Microsoft Entra ID Protection are retiring on **October 1, 2026**.

Configuring risk policies in Conditional Access provides benefits like the ability to:

- Manage access policies in one location.
- Use report-only mode and Graph APIs.
- Enforce sign-in frequency to require reauthentication every time.
- Provide granular access control combining risk with other conditions like location.
- Enhance security with multiple risk-based policies targeting different user groups or risk levels.
- Improve diagnostics experience detailing which risk-based policy applied in sign-in Logs.
- Support the backup authentication system.

## Microsoft Entra multifactor authentication registration policy

ID Protection helps organizations roll out Microsoft Entra multifactor authentication using a policy requiring registration at sign-in. Enabling this policy ensures new users in your organization register for MFA on their first day. Multifactor authentication is one of the self-remediation methods for risk events within ID Protection. Self-remediation allows your users to take action on their own to reduce helpdesk call volume.

Learn more about Microsoft Entra multifactor authentication in the article, [How it works: Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-howitworks).