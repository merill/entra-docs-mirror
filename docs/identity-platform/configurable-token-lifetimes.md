---
layout: Conceptual
title: Configurable Token Lifetimes - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/configurable-token-lifetimes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure token lifetimes for access, SAML, and ID tokens in Microsoft Identity Platform to enhance security.
manager: pmwongera
ms.custom: 
ms.date: 2026-04-08T00:00:00.0000000Z
ms.reviewer: sreyanthmora
ms.topic: concept-article
locale: en-us
document_id: 91a7cf26-4ebf-b9b5-099d-c43bfa33beb4
document_version_independent_id: 8566e04b-ee06-cc27-ab07-3e9fef576d6c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/configurable-token-lifetimes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/configurable-token-lifetimes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/configurable-token-lifetimes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 49745efe-f207-05af-9c21-078d5d9923b2
---

# Configurable Token Lifetimes - Microsoft identity platform | Microsoft Learn

You can configure the lifetime of access, ID, or Security Assertion Markup Language (SAML) tokens issued by the Microsoft identity platform. Token lifetimes can be set for all apps in your organization, multitenant applications, or specific service principals. Configuring token lifetimes for [managed identity service principals](../identity/managed-identities-azure-resources/overview) isn't supported.

In Microsoft Entra ID, policies define rules applied to individual applications or all applications in an organization. Each policy type has unique properties that determine how it is enforced on the object to which it's assigned.

A policy can be designated as the default for your organization, applying to all applications unless overridden by a higher-priority policy. Policies can also be assigned to specific applications, with priority varying by policy type.

For practical guidance, see [examples of how to configure token lifetimes](configure-token-lifetimes).

## Limitations and considerations

Before configuring token lifetime policies, be aware of the following:

- **No portal UI**: Token lifetime policies can only be managed through the Microsoft Graph API and Microsoft Graph PowerShell SDK. There's no configuration surface in the Microsoft Entra admin center.
- **SharePoint and OneDrive**: Configurable token lifetime policy only applies to mobile and desktop clients accessing SharePoint Online and OneDrive for Business resources. It doesn't apply to web browser sessions. To manage web browser session lifetimes, use [Conditional Access session lifetime](../identity/conditional-access/howto-conditional-access-session-lifetime). See the [SharePoint Online blog](https://techcommunity.microsoft.com/t5/SharePoint-Blog/Introducing-Idle-Session-Timeout-in-SharePoint-and-OneDrive/ba-p/119208) for configuring idle session timeouts.
- **Personal Microsoft accounts**: Token lifetime policies aren't supported for applications developed for personal Microsoft accounts (where `signInAudience` is set to `AzureADandPersonalMicrosoftAccount` or `PersonalMicrosoftAccount`).
- **Managed identities**: Configuring token lifetimes for [managed identity service principals](../identity/managed-identities-azure-resources/overview) isn't supported.
- **Refresh & session token lifetimes**: Refresh and session token lifetimes are no longer configurable through token lifetime policies. Microsoft Entra ID uses only the default values described below. To control how frequently users are required to sign in, use [Conditional Access sign-in frequency](../identity/conditional-access/howto-conditional-access-session-lifetime) instead.

## Token lifetime policies for access, SAML, and ID tokens

You can set token lifetime policies for access tokens, SAML tokens, and ID tokens.

### Access tokens

Clients use access tokens to access a protected resource. An access token can be used only for a specific combination of user, client, and resource. Adjusting the lifetime of an access token is a trade-off between improving system performance and increasing the amount of time that the client retains access after the user's account is disabled. Improved system performance is achieved by reducing the number of times a client needs to acquire a fresh access token.

The default lifetime of an access token is variable. When issued, an access token's default lifetime is assigned a random value ranging between 60-90 minutes (75 minutes on average). The default lifetime also varies depending on the client application requesting the token, the resource the token is issued for, and whether Conditional Access is enabled in the tenant. For more information, see [Access token lifetime](access-tokens#token-lifetime).

When both the client and the resource support [Continuous Access Evaluation (CAE)](../identity/conditional-access/concept-continuous-access-evaluation), the token lifetime may be automatically extended to 24-28 hours, when it is safe to do so. These long-lived tokens will be revoked in near real time in response to critical events such as account disablement and password changes. Learn more about [how CAE impacts the token lifetime](../identity/conditional-access/concept-continuous-access-evaluation#token-lifetime)

### SAML tokens

SAML tokens are used by many web-based SaaS applications, and are obtained using Microsoft Entra ID's SAML2 protocol endpoint. They're also consumed by applications using WS-Federation. The default lifetime of the token is 1 hour. From an application's perspective, the validity period of the token is specified by the NotOnOrAfter value of the `<conditions …>` element in the token. After the validity period of the token has ended, the client must initiate a new authentication request, which will often be satisfied without interactive sign in as a result of the Single Sign On (SSO) Session token.

The value of NotOnOrAfter can be changed using the `AccessTokenLifetime` parameter in a `TokenLifetimePolicy`. It will be set to the lifetime configured in the policy if any, plus a clock skew factor of five minutes.

The subject confirmation NotOnOrAfter specified in the `<SubjectConfirmationData>` element is not affected by the Token Lifetime configuration.

### ID tokens

ID tokens are passed to websites and native clients. ID tokens contain profile information about a user. An ID token is bound to a specific combination of user and client. ID tokens are considered valid until their expiry. Usually, a web application matches a user's session lifetime in the application to the lifetime of the ID token issued for the user. You can adjust the lifetime of an ID token to control how often the web application expires the application session, and how often it requires the user to be reauthenticated with the Microsoft identity platform (either silently or interactively).

## Configurable token lifetime properties

A token lifetime policy is a type of policy object that contains token lifetime rules. This policy controls how long access, SAML, and ID tokens for this resource are considered valid. Token lifetime policies can't be set for refresh and session tokens. If no policy is set, the system enforces the default lifetime value.

### Access, ID, and SAML2 token lifetime policy properties

Reducing the Access Token Lifetime helps limit the amount of time that a compromised access token or ID token can be used by a malicious actor. The trade-off is that performance is adversely affected, because the tokens have to be replaced more often.

For an example, see [Create a policy for web sign-in](configure-token-lifetimes).

Token lifetimes for access tokens, ID tokens, and SAML2 tokens are controlled by the following policy property:

- **Property**: Access Token Lifetime
- **Policy property string**: `AccessTokenLifetime`
- **Affects**: Access tokens, ID tokens, SAML2 tokens
- **Default**:
    - Access tokens: varies, depending on the client application requesting the token. CAE-capable clients that negotiate CAE-aware sessions may receive long-lived tokens (up to 28 hours).
    - ID tokens, SAML2 tokens: One hour
- **Minimum**: 10 minutes (`00:10:00`)
- **Maximum**: One day (`23:59:59`)

Note

Despite the name, `AccessTokenLifetime` controls the lifetime of access tokens, ID tokens, and SAML2 tokens.

## Policy evaluation and prioritization

You can create and then assign a token lifetime policy to a specific application and to your organization. Multiple policies might apply to a specific application. The token lifetime policy that takes effect follows these rules:

Important

For token lifetime policies, an **organization-level** policy takes precedence over an **application-level** policy. If your app-level policy doesn't seem to take effect, check whether an organization-level policy exists.

- If a policy is explicitly assigned to the organization, it's enforced.
- If no policy is explicitly assigned to the organization, the policy assigned to the application is enforced.
- If no policy has been assigned to the organization or the application object, the default values are enforced. (See the table in Configurable token lifetime properties.)

A token's validity is evaluated at the time the token is used. The policy with the highest priority on the application that is being accessed takes effect.

## Token lifetime policies for refresh tokens and session tokens (retired)

Important

As of January 30, 2021, refresh and session token lifetimes are no longer configurable through token lifetime policies. Microsoft Entra ID uses only the default values described below. To control how frequently users are required to sign in, use [Conditional Access sign-in frequency](../identity/conditional-access/howto-conditional-access-session-lifetime) instead.

If you have existing policies that set refresh or session token properties, those properties are ignored. New tokens are always issued with the default configuration.

### Refresh and session token defaults (not configurable)

The following table documents the default values that remain in effect. These values can't be changed through token lifetime policies.

| Property | Policy property string | Default |
| --- | --- | --- |
| Refresh Token Max Inactive Time | `MaxInactiveTime` | 90 days |
| Single-Factor Refresh Token Max Age | `MaxAgeSingleFactor` | Until-revoked |
| Multi-Factor Refresh Token Max Age | `MaxAgeMultiFactor` | Until-revoked |
| Single-Factor Session Token Max Age | `MaxAgeSessionSingleFactor` | Until-revoked |
| Multi-Factor Session Token Max Age | `MaxAgeSessionMultiFactor` | Until-revoked |

Non-persistent session tokens have a Max Inactive Time of 24 hours; persistent session tokens have a Max Inactive Time of 90 days. When the SSO session token is used within its validity period, the validity period is extended for another 24 hours or 90 days, respectively.

To find existing policies that might still contain retired refresh/session token properties, use the PowerShell cmdlets.

## REST API reference

Tip

All time durations are formatted using the C# [TimeSpan](/en-us/dotnet/api/system.timespan) format: `hh:mm:ss`. The minimum value of 10 minutes is `00:10:00` and the maximum value is `23:59:59`.

You can configure token lifetime policies and assign them to apps using Microsoft Graph. For more information, see the [`tokenLifetimePolicy` resource type](/en-us/graph/api/resources/tokenlifetimepolicy) and its associated methods.

## Cmdlet reference

These are the cmdlets in the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

### Manage policies

You can use the following commands to manage policies.

| Cmdlet | Description |
| --- | --- |
| [New-MgPolicyTokenLifetimePolicy](/en-us/powershell/module/microsoft.graph.identity.signins/new-mgpolicytokenlifetimepolicy) | Creates a new policy. |
| [Get-MgPolicyTokenLifetimePolicy](/en-us/powershell/module/microsoft.graph.identity.signins/get-mgpolicytokenlifetimepolicy) | Gets all token lifetime policies or a specified policy. |
| [Update-MgPolicyTokenLifetimePolicy](/en-us/powershell/module/microsoft.graph.identity.signins/update-mgpolicytokenlifetimepolicy) | Updates an existing policy. |
| [Remove-MgPolicyTokenLifetimePolicy](/en-us/powershell/module/microsoft.graph.identity.signins/remove-mgpolicytokenlifetimepolicy) | Deletes the specified policy. |

### Application policies

You can use the following cmdlets for application policies.

| Cmdlet | Description |
| --- | --- |
| [New-MgApplicationTokenLifetimePolicyByRef](/en-us/powershell/module/microsoft.graph.applications/new-mgapplicationtokenlifetimepolicybyref) | Links the specified policy to an application. |
| [Get-MgApplicationTokenLifetimePolicyByRef](/en-us/powershell/module/microsoft.graph.applications/get-mgapplicationtokenlifetimepolicybyref) | Gets the policies that are assigned to an application. |
| [Remove-MgApplicationTokenLifetimePolicyByRef](/en-us/powershell/module/microsoft.graph.applications/remove-mgapplicationtokenlifetimepolicybyref) | Removes a policy from an application. |