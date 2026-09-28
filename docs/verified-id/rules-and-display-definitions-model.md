---
layout: Conceptual
title: Rules and Display Definition Reference - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/rules-and-display-definitions-model
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Rules and Display Definition Reference
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-31T00:00:00.0000000Z
locale: en-us
document_id: b9562227-5b89-83cc-95db-30f0aa1a54be
document_version_independent_id: 86ce1a22-d940-22dc-909b-32915bbb09d1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/rules-and-display-definitions-model.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/rules-and-display-definitions-model
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/rules-and-display-definitions-model.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 72166bef-028a-c911-8ea8-3d83fc2e17fb
---

# Rules and Display Definition Reference - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Rules and Display definitions are used to define a credential. You can read more about it in [How to customize your credentials](credential-design).

## rulesModel type

| Property | Type | Description |
| --- | --- | --- |
| `attestations` | idTokenAttestation and/or idTokenHintAttestation and/or verifiablePresentationAttestation and/or selfIssuedAttestation | defines the attestation flows to be used for gathering claims to issue in the verifiable credential. |
| `validityInterval` | number | represents the lifespan of the credential in seconds |
| `vc` | vcType | verifiable credential types for this contract |

The attestation type example in JSON. Notice that `selfIssued` is a single instance while the others are collections. For examples of how to use the attestation type, see [Sample JSON rules definitions](how-to-use-quickstart-multiple#sample-json-rules-definitions) in the How-to guides.

```json
"attestations": {
  "idTokens": [],
  "idTokenHints": [],
  "presentations": [],
  "selfIssued": {}
}
```

### idTokenAttestation type

When you sign in the user from within Authenticator, you can use the returned ID token from the OpenID Connect compatible provider as input.

| Property | Type | Description |
| --- | --- | --- |
| `mapping` | claimMapping (optional) | rules to map input claims into output claims in the verifiable credential |
| `configuration` | string (url) | location of the identity provider's configuration document |
| `clientId` | string | client ID to use when obtaining the ID token |
| `redirectUri` | string | redirect uri to use when obtaining the ID token; MUST BE `vcclient://openid/` |
| `scope` | string | space delimited list of scopes to use when obtaining the ID token |
| `required` | boolean (default false) | indicating whether this attestation is required or not |
| `trustedIssuers` | optional string (array) | a list of DIDs allowed to issue the verifiable credential for this contract. This property is only used for specific scenarios where the `id_token_hint` can come from another issuer |

### idTokenHintAttestation type

This flow uses the ID Token Hint, which is provided as payload through the Request REST API. The mapping is the same as for the ID Token attestation.

| Property | Type | Description |
| --- | --- | --- |
| `mapping` | claimMapping (optional) | rules to map input claims into output claims in the verifiable credential |
| `required` | boolean (default false) | indicating whether this attestation is required or not. [Request Service API](presentation-request-api#http-request) fails the call if required claims aren't set in the createPresentationRequest payload. |
| `trustedIssuers` | optional string (array) | a list of DIDs allowed to issue the verifiable credential for this contract. This property is only used for specific scenarios where the `id_token_hint` can come from another issuer |

### verifiablePresentationAttestation type

When you want the user to present another verifiable credential as input for a new issued verifiable credential. The wallet allows the user to select the verifiable credential during issuance.

| Property | Type | Description |
| --- | --- | --- |
| `mapping` | claimMapping (optional) | rules to map input claims into output claims in the verifiable credential |
| `credentialType` | string (optional) | required credential type of the input |
| `required` | boolean (default false) | indicating whether this attestation is required or not |
| `trustedIssuers` | string (array) | a list of DIDs allowed to issue the verifiable credential for this contract. The service defaults to your issuer under the covers so no need to provide this value yourself. |

### selfIssuedAttestation type

When you want the user to enter information themselves. This type is also called self-attested input.

| Property | Type | Description |
| --- | --- | --- |
| `mapping` | claimMapping (optional) | rules to map input claims into output claims in the verifiable credential |
| `required` | boolean (default false) | indicating whether this attestation is required or not |

### claimMapping type

| Property | Type | Description |
| --- | --- | --- |
| `inputClaim` | string | the name of the claim to use from the input |
| `outputClaim` | string | the name of the claim in the verifiable credential |
| `indexed` | boolean (default false) | indicating whether the value of this claim is used for searching; only one clientMapping object is indexable for a given contract |
| `required` | boolean (default false) | indicating whether this mapping is required or not |
| `type` | string (optional) | type of claim |

### vcType type

| Property | Type | Description |
| --- | --- | --- |
| `type` | string (array) | a list of verifiable credential types this contract can issue |

## Example rules definition

```json
{
  "attestations": {
    "idTokenHints": [
      {
        "mapping": [
          {
            "outputClaim": "givenName",
            "required": false,
            "inputClaim": "given_name",
            "indexed": false
          },
          {
            "outputClaim": "familyName",
            "required": false,
            "inputClaim": "family_name",
            "indexed": false
          }
        ],
        "required": false
      }
    ]
  },
  "validityInterval": 2592000,
  "vc": {
    "type": [
      "VerifiedCredentialExpert"
    ]
  }
}
```

## displayModel type

| Property | Type | Description |
| --- | --- | --- |
| `locale` | string | the locale of this display |
| `card` | displayCredential | the display properties of the verifiable credential |
| `consent` | displayConsent | supplemental data when the verifiable credential is issued |
| `claims` | displayClaims array | labels for the claims included in the verifiable credential |

### displayCredential type

| Property | Type | Description |
| --- | --- | --- |
| `title` | string | title of the credential |
| `issuedBy` | string | the name of the issuer of the credential |
| `backgroundColor` | number (hex) | background color of the credential in hex format, for example, #FFAABB |
| `textColor` | number (hex) | text color of the credential in hex format, for example, #FFAABB |
| `description` | string | supplemental text displayed alongside each credential |
| `logo` | displayCredentialLogo | the logo to use for the credential |

### displayCredentialLogo type

| Property | Type | Description |
| --- | --- | --- |
| `uri` | string (url) | url of the logo. |
| `description` | string | the description of the logo |

Note

Microsoft recommends that you use widely supported image formats, such as .PNG, .JPG, or .BMP, to reduce file format errors.

### displayConsent type

| Property | Type | Description |
| --- | --- | --- |
| `title` | string | title of the consent |
| `instructions` | string | supplemental text to use when displaying consent |

### displayClaims type

| Property | Type | Description |
| --- | --- | --- |
| `label` | string | the label of the claim in display |
| `claim` | string | the name of the claim to which the label applies. For the JWT-VC format, the value needs to have the `vc.credentialSubject.` prefix. |
| `type` | string | the type of the claim |
| `description` | string (optional) | the description of the claim |

## Example display definition

```json
{
  "locale": "en-US",
  "card": {
    "backgroundColor": "#FFA500",
    "description": "This is your Verifiable Credential",
    "issuedBy": "Contoso",
    "textColor": "#FFFF00",
    "title": "Verifiable Credential Expert",
    "logo": {
      "description": "Default VC logo",
      "uri": "https://didcustomerplayground.z13.web.core.windows.net/VerifiedCredentialExpert_icon.png"
    }
  },
  "consent": {
    "instructions": "Please click accept to add this credential",
    "title": "Do you want to accept the verified credential expert identity?"
  },
  "claims": [
    {
      "claim": "vc.credentialSubject.givenName",
      "label": "Name",
      "type": "String"
    },
    {
      "claim": "vc.credentialSubject.familyName",
      "label": "Surname",
      "type": "String"
    }
  ]
}
```