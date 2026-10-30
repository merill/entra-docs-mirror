---
layout: Conceptual
title: Continuous access evaluation for workload identities in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation-workload
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how continuous access evaluation for workload identities enforces Conditional Access policies in real time, instantly revokes tokens, and improves security for service principals.
ai-usage: ai-assisted
ms.topic: concept-article
ms.date: 2026-04-22T00:00:00.0000000Z
ms.reviewer: sreyanthmora
ms.custom:
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:08/28/2025
- ai-gen-description
locale: en-us
document_id: 5400b01e-9831-79bc-6b0b-df2ad5f3d39e
document_version_independent_id: ad6cc61e-58e6-a1af-eefa-9ed9b6496db5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-continuous-access-evaluation-workload.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-continuous-access-evaluation-workload
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-continuous-access-evaluation-workload.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 9e09c8be-7f5b-b10a-2f23-7c91e4e6a0ab
---

# Continuous access evaluation for workload identities in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Continuous access evaluation (CAE) for [workload identities](../../workload-id/workload-identities-overview) improves your organization's security by enforcing Conditional Access location and risk policies in real time. CAE instantly enforces token revocation events for workload identities, helping to prevent compromised service principals from accessing resources.

## Prerequisites

- [Workload Identities Premium](https://www.microsoft.com/security/business/identity-access/microsoft-entra-workload-identities#office-StandaloneSKU-k3hubfz) licenses are required to create or modify Conditional Access policies scoped to service principals. For more information, see [Conditional Access for workload identities](workload-identity).
- To create or modify Conditional Access policies, sign in as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
- CAE for workload identities supports single-tenant service principals registered in your tenant. Third-party SaaS and multitenant apps are out of scope.
- Managed identities aren't currently supported by CAE for workload identities.

## How CAE works for workload identities

CAE for workload identities extends the continuous access evaluation model to service principals. When a service principal opts in to CAE, the following flow applies:

1. A service principal requests an access token from Microsoft Entra ID for a supported resource provider, declaring the `cp1` client capability in the claims parameter of the token request.
2. Microsoft Entra ID evaluates applicable Conditional Access policies and issues a CAE-enabled access token. CAE-enabled tokens for workload identities are long-lived tokens (LLTs) with a lifetime of up to 24 hours.
3. The service principal presents the token to the resource provider (Microsoft Graph).
4. The resource provider evaluates the token against revocation events and Conditional Access policy changes synced from Microsoft Entra ID.
5. If a revocation event occurs (such as service principal disable or high risk detection), the resource provider rejects the token and returns a `401` response with a claims challenge.
6. The CAE-capable client handles the claims challenge by requesting a new token from Microsoft Entra ID, which reevaluates all conditions before issuing a new token.

Because CAE tokens for workload identities are long-lived (up to 24 hours), they reduce the need for frequent token requests while maintaining security through continuous evaluation.

Note

The preceding flow follows the general CAE model described in [Continuous access evaluation](concept-continuous-access-evaluation#example-flow-diagrams). Workload identity behavior aligns with this model, though specific implementation details may vary.

For more information about how claims challenges work, see [Claims challenges, claims requests, and client capabilities](../../identity-platform/claims-challenge).

## Supported scenarios

The following sections describe the resource providers, identities, events, and policies that CAE supports for workload identities.

### Resource providers

CAE for workload identities is supported only on access requests sent to Microsoft Graph as a resource provider.

### Supported identities

Service principals for line-of-business (LOB) applications are supported. The following constraints apply:

- Only single-tenant service principals registered in your tenant are supported.
- Third-party SaaS and multitenant apps are out of scope.
- Managed identities aren't supported.

### Revocation events

The following revocation events are supported:

- **Service principal disable** — An administrator disables the service principal in the tenant.
- **Service principal delete** — An administrator deletes the service principal from the tenant.
- **High service principal risk** — Microsoft Entra ID Protection detects high risk for the service principal. For more information, see [Securing workload identities with Microsoft Entra ID Protection](../../id-protection/concept-workload-identity-risk).

### Conditional Access policies

CAE for workload identities supports Conditional Access policies that target location and risk. To create these policies, see the step-by-step walkthroughs in [Conditional Access for workload identities](workload-identity#implementation).

## Enable your application

Developers can opt in to CAE for workload identities by declaring the `cp1` client capability when requesting tokens. Declaring `cp1` signals to Microsoft Entra ID that the client application can handle claims challenges. Microsoft Graph (the only supported resource provider for workload identity CAE) only sends claims challenges to clients that declare this capability.

To declare CAE capability, include the following claims parameter in your token request:

```json
Claims: {"access_token":{"xms_cc":{"values":["cp1"]}}}
```

The method for declaring the `cp1` capability depends on the authentication library you use. For detailed code examples in .NET, Python, JavaScript, and other languages, see:

- [Claims challenges, claims requests, and client capabilities](../../identity-platform/claims-challenge#client-capabilities)
- [Use Continuous Access Evaluation enabled APIs in your applications](../../identity-platform/app-resilience-continuous-access-evaluation)

Important

An application won't receive claims challenges and won't receive CAE tokens unless it explicitly declares the `cp1` capability. For more information, see [Client capabilities](../../identity-platform/claims-challenge#client-capabilities).

Note

Declaring `cp1` is a client-side action. Separately, API implementers (resource apps) can request `xms_cc` as an [optional claim](../../identity-platform/optional-claims) in their application manifest to detect whether calling clients support claims challenges. For more information, see [Receiving xms_cc claim in an access token](../../identity-platform/claims-challenge#receiving-xms_cc-claim-in-an-access-token).

### Disable

To opt out of CAE at the application level, don't send the `cp1` capability in the claims parameter of token requests.

## Known limitations

Review the following limitations before you implement CAE for workload identities:

- **Microsoft Graph only.** CAE for workload identities is supported only on access requests to Microsoft Graph. Other resource providers aren't currently supported.
- **Managed identities aren't supported.** CAE doesn't support managed identities at this time.
- **Single-tenant service principals only.** Only single-tenant service principals registered in your tenant are supported. Third-party SaaS and multitenant apps are out of scope.
- **CAE enforces location and risk policies.** CAE for workload identities enforces Conditional Access policies that target location and risk in real time. For the full list of Conditional Access conditions supported for workload identities (including [authentication contexts](concept-conditional-access-cloud-apps#authentication-context)), see [Conditional Access for workload identities](workload-identity).
- **Group-based policy assignment not enforced.** Conditional Access policies assigned to a group that contains a service principal aren't enforced for that service principal. The policy must be assigned directly to the service principal as a workload identity. For more information, see [Conditional Access for workload identities](workload-identity).

## Monitor CAE for workload identities

Administrators can monitor CAE activity for workload identities using the Microsoft Entra sign-in logs.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Reader](../role-based-access-control/permissions-reference#security-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs** &gt; **Service principal sign-ins**. Use filters to simplify the process.
3. Select an entry to view activity details. The **Continuous access evaluation** field shows whether a CAE token was issued for a specific sign-in attempt.

For general CAE monitoring tools, including the **Continuous access evaluation insights** workbook and IP mismatch analysis, see [Monitor and troubleshoot continuous access evaluation](howto-continuous-access-evaluation-troubleshoot).

## Troubleshooting

When a CAE-enabled resource rejects a workload identity token, the application should handle the `401` claims challenge and request a new token from Microsoft Entra ID. Microsoft Entra ID then reevaluates conditions before deciding whether to issue a new token. Use the following steps to investigate.

**Service principal access is unexpectedly blocked:**

1. Check the [sign-in logs](../monitoring-health/concept-sign-ins) under **Service principal sign-ins**. Look for entries where the **Continuous access evaluation** field indicates a CAE token was involved.
2. Verify whether a revocation event occurred: check if the service principal was disabled, deleted, or flagged as high risk by [Microsoft Entra ID Protection](../../id-protection/concept-workload-identity-risk).
3. Review applicable Conditional Access policies to confirm the service principal's source IP is included in an allowed [named location](concept-assignment-network).

**Service principal isn't receiving CAE tokens:**

- Verify the application declares the `cp1` capability in the claims parameter of token requests.
- Confirm the application targets Microsoft Graph as the resource provider. Other resource providers aren't currently supported for CAE.
- Check that the service principal is a single-tenant LOB application registered in your tenant.

**IP address mismatch between Microsoft Entra ID and resource provider:**

- This situation can occur with split-tunnel networks or proxy configurations. When IP addresses don't match, Microsoft Entra ID issues a one-hour CAE token and doesn't enforce client location change during that period. For more information, see [Monitor and troubleshoot continuous access evaluation](howto-continuous-access-evaluation-troubleshoot#ip-address-configuration).

For more information about troubleshooting CAE, see [Monitor and troubleshoot continuous access evaluation](howto-continuous-access-evaluation-troubleshoot).