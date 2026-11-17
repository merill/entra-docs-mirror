---
layout: Conceptual
title: User self-remediation with Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/concept-identity-protection-user-experience
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: tilarso
ms.author: tilarso
ms.service: entra-id-protection
manager: dougeby
description: How can users self-remediate risk when administrators allow it? What is the experience when they don't?
ms.topic: concept-article
ms.date: 2026-11-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: chuqiaoshi
ms.custom: sfi-image-nochange, msecd-doc-authoring-108
locale: en-us
document_id: d513bc5e-0ae0-b612-2ad5-55f862660958
document_version_independent_id: 02c42630-37e9-88f6-09ce-29263188a3c6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/concept-identity-protection-user-experience.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/concept-identity-protection-user-experience
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/concept-identity-protection-user-experience.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 5973432d-dc70-d312-0e22-4517ef947e08
---

# User self-remediation with Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn

With Microsoft Entra ID Protection and Conditional Access, you can:

- Require users to register for Microsoft Entra multifactor authentication
- Automate remediation of risky sign-ins and compromised users
- Block users in specific cases.

Conditional Access policies that integrate user and sign-in risk affect the sign in experience for users. Allowing users to use tools like Microsoft Entra multifactor authentication + secure password change or self service password reset (SSPR) can lessen the impact. These tools, along with the appropriate policy choices, give users a self-remediation option when they need it while still enforcing strong security controls.

## Multifactor authentication registration

When an administrator enables the ID Protection policy requiring Microsoft Entra multifactor authentication registration, users can use Microsoft Entra multifactor authentication to self-remediate. Configuring this policy gives users a 14-day period to register, after which they're forced to register.

### Registration interrupt

1. At sign-in to any Microsoft Entra integrated application, the user gets a notification about the requirement to set up the account for multifactor authentication. This policy is also triggered in the Windows Out of Box Experience for new users with a new device.

    ![A screenshot showing the more information required prompt in a browser window.](media/concept-identity-protection-user-experience/identity-protection-experience-more-info-mfa.png)
2. Complete the guided steps to register for Microsoft Entra multifactor authentication and sign in.

## Risk self-remediation

When an administrator configures risk-based Conditional Access policies, affected users are interrupted when they reach the configured risk level. If administrators allow self-remediation using multifactor authentication, this process appears to a user as a normal multifactor authentication prompt.

If the user completes multifactor authentication, their risk is remediated and they can sign in.

[![A screenshot showing a multifactor authentication prompt at sign in.](media/concept-identity-protection-user-experience/conditional-access-mfa-prompt.png)](media/concept-identity-protection-user-experience/conditional-access-mfa-prompt.png#lightbox)

If the user is at risk, not just the sign-in, administrators can configure a user risk policy in Conditional Access to require a password change in addition to multifactor authentication. In that case, the user sees the following extra screen.

[![A screenshot showing the password change is required prompt when user risk is detected.](media/concept-identity-protection-user-experience/conditional-access-password-change-prompt.png)](media/concept-identity-protection-user-experience/conditional-access-password-change-prompt.png#lightbox)

### Adaptive risk remediation

The adaptive risk remediation policy accommodates all authentication methods, including password-based and passwordless. The grant controls for this policy automatically include **Require authentication strength** and **Sign-in frequency - Every time** to ensure that users are prompted to reauthenticate after their sessions are revoked. For more information, see [concept-identity-protection-policies#require-risk-remediation-control-preview].

When a user is required to remediate risk with this policy turned on, users must sign in immediately after their sessions are revoked. If the user just signed in but they're at risk, they'll be prompted to sign in again. The risk is remediated after the user successfully signed in the second time.

### Identity verification for risk

When a risk-based Conditional Access policy uses **Require Identity Verification (preview)**, users who meet the configured user-risk or sign-in-risk condition complete an identity verification challenge. An eligible [identity verification profile](../identity/authentication/concept-authentication-verified-id#create-and-manage-identity-verification-profiles), provider, and credential type are prerequisites. A recovery profile isn't automatically eligible for risk remediation.

The following illustrative example shows the **Additional verification required** interrupt. Use the credential type supported by your scenario's profile.

[![Illustrative identity verification interrupt for john.doe@contoso.com, prompting the user to continue in Microsoft Authenticator.](media/concept-identity-protection-user-experience/conditional-access-identity-verification-prompt.png)](media/concept-identity-protection-user-experience/conditional-access-identity-verification-prompt.png#lightbox)

This journey is independent of the adaptive **Require risk remediation** flow. Don't assume that the verification challenge revokes sessions or requires the same reauthentication sequence as adaptive remediation.

To validate the journey with an approved test user:

1. Confirm that the expected risk policy applies and presents the intended verification challenge.
2. Complete the requested credential presentation and verification. If you need a credential, follow the supported issuance path for that credential type. Credential issuance alone isn't completion of verification.
3. Return to, or restart, the original access attempt as directed by the journey. Test cancellation, verification failure, and missing or unavailable credentials separately.
4. Check the access decision and verification result independently. If you can't complete verification, use your organization's support path.

Successful verification remediates user risk or sign-in risk, depending on the risk condition in the triggering policy. Failed verification doesn't remediate risk. Administrators [check the targeted risk record separately](howto-identity-protection-remediate-unblock#validate-identity-verification-remediation); access or verification success doesn't establish that every risk was cleared.

### Risky sign-in administrator unblock

Administrators might block users upon sign-in depending on their risk level. To get unblocked, users must contact their IT staff or try signing in from a familiar location or device. Self-remediation isn't an option in this case.

[![A screenshot showing your account is blocked screen.](media/concept-identity-protection-user-experience/conditional-access-blocked.png)](media/concept-identity-protection-user-experience/conditional-access-blocked.png#lightbox)

IT staff can follow the instructions in [Unblocking users](howto-identity-protection-remediate-unblock#unblock-users) to allow users to sign back in.

## High risk technician

If the home tenant didn't enable self-remediation policies, an administrator in the technician's home tenant must remediate the risk. For example:

1. An organization has a managed service provider (MSP) or cloud solution provider (CSP) who takes care of configuring their cloud environment.
2. One of the MSPs technicians credentials are leaked and triggers high risk. That technician is blocked from signing in to other tenants.
3. The technician can self-remediate and sign in if the home tenant enabled the appropriate policies [requiring password change for high risk users](../identity/conditional-access/policy-risk-based-user) or [MFA for risky users](../identity/conditional-access/policy-risk-based-sign-in).
    - If the home tenant didn't enable self-remediation policies, an administrator in the technician's home tenant has to [remediate the risk](howto-identity-protection-remediate-unblock).