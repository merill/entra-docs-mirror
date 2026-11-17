---
layout: Conceptual
title: Account Recovery Overview in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-account-recovery-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rogulati
ms.author: rogulati
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Account recovery in Microsoft Entra ID enables users to regain access through identity verification when all authentication methods are lost. Learn how it works.
ms.reviewer: tilarso
ms.topic: concept-article
ms.custom: sfi-ga-nochange, sfi-image-nochange, msecd-doc-authoring-1026
ms.date: 2026-11-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 36b6bcb5-7610-311a-3928-8fab63baf0aa
document_version_independent_id: 36b6bcb5-7610-311a-3928-8fab63baf0aa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-account-recovery-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-account-recovery-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-account-recovery-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4ebc6a1c-1cd4-e5cb-f880-7435e011033f
---

# Account Recovery Overview in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Account recovery is a Microsoft Entra ID capability that enables users to regain access to their organizational accounts when they lose all registered authentication methods — such as when a primary device is lost, stolen, or compromised. Unlike self-service password reset (SSPR), which requires users to retain at least one authentication method, account recovery re-establishes trust in a user's identity through third-party identity verification before restoring access.

Account recovery uses automated identity proofing to reduce reliance on manual help desk verification. Social engineering attacks can manipulate support staff into granting unauthorized access. Account recovery helps reduce that risk by using government-issued identification and biometric verification through certified identity verification providers.

## Account recovery fundamentals

Account recovery is an authentication recovery mechanism for scenarios where users face complete authentication lockout — all registered methods are unavailable, and traditional self-service options can't help.

### Key characteristics

- **Identity-centric** — Shifts recovery from *what you know* (passwords) and *what you have* (devices, security keys) to *who you are* through comprehensive identity verification using government-issued ID and biometrics.
- **Trust re-establishment** — Treats recovery as a re-onboarding scenario. The organization verifies and re-establishes trust in the user's identity before granting access to register new authentication methods.
- **Built on Verified ID** — Uses Microsoft Entra Verified ID and Face Check alongside third-party identity verification providers available through the Microsoft Security Store.
- **Profile-based configuration** — Admins create identity verification profiles that define recovery behavior per user population — including which provider performs verification, what recovery mode applies, and how account validation works.

### When to use account recovery

- **Device loss or theft** — A user loses the phone or security key that contains their authenticator app, passkey, or other authentication methods.
- **Complete authentication lockout** — All registered authentication methods become unavailable simultaneously.
- **Account compromise response** — A security incident requires a complete authentication method reset as part of incident response.

### Account recovery compared to self-service password reset

Although account recovery and SSPR both restore user access, they address different scenarios:

| Aspect | Self-service password reset (SSPR) | Account recovery |
| --- | --- | --- |
| **Primary use case** | User forgot password but retains access to authentication methods | User lost access to all authentication methods |
| **Authentication requirement** | At least one registered method (policy can require up to two) | Identity verification through a certified provider |
| **Trust assumption** | User's identity is verified through existing methods | User's identity must be re-established |
| **Recovery scope** | Password only | Access to register replacement authentication methods |
| **Technology dependency** | Existing multifactor authentication (MFA) methods | Identity verification services, Verified ID |
| **Security level** | Medium — relies on pre-registered methods | High — requires comprehensive identity proofing |

### Business benefits

- **Reduced help desk burden** — Secure self-service recovery for total lockout scenarios reduces high-priority support tickets that require manual intervention.
- **Improved user experience** — Users recover accounts independently without waiting for help desk availability, reducing downtime during critical situations.
- **Stronger security posture** — Identity verification provides stronger assurance than traditional recovery methods that rely on social engineering-vulnerable information.
- **Scalable for remote work** — Organizations support distributed workforces without requiring physical presence or complex manual verification.

Tip

The Account Recovery overview page in the Microsoft Entra admin center includes a **cost savings estimator** that helps organizations project potential savings by comparing traditional help desk recovery costs against self-service account recovery.

## How account recovery works

Account recovery operates through a structured identity verification and trust re-establishment process that starts at sign-in.

### Core components

- **Identity verification providers (IDV)** — Trusted third-party services that validate user identity using government-issued documents, biometric verification, and other high-assurance methods. These providers issue verifiable credentials that attest to the user's verified identity. Providers are available through the [Microsoft Security Store](https://securitystore.microsoft.com/).
- **Microsoft Entra Verified ID** — The decentralized identity service that enables users to present cryptographically secure identity credentials during recovery. These credentials provide tamper-evident proof of identity verification without exposing sensitive personal information. For more information, see [Introduction to Microsoft Entra Verified ID](/en-us/entra/verified-id/decentralized-identifier-overview).
- **Identity verification profiles** — Configuration objects in the Microsoft Entra admin center that define how account recovery works for a specific group of users. Each profile specifies the recovery mode, target user groups, identity verification provider, and account validation rules. Organizations can create multiple profiles to support different user populations with different requirements.
- **Custom authentication extensions** — Optional Azure Function, Logic App, or REST API endpoints that add organization-specific account validation logic during recovery. Verified claims from the identity verification provider are passed to the extension, which validates them against organizational data such as a human resources information system (HRIS) or an employee directory. Extensions should use managed identities or other secretless authentication for service-to-service communication. All data processed by the extension stays within the organization's trust boundary — no organizational data is shared with Microsoft.

### Recovery flow

The account recovery process combines multiple verification layers to ensure that only legitimate account owners regain access.

### Account discovery

The user provides their account identifier at sign-in and indicates they can't access their account. The system checks whether the account is eligible for recovery based on the identity verification profiles configured by the tenant administrator, then directs the user to the appropriate identity verification provider.

### Identity verification

The user is redirected to the identity verification provider specified in their applicable profile. The provider verifies government-issued identification documents using advanced fraud detection. Liveness checks and facial recognition confirm the person is physically present. Upon successful verification, the user receives a verifiable credential (Verified ID) stored in Microsoft Authenticator.

### Credential validation

The user presents their newly acquired Verified ID to Microsoft Entra ID. The system validates the credential's authenticity. Account validation then uses the profile's configured directory claim mappings, a custom authentication extension, or both.

### Access restoration

By default, the user receives a Temporary Access Pass (TAP) with limited validity and is guided through registering new authentication methods, such as passkeys. For the preview option to register without a TAP on supported devices, see Registration with or without a TAP.

## Identity verification profiles

Identity verification profiles are the central configuration object for account recovery. Each profile defines:

- **Profile name and description** — A friendly name to identify the profile's purpose.
- **Recovery mode** — Whether the profile operates in Evaluation mode (testing only — accounts are not recovered) or Production mode (full recovery enabled).
- **User group scope** — Included groups define the profile's scope. Excluded groups are excluded globally across all identity verification profiles.
- **Identity verification provider** — The third-party provider that performs identity proofing for users in this profile.
- **Account validation rules** — How identity claims are validated through configured directory mappings (**Matches exactly** or **Contains** for name matching), a custom authentication extension, or both.

Organizations create multiple profiles to address different requirements across their user populations. For example, a profile for corporate employees might use a different identity verification provider or stricter validation rules than a profile for frontline workers.

### Evaluation and production modes

Each identity verification profile operates in one of two modes:

- **Evaluation** — Users can test the identity verification flow to confirm it works correctly. Accounts are **not** recovered in this mode. Use Evaluation mode to validate the experience with a small group before enabling full recovery.
- **Production** — Users who complete identity verification can fully recover their accounts, receive a Temporary Access Pass by default, and re-enroll authentication methods.

Start with Evaluation mode for new profiles to confirm the identity verification flow works for your users and policies before switching to Production.

Note

Identity verification involves processing government-issued documents and biometric data through third-party providers. Review your organization's privacy, data retention, and regional compliance requirements before deploying account recovery.

### Account validation and custom authentication extensions

For profiles that use first-name and last-name directory matching, identity claims are checked against the corresponding user properties in Microsoft Entra ID. The name-matching confidence levels described here are:

- **Matches exactly** — Claims must match exactly.
- **Contains** — Uses cross-field word matching to accommodate variations in names.

These options were previously named **Exact** and **Relaxed**, respectively. The labels changed, but the matching behavior is unchanged.

Tip

For sensitive user populations, consider enabling a custom authentication extension to validate additional claims beyond first and last name. Name-only matching may not provide sufficient assurance for high-risk accounts.

Custom authentication extensions can supplement directory matching or replace it entirely. During recovery, verified claims from the identity verification provider are passed to an organization-owned endpoint — an Azure Function, Logic App, or REST API — which validates them against authoritative data sources such as:

- HRIS systems (employee records)
- Employee directories
- Badge management systems
- Other organization-owned data stores

Important

Data processed by the custom authentication extension stays within the organization's trust boundary. No organizational data is shared with Microsoft — only the match result is returned to the account recovery flow.

## Understand shared profiles and registration options

Recovery requires identity verification. Configure the tenant's Account recovery policy, identity verification profiles, recovery settings, and Conditional Access scope.

### Tenant-level recovery enablement

In the new Account recovery policy experience, the policy is disabled by default for both new and existing tenants. Enable the policy before users can recover their accounts. Tenants that used an earlier preview also need to enable the new policy to continue using recovery; existing profiles alone aren't sufficient.

Tenant-level enablement is separate from TAP issuance and stale-credential cleanup. See [Enable the Account recovery policy](how-to-account-recovery-enable#enable-the-account-recovery-policy).

### Shared profiles and recovery settings

Manage shared profiles in **Verified ID** &gt; **ID verification profiles** &gt; **Profiles**. Tenant-level recovery enablement and actions after recovery are configured in the Account recovery settings blade.

Use [Create an ID verification profile](../../verified-id/how-to-create-id-verification-profile) for shared profile setup and [Configure recovery settings](how-to-account-recovery-enable#configure-recovery-settings) to choose a registration path.

### Registration with or without a TAP (preview)

TAP issuance is on by default for new and existing tenants. This default controls the registration path when recovery is enabled; it doesn't enable the tenant's Account recovery policy. An explicit preview option lets you turn issuance off.

| Path after successful validation | Registration experience |
| --- | --- |
| TAP issuance on | Issue a TAP and use the established authentication method registration flow. |
| TAP issuance off | Continue to registration within the same recovery session without receiving a TAP on supported devices. When passkey attestation is required, this path is supported only on Android; iOS continues to receive a TAP. |

Stale-credential cleanup is off by default and requires explicit preview opt-in with TAP issuance off. Turning TAP issuance back on turns cleanup off before saving. When enabled, cleanup deletes all previously registered authentication methods after successful recovery and registration of the replacement passkey. It preserves the new passkey. If deletion fails, recovery remains successful.

Note

When passkey attestation is required, turning off TAP issuance is supported only on Android. iOS continues to receive a TAP, even when TAP issuance is turned off, because the TAP-free registration path doesn't support attestation on iOS.

### Conditional Access and verification evidence

You can also apply Conditional Access to onboarding and recovery, adding an extra layer of security to the recovery flow. See [Protect onboarding and recovery with Conditional Access](../conditional-access/policy-require-identity-verification#configure-an-onboarding-and-recovery-policy) for configuration guidance.

Note

**Terms of use**, **Require authentication strength**, and most other Microsoft Entra-specific controls aren't supported for the onboarding and recovery user action. Review the [control limitations](../conditional-access/policy-require-identity-verification#review-control-limitations) and test policy enforcement before rollout.

Identity verification status shows the user's current verification state, and verification history records the user's verification events. Successful recovery writes verification history to the user's account. When the user registers a passkey during recovery, credential provenance is recorded on that passkey to describe how it was established. For more information, see [User verification status and history](concept-authentication-methods-manage#identity-verification-status-and-history) and [Passkey credential provenance](concept-authentication-passkeys-fido2#credential-provenance).

Note

During preview, credential provenance is recorded only for passkey credentials.