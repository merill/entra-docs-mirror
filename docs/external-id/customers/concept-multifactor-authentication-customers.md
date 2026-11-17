---
layout: Conceptual
title: Multifactor Authentication - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-multifactor-authentication-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Explore multifactor authentication in Microsoft Entra External ID, including methods, policies, and availability for each authentication approach.
ms.topic: concept-article
ms.date: 2026-11-13T00:00:00.0000000Z
ms.custom: it-pro, references_regions, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: faa54a1f-266c-e38b-148d-6e5bfc2805bd
document_version_independent_id: faa54a1f-266c-e38b-148d-6e5bfc2805bd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-multifactor-authentication-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-multifactor-authentication-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-multifactor-authentication-customers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fdef0068-a9a0-8dfb-c234-751298dad35f
---

# Multifactor Authentication - Microsoft Entra External ID | Microsoft Learn

Multifactor authentication (MFA) in Microsoft Entra External ID helps protect your applications by requiring additional verification during sign-up or sign-in.

**Applies to external tenants:** Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the [authentication approach overview](concept-choose-authentication-approach). Check feature availability in the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability).

The following methods can be configured in an external tenant. Runtime method and registration support depends on the selected authentication approach and API/SDK version.

- Email one-time passcode (OTP).
- SMS-based authentication, available as an add-on.
- Time-based one-time password (TOTP) from Microsoft Authenticator or a supported third-party authenticator app.
- Passkey (FIDO2), a phishing-resistant method that can satisfy MFA in a single gesture and also enable passwordless sign-in.

## Authentication approach applicability

Configure MFA policies and methods in your external tenant. Confirm method coverage and registration requirements in the [MFA support matrix](concept-supported-features-customers#multifactor-authentication-behavior). For policy enforcement and browser fallback support, see the [integration and policy comparison](concept-supported-features-customers#integration-policy-and-sessions-by-approach).

Important

The Native Authentication API V2 is in preview. The [Native Authentication API V1](../../identity-platform/reference-native-authentication-api-v1) remains generally available. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

With the Native Authentication API, inline registration uses the returned `enroll` and `activate` operations and can satisfy the policy without a separate MFA challenge. Complete required verification after sign-up or password reset before requesting tokens or completing a BYO UX browser flow.

A separate native-app browser sign-in restarts authentication. It isn't an escape-to-web-and-resume mechanism for an active native or BYO UX transaction. See the [Native authentication overview](../../identity-platform/concept-native-authentication) and [Bring Your Own UX guidance](concept-choose-authentication-approach#when-to-use-bring-your-own-ux).

For architectural guidance, see [Choose an authentication approach](concept-choose-authentication-approach).

## Create an MFA policy

In an external tenant, you can use Microsoft Entra Conditional Access to create a policy that prompts users for MFA when they sign up or sign in to your app. You create this policy in the Microsoft Entra admin center under Conditional Access in the Protection section. You can specify which users and groups the policy applies to, including all users and excluding any emergency access or break-glass accounts.

In the policy, you define the applications that require MFA. You can apply the policy to all cloud apps or select specific apps, while excluding any applications that don't require MFA. Then you configure the policy to grant access only if users complete the MFA requirement.

For details, see [how to create a Conditional Access policy in an external tenant](how-to-multifactor-authentication-customers#create-a-conditional-access-policy).

### Step-up MFA with Conditional Access authentication context

MFA with authentication context lets you require additional verification when users access sensitive data or perform critical actions, rather than for the entire app. With Microsoft Entra [Conditional Access authentication context](/en-us/entra/identity-platform/developer-guide-conditional-access-authentication-context), developers can add step-up authentication, such as MFA, inside their apps. Use this for scenarios like high-value transactions or viewing personal information. This approach supports Zero Trust principles and least-privilege access while reducing user friction.

This later-operation step-up capability applies to Microsoft-hosted authentication and BYO UX, not Embedded native authentication. Satisfying claims and MFA requirements established at the start of a native authorization transaction is different from requesting step-up for a later operation.

## Enable MFA methods

When you select identity provider options in your user flows, you define the first-factor authentication methods for sign-up and sign-in. Second-factor verification methods for MFA are configured in the Microsoft Entra admin center under **Entra ID** &gt; **Authentication methods**.

With Microsoft-hosted authentication, the first-factor choice determines which second-factor methods are available for [multifactor authentication (MFA)](how-to-multifactor-authentication-customers). Native Authentication API and SDK availability is scoped separately in the comparison.

The following method combinations describe Microsoft-hosted coverage. For the Native Authentication API and BYO UX, the supported second factors are email and SMS, subject to the same restriction against reusing email OTP as both factors.

- **Email with password or username with password**: For these first-factor methods, you can enable email one-time passcode, SMS, TOTP, passkey (FIDO2), or a combination as second-factor verification methods for MFA.
- **External identity providers**: You can enable email one-time passcode, SMS, TOTP, or a combination as second-factor verification methods for MFA. Passkey (FIDO2) isn't currently available for users who sign in with an external identity provider.
- **Email one-time passcode**: When email with one-time passcode is selected as the first-factor authentication method, it can't be used for second-factor verification. You can enable SMS or TOTP for MFA. Passkey (FIDO2) isn't currently available for email one-time passcode users.

For details, see [how to enable MFA methods in an external tenant](how-to-multifactor-authentication-customers).

## Email one-time passcode

Email one-time passcode authentication is available in an external tenant both as a first- and second-factor verification method. To allow the use of email one-time passcodes for MFA, your local account authentication method must be set to *Email with password*. If you choose *Email with one-time passcode*, customers who use this method for primary sign-in aren't able to use it for MFA secondary verification.

When email one-time passcode is enabled for MFA, the user signs in with their primary sign-in method and is notified that a code will be sent to the user's email address. The user chooses to send the code, retrieves the passcode from their email inbox, and enters it in the sign-in window. The user must complete this verification process within 10 minutes.

## SMS-based authentication

SMS is available at an additional cost for second-factor verification and for self-service password reset in external tenants. It isn't currently supported for first-factor authentication.

When SMS is enabled for MFA, users sign in with their primary method and are prompted to verify their identity with a code sent via text. They enter their phone number and receive an SMS with the verification code.

![Screenshot of an SMS message with an MFA verification code.](media/concept-multifactor-authentication-customers/sms-text.png)

External ID helps prevent fraudulent sign-ups and sign-ins via SMS with these measures:

- Telephony throttling limits help prevent outages and slowdowns. See [Service limits and restrictions](reference-service-limits).
- CAPTCHA for SMS MFA helps prevent automated attacks by distinguishing human users from bots. Microsoft-hosted pages can present this challenge before an SMS is sent.

### SMS pricing tiers by country/region

The following table lists SMS authentication pricing tiers by country or region. For pricing details, see [Microsoft Entra External ID pricing](https://aka.ms/ExternalIDPricing).

SMS is an add-on feature and requires a [linked subscription](../external-identities-pricing#link-an-external-tenant-to-a-subscription). If your subscription expires or is canceled, end users will no longer be able to authenticate using SMS, which could block them from signing in depending on your MFA policy.

| Tier | Countries/Regions |
| --- | --- |
| Phone Authentication Low Cost | Australia, Brazil, Brunei, Canada, Chile, China, Colombia, Cyprus, North Macedonia, Poland, Portugal, South Korea, Thailand, Türkiye, United States |
| Phone Authentication Mid Low Cost | Greenland, Albania, American Samoa, Austria, Bahamas, Bahrain, Bosnia & Herzegovina, Botswana, Costa Rica, Czech Republic, Denmark, Estonia, Faroe Islands, Finland, France, Greece, Hong Kong SAR, Hungary, Iceland, Ireland, Italy, Japan, Latvia, Lithuania, Luxembourg, Macao SAR, Malta, Mexico, Micronesia, Moldova, Namibia, New Zealand, Nicaragua, Norway, Romania, São Tomé and Príncipe, Seychelles Republic, Singapore, Slovakia, Solomon Islands, Spain, Sweden, Switzerland, Taiwan, United Kingdom, United States Virgin Islands, Uruguay |
| Phone Authentication Mid High Cost | Andorra, Angola, Anguilla, Antarctica, Antigua and Barbuda, Argentina, Armenia, Aruba, Barbados, Belgium, Benin, Bolivia, Bonaire, Curaçao, Saba, Sint Eustatius and Sint Maarten, British Virgin Islands, Bulgaria, Burkina Faso, Cameroon, Cayman Islands, Central African Republic, Cook Islands, Côte d’Ivoire, Croatia, Diego Garcia, Djibouti, Dominican Republic, Ecuador, El Salvador, Eritrea, Falkland Islands, Fiji, French Guiana, French Polynesia, Gambia, Georgia, Germany, Gibraltar, Grenada, Guadeloupe, Guam, Guinea, Guyana, Honduras, India, Kenya, Kiribati, Laos, Liberia, Malaysia, Marshall Islands, Martinique, Mauritius, Monaco, Montenegro, Montserrat, Netherlands, New Caledonia, Niue, Oman, Palau, Panama, Paraguay, Peru, Puerto Rico, Réunion, Rwanda, Saint Helena, Ascension and Tristan da Cunha, Saint Kitts & Nevis, Saint Lucia, Saint Pierre & Miquelon, Saint Vincent and the Grenadines, Saipan, Samoa, San Marino, Saudi Arabia, Sint Maarten, Slovenia, South Africa, South Sudan, Suriname, Eswatini, Timor-Leste, Tokelau, Tonga, Turks & Caicos, Tuvalu, United Arab Emirates, Vanuatu, Venezuela, Vietnam, Wallis and Futuna |
| Phone Authentication High Cost | Liechtenstein, Bermuda, Cabo Verde, Cambodia, Democratic Republic of Congo, Dominica, Egypt, Equatorial Guinea, Ghana, Guatemala, Guinea-Bissau, Israel, Jamaica, Kosovo, Lesotho, Maldives, Mali, Mauritania, Morocco, Mozambique, Papua New Guinea, Philippines, Qatar, Sierra Leone, Trinidad & Tobago, Ukraine, Zimbabwe, Afghanistan, Algeria, Azerbaijan, Bangladesh, Belarus, Belize, Bhutan, Burundi, Chad, Comoros, Congo, Ethiopia, Gabonese Republic, Haiti, Indonesia, Iraq, Jordan, Kuwait, Kyrgyzstan, Lebanon, Libya, Madagascar, Malawi, Mongolia, Myanmar, Nauru, Nepal, Niger, Nigeria, Pakistan, Palestinian National Authority, Russia, Senegal, Serbia, Somalia, Sri Lanka, Sudan, Tajikistan, Tanzania, Togolese Republic, Tunisia, Turkmenistan, Uganda, Uzbekistan, Yemen, Zambia |

### Opt-in regions for SMS

Since January 2025, certain country codes are deactivated by default for SMS verification. To allow traffic from deactivated regions, activate them for your application using the Microsoft Graph `onPhoneMethodLoadStart` event policy. See [Regions requiring opt-in for SMS verification](how-to-region-code-opt-in).

## Time-based one-time password (TOTP)

Note

TOTP authentication in external tenants will become generally available at the end of November 2026. Rollout will finish in early December 2026.

TOTP is a standards-based method that generates a temporary verification code in Microsoft Authenticator or a supported third-party authenticator app. It works as a second-factor verification method with Microsoft-hosted authentication. It isn't supported through the Native Authentication API or BYO UX.

When TOTP is enabled and MFA is required, users register an authenticator app by scanning a QR code. For subsequent MFA challenges, users enter the verification code displayed in their authenticator app.

For setup steps, see [Add multifactor authentication (MFA) to an app](how-to-multifactor-authentication-customers#enable-totp-as-an-mfa-method).

## Passkey (FIDO2)

Passkeys (FIDO2) provide phishing-resistant, passwordless authentication that uses public-key cryptography. A passkey can be used to satisfy MFA in a single gesture (face, fingerprint, PIN, or security key) or as a primary, passwordless sign-in method. Only email + password and username + password local account users can register a passkey. Passkey registration requires a [custom URL domain](how-to-custom-url-domain), and users must complete MFA before registering a passkey.

These passkey capabilities apply to Microsoft-hosted authentication, not the Native Authentication API or BYO UX.

For setup steps, see [Sign in with passkeys](how-to-sign-in-with-passkey).