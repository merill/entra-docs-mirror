---
layout: Conceptual
title: Issue verifiable credentials by presenting claims from an existing verifiable credential - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart-presentation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to use a quickstart to create custom credentials from other Verifiable Credential attestation.
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: da32b7ba-4780-2aa9-8d82-0deb624404cd
document_version_independent_id: cf45d498-dfed-c005-ddf8-06edd8d9e4d4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-use-quickstart-presentation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-use-quickstart-presentation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-use-quickstart-presentation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 569c31d8-035e-2576-3f81-4c7841009e90
---

# Issue verifiable credentials by presenting claims from an existing verifiable credential - Microsoft Entra Verified ID | Microsoft Learn

## Overview

A [rules definition](rules-and-display-definitions-model#rulesmodel-type) that uses the [presentations attestation](rules-and-display-definitions-model#verifiablepresentationattestation-type) type produces an issuance flow where you want the user to present another verifiable credential in the wallet during issuance and where claim values for issuance of the new credential are taken from the presented credential. An example of this type of flow can be when you present your VerifiedEmployee credential to get a visitors pass credential.

## Create a custom credential with the presentations attestation type

In the **Azure portal**, when you select **Add credential**, you get the option to launch two quickstarts. Select **custom credential**, and then select **Next**.

![Screenshot of the 'Issue credentials' quickstart for creating a custom credential.](media/how-to-use-quickstart/quickstart-startscreen.png)

On the **Create a new credential** page, enter the JSON code for the display and the rules definitions. In the **Credential name** box, give the credential a name. This name is just an internal name for the credential in the portal. The type name of the credential is defined in the `vc.type` property name in the rules definition. To create the credential, select **Create**.

![Screenshot of the 'Create a new credential' page, displaying JSON samples for the display and rules files.](media/how-to-use-quickstart/quickstart-create-new.png)

## Sample JSON display definitions

The JSON display definition is nearly the same, regardless of attestation type. You only have to adjust the labels according to the claims that your verifiable credential has. The expected JSON for the display definitions is the inner content of the displays collection. The JSON is a collection, so if you want to support multiple locales, add multiple entries with a comma as a separator.

```json
{
  "locale": "en-US",
  "card": {
    "backgroundColor": "#000000",
    "description": "Use your verified credential to prove to anyone that you know all about verifiable credentials.",
    "issuedBy": "Microsoft",
    "textColor": "#ffffff",
    "title": "Verified Credential Expert",
    "logo": {
      "description": "Verified Credential Expert Logo",
      "uri": "https://didcustomerplayground.z13.web.core.windows.net/VerifiedCredentialExpert_icon.png"
    }
  },
  "consent": {
    "instructions": "Present your True Identity card to issue your VC",
    "title": "Do you want to get your Verified Credential?"
  },
  "claims": [
    {
      "claim": "vc.credentialSubject.firstName",
      "label": "First name",
      "type": "String"
    },
    {
      "claim": "vc.credentialSubject.lastName",
      "label": "Last name",
      "type": "String"
    }
  ]
}
```

## Sample JSON rules definitions

The JSON attestation definition should contain the **presentations** name. The **inputClaim** in the mapping section defines what claims should be captured in the credential the user presents. They need to have the prefix `$.vc.credentialSubject`. The **outputClaim** defines the name of the claims in the credential being issued.

The following rules definition prompts the user to present the **True Identity** credential during issuance. This credential comes from the [public demo application](https://woodgroveemployee.azurewebsites.net/).

```json
{
  "attestations": {
    "presentations": [
      {
        "mapping": [
          {
            "outputClaim": "firstName",
            "required": true,
            "inputClaim": "$.vc.credentialSubject.firstName",
            "indexed": false
          },
          {
            "outputClaim": "lastName",
            "required": true,
            "inputClaim": "$.vc.credentialSubject.lastName",
            "indexed": false
          }
        ],
        "required": false,
        "credentialType": "TrueIdentity",
        "contracts": [
          "https://verifiedid.did.msidentity.com/v1.0/tenants/aaaabbbb-0000-cccc-1111-dddd2222eeee/verifiableCredentials/contracts/M2MzMmVkNDAtOGExMC00NjViLThiYTQtMGIxZTg2ODgyNjY4dHJ1ZSBpZGVudGl0eSBwcm9k/manifest"
        ]
      }
    ]
  },
  "validityInterval": 2592001,
  "vc": {
    "type": [
      "VerifiedCredentialExpert"
    ]
  }
}
```

| **Property** | **Type** | **Description** |
| --- | --- | --- |
| `credentialType` | string | credential type being requested during issuance. `TrueIdentity` in the previous example. |
| `contracts` | string (array) | list of manifest URLs of credentials requested. In the earlier example, the manifest URL is the manifest for `True Identity` |
| `trustedIssuers` | string (array) | a list of allowed issuer decentralized identifiers (DIDs) for the credential being requested. In the earlier example, the DID is the DID of the `True Identity` issuer. |

## Authenticator experience during issuance

During issuance, Authenticator prompts the user to select a matching credential. If the user has multiple matching credentials in the wallet, the user must select which one to present.

![Screenshot of presentations claims input.](media/how-to-use-quickstart-presentation/issue-presentation.png)

## Configure the samples to issue your custom credential

To configure your sample code to issue and verify your custom credential, you need:

- Your tenant's issuer decentralized identifier (DID).
- The credential type.
- The manifest URL to your credential.

The easiest way to find this information for a custom credential is to go to your credential in the Azure portal. Select **Issue credential**. Then you have access to a text box with a JSON payload for the Request Service API.Replace the placeholder values with your environment's information. The issuer’s DID is the authority value.

![Screenshot of the quickstart custom credential issue.](media/how-to-use-quickstart/quickstart-config-sample-2.png)