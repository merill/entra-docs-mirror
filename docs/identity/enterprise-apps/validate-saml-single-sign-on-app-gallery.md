---
layout: Conceptual
title: Validate a SAML single sign-on app for Microsoft Entra App Gallery onboarding - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/validate-saml-single-sign-on-app-gallery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: HildaK-pm
ms.author: hkinyunyu
ms.service: entra-id
ms.subservice: enterprise-apps
manager: msteele
description: Use the Microsoft Entra App Validator browser extension to validate a SAML 2.0 single sign-on integration before submitting an application for Microsoft Entra App Gallery onboarding.
ms.topic: tutorial
ms.date: 2026-08-19T00:00:00.0000000Z
ms.reviewer: hkinyunyu
ms.custom: enterprise-apps-article, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: aef2e302-ee16-cbb7-cefe-ad3ce1feb63e
document_version_independent_id: aef2e302-ee16-cbb7-cefe-ad3ce1feb63e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/validate-saml-single-sign-on-app-gallery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/validate-saml-single-sign-on-app-gallery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/validate-saml-single-sign-on-app-gallery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f2441cdc-92a7-5ac5-ff17-0884ae3e7067
---

# Validate a SAML single sign-on app for Microsoft Entra App Gallery onboarding - Microsoft Entra ID | Microsoft Learn

Use the Microsoft Entra App Validator browser extension to validate your application's Security Assertion Markup Language (SAML) 2.0 single sign-on (SSO) integration before you submit the application for Microsoft Entra App Gallery onboarding. The validator observes a sign-in to your application, captures protocol evidence, tracks scenario completion, and packages the result for submission.

Important

The validator doesn't cryptographically verify SAML signatures, change your Microsoft Entra tenant configuration, or replace your application's test suite. Your application is responsible for validating signatures and enforcing its authentication and authorization requirements.

In this tutorial, you learn how to:

- Prepare a Microsoft Entra environment for SAML validation.
- Configure a non-gallery enterprise application for SAML SSO.
- Install and open the Entra App Validator.
- Validate identity provider (IdP)-initiated and service provider (SP)-initiated SAML flows.
- Run working-certificate and expired-certificate scenarios.
- Optionally validate Single Logout.
- Review and submit validation results.

## Prerequisites

Before you begin, make sure that you have:

- A Microsoft Entra tenant.
- Permission to manage enterprise applications, such as **Cloud Application Administrator**, **Application Administrator**, or ownership of the service principal.
- A test user account that you can assign to the application.
- Microsoft Edge.
- An application sign-in endpoint that your test user can reach.
- The SAML values that your application expects:
    - **Identifier (Entity ID)**
    - **Reply URL (Assertion Consumer Service URL)**
    - **Sign on URL**, if your application supports SP-initiated SSO
- A gallery submission ID. Create your gallery submission before you start validation because you can't submit validation results without a valid submission ID.

Important

Use a nonproduction tenant and a nonproduction application for validation. The expired-certificate scenario intentionally interrupts sign-in to the application under test.

## Get your gallery submission ID

Before you start validation, create your Microsoft Entra gallery submission and copy its submission ID.

1. In the Microsoft Entra admin center, start the process to publish your application to the Microsoft Entra gallery.
2. Select **Publish your application**. If you already have a draft submission, select **Your published applications**.

    [![Screenshot of the Browse Microsoft Entra App Gallery page with the Publish to the app gallery option highlighted and Your published applications shown below it.](media/validate-oidc-multitenant-app-gallery/publish-your-application-gallery.png)](media/validate-oidc-multitenant-app-gallery/publish-your-application-gallery.png#lightbox)
3. Go to the **Integration type** step.

    [![Screenshot of the Publish Application to Gallery workflow on the Integration type step, with the Your Submission ID field highlighted.](media/validate-oidc-multitenant-app-gallery/integration-type-step-gallery.png)](media/validate-oidc-multitenant-app-gallery/integration-type-step-gallery.png#lightbox)
4. Copy the value shown under **Your Submission ID**.

Your submission ID is a GUID, such as `11680398-5b31-4e47-a61d-191e7e638e85`. Keep it available while you run the validator.

When the validator asks for a submission ID:

- If the submission belongs to the tenant where you're signed in, select it from **Pick one of your submissions**.
- If the submission belongs to a different tenant, paste the submission ID into the field.

If no submissions appear in the list, you can still paste the submission ID manually.

Important

You can't submit validation results without a valid gallery submission ID.

## Configure your application

The validator tests an application that exists in your tenant as a non-gallery enterprise application.

### Create the application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Go to **Enterprise applications**.
3. Select **New application** &gt; **Create your own application**.
4. Enter a name for the application.
5. Select **Integrate any other application you don't find in the gallery (Non-gallery)**.
6. Select **Create**.

### Configure SAML single sign-on

1. Open the enterprise application that you created.
2. Select **Single sign-on**.
3. Select **SAML**.
4. Configure the following values in **Basic SAML Configuration**.

| Field | Description |
| --- | --- |
| **Identifier (Entity ID)** | The identifier that your application uses to identify itself to Microsoft Entra ID. |
| **Reply URL (ACS URL)** | The endpoint where Microsoft Entra ID posts the SAML response. |
| **Sign on URL** | Your application's sign-in page. Configure this value when your application supports SP-initiated SSO. |

Note

The **Sign on URL** affects test behavior. When a Sign on URL is configured, the My Apps tile can redirect to your application's sign-in page and produce an SP-initiated sign-in. To test IdP-initiated SSO from My Apps, clear the Sign on URL for that test run. Restore it afterward if your application also supports SP-initiated SSO.

### Configure claims, if required

If your application requires additional attributes, custom claims, application roles, or a specific NameID format, configure them in **Attributes & Claims** on the application's **Single sign-on** page.

### Assign a test user

1. Open the enterprise application.
2. Select **Users and groups**.
3. Select **Add user/group**.
4. Assign your test user to the application.
5. Open [My Apps](https://myapps.microsoft.com) and confirm that the application tile appears.

The My Apps tile is required for IdP-initiated validation because that flow starts from Microsoft Entra ID.

## Install and open Entra App Validator

1. Install [Entra App Validator](https://microsoftedge.microsoft.com/addons/detail/entra-app-validator/iglkgnbeekgcnlapikofffkhkoldbaoj) from Microsoft Edge Add-ons.
2. Pin the extension to the browser toolbar.
3. Select the extension icon to open the validator.
4. In the validator, open the **Test** tab.
5. Select **SAML 2.0**.
6. Create a new test or select an existing test to continue.

Test progress is saved automatically, so you can close the validator and resume a test later.

## Choose the SAML flows to validate

Choose the sign-in flows that your application supports:

- IdP-initiated
- SP-initiated
- Both

[![Screenshot showing the Entra App Validator beside a Microsoft Entra enterprise application. The validator asks which SAML sign-in flows the application supports, with IdP sign-in and SP sign-in selected.](media/validate-saml-single-sign-on-app-gallery/validate-a-saml-app.png)](media/validate-saml-single-sign-on-app-gallery/validate-a-saml-app.png#lightbox)

Only the flows that you declare are offered as validation scenarios. If you later remove a flow that already has captured runs, the validator deletes those runs because they no longer match the capabilities that you declared.

## Understand SAML scenarios

Each SAML scenario follows the same process: choose a scenario, open your app, capture the sign-in, then review and save the run.

| Scenario | What it validates | Required |
| --- | --- | --- |
| Working certificate | Normal sign-in with a valid SAML signing certificate. | Yes |
| Expired certificate | Application behavior when an assertion is signed with an expired certificate. | Yes |
| Single Logout | Logout-request capture after sign-out. | No |

Only the working-certificate and expired-certificate scenarios count toward SAML completion. Single Logout is optional and doesn't block submission.

## Understand supported SAML capabilities and behaviors

The validation results reflect the capabilities that your application supports and that you choose to test. Depending on your implementation, validated SAML capabilities can include:

- IdP-initiated single sign-on
- SP-initiated single sign-on
- Single Logout (SLO)
- Support for application-specific claims and user identifiers

> 
> Select only the capabilities that your application implements. Capabilities that aren't implemented or validated shouldn't be represented as supported functionality.

## Run IdP-initiated validation

IdP-initiated sign-on starts from Microsoft Entra ID. The user selects the application tile in My Apps, and Microsoft Entra ID posts an unsolicited SAML response to the application's ACS URL.

[![Screenshot of the Entra App Validator Test tab for SAML 2.0. The IdP sign-in My Apps scenario is expanded and shows required Working certificate and Expired certificate scenarios, plus an optional Single Logout scenario.](media/validate-saml-single-sign-on-app-gallery/run-idp-initiated-validation.png)](media/validate-saml-single-sign-on-app-gallery/run-idp-initiated-validation.png#lightbox)

1. In the validator, select an **IdP-initiated working-certificate** scenario.
2. Select your application from the My Apps tiles displayed by the validator.
3. Start capture.
4. When My Apps opens, select your application tile.
5. Complete sign-in.
6. Confirm the observed sign-in outcome in the validator.
7. Review and save the validation run.

Expected observations include the application tile, an unsolicited SAML response posted to the ACS URL, a non-Microsoft landing page, and manual confirmation of the outcome.

Tip

If the captured response contains an `InResponseTo` value, the sign-in was SP-initiated, not IdP-initiated. The `InResponseTo` value ties the response to an `AuthnRequest` from your application.

## Run SP-initiated validation

SP-initiated SSO starts from your application. Your application redirects the browser to Microsoft Entra ID with a SAML request. After the user authenticates, Microsoft Entra ID posts a SAML response to the ACS URL.

[![Screenshot of the Entra App Validator Test tab for SAML 2.0. The SP sign-in your app's login page scenario is expanded and shows required Working certificate and Expired certificate scenarios, plus an optional Single Logout scenario.](media/validate-saml-single-sign-on-app-gallery/run-sp-initiated-validation.png)](media/validate-saml-single-sign-on-app-gallery/run-sp-initiated-validation.png#lightbox)

1. In the validator, select an **SP-initiated working-certificate** scenario.
2. Identify the application.
3. Enter the application Sign on URL.
4. Start capture.
5. Complete sign-in in the browser tab opened by the validator.
6. Confirm the observed sign-in outcome.
7. Review and save the validation run.

Expected observations include the application Sign on URL loading, a SAML request sent to Microsoft Entra ID, a SAML response received at the ACS URL, a non-Microsoft landing page, and manual confirmation of the outcome.

## Run expired-certificate validation

The expired-certificate scenario records evidence that your application rejects a sign-in whose assertion is signed with an expired certificate. Run this scenario against the same application that you used for the working-certificate scenario.

Caution

This scenario interrupts sign-in for the application under test until you restore the working certificate. Run this test only against the non-gallery application created for this validation, and make sure the application is not being used by other users or workloads.

Use the following steps to complete the validation:

1. Open the enterprise application in the Microsoft Entra admin center.
2. Select **Single sign-on** &gt; **SAML Certificates**.
3. Import the approved test certificate that has already expired.
4. Make the expired certificate active.
5. Wait for the configuration change to apply.
6. In the validator, run the **Expired certificate** scenario.
7. Complete sign-in.
8. Confirm that sign-in fails at your application.
9. Restore the working certificate.

> 
> Expected result: The application should reject the sign-in attempt when the SAML assertion is signed with an expired certificate.
> 
> If the application continues to authenticate users by using assertions signed with an expired certificate, review the certificate-validation logic in your application because this behavior can indicate a security or implementation issue.

Note: For testing purposes, you can generate a self-signed certificate with an expiration date in the past and use it for this scenario. Import the certificate into SAML Certificates and make it active before you run the validation. Generate an expired self-signed certificate To generate an expired self-signed certificate for testing, open Windows PowerShell and run the following script.

Password: ExpiredCert-TestOnly-123!

```powershell
# Test-only PFX password
$password = ConvertTo-SecureString `
    "ExpiredCert-TestOnly-123!" `
    -AsPlainText `
    -Force

# Create a certificate that was valid from two years ago
# until one year ago, meaning it is already expired.
$cert = New-SelfSignedCertificate `
    -Type Custom `
    -Subject "CN=Expired-Entra-SAML-Test" `
    -FriendlyName "Expired Entra SAML Test" `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -KeyAlgorithm RSA `
    -KeyLength 2048 `
    -HashAlgorithm SHA256 `
    -KeyExportPolicy Exportable `
    -KeyUsage DigitalSignature `
    -NotBefore (Get-Date).AddYears(-2) `
    -NotAfter (Get-Date).AddYears(-1)

# Export certificate and private key for importing into Entra
Export-PfxCertificate `
    -Cert $cert `
    -FilePath "$PWD\expired-saml-signing.pfx" `
    -Password $password

# Optional: export only the public certificate
Export-Certificate `
    -Cert $cert `
    -FilePath "$PWD\expired-saml-signing.cer"

# Confirm its dates
$cert | Format-List `
    Subject,
    Thumbprint,
    NotBefore,
    NotAfter,
    HasPrivateKey
```

Wait 5–10 minutes after uploading and activating the expired certificate to allow the change to propagate before running the scenario. This helps ensure the run captures the newly activated certificate rather than the previous one. If the expired certificate does not propagate after 5–10 minutes, delete the non-expired certificate before running the scenario.

[![Screenshot of SAML signature details in the Entra App Validator. The Cert valid to value is marked EXPIRED.](media/validate-saml-single-sign-on-app-gallery/expired-certificate-signature.png)](media/validate-saml-single-sign-on-app-gallery/expired-certificate-signature.png#lightbox)

Note

Use a dedicated test certificate and test application. Do not use a production signing certificate for this scenario.

## Optionally validate Single Logout

If your application supports SAML Single Logout, run the **Single Logout** scenario.

1. Sign in through the validator.
2. Sign out from the application.
3. Allow the validator to capture the logout request.
4. Save the result.

If your application doesn't support Single Logout, select **My app does not support this**. Skipping Single Logout is recorded and doesn't block submission.

## Review and submit validation results

After each run, review the captured evidence before submission. For SAML runs, the validator can show decoded request and response details, assertion information, claims, certificate details, and signature information.

Before submission, declare how your application identifies users. The validator asks which token value your application uses to match the sign-in to a user record, such as object ID, user principal name (UPN), email address, employee ID, on-premises SAM account name, or a named custom claim.

Important

Don't rely only on a mutable value, such as an email address, to match users. Email addresses and usernames can change or be reassigned. Matching only on a mutable value can allow a person who inherits a previous user's identifier to access that user's application account.

If your application uses a mutable identifier, pair it with an immutable identifier, such as object ID. A named custom claim is sufficient on its own if that's how your application identifies users.

For SAML, submission requires:

- A completed **Working certificate** scenario for each declared flow.
- A completed **Expired certificate** scenario for each declared flow.
- Manual outcome confirmation for each required scenario.
- The identity-mapping declaration.

Single Logout is optional and doesn't block submission.

## Troubleshoot common issues

### My application tile doesn't appear in My Apps

Assign your test user to the application, then reload My Apps. An unassigned application doesn't appear in My Apps, and IdP-initiated validation starts from the My Apps tile.

### I selected IdP-initiated, but the response includes `InResponseTo`

A response with `InResponseTo` is tied to a request from your application, which means that the sign-in is SP-initiated. A common cause is a configured **Sign on URL**, which can cause the My Apps tile to redirect to the application's sign-in page.

### The expired-certificate run captured the old certificate

The certificate change might not have propagated yet. Follow the approved product procedure for propagation time and cleanup, then rerun the scenario.

### Sign-in fails with an `AADSTS` error

Review the validator's inline diagnosis first.

| Error code | Meaning | Suggested action |
| --- | --- | --- |
| `AADSTS750054` | No SAML request was found in the request to Microsoft Entra ID. | Confirm that your application sends an `AuthnRequest` with the `SAMLRequest` query parameter. |
| `AADSTS50011` | Reply URL mismatch. | Confirm that the ACS URL requested by the application is in the application's Reply URL list. |
| `AADSTS700016` | Application not found. | Confirm that the Identifier (Entity ID) matches an application in the tenant. |

For additional troubleshooting, use Microsoft Entra sign-in logs and the SAML troubleshooting guidance.