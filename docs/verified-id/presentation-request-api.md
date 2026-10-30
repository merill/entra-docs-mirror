---
layout: Conceptual
title: Specify the Request Service REST API verify request - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/presentation-request-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to start a presentation request in Verifiable Credentials.
documentationCenter: ''
ms.topic: reference
ms.date: 2025-01-30T00:00:00.0000000Z
locale: en-us
document_id: c4fcc0e1-7256-01f1-3b8a-a8cf536ffd8e
document_version_independent_id: 7e80041b-7f0f-f86a-a121-a1dbac207830
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/presentation-request-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/presentation-request-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/presentation-request-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: 483778cf-5531-bed9-0db0-dacdac3f2a79
---

# Specify the Request Service REST API verify request - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Microsoft Entra Verified ID includes the Request Service REST API. This API allows you to issue and verify a credential. This article specifies the Request Service REST API for a presentation request. The presentation request asks the user to present a verifiable credential, and then verify the credential. Another article describes [how to call the Request Service REST API](get-started-request-api).

## HTTP request

The Request Service REST API presentation request supports the following HTTP method:

| Method | Notes |
| --- | --- |
| POST | With JSON payload as specified in this article. |

The Request Service REST API presentation request requires the following HTTP headers:

| Name | Value |
| --- | --- |
| `Authorization` | Attach the access token as a bearer token to the authorization header in an HTTP request. For example, `Authorization: Bearer <token>`. |
| `Content-Type` | `application/json` |

Construct an HTTP POST request to the Request Service REST API. The `tenantId` isn't needed in the URL anymore since it's present as a claim in the `access_token`.

```http
https://verifiedid.did.msidentity.com/v1.0/verifiableCredentials/createPresentationRequest
```

The following HTTP request demonstrates a presentation request to the Request Service REST API:

```http
POST https://verifiedid.did.msidentity.com/v1.0/verifiableCredentials/createPresentationRequest
Content-Type: application/json
Authorization: Bearer  <token>

{
    "callback": {
      "url": "https://contoso.com/api/verifier/presentationCallback",
      "state": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
      "headers": {
        "api-key": "an-api-key-can-go-here"
      }
    },
    ...
}
```

The following permission is required to call the Request Service REST API. For more information, see [Grant permissions to get access tokens](verifiable-credentials-configure-tenant#grant-permissions-to-get-access-tokens).

| Permission type | Permission |
| --- | --- |
| Application | 3db474b9-6a0c-4840-96ac-1fceb342124f/.default |

## Presentation request payload

The presentation request payload contains information about your verifiable credentials presentation request. The following example demonstrates a presentation request from a specific issuer. The result of this request returns a QR code with a link to start the presentation process.

```json
{
  "authority": "did:web:verifiedid.contoso.com",
  "includeReceipt": true,
  "registration": {
    "clientName": "Veritable Credential Expert Verifier"
  },
  "callback": {
    "url": "https://contoso.com/api/verifier/presentationCallback",
    "state": "92d076dd-450a-4247-aa5b-d2e75a1a5d58",
    "headers": {
      "api-key": "OPTIONAL API-KEY for CALLBACK EVENTS"
    }
  },
  "requestedCredentials": [
    {
      "type": "VerifiedCredentialExpert",
      "purpose": "So we can see that you are a veritable credentials expert",
      "acceptedIssuers": [
        "did:web:verifiedid.contoso.com"
      ],
      "configuration": {
        "validation": {
          "allowRevoked": false,
          "validateLinkedDomain": false
        }
      }
    }
  ]
}
```

The payload contains the following properties.

| Parameter | Type | Description |
| --- | --- | --- |
| `includeQRCode` | Boolean | Optional. Determines whether a QR code is included in the response of this request. Present the QR code and ask the user to scan it. Scanning the QR code launches the authenticator app with this presentation request. Possible values are `true` or `false` (default). When you set the value to `false`, use the return `url` property to render a deep link. |
| `includeReceipt` | Boolean | Optional. Determines whether a receipt should be included in the response of this request. Possible values are `true` or `false` (default). The receipt contains the original payload sent from the authenticator to the Verifiable Credentials service. The receipt is useful for troubleshooting or if you have the need to get the full details of the payload. There's otherwise no need to set this value to `true` by default. In the `OpenId Connect SIOP` request, the receipt contains the ID token from the original request. |
| `authority` | string | The decentralized identifier (DID) of your verifier Microsoft Entra tenant. For more information, see [Gather tenant details to set up your sample application](verifiable-credentials-configure-verifier#gather-tenant-details-to-set-up-your-sample-application). |
| `registration` | RequestRegistration | Provides information about the verifier. |
| `callback` | Callback | Mandatory. Allows the developer to update the UI during the verifiable credential presentation process. When the user completes the process, continue the process after the results are returned to the application. |
| `requestedCredentials` | collection | A collection of RequestCredential objects. |

### RequestRegistration type

The `RequestRegistration` type provides registration information for the issuer. The `RequestRegistration` type contains the following properties:

| Property | Type | Description |
| --- | --- | --- |
| `clientName` | string | A display name of the verifier of the verifiable credential. This name is presented to the user in the authenticator app. |
| `purpose` | string | Optional. A string that is displayed to inform the user why the verifiable credentials are being requested. |
| `logoUrl` | URL | Optional. A URL for a logotype of the verifier. This value isn't used by the Authenticator app. |
| `termsOfServiceUrl` | URL | Optional. A URL to the terms of service for the verifier. This value isn't used by the Authenticator app. |

The following screenshot shows the `clientName` property and the display name of the `authority` (the verifier) in the presentation request.

![Screenshot that shows how to approve the presentation request.](media/presentation-request-api/approve-presentation-request.jpg)

### Callback type

The Request Service REST API generates several events to the callback endpoint. Those events allow you to update the UI and continue the process after the results are returned to the application. The `Callback` type contains the following properties:

| Property | Type | Description |
| --- | --- | --- |
| `url` | string | URI to the callback endpoint of your application. The URI must point to a reachable endpoint on the internet, otherwise the service throws a callback URL unreadable error. Accepted inputs include IPv4, IPv6, or DNS resolvable hostnames. To harden your network, see [FAQ](verifiable-credentials-faq#network-hardening-for-callback-events). |
| `state` | string | Correlates the callback event with the state passed in the original payload. |
| `headers` | string | Optional. You can include a collection of HTTP headers required by the receiving end of the POST message. The current supported header values are the `api-key` or the `Authorization` headers. Any other header throws an invalid callback header error. |

### RequestCredential type

The `RequestCredential` provides information about the requested credentials the user needs to provide. `RequestCredential` contains the following properties:

| Property | Type | Description |
| --- | --- | --- |
| `type` | string | The verifiable credential type. The `type` must match the type as defined in the `issuer` verifiable credential manifest (for example, `VerifiedCredentialExpert`). To get the issuer manifest, see [Gather credentials and environment details to set up your sample application](verifiable-credentials-configure-issuer). Copy the **Issue credential URL**, open it in a web browser, and check the **id** property. |
| `purpose` | string | Optional. Provide information about the purpose of requesting this verifiable credential. This data isn't used by the **Authenticator** app. |
| `acceptedIssuers` | string collection | Optional. A collection of issuers' DIDs that could issue the type of verifiable credential that subjects can present. To get your issuer DID, see [Gather credentials and environment details to set up your sample application](verifiable-credentials-configure-issuer), and copy the value of the **Decentralized identifier (DID)**. If the `acceptedIssuers` collection is empty or not present, then the presentation request accepts a credential type issued by any issuer. |
| `configuration.validation` | Configuration.Validation | Optional settings for presentation validation. |
| `constraints` | Constraints | Optional. Collection of claims constraints. |

### Configuration.Validation type

The `Configuration.Validation` provides information about how the presented credentials should be validated. It contains the following properties:

| Property | Type | Description |
| --- | --- | --- |
| `allowRevoked` | Boolean | Optional. Determines if a revoked credential should be accepted. Default is `false` (it shouldn't be accepted). |
| `validateLinkedDomain` | Boolean | Optional. Determines if the linked domain should be validated. Default is `false`. Setting this flag to `false` means you as a Relying Party application accept credentials from an unverified linked domain. Setting this flag to `true` means the linked domain is validated and only verified domains are accepted. |
| `faceCheck` | faceCheck | Optional. Allows requesting a liveness check during presentation. |

### Constraints type

The `constraints` type contains a collection of claims constraints that must be met when a wallet selects the candidate credentials. This enables requesting a credential with specific claim value. Constraints specified use the AND logic, that is, if you specify three constraints, all of them have to be met. For each constraint in the collection, you must select one operand of values, contains, or startsWith. Values can't be regular expressions. All comparisons are case-insensitive.

| Property | Type | Description |
| --- | --- | --- |
| `claimName` | string | Mandatory. Name of the claim for the constraint. This value is the claim name in the verifiable credential. See [outputClaim](rules-and-display-definitions-model#claimmapping-type) in claimMapping type. |
| `values` | string collection | Set of values that should match the claim value. If you specify multiple values, like ["red", "green", "blue"] it's a match if the claim value in the credential has any of the values in the collection. |
| `contains` | string | The constraint evaluates to true if the claim value contains the specified value. |
| `startsWith` | string | The constraint evaluates to true if the claim value starts with the specified value. |

### `faceCheck` type

The faceCheck type contains information for performing liveness check during presentation of a credential. The credential requested must contain a photo of the holder in the claim named by the sourcePhotoClaimName. The presentation succeeds if the liveness check reaches a confidence level equal or greater to what is specified in the property matchConfidenceThreshold. If the threshold isn't met, the entire presentation fails.

| Property | Type | Description |
| --- | --- | --- |
| `sourcePhotoClaimName` | string | Mandatory. The name of the claim in the credential that contains the photo. See [outputClaim](rules-and-display-definitions-model#claimmapping-type) in claimMapping type. |
| `matchConfidenceThreshold` | integer | Optional. The confidence threshold for a successful check between the photo and the liveness data. Must be an integer between 50 and 100. The default is 70. |

## Successful response

If successful, this method returns a response code (*HTTP 201 Created*), and a collection of event objects in the response body. The following JSON demonstrates a successful response:

```json
{
    "requestId": "e4ef27ca-eb8c-4b63-823b-3b95140eac11",
    "url": "openid-vc://?request_uri=https://verifiedid.did.msidentity.com/v1.0/00001111-aaaa-2222-bbbb-3333cccc4444/verifiableCredentials/presentationRequests/e4ef27ca-eb8c-4b63-823b-3b95140eac11",
    "expiry": 1633017751,
    "qrCode": "data:image/png;base64,iVBORw0KGgoA<SNIP>"
}
```

The response contains the following properties:

| Property | Type | Description |
| --- | --- | --- |
| `requestId` | string | An autogenerated request ID. The callback uses the same request, allowing you to keep track of the presentation request and its callbacks. |
| `url` | string | A URL that launches the authenticator app and starts the presentation process. You can present this URL to the user if they can't scan the QR code. |
| `expiry` | integer | Indicates when the response expires. |
| `qrCode` | string | A QR code that the user can scan to start the presentation flow. |

When your app receives the response, the app needs to present the QR code to the user. The user scans the QR code, which opens the authenticator app and starts the presentation process.

## Error response

If there's an error with the request, an [error response](error-codes) is returned. The app needs to handle the error appropriately.

## Callback events

The callback endpoint is called when a user scans the QR code, uses the deep link to the authenticator app, or finishes the presentation process.

| Property | Type | Description |
| --- | --- | --- |
| `requestId` | string | Mapped to the original request when the payload was posted to the Verifiable Credentials service. |
| `requestStatus` | string | The status returned when the authenticator app retrieved the request. Possible values: <br>- `request_retrieved`: The user scanned the QR code or selected the link that starts the presentation flow.<br>- `presentation_verified`: The verifiable credential validation completed successfully.<br>- `presentation_error`: There was an error in the presentation. |
| `state` | string | Returns the state value that you passed in the original payload. |
| `subject` | string | The verifiable credential user DID. |
| `verifiedCredentialsData` | array | Returns an array of verifiable credentials requested. For each verifiable credential, it provides: <br>- The verifiable credential types.<br>- The issuer's DID<br>- The claims retrieved.<br>- The verifiable credential issuer's domain.<br>- The verifiable credential issuer's domain validation status. |
| `receipt` | string | Optional. The receipt contains the original payload sent from the wallet to the Verifiable Credentials service. The receipt should be used for troubleshooting/debugging only. The format in the receipt isn't fixed and can change based on the wallet and version used. |

The following example demonstrates a callback payload when the authenticator app starts the presentation request:

```json
{
    "requestId": "e4ef27ca-eb8c-4b63-823b-3b95140eac11",
    "requestStatus":"request_retrieved",
    "state": "92d076dd-450a-4247-aa5b-d2e75a1a5d58"
}
```

The following example shows a callback payload after the verifiable credential presentation successfully completes:

```json
{
  "requestId": "e4ef27ca-eb8c-4b63-823b-3b95140eac11",
  "requestStatus": "presentation_verified",
  "state": "92d076dd-450a-4247-aa5b-d2e75a1a5d58",
  "subject": "did:web:verifiedid.contoso.com",
  "verifiedCredentialsData": [
    {
      "issuer": "did:web:issuer...",
      "type": [
        "VerifiableCredential",
        "VerifiedCredentialExpert"
      ],
      "claims": {
        "firstName": "Megan",
        "lastName": "Bowen"
      },
      "credentialState": {
        "revocationStatus": "VALID"
      },
      "domainValidation": {
        "url": "https://contoso.com/"
      },
      "issuanceDate": "yyyy-MM-ddTHH:mm:ssZ",
      "expirationDate": "yyyy-MM-ddTHH:mm:ssZ"
    }
  ],
  "receipt": {
    "id_token": "eyJraWQiOiJkaWQ6aW<SNIP>",
    "vp_token": "...",
    "state": "..."
  }
}
```