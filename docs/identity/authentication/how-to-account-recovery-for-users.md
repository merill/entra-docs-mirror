---
layout: Conceptual
title: Perform Account Recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-account-recovery-for-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how end users can recover their Microsoft Entra ID accounts through identity verification when all authentication methods are lost. Follow the step-by-step recovery process.
ms.topic: how-to
ms.date: 2026-04-02T00:00:00.0000000Z
ms.reviewer: tilarso
ms.custom: sfi-ga-nochange, sfi-image-nochange, msecd-doc-authoring-1012
locale: en-us
document_id: 7a93b2d0-1bcb-52dc-0ac2-9e5e10088d76
document_version_independent_id: 7a93b2d0-1bcb-52dc-0ac2-9e5e10088d76
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-account-recovery-for-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-account-recovery-for-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-account-recovery-for-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: c07752aa-0f4f-1f97-f66d-b8b26241c52a
---

# Perform Account Recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Users can recover their accounts in a few simple steps. This article describes how users discover and start the account recovery process and what to expect during identity verification through an organization's configured provider.

## Video: Recover your work or school account in Microsoft Entra ID

## User steps

1. Start by attempting to sign in to an application such as Microsoft Teams or directly at https://login.microsoftonline.com.
2. You're presented with an initial authentication method to sign in with.
3. As you're unable to use this method, select **Other ways to sign in**. You're presented with additional sign-in options.
4. If you're unable to sign in with any methods, select **Recover your account**.

    [![Screenshot that shows how to sign in to set up account recovery.](media/how-to-account-recovery-for-users/sign-in.png)](media/how-to-account-recovery-for-users/sign-in.png#lightbox)
5. You're presented with an informational screen that explains the account recovery process and provides guidance to complete identity verification through the organization's configured external identity proofing service.
6. You're redirected to the identity proofing service configured by your organization, and you start the identity proofing process.

    Note

    The specific steps required for identity verification may vary depending on the identity verification partner configured by your organization. Below are common steps which a provider may present to a user.
7. Open the camera on your mobile device, and scan the QR code on the website of the identity proofing application.
8. After the identity proofing application or page opens on your mobile device, select **Continue**.
9. Enter your name and email, agree to the terms of use for the app, and select **Continue**.
10. Choose your country/region, and the type of identity verification document you have, such as a **Passport** or **Driver's License**.
11. Review how to take a clear document photo, and select **Continue** after you read each step.
12. After you take the photo, select **Submit photos**.
13. Review how to take a clear photo of your face, and select **Continue** after you read each step.
14. After you take the photo, the identity proofing application or page verifies your identity, and will issue a Verifiable Credential into your Microsoft Authenticator app.

    Note

    This may be presented by the provider as an option such as **Add a Verified ID** or **Open in Authenticator**.
15. When you're prompted, select **Open** and unlock Microsoft Authenticator.
16. You're asked to complete a quick Face Check before your account ownership can be validated.
17. When the process is complete, you get a Temporary Access Pass. Copy this code and select **Sign in**.
18. Finally, you're redirected to [Security info](https://mysignins.microsoft.com/security-info), where you can register a new authentication method and fully regain access.

    [![Screenshot that shows how to create a passkey for account recovery.](media/how-to-account-recovery-for-users/create-passkey.png)](media/how-to-account-recovery-for-users/create-passkey.png#lightbox)

## Troubleshooting

### User can't recover their account in Evaluation mode

When a profile is in the default Evaluation mode, the user sees the following screen after user verification passes with the identity verification (IDV) provider and Face Check. This experience is expected in Evaluation mode. An Authentication Policy Administrator needs to place users in Production mode before they can be issued a Temporary Access Pass (TAP).

[![Screenshot that shows the profile for a user is in Evaluation mode.](media/how-to-account-recovery-for-users/policy-evaluation-mode.png)](media/how-to-account-recovery-for-users/policy-evaluation-mode.png#lightbox)

### User not issued a TAP

If the user sees a red error message on the TAP screen and doesn't get a TAP issued, confirm that the claims ID info and Microsoft Graph match the real name.

[![Screenshot that shows a red error message on the TAP screen.](media/how-to-account-recovery-for-users/mismatch.png)](media/how-to-account-recovery-for-users/mismatch.png#lightbox)

### User might not see the Recover your account option when they choose other ways to sign in

Account recovery is designed for actively used accounts that have prior authentication events. After you enable or change the scope of account recovery, users might need to complete an initial authentication before the recovery option is made available. If evaluating recovery with a test account, ensure the user authenticates first before attempting account recovery.

If you still don't see the **Recover your account** when you sign in later, make sure that the group you include in the account recovery profile (for example, Engineering) has all the users you want to allow for self-service recovery in it. If they aren't part of the selected group, then they won't be offered the recovery task during login.

[![Screenshot that shows how to choose another way to sign in.](media/how-to-account-recovery-for-users/choose-way-to-sign-in.png)](media/how-to-account-recovery-for-users/choose-way-to-sign-in.png#lightbox)

### User might get an error stating requests can't be completed at the start of recovery

This happens when the identity verification provider set up in account recovery is unavailable or there are issues with the Security Store. Admins should review the account recovery configuration and Security Store status for the provider.

[![Screenshot that shows an error and to try again.](media/how-to-account-recovery-for-users/try-again-later.png)](media/how-to-account-recovery-for-users/try-again-later.png#lightbox)

### Identity verification provider errors

During document verification, the identity verification (IDV) provider might have trouble reading the photo image of a government document or driver's license upload or selfie. Overhead lights or glare from a window can make it difficult to photograph plastic cards and still see all the data for the IDV to process.

The identity verification provider commonly does their own facial biometric checks against the photo in the ID you uploaded.

Sometimes changing the lighting environment or using a different available government document can help.

[![Screenshot that shows a name mismatch error during identity verification provider document validation.](media/how-to-account-recovery-for-users/mismatch.png)](media/how-to-account-recovery-for-users/mismatch.png#lightbox)

### Errors when completing Face Check

Face Check's performance can be influenced by the user's lighting conditions and background during capture. In the event of a failure, the event log allows administrators to review the confidence score achieved by Face Check. For improved results, users are advised to conduct Face Check in darker environments, away from bright windows and lights.

Face Check includes an active mode designed to adapt to excessively bright settings; this mode utilizes user posture cues to enhance accuracy under challenging lighting conditions.

[![Screenshot that shows common errors during account recovery.](media/how-to-account-recovery-for-users/errors.png)](media/how-to-account-recovery-for-users/errors.png#lightbox)

As part of account recovery, the photo in the presented Verified ID is matched against the active Face Check. The photo in the Verified ID may be problematic if it's too blurry or low quality, though it's usually fine since it comes from a government document and identity verification provider process. Check the Verified ID photo in the Microsoft Authenticator wallet to ensure it's clear enough for accurate face comparison.

[![Screenshot that shows photo match.](media/how-to-account-recovery-for-users/photo.png)](media/how-to-account-recovery-for-users/photo.png#lightbox)

### Temporary Access Pass code issues following Identity Verification document validation

After the user has shared their Verified ID with Microsoft Entra, we attempt an account validation and match against the verified claims in the ID issued by your Identity Verification Provider. This error may be present when account ownership couldn't be confirmed—often due to mismatches between the first and last names in the user's profile and those on the ID. Differences such as "John" versus "Jonathan", or complex surnames, might cause these issues. Admins can resolve this during the preview by updating profile information. Another possible cause is improper Temporary Access Pass issuance group configuration for users in recovery. Check the Authentication methods policy and confirm that users in scope for recovery are also enabled for the Temporary Access Pass method.

### Passkey not issued

Once the user is fully verified and is redirected to MySignIns to register a new credential, any passkey registration failures should be evaluated through review of audit logs. For more guidance, see [How to register passkeys (FIDO2)](how-to-register-passkey).

For synced passkeys, ensure the device's operating system is updated, as these passkeys are native to the operating system. If no new authentication method is registered before the Temporary Access Pass expires, the user must restart account recovery to get a new Temporary Access Pass.

[![Screenshot that shows an error when a passkey isn't registered.](media/how-to-account-recovery-for-users/passkey-not-registered.png)](media/how-to-account-recovery-for-users/passkey-not-registered.png#lightbox)