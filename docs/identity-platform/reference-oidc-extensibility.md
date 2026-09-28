---
layout: Conceptual
title: Microsoft identity platform OIDC extensibility reference - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/reference-oidc-extensibility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: jenniferf-skc
ms.author: jfields
ms.service: identity-platform
description: Map each Microsoft identity platform OpenID Connect (OIDC) extensibility surface to the configuration article and the Microsoft Graph API resource that programs it.
manager: pmwongera
ms.topic: reference
ms.date: 2026-06-23T00:00:00.0000000Z
ms.reviewer: jmprieur, ludwignick
ai-usage: ai-assisted
locale: en-us
document_id: 79e79541-942f-e20e-58a3-3ded169246fc
document_version_independent_id: 79e79541-942f-e20e-58a3-3ded169246fc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/reference-oidc-extensibility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/reference-oidc-extensibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/reference-oidc-extensibility.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: a78cdb4e-3b5e-40b7-9492-1dab266074fc
---

# Microsoft identity platform OIDC extensibility reference - Microsoft identity platform | Microsoft Learn

Use this reference to find every supported way to extend Microsoft identity platform OpenID Connect (OIDC) behavior. Each row links to the concept or how-to article in this repo and to the Microsoft Graph API resource that programs the surface.

Extensibility refers to changing how Microsoft Entra issues OIDC tokens or processes OIDC requests for apps you own — for example, adding claims from an external store, customizing token contents per app, or trusting tokens from external workload identities. Configuring an existing OIDC app (such as GitHub, Salesforce, or another SaaS app) to use Microsoft Entra for sign-in is *integration*, not extensibility. For app integration guidance, see [Microsoft Entra application gallery](../identity/enterprise-apps/overview-application-gallery).

For the underlying endpoint contracts, see [OpenID Connect on the Microsoft identity platform](v2-protocols-oidc).

## Extensibility surfaces at a glance

| Capability | What it lets you do | Concept and how-to | Microsoft Graph API |
| --- | --- | --- | --- |
| Custom claims provider | Call an external REST API during token issuance to enrich tokens with claims from a remote store. | [Custom claims provider overview](custom-claims-provider-overview), [Reference](custom-claims-provider-reference) | [customAuthenticationExtension](/en-us/graph/api/resources/customauthenticationextension), [onTokenIssuanceStartListener](/en-us/graph/api/resources/ontokenissuancestartlistener) |
| Token issuance start event | Configure the event listener that triggers your custom claims provider during token issuance. | [Set up token issuance start event](custom-extension-tokenissuancestart-setup), [Configure](custom-extension-tokenissuancestart-configuration) | [onTokenIssuanceStartCustomExtension](/en-us/graph/api/resources/ontokenissuancestartcustomextension), [onTokenIssuanceStartHandler](/en-us/graph/api/resources/ontokenissuancestarthandler), [onTokenIssuanceStartReturnClaim](/en-us/graph/api/resources/ontokenissuancestartreturnclaim) |
| Optional claims | Add Microsoft Entra-sourced claims (such as `groups`, `idtyp`, `login_hint`) to ID, access, and SAML tokens. | [Provide optional claims to your app](optional-claims), [Reference](optional-claims-reference) | [optionalClaim](/en-us/graph/api/resources/optionalclaim), [optionalClaims](/en-us/graph/api/resources/optionalclaims) on [application](/en-us/graph/api/resources/application) |
| Custom claims policy (per-app) | Map directory attributes to claims in tokens issued for a specific app, including transformations. | [JWT claims customization](jwt-claims-customization), [SAML claims customization](saml-claims-customization), [Custom claims policy](claims-customization-custom-claims-policy) | [customClaimsPolicy](/en-us/graph/api/resources/customclaimspolicy), [claimsMappingPolicy](/en-us/graph/api/resources/claimsmappingpolicy) |
| Token lifetime policy | Configure access, refresh, and ID token lifetimes for an app or tenant. | [Configurable token lifetimes](configurable-token-lifetimes), [Configure](configure-token-lifetimes) | [tokenLifetimePolicy](/en-us/graph/api/resources/tokenlifetimepolicy) |
| Token issuance policy | Configure SAML token signing and encryption behavior at issuance. | [SAML claims customization](saml-claims-customization) | [tokenIssuancePolicy](/en-us/graph/api/resources/tokenissuancepolicy) |
| Federated identity credentials | Trust tokens from external issuers (GitHub, Kubernetes, other clouds) instead of using a client secret or certificate. | [Workload identity federation](../workload-id/workload-identity-federation) | [federatedIdentityCredential](/en-us/graph/api/resources/federatedidentitycredential), [Federated identity credentials overview](/en-us/graph/api/resources/federatedidentitycredentials-overview) |
| Application manifest | Declaratively configure redirect URIs, audiences, allowed grant types, and token settings. | [Application manifest reference](reference-app-manifest) | [application](/en-us/graph/api/resources/application), [servicePrincipal](/en-us/graph/api/resources/serviceprincipal) |
| Delegated permission grants | Authorize delegated scopes for a user or tenant. | [Permissions and consent overview](permissions-consent-overview) | [oAuth2PermissionGrant](/en-us/graph/api/resources/oauth2permissiongrant) |
| App role assignments | Assign app roles to users, groups, or service principals for token-based authorization. | [App roles overview](howto-add-app-roles-in-apps) | [appRoleAssignment](/en-us/graph/api/resources/approleassignment) |
| Continuous access evaluation (CAE) | Enable token revocation in near real time for events such as user sign-out, password change, and risk detection. | [Continuous access evaluation](../identity/conditional-access/concept-continuous-access-evaluation) | [conditionalAccessPolicy](/en-us/graph/api/resources/conditionalaccesspolicy) |
| Claims challenge (step-up) | Request stronger authentication or fresher claims mid-session. | [Claims challenges](claims-challenge), [Claims validation](claims-validation) | N/A (protocol-level; signaled in the `claims` request parameter) |

## Choosing an extensibility surface

Use the following guidance to decide which surface fits your scenario:

- To add claims **sourced from Microsoft Entra ID**, use [optional claims](optional-claims) or a [custom claims policy](claims-customization-custom-claims-policy).
- To add claims **sourced from an external system**, use a [custom claims provider](custom-claims-provider-overview) backed by an Azure Functions endpoint or other REST API.
- To **trust an external workload identity** instead of using a client secret or certificate, configure a [federated identity credential](../workload-id/workload-identity-federation).
- To **react to security events** (revoked sessions, risk changes, password resets) on existing tokens, enable [continuous access evaluation](../identity/conditional-access/concept-continuous-access-evaluation).
- To **request fresher authentication** during a session, issue a [claims challenge](claims-challenge).

## Programming model

Most surfaces in the table are configured through the [Microsoft Graph application](/en-us/graph/api/resources/application) and [servicePrincipal](/en-us/graph/api/resources/serviceprincipal) resources or through the `policies` endpoint. Authentication libraries don't configure these surfaces; use Microsoft Graph SDKs, the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/overview), or direct REST calls.

For an end-to-end example that combines a custom authentication extension with a token issuance start event, see [Configure a custom claim provider with a token issuance start event](custom-extension-tokenissuancestart-configuration).