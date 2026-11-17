---
layout: FAQ
title: Frequently asked questions about account recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/self-service-account-recovery
summary: >
  <p>The following are frequently asked questions about account recovery in Microsoft Entra ID. For questions not answered here, ask the community on the <a href="/answers/topics/azure-active-directory.html">Microsoft Q&amp;A question page for Microsoft Entra ID</a>.</p>

  <p>This FAQ covers:</p>

  <ul>

  <li><a href="#how-account-recovery-works">How account recovery works</a></li>

  <li><a href="#identity-verification-profiles">Identity verification profiles</a></li>

  <li><a href="#account-validation-and-custom-authentication-extensions">Account validation and custom authentication extensions</a></li>

  <li><a href="#identity-verification-provider--idv--selection-and-usage">Identity verification provider (IDV) selection and usage</a></li>

  <li><a href="#troubleshooting">Troubleshooting</a></li>

  <li><a href="#shared-profiles-and-registration-options">Shared profiles and registration options</a></li>

  </ul>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: tilarso
ms.author: tilarso
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Find answers about Microsoft Entra ID account recovery, identity verification profiles, registration options, licensing, and troubleshooting.
ms.reviewer: tilarso
ms.topic: faq
ms.custom: msecd-doc-authoring-108, msecd-doc-authoring-1026
ms.date: 2026-11-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 151ff69c-d586-0a5e-ad16-7faabd5effb5
document_version_independent_id: 151ff69c-d586-0a5e-ad16-7faabd5effb5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/self-service-account-recovery.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/self-service-account-recovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/self-service-account-recovery.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 201c67ba-3b1a-d856-09c6-c29fbb1e4919
---

# Frequently asked questions about account recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The following are frequently asked questions about account recovery in Microsoft Entra ID. For questions not answered here, ask the community on the [Microsoft Q&A question page for Microsoft Entra ID](/en-us/answers/topics/azure-active-directory.html).

This FAQ covers:

- How account recovery works
- Identity verification profiles
- Account validation and custom authentication extensions
- Identity verification provider (IDV) selection and usage
- Troubleshooting
- Shared profiles and registration options

## How account recovery works

### Is account recovery enabled by default?

No. In the new Account recovery policy experience, the policy is disabled by default for both new and existing tenants. Enable the tenant's policy before users can use account recovery.

Tenant-level enablement is separate from actions after recovery. Temporary Access Pass (TAP) issuance being on by default doesn't mean that account recovery is enabled. See [Enable the Account recovery policy](how-to-account-recovery-enable#enable-the-account-recovery-policy).

### Do existing preview tenants need to enable the new Account recovery policy?

Yes. If your tenant already uses account recovery from an earlier preview, enable the new policy to continue using the feature. Existing identity verification profiles alone don't enable the new policy. See [Enable the Account recovery policy](how-to-account-recovery-enable#enable-the-account-recovery-policy).

### Does account recovery support B2B users, external guest users, or federated users?

No. Account recovery doesn't support B2B users, external guest users, or federated users.

### What license is required to use account recovery?

Users need a [Microsoft Entra ID P1 license](https://www.microsoft.com/security/business/microsoft-entra-pricing) to use account recovery. A [Face Check license](/en-us/entra/verified-id/using-facecheck) is also required, either through Entra Suite or standalone. The identity verification provider cost depends on the offer you subscribe to in the Microsoft Security Store.

### Where does user data go during the identity verification process?

Identity verification providers have their own privacy and data retention policies as part of the verification offer from the Microsoft Security Store. For details, see your provider's documentation.

### How is the Verified ID matched against Microsoft Entra ID account details?

Account recovery first verifies proof of presence by comparing the photo on the user's government-issued ID to a real-time [Face Check](/en-us/entra/verified-id/using-facecheck).

For profiles configured to use first-name and last-name directory matching, the system compares those credential claims with the corresponding Microsoft Entra ID user properties. This name-matching configuration doesn't use **Display name** or **User principal name**. Other profile configurations can use different claim mappings or extension-only validation.

The name-matching confidence levels described here are:

- **Matches exactly** — The first name and last name from the verified credential must match the user's **First name** and **Last name** properties in Microsoft Entra ID exactly.
- **Contains** — Uses cross-field word matching to accommodate variations in how names appear on government-issued documents versus Microsoft Entra ID user profiles.

**How Contains matching works**

Government-issued documents — particularly passports — may contain a user's full legal name in a single field without distinguishing between first name and last name. Some identity verification providers place the full name entirely in the first name or last name claim of the verified credential. Additionally, a user's Microsoft Entra ID profile may contain only a subset of the names in their full legal name. For example, a user whose passport reads "Maria Elena Garcia Lopez" might have only "Maria" as the **First name** and "Garcia" as the **Last name** in their Microsoft Entra ID profile.

To handle these variations, **Contains** matching uses the following logic:

- The **First name** property in Microsoft Entra ID must match **any word** in either the first name or last name claim from the verified credential.
- **AND** the **Last name** property in Microsoft Entra ID must match **any word** in either the first name or last name claim from the verified credential.
- Both conditions must be true for the match to succeed.

In the example above, "Maria" matches a word in the verified credential's first name claim ("Maria Elena"), and "Garcia" matches a word in the last name claim ("Garcia Lopez") — so the match succeeds even though the Microsoft Entra ID profile contains only a subset of the full legal name.

This approach allows successful matching when names are split differently between the verified credential and Microsoft Entra ID, or when a user profile contains a subset of the full legal name on the government-issued document.

If a profile requires name matching and the match fails, the user can't complete recovery and needs to follow their normal help desk process.

Custom authentication extensions can validate claims against organizational data. An extension can supplement directory matching or replace it entirely.

**Matches exactly** and **Contains** were previously named **Exact** and **Relaxed**, respectively. The labels changed, but the matching behavior is unchanged.

### What happens when people with the same name try to recover an account?

Admins can use custom authentication extensions to process identity claims from the verification provider and compare them against organizational data, such as a human resources information system (HRIS) or employee directory. These checks help distinguish users with similar names.

Without a custom authentication extension, recovery attempts from users with the same name as another user may be blocked. To avoid this, enable a custom authentication extension on the identity verification profile and validate additional attributes beyond first and last name.

### Do I have to use a Temporary Access Pass (TAP) for account recovery?

TAP is required for the established recovery experience and remains on by default. An explicit preview option allows registration without a TAP on supported devices. When passkey attestation is required, TAP-free registration is supported only on Android; iOS continues to receive a TAP even when issuance is turned off. For details, see Is a Temporary Access Pass required when inline registration is enabled?

### What if the user doesn't have Microsoft Authenticator on their device?

During the recovery flow, the identity verification provider reminds the user to download the app if needed. Microsoft Authenticator just needs to be installed — the user doesn't have to sign in to it to store the Verified ID issued by the provider.

### Do Conditional Access policies apply during account recovery?

Yes. Conditional Access can add an extra layer of security during account recovery. Policies that block access or require unsupported controls can interrupt or block the recovery attempt, or leave intended requirements unenforced.

**Terms of use**, **Require authentication strength**, and most other Microsoft Entra-specific controls aren't supported for the onboarding and recovery user action. Review the [control limitations](../conditional-access/policy-require-identity-verification#review-control-limitations) before rollout.

Review and test your Conditional Access policies with a small group of users before you roll out account recovery more broadly.

### Should I enable account recovery for all users in my organization?

Account recovery supports a phased rollout through identity verification profiles. Each profile targets specific user groups, so you can start with a small test group in Evaluation mode and expand as you gain confidence.

A recommended approach:

- Create a profile in **Evaluation** mode targeting a small test group to validate the identity verification flow.
- Switch the profile to **Production** mode once testing confirms the flow works for your users.
- Create additional profiles for broader user populations as needed.

For certain accounts — such as those belonging to a CEO or finance controller — you might restrict recovery to in-person or remote processes that include a human in the loop. These accounts may not be appropriate for self-service recovery due to their sensitive nature.

### How do I estimate the cost of account recovery across my organization?

Account recovery requests typically affect about 1%–3% of users each month. The **cost savings estimator** in the Microsoft Entra admin center (under **Entra ID** &gt; **Account recovery**) helps you project potential savings. Enter your current helpdesk costs, target user count, and the cost per verification from your chosen provider. The estimator compares current spending with projected self-service recovery costs so you can model savings for your scenario.

## Identity verification profiles

### What is an identity verification profile?

An identity verification profile is a configuration object that defines how identity verification is set up for a specific group of users. Profiles control the verification method, which users are in scope, and how account validation is handled. Shared profiles support recovery, onboarding, and verification.

Each profile specifies:

- **User group scope** — Which users the profile applies to, defined by included and excluded groups
- **Identity verification provider** — The third-party provider that performs identity proofing
- **Account validation rules** — How identity claims are matched, including match confidence and optional custom authentication extension
- **Recovery mode** — For account recovery scenarios: Evaluation (testing) or Production (full recovery)

Create profiles in the Microsoft Entra admin center under **Verified ID** &gt; **ID verification profiles** &gt; **Profiles**. For the procedure, see [Create an ID verification profile](../../verified-id/how-to-create-id-verification-profile). Select **Recovery** as the purpose for account recovery.

### Can I create multiple identity verification profiles?

Yes. Organizations can create multiple profiles to support different user populations with different configurations. For example:

- A profile for corporate employees using one identity verification provider with strict matching
- A profile for frontline workers using a different provider with relaxed matching
- A profile in Evaluation mode for a pilot group testing a new provider

Each profile operates independently with its own user scope, provider, validation rules, and mode settings.

### What are Evaluation and Production modes?

Each identity verification profile operates in one of two modes:

- **Evaluation** — Users can test the identity verification flow to confirm it works correctly. Accounts are **not** recovered in this mode. Use Evaluation to validate the experience before enabling full recovery.
- **Production** — Users who complete identity verification can fully recover their accounts, receive a Temporary Access Pass by default, and re-enroll authentication methods.

Profile mode is configured in Microsoft Entra Verified ID, separately from the tenant's Account recovery policy and actions after recovery. For mode selection and validation, see [Create an ID verification profile](../../verified-id/how-to-create-id-verification-profile#choose-a-profile-mode).

### How do I set the priority when a user matches multiple profiles?

Open **Verified ID** &gt; **ID verification profiles** &gt; **Profiles** and use **Set priority**. When a user belongs to groups that match multiple profiles, the system evaluates profiles in priority order and applies the first matching profile.

## Account validation and custom authentication extensions

### What match confidence levels are available?

Configure a match rule for each claim-to-directory mapping in the ID verification profile. Review the available rules and test with known matching and nonmatching data rather than copying example selections. See [Review claim matching](../../verified-id/how-to-create-id-verification-profile#review-claim-matching).

### How do custom authentication extensions work with account recovery?

Custom authentication extensions add organization-specific account validation logic during the recovery process. When a user completes identity verification, the verified claims from the provider are passed to your organization's endpoint — an Azure Function, Logic App, or REST API — which validates them against authoritative data sources such as:

- HRIS systems (employee records)
- Employee directories
- Badge management systems

The extension returns a match decision to the account recovery flow. This enables validation beyond first and last name matching and helps disambiguate users with similar names.

Important

All data processed by the custom authentication extension stays within your organization's trust boundary. No organizational data is shared with Microsoft — only the match result is returned to account recovery.

### What do I need to set up a custom authentication extension?

To use a custom authentication extension with account recovery, you need:

- An Azure Function, Logic App, or REST API endpoint that can receive verified claims and return a match decision
- Access to your organization's authoritative data source (HRIS, employee directory, or similar)
- The endpoint registered as a custom authentication extension in Microsoft Entra ID

Enable the extension in the **Account validation** step of the identity verification profile wizard.

## Identity verification provider (IDV) selection and usage

### Can I bring my own IDV and contract to account recovery?

Account recovery only supports reviewed and approved providers through the [Microsoft Security Store](https://securitystore.microsoft.com/).

### Can I use my own IDV in the recovery flow?

Currently, account recovery only supports identity verification providers from the Microsoft Security Store. This ensures consistency in the recovery flow for users.

### Can I skip the IDV document verification if I already have a Verified ID from the provider?

In the most common total-lockout recovery scenario, the user doesn't have an existing Verified ID in their wallet because they're on a new device. Account recovery focuses on this most common case — acquiring a new Verified ID from the provider during recovery.

### If a user's government ID is denied by the IDV, what should they do?

As part of the IDV sign-up and provisioning process, the tenant receives contact instructions to work with the provider's support team to debug specific ID issuance failures for individual users.

### Does the IDV flow support mobile driver's licenses, European Digital Identity (EUDI), or electronic identification (eID)?

Currently, account recovery supports user verification through standard verified credentials with Microsoft Entra Verified ID.

## Troubleshooting

### I'm seeing "Application Management" errors for Core Directory in the admin audit logs.

These errors are unrelated to account recovery and can be safely ignored.

## Shared profiles and registration options

### Is a Temporary Access Pass required when inline registration is enabled?

A Temporary Access Pass (TAP) is required for the established recovery experience. TAP issuance remains **on by default** for new and existing tenants. An explicit preview option lets an administrator turn issuance off.

With TAP issuance off, successful account validation grants access to authentication method registration in the same recovery session without issuing a TAP on supported devices. When passkey attestation is required, this path is supported only on Android; iOS continues to receive a TAP. Confirm that the preview option and required registration path are available for your tenant and devices before enabling it.

Android support also depends on the work-profile configuration. For users enrolled through Android Management API (AM API), keep TAP issuance on and configure recovery to issue a TAP at completion instead of requiring passkey setup. Recovery remains supported for these users, but a device-bound passkey created in the personal profile can't currently be used from the work profile. Review [Enable passkeys in Microsoft Authenticator](how-to-enable-authenticator-passkey).

### Can recovery remove stale credentials?

**Stale credential cleanup** is off by default and requires explicit opt-in during preview. Cleanup is available only when TAP issuance is off. With TAP issuance on, cleanup is unavailable. Turning TAP issuance back on turns cleanup off before saving. Both controls are preview settings.

When cleanup is enabled, it deletes all previously registered authentication methods after both recovery and registration of the replacement passkey succeed. The newly registered passkey isn't deleted.

If cleanup fails, recovery remains successful. Partial-deletion behavior, retries, and required support actions still need confirmation.

### Where do I manage profiles and recovery settings?

Create and manage shared profiles in **Verified ID** &gt; **ID verification profiles** &gt; **Profiles**. The Account recovery settings blade contains tenant-level recovery enablement and actions after recovery, including TAP issuance and stale-credential cleanup.

For recovery setup, use [Configure account recovery settings](how-to-account-recovery-enable). For profile creation and provider selection, see [Create an ID verification profile](../../verified-id/how-to-create-id-verification-profile).

### Which devices can use the TAP-free path?

When passkey attestation is required, turning off TAP issuance is supported only on Android. iOS continues to receive a TAP, even when TAP issuance is turned off, because the TAP-free registration path doesn't support attestation on iOS. This limitation doesn't establish a complete device support matrix for other configurations.

Android alone doesn't establish eligibility. For users enrolled through Android Management API (AM API), configure recovery to issue a TAP at completion instead of requiring passkey setup. This Android work-profile limitation is separate from the iOS attestation limitation. See [Enable passkeys in Microsoft Authenticator](how-to-enable-authenticator-passkey) for app-version, provider, and profile requirements.

Until the supported combinations are verified, don't treat successful identity verification as proof that passkey registration can complete on that device.

### Does recovery support multiple custom authentication extensions?

No. Recovery currently supports one custom authentication extension. You can link the same extension to multiple identity verification profiles.

### Does a recovery profile configure Conditional Access scope?

No. A shared profile and a Conditional Access policy are separate configuration tasks. Configure policies targeting the **Account onboarding and recovery** user action separately from the profile.

See [Protect onboarding and recovery with Conditional Access](../conditional-access/policy-require-identity-verification#configure-an-onboarding-and-recovery-policy) for configuration guidance.

Policies targeting **All resources** can prevent users from completing account recovery. Review the [global onboarding and recovery exclusion](../conditional-access/policy-require-identity-verification#enable-the-global-onboarding-and-recovery-exclusion-preview). When enabled, it excludes onboarding and recovery events from **All resources** policies; policies directly targeting the user action still apply. Review the tenant-wide impact before enabling the exclusion.

**Terms of use**, **Require authentication strength**, and most other Microsoft Entra-specific controls aren't supported for the onboarding and recovery user action. Review the [control limitations](../conditional-access/policy-require-identity-verification#review-control-limitations) and test policy enforcement before rollout.

### What licenses and audit events apply to shared profiles and inline recovery?

The existing FAQ answer contains recovery and Face Check license guidance. For the expanded experience, see the [identity verification licensing requirements](../../fundamentals/licensing#identity-verification). Don't assume that implemented functionality establishes entitlement for every license tier.

Successful recovery writes verification history to the user's account. When the user registers a passkey during recovery, credential provenance is recorded on that passkey. During preview, credential provenance is recorded only for passkey credentials. See [Manage user authentication methods](concept-authentication-methods-manage) and [Passkeys (FIDO2)](concept-authentication-passkeys-fido2) for more information.

Possible recovery audit events include `Account recovery initiated`, `Account recovery completed`, and `Account recovery failed`, logged by the `Verified ID` service. An initiation event doesn't establish successful recovery. For the event list and interpretation guidance, see [Verified ID audit activities](../monitoring-health/reference-audit-activities#verified-id).