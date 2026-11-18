---
layout: Conceptual
title: Supported Features - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-supported-features-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Compare Microsoft Entra External ID features in workforce and external tenants, and confirm authentication approach support to plan your customer apps.
ms.topic: concept-article
ms.date: 2026-11-17T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024, sfi-ropc-nochange, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: 2bb93356-67a7-32cd-fd3b-cdce20871675
document_version_independent_id: a5c1d845-10eb-c72e-4560-ff2206c4ee7e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-supported-features-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-supported-features-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-supported-features-customers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 82b38328-5842-5455-5bd3-9a2828bdaf81
---

# Supported Features - Microsoft Entra External ID | Microsoft Learn

Microsoft Entra External ID supports two tenant configurations, depending on your audience and the resources you want to manage:

- A *workforce* tenant configuration is for your employees, internal business apps, and other organizational resources. A workforce tenant uses business-to-business (B2B) collaboration in Microsoft Entra External ID to work with external business partners and guests.
- An *external* tenant configuration is exclusively for External ID scenarios where you want to publish apps to consumers or business customers.

This article provides two comparisons:

- To choose how customer apps present authentication, review authentication approach support in external tenants.
- To compare workforce and external tenant capabilities, start with the general feature comparison.

For more information about these tenants, see [Workforce and external tenant configurations in Microsoft Entra External ID](../tenant-configurations).

Important

The Embedded native authentication and Bring Your Own UX (BYO UX) comparisons describe the current Native Authentication API (V2, preview). BYO UX is also in preview. SDK support varies by platform and version. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

## Authentication approach support

Compare methods and journeys and integration, policy, and sessions for customer-app authentication in **external tenants**. For architectural choices, see [Choose an authentication approach](concept-choose-authentication-approach). Company branding and branding themes are presentation options within Microsoft-hosted authentication, not separate authentication approaches.

For SDK integrations, use a release compatible with the current API that supports the operations your app requires. See the [Native authentication overview](../../identity-platform/concept-native-authentication) and [platform-specific SDK guidance](../../identity-platform/concept-native-authentication#how-to-use-native-authentication). SDK support varies by platform and version.

For API operations, see the [Native Authentication API reference](../../identity-platform/reference-native-authentication).

**How to read the comparison:** "Supported" applies to the approach and API version described here, not to every SDK. Configure required tenant methods and policies before using a supported operation.

### Methods and journeys by approach

The following table compares local-account methods and federation. For provider configuration, see [Identity providers for external tenants](concept-authentication-methods-customers). Password recovery and multifactor authentication (MFA) have separate comparisons.

Important

Username or alias sign-in is in preview. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

| Journey or method | Microsoft-hosted authentication | Embedded native authentication | Bring Your Own UX |
| --- | --- | --- | --- |
| **Sign-up: email and password** | Supported. | Supported. | Supported. |
| **Sign-up: email one-time passcode** | Supported. | Supported. | Supported. |
| **Sign-in: email and password** | Supported. | Supported. | Supported. |
| **Sign-in: username and password** | Supported for configured local accounts. | Supported for configured local accounts. | Supported for configured local accounts. |
| **Sign-in: email one-time passcode** | Supported. | Supported. | Supported. |
| **Phone number as first factor** | Not supported. | Not supported. | Not supported. |
| **Social or federated identity providers** | Supported through configured identity providers. | Not supported. | Not supported. |

Use only methods and operations returned for the active transaction. A tenant can contain providers or methods that aren't available through the selected integration.

### Password reset behavior and controls

Password recovery support doesn't imply support for Microsoft-hosted reset-page settings. Passwordless email one-time-passcode accounts don't have a password to reset.

| Capability | Microsoft-hosted authentication | Embedded native authentication | Bring Your Own UX |
| --- | --- | --- | --- |
| **Recovery: email one-time passcode** | Supported. | Supported. | Supported. |
| **Recovery: SMS** | Supported. | Supported. | Supported. |
| **Recovery during sign-in** | Supported through configured sign-in pages. | Supported when offered through the current password method. | Supported when offered by the current transaction. |

### Multifactor authentication behavior

For [tenant MFA configuration](concept-multifactor-authentication-customers) and [first-factor restrictions](concept-multifactor-authentication-customers#enabling-mfa-methods), see the MFA guidance. For SDK integrations, confirm that the SDK supports the steps to enroll and activate an MFA method.

| Capability | Microsoft-hosted authentication | Embedded native authentication | Bring Your Own UX |
| --- | --- | --- | --- |
| **Email or SMS one-time passcode (OTP)** | Supported, subject to first-factor restrictions in [MFA methods](concept-multifactor-authentication-customers#enabling-mfa-methods). | Supported. Accounts that use email OTP as the first factor use a different second factor, such as SMS. | Supported. Accounts that use email OTP as the first factor use a different second factor, such as SMS. |
| **Method registration during sign-in** | Supported. | Supported for offered email and SMS methods. | Supported for offered email and SMS methods. |
| **Time-based one-time password (TOTP)** | Supported. | Not supported. | Not supported. |
| **Passkey sign-in or MFA** | Supported, subject to [passkey restrictions](concept-multifactor-authentication-customers#enabling-mfa-methods). | Not supported. | Not supported. |
| **Additional verification for sensitive actions after sign-in** | Supported through configured authentication context. | Not supported. | Supported through configured authentication context. |

### Branding and language scope

These rows describe Microsoft-hosted customization settings, not whether an application or website can implement its own design.

| Capability | Microsoft-hosted authentication | Embedded native authentication | Bring Your Own UX |
| --- | --- | --- | --- |
| **Tenant-wide company branding** | Supported. See [Branding](concept-branding-customers). | Hosted branding settings don't apply to native screens. | Hosted branding settings don't apply to the self-hosted page. |
| **Application-specific branding themes** | Supported. See [Branding themes](../../fundamentals/how-to-customize-branding-themes-apps). | Hosted themes don't apply to native screens. | Hosted themes don't apply to the self-hosted page. |
| **Hosted language customization** | Supported for Microsoft-hosted pages. | Hosted language settings don't configure native interface text. | Hosted language settings don't configure the self-hosted page's text. |
| **Service custom URL domain** | Optional for Microsoft-hosted authentication. | Required for browser-based apps using the Native Authentication API V2, such as SPAs; not required for non-browser clients using native HTTP transports. | Required for calls to the Native Authentication API, the custom authentication page, and the Microsoft Entra authentication endpoints. |

### Custom authentication extension applicability

The following comparison describes event availability, not interchangeable request or response payloads. Use the event's documented contract and the current operation's returned data.

**Legend:**![Supported](../media/common/applies-to-yes.png) Supported; ![Not supported](../media/common/applies-to-no.png) Not supported.

| Event | Microsoft-hosted authentication | Embedded native authentication | Bring Your Own UX |
| --- | --- | --- | --- |
| **`OnAttributeCollectionStart`** | ![Supported](../media/common/applies-to-yes.png) | ![Not supported](../media/common/applies-to-no.png) | ![Not supported](../media/common/applies-to-no.png) |
| **`OnAttributeCollectionSubmit`** | ![Supported](../media/common/applies-to-yes.png) | ![Not supported](../media/common/applies-to-no.png) | ![Not supported](../media/common/applies-to-no.png) |
| **`OnOtpSend` (email)** | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) |
| **`OnPasswordSubmit`** | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) |
| **`OnTokenIssuanceStart`** | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) |

`OnPasswordSubmit` supports [just-in-time password migration](how-to-migrate-passwords-just-in-time) from a legacy identity provider during sign-in. It isn't a general-purpose password-validation event.

### Integration, policy, and sessions by approach

Session reuse, persistent sessions, and coordinated sign-out are different capabilities. See Single sign-on and Conditional Access for tenant configuration.

| Capability | Microsoft-hosted authentication | Embedded native authentication | Bring Your Own UX |
| --- | --- | --- | --- |
| **Application model** | Browser-based integration, including single-page applications (SPAs). | Public clients, including SPAs; browser integrations require a cross-origin resource sharing (CORS) proxy or edge origin policy. | Public or confidential relying applications with a registered web-type redirect URI. |
| **MFA policy enforcement** | Supported through Conditional Access. | Supported through Conditional Access and orchestrated by the native app. | Supported through Conditional Access and orchestrated by the custom authentication page. |
| **Existing browser session reuse** | Supported when the session satisfies the request. | Native authentication does not establish an Entra session. | A session that satisfies the authorization request skips the self-hosted page. |
| **Persistent browser session** | Controlled through [Conditional Access](../../identity/conditional-access/concept-conditional-access-session#persistent-browser-session) and/or the [**Stay signed in?**](how-to-user-flow-sign-up-sign-in-customers#control-the-stay-signed-in-prompt) user prompt. | Native authentication does not establish an Entra session. | Use the [**Persistent browser session**](../../identity/conditional-access/concept-session-lifetime#persistence-of-browsing-sessions) Conditional Access control. |
| **Browser fallback and transaction resume** | Uses Microsoft-hosted pages. | A separately configured browser sign-in starts a new attempt; it doesn't resume native progress. | Inline escape to Microsoft-hosted pages and resumption of the same transaction isn't supported. |
| **Account selection on the authentication page** | Microsoft-hosted account selection appears during OAuth processing. | Not used by the current Native Authentication API integrations. | An account picker on the self-hosted authentication page isn't currently supported. |
| **Sign-out across applications** | Supported for configured browser applications as described in Single sign-on. | Sign-out is application-specific. | Manage relying-application and browser sessions separately; the self-hosted authentication page doesn't currently offer a logout hook. |
| **Authentication diagnostics** | Use sign-in logs. | Record HTTP status codes, request IDs, correlation IDs, and timestamps without exposing sensitive data. See [API diagnostics](../../identity-platform/reference-native-authentication#security-and-diagnostics). | Use the Native Authentication API request diagnostics and relying-application authorization diagnostics. |

For platform guidance, see [Supported languages and frameworks](concept-choose-authentication-approach#supported-languages-and-frameworks). For package versions and continuation interfaces, see [SDK compatibility](../../identity-platform/how-to-migrate-native-authentication-v1-v2#sdk-compatibility). Native SDKs don't orchestrate the BYO UX handoff-to-finish transaction.

For architecture and integration guidance, see the [Bring Your Own UX overview](concept-bring-your-own-ux).

## General feature comparison

The remaining tables compare **tenant-level capabilities** in workforce and external tenants. An external-tenant capability doesn't establish that every authentication approach or SDK supports it; use the approach comparison for those differences.

The following table compares the general features and capabilities in workforce and external tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| External identities scenario | Allow business partners and other external users to collaborate with your workforce. Guests can securely access your business applications through invitations or self-service sign-up. | Use External ID to help secure your applications. Consumers and business customers can access your consumer apps through self-service sign-up. Invitations are also supported. |
| Local accounts | Local accounts are supported for *internal* members of your organization only. | Local accounts are supported for:<br>- Consumers and business customers who use self-service sign-up.<br>- Admin-created internal accounts (with or without an admin role).<br><br> All users in an external tenant have [default permissions](reference-user-permissions) unless they're [assigned an admin role](how-to-manage-admin-accounts). |
| Groups | Use [groups](/en-us/entra/fundamentals/how-to-manage-groups) to manage administrative and user accounts. | Use groups to manage administrative accounts. Support for Microsoft Entra groups and [application roles](how-to-use-app-roles-customers) is being phased into customer tenants. For the latest updates, see [Groups and application roles support](reference-group-app-roles-support). |
| Roles and administrators | [Roles and administrators](../../fundamentals/how-subscriptions-associated-directory) are fully supported for administrative and user accounts. | Roles are supported for all users. All users in an external tenant have [default permissions](reference-user-permissions) unless they're assigned an [admin role](how-to-manage-admin-accounts). |
| Microsoft Entra ID Protection | This product provides ongoing risk detection for your Microsoft Entra tenant. It allows organizations to discover, investigate, and remediate identity-based risks. | Not supported. |
| Microsoft Entra ID Governance | This product enables organizations to govern identity and access lifecycles, along with secure privileged access. [Learn more](../../id-governance/identity-governance-overview). | Not supported. |
| Self-service password reset | Allow users to reset their password by using up to two authentication methods. | Allow users to reset their password by using email with a one-time passcode or SMS. [Learn more](how-to-enable-password-reset-customers). |
| Language customization | Customize the sign-in experience based on browser language when users authenticate into your corporate intranet or web-based applications. | Use languages to modify the strings displayed to your customers as part of the sign-in and sign-up process. [Learn more](concept-branding-customers). |
| Custom attributes | Use directory extension attributes to store more data in the Microsoft Entra directory for user objects, groups, tenant details, and service principals. | Use directory extension attributes to store more data in the customer directory for user objects. Create custom user attributes and add them to your sign-up user flow. [Learn more](how-to-define-custom-attributes). |
| Pricing | Get [monthly active users (MAU) pricing](../external-identities-pricing) for external guests through B2B collaboration (`UserType=Guest`). | Get [MAU pricing](../external-identities-pricing) for all users in the external tenant regardless of role or `UserType` value. |

## Interface customization

The following table compares the features for interface customization in workforce and external tenants. Company branding and language customization apply to Microsoft-hosted pages. For Embedded native authentication and BYO UX, your team styles and localizes the interface it manages.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Company branding | You can add [company branding](../../fundamentals/how-to-customize-branding) that applies to all these experiences to create a consistent sign-in experience for your users. | Supported. [Customize branding](how-to-customize-branding-customers). |
| Language customization | [Customize the sign-in experience by browser language](../../fundamentals/how-to-customize-branding). | Supported. [Customize languages](how-to-customize-languages-customers). |
| Custom domain names | You can use [custom domains](../../fundamentals/add-custom-domain) for administrative accounts only. | A [tenant-verified custom URL domain](concept-custom-url-domain) is required for browser-based apps using the Native Authentication API V2 and for BYO UX. It isn't required for non-browser native HTTP clients and is optional for Microsoft-hosted authentication. |
| Embedded native authentication for mobile apps | Not supported. | [Embedded native authentication](../../identity-platform/concept-native-authentication) gives you control over the design of your mobile application's sign-in experiences. Confirm support for your API or SDK version in the [Native Authentication API reference](../../identity-platform/reference-native-authentication) or [SDK integration guidance](../../identity-platform/concept-native-authentication#how-to-use-native-authentication). |

## Add your own business logic

Use [custom authentication extensions](concept-custom-extensions) to integrate external systems with the Microsoft Entra authentication experience. A custom authentication extension listens for an event and makes an HTTP call to a REST API endpoint where you define your business logic.

The following table compares the events for custom authentication extensions in workforce and external tenants. For support by authentication approach, see the custom authentication extension comparison.

| Event | Workforce tenant | External tenant |
| --- | --- | --- |
| **`OnAttributeCollectionStart`** | Not supported. | This event occurs at the beginning of the sign-up's attribute collection step, before the attribute collection page renders. You can add actions such as prefilling values and displaying a blocking error. [Learn more](../../identity-platform/custom-extension-attribute-collection?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=start-continue,submit-continue). |
| **`OnAttributeCollectionSubmit`** | Not supported. | This event occurs during the sign-up flow, after the user enters and submits attributes. You can add actions such as validating or modifying the user's entries. [Learn more](../../identity-platform/custom-extension-attribute-collection?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=start-continue,submit-continue). |
| **`OnOtpSend` (email)** | Not supported. | Configure a custom email provider for one-time passcode send events. [Learn more](../../identity-platform/custom-extension-email-otp-get-started?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=azure-communication-services,azure-portal). |
| **`OnPasswordSubmit`** | Not supported. | Migrate a customer's password from a legacy identity provider during sign-in. See [Just-in-time password migration](how-to-migrate-passwords-just-in-time). |
| **`OnTokenIssuanceStart`** | [Add claims from external systems](../../identity-platform/custom-extension-overview). | [Add claims from external systems](concept-custom-extensions). |

## Identity providers and authentication methods

The following table compares the [identity providers](../identity-providers) and methods for primary authentication and MFA in workforce and external tenants. Federation options include Security Assertion Markup Language (SAML), WS-Federation (WS-Fed), and OpenID Connect (OIDC).

Important

Invitations in external tenants are in preview. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Identity providers for external users (primary authentication) | For self-service sign-up guests:<br>- Microsoft Entra accounts<br>- Microsoft accounts<br>- Emailed one-time passcode<br>- Google federation<br>- Facebook federation<br><br>For invited guests:<br>- Microsoft Entra accounts<br>- Microsoft accounts<br>- Emailed one-time passcode<br>- Google federation<br>- SAML/WS-Fed federation | For self-service sign-up users (consumers, business customers):<br>- Authentication methods available in External ID<br><br>For invited guests via a directory role (for example, admins):<br>- Microsoft Entra accounts<br>- Microsoft accounts<br>- [Emailed one-time passcode](concept-authentication-methods-customers#email-with-one-time-passcode-sign-in)<br>- [SAML/WS-Fed federation](../direct-federation)<br><br> You can invite external users for administrative purposes only. You can't use this feature to invite customers to sign in to your apps. This feature isn't compatible with customer identity and access management (CIAM) user flows. |
| Authentication methods for MFA | For internal users (employees and admins):<br>- [Authentication and verification methods](../../identity/authentication/overview-authentication)<br><br>For guests (invited or self-service sign-up):<br>- [Authentication methods for guest MFA](../authentication-conditional-access#table-1-authentication-strength-mfa-methods-for-external-users) | For self-service sign-up users (consumers, business customers):<br>- [Emailed one-time passcode](concept-multifactor-authentication-customers#email-one-time-passcode)<br>- [SMS-based authentication](concept-multifactor-authentication-customers#sms-based-authentication)<br>- [Time-based one-time password (TOTP)](concept-multifactor-authentication-customers#time-based-one-time-password-totp)<br>- [Passkey (FIDO2)](how-to-sign-in-with-passkey)<br><br>For invited users:<br>- [Emailed one-time passcode](concept-multifactor-authentication-customers#email-one-time-passcode)<br>- [SMS-based authentication](concept-multifactor-authentication-customers#sms-based-authentication) |

### Authentication methods available in External ID

You can use some authentication methods as the primary factor when users sign in to an application, such as username and password. Other authentication methods are available only as a secondary factor. The following table outlines when you can use an authentication method during sign-in, self-service sign-up, self-service password reset, and MFA in External ID.

This table lists tenant-level method availability. Confirm method and journey availability for your approach in the approach-specific guidance.

**Legend:**![Supported](../media/common/applies-to-yes.png) Supported. Not applicable means the method isn't used for that operation.

| Method | Sign-in | Sign-up | Password reset | MFA |
| --- | --- | --- | --- | --- |
| [Email with password](concept-authentication-methods-customers#email-and-password-sign-in) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| [Email one-time passcode](concept-authentication-methods-customers#email-with-one-time-passcode-sign-in) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) |
| [SMS-based authentication](concept-multifactor-authentication-customers#sms-based-authentication) | Not applicable | Not applicable | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) |
| [Time-based one-time password (TOTP)](concept-multifactor-authentication-customers#time-based-one-time-password-totp) | Not applicable | Not applicable | Not applicable | ![Supported](../media/common/applies-to-yes.png) |
| [Passkey (FIDO2)](how-to-sign-in-with-passkey) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable | ![Supported](../media/common/applies-to-yes.png) |
| [Apple federation](how-to-apple-federation-customers) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| [Facebook federation](how-to-facebook-federation-customers) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| [Google federation](how-to-google-federation-customers) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| Microsoft personal account ([OpenID Connect](how-to-custom-oidc-federation-customers)) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| [Microsoft Entra ID federation](how-to-entra-id-federation-customers) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| [OpenID Connect federation](how-to-custom-oidc-federation-customers) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |
| [SAML/WS-Fed federation](../direct-federation) | ![Supported](../media/common/applies-to-yes.png) | ![Supported](../media/common/applies-to-yes.png) | Not applicable | Not applicable |

## Application registration

The following table compares the features for [application registration](../../identity-platform/quickstart-register-app) in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Protocol | Protocols include SAML relying parties, OpenID Connect, and OAuth2. | Protocols include [SAML relying parties](how-to-register-saml-app), [OpenID Connect](../../identity-platform/quickstart-register-app), and OAuth2. |
| Supported account types | The following [account types](../../identity-platform/quickstart-register-app#register-an-application) are available: <br>- Accounts in this organizational directory only (single tenant)<br>- Accounts in any organizational directory (any Microsoft Entra tenant in a multitenant configuration)<br>- Accounts in any organizational directory (any Microsoft Entra tenant in a multitenant configuration) and personal Microsoft accounts (such as Skype and Xbox)<br>- Personal Microsoft accounts only | Always use accounts in this organizational directory only (single tenant). |
| Platform | The following [platforms](../../identity-platform/how-to-add-redirect-uri) are available: <br>- Public client/native (mobile and desktop)<br>- Web<br>- Single-page application (SPA) | The following [platforms](../../identity-platform/how-to-add-redirect-uri) are available: <br>- Public client (mobile and desktop)<br>- Web<br>- SPA<br>- Embedded native authentication for [mobile](../../identity-platform/concept-native-authentication) and [single-page](../../identity-platform/concept-native-authentication-cors#proxy-contract) applications |
| Redirect URIs for authentication | Microsoft Entra ID accepts these URIs as destinations when it returns authentication responses (tokens) after successfully authenticating or signing out users. | Supported. |
| Front-channel logout URL for authentication | This URL is where Microsoft Entra ID sends a request to have the application clear the user's session data. The front-channel logout URL is required for single sign-out to work correctly. | Supported; required for single sign-out. |
| Implicit grant and hybrid flows for authentication | Request a token directly from the authorization endpoint. | Supported. |
| Certificates and secrets | Multiple credentials are available: <br>- [Certificates](../../identity-platform/how-to-add-credentials?tabs=certificate)<br>- [Client secrets](../../identity-platform/how-to-add-credentials?tabs=client-secret)<br>- [Federated credentials](../../identity-platform/how-to-add-credentials?tabs=federated-credential) | Certificates, client secrets, and federated credentials. |
| Rotation for certificates and secrets | Update client credentials to help ensure that they remain valid and secure, while users can continue to sign-in. You can rotate [certificates](../../identity-platform/how-to-add-credentials?tabs=certificate), [secrets](../../identity-platform/how-to-add-credentials?tabs=client-secret), and [federated credentials](../../identity-platform/how-to-add-credentials?tabs=federated-credential) by adding a new one and then removing the old one. | Supported for certificates, client secrets, and federated credentials. |
| Policy for certificates and secrets | Configure the [application management policies](../../identity/enterprise-apps/tutorial-enforce-secret-standards) to enforce secret and certificate restrictions. | Not supported. |
| API permissions | Add, remove, and replace permissions to an application. After permissions are added to your application, users or admins need to grant consent to the new permissions. [Learn more about updating an app's requested permissions in Microsoft Entra ID](../../identity-platform/howto-update-permissions). | The following permissions are allowed: Microsoft Graph `offline_access`, `openid`, and `User.Read`, along with your **My APIs** delegated permissions. Only an admin can consent on behalf of the organization. |
| Expose an API | [Define custom scopes](../../identity-platform/quickstart-configure-app-expose-web-apis) to restrict access to data and functionality that the API helps protect. An application that requires access to parts of this API can request user or admin consent to one or more of these scopes. | Supported. |
| Owners | Application owners can view and edit the application registration. Additionally, any user (who might not be listed) with administrative privileges to manage any application (for example, [Cloud Application Administrator](../../identity/role-based-access-control/permissions-reference#cloud-application-administrator)) can view and edit the application registration. | App ownership is supported, but [default permissions](reference-user-permissions#default-permissions) differ from workforce tenants. Owners, including invited users, should be assigned the Application Developer role to manage credentials and other properties of owned app registrations. The Application Administrator and Cloud Application Administrator roles provide broader application-management permissions, regardless of ownership. |
| Roles and administrators | [Administrative roles](../../identity/role-based-access-control/permissions-reference) are used for granting access for privileged actions in Microsoft Entra ID. | [Cloud Application Administrators](../../identity/role-based-access-control/permissions-reference#cloud-application-administrator) can create and manage application registrations and enterprise applications in external tenants. Other roles support application management according to their permissions. For users who need to manage only app registrations they own, Application Developer is the least-privileged built-in role. |

### Access control for applications

The following table compares the features for application authorization in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Role-based access control (RBAC) | You can define [application roles](../../identity-platform/custom-rbac-for-developers#app-roles) for your application and assign those roles to users and groups. Microsoft Entra ID includes the user roles in the security token. Your application can then make authorization decisions based on the values in the security token. | Supported. [Use role-based access control for applications in an external tenant](how-to-use-app-roles-customers). For available features, see [Groups and application roles support](reference-group-app-roles-support). |
| Security groups | You can use [security groups](../../identity-platform/custom-rbac-for-developers#groups) to implement RBAC in your applications, where the memberships of users in specific groups are interpreted as their role memberships. Microsoft Entra ID includes user group membership in the security token. Your application can then make authorization decisions based on the values in the security token. | Supported. The [group optional claims](../../identity-platform/optional-claims#configure-groups-optional-claims) are limited to the group object ID. |
| Attribute-based access control (ABAC) | You can configure the app to include user attributes in the access token. Your application can then make authorization decisions based on the values in the security token. For more information, see Token customization. | Supported. |
| Require user assignment | When user assignment is required, only the users you assign to the application (either through direct user assignment or based on group membership) can sign in. For more information, see [Manage user and group assignments to an application](../../identity-platform/howto-restrict-your-app-to-a-set-of-users). | Supported. For details, see [Groups and application roles support](reference-group-app-roles-support). |

## Enterprise applications

The following table compares the unique features for [enterprise application](/en-us/entra/identity/enterprise-apps/) registration in workforce and external tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Application gallery | The [application gallery](/en-us/entra/identity/enterprise-apps/overview-application-gallery) contains thousands of applications that are integrated into Microsoft Entra ID. | Choose from a range of integrated apps. To find a partner app, use the search bar. The application gallery catalog isn't available. |
| Register a custom enterprise application | [Add an enterprise application.](/en-us/entra/identity/enterprise-apps/add-application-portal) | [Register a SAML app in your external tenant.](/en-us/entra/external-id/customers/how-to-register-saml-app) |
| Self-service application assignment | Let users [self-discover apps](/en-us/entra/identity/enterprise-apps/manage-self-service-access). | Self-service application assignment in the [My Apps portal](/en-us/entra/identity/enterprise-apps/myapps-overview) isn't available. |
| Application proxy | [Microsoft Entra application proxy](/en-us/entra/identity/app-proxy/overview-what-is-app-proxy) provides secure remote access to on-premises web applications. | Not supported. |
| Deactivate app registration | [Deactivate an app registration](/en-us/entra/identity/enterprise-apps/deactivate-app-registration) to prevent token issuance while preserving configuration. | Supported. |

### Consent and permission features for enterprise applications

The following table shows which consent and permission features are available for enterprise applications in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Admin consent for enterprise applications | You can [grant tenant-wide admin permissions](/en-us/entra/identity/enterprise-apps/grant-admin-consent). You can also [review and revoke](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=portal) them. | Supported. |
| User consent for enterprise applications | You can configure how [users consent to applications](/en-us/entra/identity/enterprise-apps/configure-user-consent), and you can [update these permissions](/en-us/entra/identity-platform/howto-update-permissions). | Limited to permissions that don't require [admin consent](/en-us/entra/identity/enterprise-apps/grant-admin-consent). |
| Review or revoke admin consent | [Review and revoke](/en-us/entra/identity/enterprise-apps/manage-application-permissions) permissions. | [Use the Microsoft Entra admin center](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=portal) to revoke admin consent. |
| Review or revoke user consent | [Review and revoke](/en-us/entra/identity/enterprise-apps/manage-application-permissions) permissions. | Use [Microsoft Graph API](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=ms-graph) or [PowerShell](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=entra-powershell) to revoke user consent. |
| Assign users or groups to apps | You can [manage access to apps](/en-us/entra/identity/enterprise-apps/what-is-access-management) in an individual or group-based assignment. [Nested group](/en-us/entra/fundamentals/how-to-manage-groups) memberships aren't supported. | Supported; nested groups aren't supported. |
| RBAC for app roles | You can define and assign roles for fine-grained [access control](/en-us/entra/external-id/customers/how-to-use-app-roles-customers). | Supported. |

## OpenID Connect and OAuth2 flows

The following table compares tenant-level OAuth 2.0 and OpenID Connect capabilities. It doesn't define the supported request parameters for the Native Authentication API or the BYO UX handoff.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| [OpenID Connect](../../identity-platform/v2-protocols-oidc) | Supported. | Supported. |
| [Authorization code](../../identity-platform/v2-oauth2-auth-code-flow) | Supported. | Supported. |
| [Authorization code with Proof Key for Code Exchange (PKCE)](../../identity-platform/v2-oauth2-auth-code-flow) | Supported. | Supported. |
| [Client credentials](../../identity-platform/v2-oauth2-client-creds-grant-flow) | Supported. | Supported for [v2.0 applications](../../identity-platform/reference-app-manifest). |
| [Device authorization](../../identity-platform/v2-oauth2-device-code) | Supported. | Supported. |
| [On-behalf-of flow](../../identity-platform/v2-oauth2-on-behalf-of-flow) | Supported. | Supported. |
| [Implicit grant](../../identity-platform/v2-oauth2-implicit-grant-flow) | Supported. | Supported. |
| [Resource owner password credentials](../../identity-platform/v2-oauth-ropc) | Supported. | Not supported; for mobile applications, use [Embedded native authentication](../../identity-platform/concept-native-authentication). |

### Authority URL in OpenID Connect and OAuth2 flows

The authority URL indicates a directory that the Microsoft Authentication Library (MSAL) can request tokens from. For Microsoft-hosted authentication in external tenants, use the default `<tenant-name>.ciamlogin.com` domain or a tenant-verified custom URL domain.

For browser-based apps using the Native Authentication API V2 and Bring Your Own UX (BYO UX), use a [tenant-verified custom domain](concept-custom-url-domain) and include the tenant GUID in the URL path. This browser requirement helps protect against cross-site request forgery (CSRF). Non-browser clients, such as iOS and Android apps using native HTTP transports, don't require a custom domain. See [Configure the API authority](../../identity-platform/how-to-native-authentication-configure-app#configure-the-api-authority).

The following JSON shows a Microsoft-hosted authentication example in a .NET application's `appsettings.json` file:

```json
{
    "AzureAd": {
        "Authority": "https://<Enter_the_Tenant_Subdomain_Here>.ciamlogin.com/",
        "ClientId": "<Enter_the_Application_Id_Here>"
    }
}
```

## Conditional Access

The following table compares the features for Microsoft Entra Conditional Access in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Assignments | [Users, groups](../../identity/conditional-access/concept-conditional-access-users-groups), and [workload identities](../../identity/conditional-access/concept-conditional-access-users-groups#workload-identities). | Include all users, and exclude users and groups. For more information, see [Add multifactor authentication (MFA) to an app](how-to-multifactor-authentication-customers). |
| Target resources | - [Cloud apps](../../identity/conditional-access/concept-conditional-access-cloud-apps)<br>- [User actions](../../identity/conditional-access/concept-conditional-access-cloud-apps#user-actions)<br>- [Global Secure Access](../../identity/conditional-access/concept-conditional-access-cloud-apps#traffic-forwarding-profiles)<br>- [Authentication context](../../identity/conditional-access/concept-conditional-access-cloud-apps#authentication-context) | - [All resources, selected apps](how-to-multifactor-authentication-customers), or [filter applications](../../identity/conditional-access/concept-filter-for-applications)<br>- [Authentication context](../../identity/conditional-access/concept-conditional-access-cloud-apps#authentication-context) |
| Conditions | - [Sign-in risk](../../identity/conditional-access/concept-conditional-access-conditions#sign-in-risk)<br>- [User risk](../../identity/conditional-access/concept-conditional-access-conditions#user-risk)<br>- [Device platforms](../../identity/conditional-access/concept-conditional-access-conditions#device-platforms)<br>- [Locations](../../identity/conditional-access/concept-conditional-access-conditions#locations)<br>- [Client apps](../../identity/conditional-access/concept-conditional-access-conditions#client-apps)<br>- [Filter for devices](../../identity/conditional-access/concept-conditional-access-conditions#filter-for-devices) | - [Device platforms](../../identity/conditional-access/concept-conditional-access-conditions#device-platforms)<br>- [Locations](../../identity/conditional-access/concept-conditional-access-conditions#locations) |
| Grant | [Grant or block access to resources](../../identity/conditional-access/concept-conditional-access-grant) | - [Block access](../../identity/conditional-access/concept-conditional-access-grant#block-access)<br>- [Require multifactor authentication](how-to-multifactor-authentication-customers)<br>- [Require password reset](how-to-enable-password-reset-customers) |
| Session | [Session controls](../../identity/conditional-access/concept-conditional-access-session) | The following session controls are available: <br>- [Sign-in frequency (SIF)](../../identity/conditional-access/concept-session-lifetime#user-sign-in-frequency) for Microsoft-hosted authentication and supported Embedded native authentication integrations. Availability can differ by approach and API or SDK version.<br>- Persistent browser session for browser-based sessions. |

## Terms-of-use policies

The following table compares the features for terms-of-use policies in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Conditional Access policies | See the [Microsoft Entra terms of use](../../identity/conditional-access/terms-of-use). | Not supported. |
| Self-service sign-up | Not supported. | Add a [required attribute](how-to-define-custom-attributes#configure-a-single-select-checkbox-checkboxsingleselect) linked to your terms-of-use policies on the sign-up page. You can customize the hyperlink to support various languages. |
| Sign-in page | You can add links to the lower-right corner for privacy information by using [company branding](../../fundamentals/how-to-customize-branding). | [Add privacy and terms-of-use links](how-to-customize-branding-customers#to-customize-the-logo-privacy-link-and-terms-of-use). |

## Account management

The following table compares the features for user management in each type of tenant. As noted in the table, certain account types are created through invitation or self-service sign-up. A user admin in the tenant can also create accounts via the admin center.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Types of accounts | - Internal members, such as employees and admins.<br>- External users who are [invited](../what-is-b2b) or use self-service sign-up. | - External users created through self-service sign-up or [by an admin](how-to-manage-customer-accounts).<br>- Internal users, with or without an admin role.<br>- Invited users, with or without an admin role.<br><br> All users in an external tenant have [default permissions](reference-user-permissions) unless they're assigned an [admin role](how-to-manage-admin-accounts). |
| Manage user profile info | - Manage users programmatically and by [using the admin center](../../fundamentals/how-to-manage-user-profile-info).<br>- Manage guest users across tenants with [cross-tenant synchronization](/en-us/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview). | Manage users in the admin center or programmatically. Cross-tenant synchronization isn't available. |
| Reset a user's password | Administrators can [reset a user's password](../../fundamentals/users-reset-password-azure-portal) if the user forgets the password, is locked out of a device, or never received a password. | Supported. |
| Restore or remove a recently deleted user | After you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, the user account can be restored, along with all its properties. | Supported. Restore users and their properties within 30 days. |
| Disable accounts | Prevent the new user from signing in. | Supported. |

## Password protection

The following table compares the features for password protection in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Smart lockout | [Smart lockout](../../identity/authentication/howto-password-smart-lockout) helps lock out bad actors who try to guess your users' passwords or use brute-force methods to get in. | Supported. |
| Global banned passwords | The [global banned passwords list](../../identity/authentication/concept-password-ban-bad#global-banned-password-list) automatically blocks commonly used weak or compromised passwords based on analysis of Microsoft Entra security data. | Supported. |
| Custom banned passwords | Use the [custom banned passwords list](../../identity/authentication/tutorial-configure-custom-password-protection) to add specific strings to evaluate and block during password creation and reset. | Supported. |

## Token customization

The following table compares the features for token customization in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Claims mapping | [Customize claims](../../identity-platform/jwt-claims-customization) issued in the JSON web token (JWT) for enterprise applications. | Supported. Configure optional claims through [Attributes & Claims](how-to-add-attributes-to-token). |
| Claims transformation | [Apply a transformation to a user attribute](../../identity-platform/jwt-claims-customization) issued in the JWT for enterprise applications. | Supported. |
| Custom claims provider | Use a [custom authentication extension](../../identity-platform/custom-extension-overview) that calls an external REST API to fetch claims from external systems. | Supported. [Custom claims provider](../../identity-platform/custom-claims-provider-overview). |
| Security groups | [Configure group optional claims](../../identity-platform/optional-claims#configure-groups-optional-claims). | [Configure group optional claims](../../identity-platform/optional-claims#configure-groups-optional-claims), limited to the group object ID. |
| Token lifetimes | [Specify the lifetime](../../identity-platform/configurable-token-lifetimes) of security tokens issued by Microsoft Entra ID. | Supported. |
| Session and token revocation | An administrator can [invalidate all the refresh tokens and session](/en-us/graph/api/user-revokesigninsessions) for a user. | Supported. |

## Single sign-on

[Single sign-on (SSO)](../../identity-platform/msal-js-sso) provides a more seamless experience by reducing the number of times a user is asked for credentials. Users enter their credentials once. Other applications can reuse the established session on the same device and web browser without further prompting.

The following table compares browser-based SSO in each type of tenant. For Embedded native authentication and BYO UX session boundaries, see Integration, policy, and sessions by approach.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Types of application registration | - OpenID Connect<br>- OAuth 2.0<br>- SAML (enterprise application)<br><br>Enterprise applications offer [more options](../../identity/enterprise-apps/plan-sso-deployment), like password-based, linked, and header-based registration. | - OpenID Connect<br>- OAuth 2.0<br>- SAML (enterprise application) |
| Domain name | When a user is authenticated, a session cookie is set on the Microsoft Entra domain `login.microsoftonline.com` in the web browser. | When a user is authenticated, a session cookie is set on the Microsoft Entra External ID domain `<tenant-name>.ciamlogin.com` or a [custom URL domain](concept-custom-url-domain) in the web browser. To ensure that SSO functions correctly, use a single URL domain. |
| Stay signed in | You can turn on or turn off the option to [stay signed in](../../fundamentals/how-to-manage-stay-signed-in-prompt). | The **Stay signed in?** prompt appears by default. To change or suppress it, use the **Persistent browser session** session control in a Conditional Access policy. [Learn more](how-to-user-flow-sign-up-sign-in-customers#control-the-stay-signed-in-prompt). |
| User provisioning | Use [automatic user provisioning](/en-us/entra/architecture/sync-scim) with System for Cross-domain Identity Management (SCIM) to sync user accounts between External ID and supported apps. This approach keeps user data up to date automatically. User provisioning supports differential queries. These queries sync only the changes since the last update. This behavior improves performance and reduces system load. | Supported, including differential queries. |
| Session invalidation | Scenarios where SSO might be invalidated, which requires reauthentication: <br>- Session expiry<br>- Browser issues, such as clearing browser cookies or cache<br>- Conditional Access policy, such as a multifactor authentication requirement<br>- [Session revocation](/en-us/graph/api/user-revokesigninsessions)<br>- Security issues, such as suspicious activity<br><br>The application specifies in the authorization request to prompt the user for credentials by using the `prompt=login` query string parameter in OpenID Connect and the `ForceAuthn` attribute in the SAML request. | Session expiration, browser state, Conditional Access, revocation, and security events can require reauthentication. Apps can also request reauthentication. |
| Conditional Access | Check the Conditional Access section. | Check the Conditional Access section. |
| Sign-out | When a [SAML](../../identity-platform/single-sign-out-saml-protocol) or [OpenID Connect](../../identity-platform/v2-protocols-oidc#send-a-sign-out-request) application directs the user to the logout endpoint, Microsoft Entra ID removes and invalidates the user's session from the browser. | Supported for SAML and OpenID Connect apps. |
| Single sign-out | Upon successful sign-out, Microsoft Entra ID sends a sign-out notification to all other [SAML](../../identity-platform/single-sign-out-saml-protocol) and [OpenID Connect](../../identity-platform/v2-protocols-oidc#single-sign-out) applications that the user is signed in to. | Supported for SAML and OpenID Connect apps. |

Review your approach's session requirements for browser-session reuse and single sign-out.

## Integrated security solutions

Microsoft Entra External ID supports integrated security features and partner solutions to help protect identities across the lifecycle. These capabilities include protection against distributed denial-of-service (DDoS) attacks, prevention of sign-up fraud, and unified monitoring.

You can enable these solutions directly in External ID and access partner integrations through the [Microsoft Security Store](https://securitystore.microsoft.com/). This approach allows organizations to deploy trusted security tools quickly without complex setup.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Sign-up fraud protection | The Security Store wizard experience isn't available. | Use [Arkose Labs](/en-us/entra/external-id/customers/how-to-integrate-fraud-protection?pivots=arkose) and [HUMAN Security](/en-us/entra/external-id/customers/how-to-integrate-fraud-protection?pivots=human) to help protect against sign-up fraud and block automated bot attacks. |
| DDoS and web application firewall (WAF) protection | The Security Store wizard experience isn't available. | Use [Cloudflare](/en-us/entra/external-id/customers/how-to-configure-waf-integration) and [Akamai](/en-us/entra/external-id/customers/how-to-configure-akamai-integration) to help protect against DDoS attacks and secure apps with a WAF. |
| Security analytics | The Security Store wizard experience isn't available. | Use [Azure Monitor and Microsoft Sentinel](/en-us/entra/external-id/customers/how-to-azure-monitor) to enable one-click monitoring, Log Analytics, and advanced threat detection. |

### Akamai and Cloudflare

[Akamai](/en-us/entra/external-id/customers/how-to-configure-akamai-integration) and [Cloudflare](/en-us/entra/external-id/customers/how-to-configure-waf-integration) provide DDoS protection, bot mitigation, and WAF capabilities. These capabilities help defend applications against malicious traffic, abusive automation, and common web vulnerabilities such as SQL injection, cross‑site scripting, and API‑based attacks.

When you integrate either service with External ID, you can apply these security controls in front of your customer-facing identity flows. This action improves resilience and reduces exposure to credential stuffing and other identity‑targeted threats.

## Activity logs and reports

The following table compares the features for activity logs and reports across various types of tenants.

Important

Sign-up logs and Azure Monitor for external tenants are in preview. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| [Audit logs](../../identity/monitoring-health/concept-audit-logs) | These logs provide a detailed report of all events logged in Microsoft Entra ID, including modifications to applications, groups, and users. | Supported. |
| [Sign-in logs](../../identity/monitoring-health/concept-sign-ins) | The sign-in logs track all sign-in activities within a Microsoft Entra tenant, including access to your applications and resources. | Supported. |
| [Sign-up logs](../../identity/monitoring-health/concept-sign-ups) | Not supported. | Microsoft Entra External ID logs all self-service sign-up events, including both successful sign-ups and failed attempts. |
| [Provisioning logs](../../identity/monitoring-health/concept-provisioning-logs) | The provisioning logs provide detailed records of provisioning events within a tenant, such as user account creations, updates, and deletions. | Not supported. |
| [Activity logs for retention policies](../../identity/monitoring-health/concept-provisioning-logs) | Microsoft Entra data retention policies determine how long various types of logs (like audit, sign-in, and provisioning logs) are stored. | Seven days. |
| [Export activity logs](../../identity/monitoring-health/howto-configure-diagnostic-settings) | By using diagnostic settings in Microsoft Entra ID, you can integrate logs with Azure Monitor, stream logs to an event hub, or integrate with security information and event management (SIEM) tools. | [Azure Monitor for external tenants](how-to-azure-monitor). |
| [Reports for application user activity](how-to-user-insights) (retiring August 31, 2026; see [migration guidance](how-to-user-insights#migrate-from-user-insights)) | Not supported. | Application user activity provides analytics on how users interact with registered applications in your tenant. It tracks metrics like active users, new users, sign-ins, and MFA success rates. |

## Microsoft Graph APIs

Use Microsoft Graph APIs to automate supported tenant administration operations. Check each operation's permissions and requirements; tenant administration support doesn't establish direct Microsoft Graph access from a BYO UX page or interoperability with native-issued tokens. For more information, see [Manage Microsoft Entra identity and network access by using Microsoft Graph](/en-us/graph/api/resources/identity-network-access-overview).