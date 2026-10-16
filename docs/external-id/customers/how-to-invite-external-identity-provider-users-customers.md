---
layout: Conceptual
title: Route Invited Users to an External Identity Provider - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-invite-external-identity-provider-users-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: nanguil
ms.author: nguilanians
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to invite users to a Microsoft Entra external tenant and route them to a configured OpenID Connect, SAML/WS-Federation, or social identity provider.
ms.topic: how-to
ms.date: 2026-10-12T00:00:00.0000000Z
ms.custom: it-pro, msecd-doc-authoring-1026
ai-usage: ai-assisted
locale: en-us
document_id: 87f07353-3fb2-4779-484c-8834269c59fa
document_version_independent_id: 87f07353-3fb2-4779-484c-8834269c59fa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-invite-external-identity-provider-users-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-invite-external-identity-provider-users-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-invite-external-identity-provider-users-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b17504fc-0d9b-8ec4-20e3-dae015e22086
---

# Route Invited Users to an External Identity Provider - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

You can invite consumers, business customers, and admins to a Microsoft Entra external tenant. By default, the [invitation redemption flow](../redemption-experience#invitation-redemption-flow) determines how an invited user authenticates. This article describes how to explicitly route an invited user to a configured external identity provider (IdP), such as a social provider, custom OpenID Connect (OIDC) provider, or Security Assertion Markup Language (SAML)/WS-Federation provider.

Explicit identity provider routing is useful when:

- Only invited users should be able to access your application (no self-service sign-up).
- Users must authenticate with a specific external identity provider.
- You want full control over the invitation experience and communication.

Before you begin, ensure you have an external tenant, registered application, associated user flow, configured identity provider, and the provider's `domain_hint` value.

## Prerequisites

- A [Microsoft Entra External ID tenant](how-to-create-external-tenant-portal).
- A configured external identity provider: [Custom OIDC](how-to-custom-oidc-federation-customers), [Microsoft Entra ID](how-to-entra-id-federation-customers), [SAML/WS-Fed](../direct-federation), or a social provider ([Google](how-to-google-federation-customers), [Facebook](how-to-facebook-federation-customers), [Apple](how-to-apple-federation-customers)).
- A [registered application](/en-us/entra/identity-platform/quickstart-register-app) in your external tenant.
- A [user flow](how-to-user-flow-sign-up-sign-in-customers) associated with your application. The user flow is required even if sign-up is disabled. You don't need to add the identity provider to the user flow when you route invited users by using `domain_hint`.
- The `domain_hint` value for the identity provider, as described in [Issuer acceleration](concept-authentication-methods-customers#issuer-acceleration).

Important

The `domain_hint` parameter changes authentication routing during invitation redemption. It isn't required to invite a user, doesn't determine who is eligible for an invitation, and doesn't grant access to an application. When you use `domain_hint` to route a user from another Microsoft Entra tenant to custom OIDC federation, the sign-in doesn't use the native Microsoft Entra business-to-business (B2B) federation path or its home-tenant multifactor authentication (MFA) trust.

## Disable self-service sign-up (optional)

If you want only explicitly invited users to access your application, disable sign-up in your user flow. This prevents users who aren't invited from creating accounts through self-service registration. Your application still controls authorization for invited users.

For detailed steps on finding your user flow ID and disabling sign-up, see [Disable sign-up in a user flow](how-to-disable-sign-up-user-flow).

## Invite users

You can invite users by using either the Microsoft Graph API or the admin center. Configure the invitation not to send the default email. Instead, send a custom email with an application link after you create the invitation (next step).

Regardless of which option you use, when the invitation is created:

- A user object is created in the external tenant with `externalUserState` set to `PendingAcceptance`.
- No identity provider is yet associated with the user object.

Note

Unlike self-service sign-up users, invited users aren't prompted for additional attributes during sign-in. Their user properties are based on the invitation and claims received from the external identity provider.

### Option 1: Use the Microsoft Graph invitation API

Create a user in the External ID tenant using the [Microsoft Graph Invitation API](/en-us/graph/api/invitation-post).

```http
POST https://graph.microsoft.com/v1.0/invitations
Content-Type: application/json

{
    "invitedUserEmailAddress": "user@contoso.com",
    "inviteRedirectUrl": "https://your-app-url.com",
    "sendInvitationMessage": false
}
```

### Option 2: Use the admin center

You can also invite users through the Microsoft Entra admin center using the [Invite external user](../../fundamentals/how-to-create-delete-users#invite-an-external-user) option. To use this pattern, disable the default Microsoft invitation email and send your own custom invitation containing the `domain_hint` parameter as described in the next step.

## Send a custom invitation email with the `domain_hint` parameter

After creating the user, send your own email with a link to an application route that starts the External ID authorization request. Configure the application route to pass the `domain_hint` parameter in the authorization request so that External ID routes the user to the specified identity provider.

The application route depends on your application. For example:

```text
https://<app-url>/<sign-in-route>?domain_hint=<identity-provider-domain>
```

Use the `domain_hint` value specified for your provider in [Issuer acceleration](concept-authentication-methods-customers#issuer-acceleration). For example, for custom OIDC, use the domain part of the issuer URI. For a Microsoft Entra ID tenant configured as a custom OIDC provider, use the tenant domain, such as `contoso.onmicrosoft.com`.

Include this link in your custom invitation email. For example:

> 
> **Subject**: You're invited to access [Your Application Name]
> 
> Hello,
> 
> You've been invited to access [Your Application Name]. Select the following link to get started:
> 
> [Accept invitation and sign in](https://your-app-url.com/signin?domain_hint=contoso.onmicrosoft.com)
> 
> You'll be asked to sign in with your existing credentials.

Note

If you use the default Microsoft invitation email, the [invitation redemption flow](../redemption-experience#invitation-redemption-flow) determines how the user authenticates and might not route the user to your intended identity provider.

## End-user experience

After you complete the configuration and send the invitation, here's what the invited user experiences.

### First sign-in (invitation redemption)

1. The user receives your custom invitation email and selects the link that includes the `domain_hint` parameter.
2. The application starts the External ID authorization request with the `domain_hint` parameter, and the user is routed to the specified identity provider.
3. The user authenticates with their existing credentials at the identity provider.
4. The invitation is redeemed. In your external tenant, the user object is updated:
    - A federated identity is added to the `identities` collection.
    - The `externalUserState` changes to `Accepted`.

Note

The `domain_hint` parameter is only required during this initial invitation redemption step.

### Subsequent sign-ins

After the user completes invitation redemption:

1. The user navigates to your application (no `domain_hint` parameter is needed).
2. The user enters their email address on the sign-in page.
3. The user is recognized as an existing user and is redirected to the identity provider used during invitation redemption.