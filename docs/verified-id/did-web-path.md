---
layout: Conceptual
title: How to add did:web:path support - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/did-web-path
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to enable support for did:web:path
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 7b0f9080-7e7f-8a5d-9297-9bb4e1176705
document_version_independent_id: 7b0f9080-7e7f-8a5d-9297-9bb4e1176705
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/did-web-path.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/did-web-path
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/did-web-path.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 92514014-f9cf-2e6f-8940-e3baacb559c2
---

# How to add did:web:path support - Microsoft Entra Verified ID | Microsoft Learn

## Overview

This article covers the steps to enable support for did:web:path to your authority.

## Prerequisites

- Verified ID authority is [manually onboarded](verifiable-credentials-configure-tenant) using did:web. [Quick setup](verifiable-credentials-configure-tenant-quick) uses a domain name managed by Microsoft which can't be extended.

## What is did:web:path?

Did:web:path is described in the [did:web Method Specification](https://w3c-ccg.github.io/did-method-web/#optional-path-considerations). If you have an environment where you're required to use a high number of [authorities](admin-api#authorities), acquiring domain names for them becomes an administrative problem. Using one single domain and having the different authorities appear as paths under the domain may be a more favorable approach.

## Enable domain for did:web:path support

By default, a tenant and an authority aren't enabled to support did:web:path. You request enablement of did:web:path for your authority via creating a new support request in the [Microsoft Entra admin center](https://entra.microsoft.com/#blade/Microsoft_Azure_Support/NewSupportRequestV3Blade/callerName/ActiveDirectory/issueType/technical).

Support ticket details:

- Issue type: `Technical`
- Service type: `Microsoft Entra Verified ID`
- Problem type: `Configuration organization and domains`
- Summary: `Enable did:web:path request`
- Description: Make sure to include
    - Your Microsoft Entra `tenant ID`
    - Your `did` (example: did:web:verifiedid.contoso.com)
    - Estimated number of sub paths
    - Business justification

## How can I test that my authority is enabled?

You receive confirmation in your support request. You can also verify if a did:web domain is enabled for did:web:path by testing it in a normal browser. By adding a path that doesn't exist (`:do-not-exist` in the following example) you get an error message with code `discovery_service.web_method_path_not_supported` if your authority isn't enabled, but the code `discovery_service.not_found` if enabled.

```http
https://discover.did.msidentity.com/v1.0/identifiers/did:web:my-domain.com:do-not-exist
```

## How do I configure an authority using did:web:path?

Once your tenant and authority is enabled for did:web:path, you can create a new authority in the same tenant that uses did:web:path. Currently this configuration option requires using the [Admin API](admin-api) as there's no support in the portal for it.

1. Get details of your existing authority.

    - Go to `Verified ID | Overview` and copy domain (example: `https://verifiedid.contoso.com/`)
    - Go to `Verified ID | Organization settings` and take a note of which Key vault is being configured.
    - Go to the Key vault resource and copy the `resource group`, the `subscription ID`, and the `Vault URI`
2. Call the [creating authority](admin-api#create-authority) with the following JSON body (modify as required). The `/my-path` in the path is where you specify the path name to be used.

    ```JSON
    POST /v1.0/verifiableCredentials/authorities
    
    {
      "name":"ExampleNameForPath",
      "linkedDomainUrl":"https://my-domain.com/my-path",
      "didMethod": "web",
      "keyVaultMetadata":
      {
        "subscriptionId":"aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e",
        "resourceGroup":"verifiablecredentials",
        "resourceName":"vccontosokv",
        "resourceUrl": "https://vccontosokv.vault.azure.net/"
      }
    }
    ```
3. Generate the did document for the new authority by calling [generateDidDocument](admin-api#generate-did-document) where `newAuthorityIdForPath` is the `id` attribute in the response:

    ```JSON
    POST /v1.0/verifiableCredentials/authorities/:newAuthorityIdForPath/generateDidDocument
    ```
4. Save the DID document response to a file named `did.json` and upload it to location on your webserver that matches the `linkedDomainUrl` in the API call for creating the authority. If your path is `https://my-domain.com/my-path`, the new did.json file must reside in that location.
5. Retrieve the linked domain did configuration via calling [generateWellknownDidConfiguration](admin-api#well-known-did-configuration) API with the following JSON body (modify as required). The domainUrl is the domain name ***without*** the path

    ```JSON
    POST /v1.0/verifiableCredentials/authorities/:newAuthorityIdForPath/generateWellknownDidConfiguration
    
    {
        "domainUrl":"https://my-domain.com/"
    }
    ```
6. From the response, copy the JSON Web Token (JWT) inside the `linked_dids` collection.
7. On your webserver, open the file `https://my-domain.com/.well-known/did.configuration.json` in an editor and add the JWT as a new entry inside the linked\_dids collection. It should look something like this after adding it.

    ```JSON
    {
      "@context": "https://identity.foundation/.well-known/contexts/did-configuration-v0.0.jsonld",
      "linked_dids": [
        "eyJh...old...U7cw",
        "eyJh...new...V8dx",
      ]
    }
    ```
8. Save the file.

## Create contracts using the new did:web:path authority

Contracts need to be created using the [Admin API](admin-api#contracts). There's currently no user interface support for secondary authorities.

## Issue credentials based on contracts in the new did:web:path authority

To have apps issue credentials based on contracts in the new did:web:path authority, you only need to change the `authority` field in the request payload to [createIssuanceRequest](issuance-request-api#issuance-request-payload) API.

```JSON
{
  "authority": "did:web:my-domain.com:my-path",
  "includeQRCode": false,
  ... the rest is the same...
}
```