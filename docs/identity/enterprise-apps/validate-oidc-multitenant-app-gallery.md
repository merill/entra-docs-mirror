---
layout: Conceptual
title: Validate an OIDC multitenant app for Microsoft Entra App Gallery onboarding - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/validate-oidc-multitenant-app-gallery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: hkinyunyu
ms.service: entra-id
ms.subservice: enterprise-apps
manager: mwongerapk
description: Use the Microsoft Entra App Validator browser extension to validate your OpenID Connect multitenant app and generate a Test ID for app gallery publishing.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
ms.reviewer: hkinyunyu
ms.custom: enterprise-apps-article, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2b04834e-7043-1e64-518f-9cc3c4ad2bb4
document_version_independent_id: 2b04834e-7043-1e64-518f-9cc3c4ad2bb4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/validate-oidc-multitenant-app-gallery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/validate-oidc-multitenant-app-gallery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/validate-oidc-multitenant-app-gallery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3bc5a9f0-de4b-cc81-f279-8b3637e5f057
---

# Validate an OIDC multitenant app for Microsoft Entra App Gallery onboarding - Microsoft Entra ID | Microsoft Learn

Before publishing your OpenID Connect (OIDC) multitenant application to the Microsoft Entra app gallery, you must validate that your sign-in implementation meets gallery requirements. Validation is a self-service step that confirms your app is ready to publish and generates a Test ID required for submission.

The Microsoft Entra App Validator evaluates your OIDC multitenant sign-in flow against Microsoft Entra app gallery requirements while you sign in to your application.

After validation, you'll have:

- A validation report highlighting required and recommended fixes
- A Test ID required to publish your app to the Microsoft Entra app gallery

## Prerequisites

Before starting validation, ensure the following are already true:

- Your app is registered as a [multitenant application](../../identity-platform/single-and-multi-tenant-apps) in Microsoft Entra ID.
- [OIDC sign-in](../../identity-platform/v2-protocols-oidc) is implemented and working correctly.
- Your app is deployed and accessible via a public URL.
- Redirect URIs, scopes, and permissions are configured.
- You can successfully sign in with a Microsoft account.
- You're signed out of any existing sessions in your application.
- A gallery submission ID, create your gallery submission first (see below). This will be required before you submit your validation results.

Important

Validation fails if these prerequisites aren't met. Complete and test your OIDC implementation before attempting validation.

## Microsoft identity platform v1 endpoints aren't supported

Self-service Microsoft Entra App Gallery onboarding supports applications that use Microsoft identity platform v2 OpenID Connect (OIDC) endpoints.

Applications that use Microsoft identity platform v1 endpoints can't be validated through the self-service onboarding experience. Microsoft recommends migrating to v2 endpoints to take advantage of self-service validation, publishing, and lifecycle management capabilities.

The v2 endpoint uses a scope-based authorization model, including standard OIDC scopes such as `openid`, `profile`, and `email`, and provides a consistent authorization and token model that can be validated through the self-service experience. It also supports capabilities such as incremental consent, allowing applications to request delegated permissions as needed.

Microsoft identity platform v1.0 and v2.0 ID tokens differ in the claims and token semantics they expose. For more information, see [ID token claims reference](../../identity-platform/id-token-claims-reference).

Note

Applications configured to use Microsoft identity platform v1 endpoints can't be validated through the self-service onboarding experience. Migrate to v2 endpoints before starting validation.

## Your gallery submission ID

Before you start validation, create your Microsoft Entra gallery submission and copy its Submission ID. You will need this ID to submit your validation results.

To find your submission ID:

1. In the Microsoft Entra admin center, start the process to publish your application to the Microsoft Entra gallery.
2. Select **Publish your application**. If you already have a draft submission, select **Your published applications** instead.

    [![Screenshot of the Microsoft Entra admin center showing the Publish your application option.](media/validate-oidc-multitenant-app-gallery/publish-your-application-gallery.png)](media/validate-oidc-multitenant-app-gallery/publish-your-application-gallery.png#lightbox)
3. Go to the **Integration type** step.

    [![Screenshot of the Integration type step showing the submission ID.](media/validate-oidc-multitenant-app-gallery/integration-type-step-gallery.png)](media/validate-oidc-multitenant-app-gallery/integration-type-step-gallery.png#lightbox)
4. Copy the value shown under **Your Submission ID**.

Your submission ID is a GUID. Keep this ID available while you run the validator.

When the validator asks for a submission ID:

1. If the submission belongs to the tenant you're signed in to, select it from **Pick one of your submissions**.
2. If the submission belongs to a different tenant, paste the submission ID into the field instead.

If no submissions appear in the list, you can still paste the ID manually.

Important

You can't submit validation results without a valid gallery submission ID.

## Install the Microsoft Entra App Validator browser extension

The Microsoft Entra App Validator browser extension is required to perform validation.

1. Open **Microsoft Edge**.
2. Go to [Get Entra App Validator](https://microsoftedge.microsoft.com/addons/detail/entra-app-validator/iglkgnbeekgcnlapikofffkhkoldbaoj).
3. Select **Get** to begin installation.
4. When prompted, select **Add extension**.
5. Verify that **Entra App Validator** appears in the Extensions list and is enabled.

[![Screenshot of Microsoft Edge showing the Microsoft Entra App Validator extension installed and pinned to the toolbar.](media/validate-oidc-multitenant-app-gallery/extension-installed-toolbar.png)](media/validate-oidc-multitenant-app-gallery/extension-installed-toolbar.png#lightbox)

## Start a new validation session

Start a validation session by signing in to the extension and confirming your application's sign-in page as the starting point.

1. Open a new browser tab and go to your application's sign-in page. This should be the same page customers use when signing in through Microsoft Entra ID.
2. If you're already signed in, sign out completely to ensure a clean validation session.
3. Select the **Entra App Validator** extension icon from the browser toolbar.
4. Sign in to the extension using your Microsoft account.
5. Select **Start test**.
6. When prompted, confirm the starting page and select **Yes, Start test**.

The extension initializes the validation session and lists the checks it performs.

[![Screenshot of the Microsoft Entra App Validator extension showing the Start test button and test initialization screen.](media/validate-oidc-multitenant-app-gallery/start-test-initialization.png)](media/validate-oidc-multitenant-app-gallery/start-test-initialization.png#lightbox)

## Run the OIDC authentication flow

Sign in with a Microsoft account so the validator can capture and evaluate your application's OIDC authentication flow.

1. The validator checks that your app exposes a **Sign in with Microsoft** entry point. This is required for OIDC-based gallery apps.
2. When prompted, select **Authenticate**.
3. Complete the Microsoft sign-in process using your Microsoft account.

During authentication, the validator evaluates:

- Microsoft sign-in entry point configuration
- Tenant endpoint usage (`/common` or `/organizations` for multitenant apps)
- OIDC v2.0 endpoint compliance
- Required scopes, including `openid` and `profile`
- Authorization request structure and parameters

Tip

The most common validation failures are single-tenant endpoints, missing required scopes, and mismatched redirect URIs. These issues must be fixed before publishing.

## Review the validation report

After authentication completes:

1. In the Microsoft Entra App Validator extension, select **Preview report**.
2. Review the following sections:
    - **Tests executed** – Validation checks that ran
    - **Tests passed** – Requirements your app met
    - **Issues identified** – Blocking and nonblocking issues
    - **Authentication data captured** – Details from the OIDC flow
    - **Recommendations** – Guidance for resolving issues

[![Screenshot of the Microsoft Entra App Validator report showing tests executed, tests passed, issues identified, and recommendations sections.](media/validate-oidc-multitenant-app-gallery/oidc-report-summary.png)](media/validate-oidc-multitenant-app-gallery/oidc-report-summary.png#lightbox)

If the report shows blocking issues, resolve them in your app and rerun validation until all required checks pass.

Important

Blocking issues must be resolved before publishing. Nonblocking issues are recommendations and don't prevent submission.

## Declare how your app identifies users

Before you can submit, the validator asks which identifier from the token your application uses to match the signed-in user to a user record in its own system. Select all identifier types that your application uses, such as object ID (oid), User Principal Name (UPN), email address, employee ID, on-premises SAM account name, or a named custom claim.

## Why this is asked

Matching a user only on a mutable, self-assertable value, such as an email address, can create an account takeover risk. If an attacker obtains an email address that was previously associated with another user and the application relies only on that email address for account matching, the attacker could be matched to the existing application account. To reduce this risk, the validator does not accept a mutable identifier by itself. If your application uses a mutable identifier, select it together with an immutable identifier that your application also uses to identify the user.

If you select Custom claim, you must provide the name of the claim. A named custom claim is sufficient on its own, and no additional identifier is required.

## Submit validation and obtain a Test ID

Once your application passes all required validation checks:

1. In the validation report, select **Submit**.
2. A unique **Test ID** is generated as proof of successful validation.
3. Save the Test ID. You need it during the gallery publishing process.

Test IDs are time-bound and expire after two weeks.

Important

Without a valid Test ID, you can't proceed with Microsoft Entra app gallery publishing.

[![Screenshot of the validation submission confirmation displaying the generated Test ID.](media/validate-oidc-multitenant-app-gallery/submission-confirmation-test-id.png)](media/validate-oidc-multitenant-app-gallery/submission-confirmation-test-id.png#lightbox)

With validation complete and a Test ID generated, you're ready to proceed with publishing your app to the Microsoft Entra app gallery. If validation fails, review the report, resolve blocking issues, and rerun validation before continuing.