---
layout: Conceptual
title: Configure account recovery settings in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-account-recovery-enable
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rogulati
ms.author: rogulati
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Enable the Account recovery policy in Microsoft Entra ID and configure actions after recovery, including Temporary Access Pass issuance and stale credential cleanup.
ms.reviewer: tilarso
ms.topic: how-to
ms.custom: sfi-ga-nochange, sfi-image-nochange, msecd-doc-authoring-108, msecd-doc-authoring-1012, msecd-doc-authoring-1026
ms.date: 2026-11-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 92772aeb-f24b-9749-9f52-b24aeefe235f
document_version_independent_id: 92772aeb-f24b-9749-9f52-b24aeefe235f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-account-recovery-enable.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-account-recovery-enable
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-account-recovery-enable.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b5e832ac-6e6a-c207-d102-2d2b247b75e9
---

# Configure account recovery settings in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Account recovery settings control whether users can recover their accounts and how they register replacement authentication methods after identity verification. Use this article to enable the tenant's Account recovery policy, choose Temporary Access Pass (TAP) issuance and stale-credential cleanup settings, and test the recovery experience.

ID verification profiles are created and managed in Microsoft Entra Verified ID, separately from Account recovery settings.

Before you begin, prepare a recovery profile and confirm licensing, Face Check setup, and administrative permissions. See Prerequisites.

## Prerequisites

Before configuring recovery settings, prepare:

- A Microsoft Entra ID P1 license and the applicable [identity verification licenses](../../fundamentals/licensing#identity-verification).
- [Verified ID](../../verified-id/verifiable-credentials-configure-tenant-quick) enabled and [Face Check](../../verified-id/using-facecheck) configured in your tenant.
- The [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) role to manage Account recovery settings.
- An ID verification profile for recovery, configured in Microsoft Entra Verified ID, and a dedicated test group.
- Microsoft Authenticator version 6.2610.7075 or later for Android, or version 6.8.58 or later for iOS, installed on users' devices.
- Supported replacement authentication methods enabled for the users in scope. For the TAP-based path, confirm that users are enabled for the Temporary Access Pass method.

## Open Account recovery settings

To open the settings blade:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with permission to manage recovery settings.
2. Go to **Entra ID** &gt; **Account recovery**.
3. Open **Settings (preview)**.

## Configure an ID verification profile

Create and manage profiles in **Verified ID** &gt; **ID verification profiles** &gt; **Profiles**. For provider selection, user groups, profile mode, and account-validation steps, follow [Create an ID verification profile](../../verified-id/how-to-create-id-verification-profile). Select **Recovery** as the profile purpose.

Profile configuration isn't part of the Account recovery settings blade. Creating a profile doesn't enable the tenant's Account recovery policy or choose actions after recovery.

## Enable the Account recovery policy

In the new Account recovery policy experience, the policy is disabled by default for both new and existing tenants. Enable the policy before users can use account recovery.

If your tenant already uses account recovery from an earlier preview, you also need to enable the new policy to continue using the feature. Existing identity verification profiles alone don't enable the new policy.

To prepare tenant-level recovery:

1. In Account recovery settings, enable the tenant's Account recovery policy.
2. Confirm that the policy is enabled before testing recovery with users in scope.

Enabling the policy is separate from configuring actions after recovery, such as issuing a TAP or removing stale credentials. The default TAP issuance setting doesn't enable account recovery for your tenant.

## Configure recovery settings

Use **Actions after recovery** in Account recovery settings to choose how users register replacement methods. These settings are separate from tenant-level enablement and ID verification profile management.

First, enable the Account recovery policy. Confirm that the preview controls are available in your tenant before changing them.

| Setting | Behavior |
| --- | --- |
| **Issue Temporary Access Pass** on | Default for new and existing tenants. Successful account validation issues a TAP for the established registration flow. Stale-credential cleanup isn't available. |
| **Issue Temporary Access Pass** off | Explicit preview opt-in. Successful account validation grants access to registration in the same recovery session without a TAP on supported devices. When passkey attestation is required, this path is supported only on Android; iOS continues to receive a TAP. Stale-credential cleanup becomes available. |
| **Stale credential cleanup** | Off by default; explicitly opt in during preview with TAP issuance off. After successful recovery and replacement-passkey registration, deletes all previously registered authentication methods while preserving the new passkey. If deletion fails, recovery remains successful. Turning TAP issuance on turns cleanup off before saving. |

To choose the actions after recovery:

1. Review whether users should receive a TAP or continue to registration without a TAP on supported devices.
2. Choose the TAP issuance setting for the intended registration path.
3. If TAP issuance is off, review the scope and timing of stale-credential cleanup before explicitly enabling it.
4. If you turn TAP issuance back on, confirm that cleanup is off before saving the settings.
5. Apply your settings and test recovery through registration of a replacement method, not just successful identity verification.

Note

When passkey attestation is required, turning off TAP issuance is supported only on Android. iOS continues to receive a TAP, even when TAP issuance is turned off, because the TAP-free registration path doesn't support attestation on iOS.

## Test recovery settings

Use a small test group to validate the selected registration path:

1. Confirm the recovery profile's mode and user scope in Microsoft Entra Verified ID. **Evaluation** tests verification without recovering the account; use **Production** only for a deliberate end-to-end recovery test.
2. Confirm that the tenant's Account recovery policy is enabled.
3. Complete identity verification and account validation with a test user.
4. With TAP issuance on, confirm that the user receives a TAP and can register a replacement authentication method.
5. With TAP issuance off, validate the required device and registration-method combination. If passkey attestation is required, use Android for the TAP-free path; iOS continues to receive a TAP.
6. Confirm that replacement-method registration completes. Successful identity verification alone doesn't establish that recovery is complete.

Caution

Review which users are in scope before using a recovery profile in Production mode. Confirm that only the intended test users can participate before expanding the deployment.

For the user journey, see [Perform account recovery](how-to-account-recovery-for-users).

## Review policy and extension integration

Use Conditional Access to protect the **Account onboarding and recovery** user action. Review targeting and exclusions with your policy owner so that unrelated access requirements don't block the recovery journey. See [Protect onboarding and recovery with Conditional Access](../conditional-access/policy-require-identity-verification#configure-an-onboarding-and-recovery-policy) for configuration guidance.

Review the [global onboarding and recovery exclusion](../conditional-access/policy-require-identity-verification#enable-the-global-onboarding-and-recovery-exclusion-preview) with your Conditional Access policy owner. This tenant-wide setting excludes the combined onboarding and recovery user action from **All resources** policies. Policies targeting the user action still apply, and ordinary application access remains subject to resource-access policies. Configure and test the intended user-action policy rather than using the exclusion as a replacement for protecting recovery.

Conditional Access policies can block account recovery if they require controls that aren't supported for the onboarding and recovery user action.

Note

**Terms of use**, **Require authentication strength**, and most other Microsoft Entra-specific controls aren't supported for the onboarding and recovery user action. Unsupported recovery policy requirements can block recovery or leave intended requirements unenforced. Review the [control limitations](../conditional-access/policy-require-identity-verification#review-control-limitations) and test policy enforcement before rollout.

Before enabling account recovery, review your Conditional Access policies and test the recovery experience with a small group of users. Successful identity verification alone doesn't confirm that recovery can complete.

If recovery is blocked, review the Conditional Access results in the sign-in logs to identify the blocking policy.

If you can't save the Conditional Access policy, review [Policy configuration errors](../conditional-access/policy-require-identity-verification#troubleshoot-onboarding-and-recovery-policy-configuration-errors) for client-app and named-location validation guidance. Policy-save errors are separate from a saved policy blocking recovery.

Configure custom claim validation in the [ID verification profile](../../verified-id/how-to-create-id-verification-profile#configure-an-optional-custom-extension), not in recovery settings.

Recovery currently supports one custom authentication extension. You can link the same extension to multiple identity verification profiles.