---
layout: Conceptual
title: Create verifiable credentials with multiple attestations - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart-multiple
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to use a quickstart to create custom credentials with multiple attestations.
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-17T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f19667a9-9732-6b69-b3ce-64b5ddde7847
document_version_independent_id: 1d19282b-229d-8944-60fd-55303131a5f8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-use-quickstart-multiple.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-use-quickstart-multiple
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-use-quickstart-multiple.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 4d44f057-9e77-4a87-eeee-8c97a2c3b1b9
---

# Create verifiable credentials with multiple attestations - Microsoft Entra Verified ID | Microsoft Learn

## Overview

A [rules definition](rules-and-display-definitions-model#rulesmodel-type) that uses multiple attestations types produces an issuance flow where claims come from more than one source. For instance, you might be required to present an existing credential and also manually enter values for claims in Microsoft Authenticator.

In this how-to guide, we extend the [ID token hint attestation](how-to-use-quickstart-idtoken) example by adding a self attested claim that the user has to enter in the Authenticator during issuance. The issuance request to Verified ID contains an ID token hint with the claim values for `given_name` and `family_name`, and a self-issued attestation type for claim `displayName` that the user enters themselves.

## Create a custom credential with multiple attestation types

In the Azure portal, when you select **Add credential**, you get the option to launch two quickstarts. Select **custom credential**, and then select **Next**.

![Screenshot of the Issue credentials quickstart for creating a custom credential.](media/how-to-use-quickstart/quickstart-startscreen.png)

On the **Create a new credential** page, enter the JSON code for the display and the rules definitions. In the **Credential name** box, give the credential a type name. To create the credential, select **Create**.

![Screenshot of the Create a new credential page, displaying JSON samples for the display and rules files.](media/how-to-use-quickstart/quickstart-create-new.png)

## Sample JSON display definitions

The JSON display definition has one extra claim named **displayName** compared to the [ID token hint display definition](how-to-use-quickstart-idtoken#sample-json-display-definitions).

```json
{
    "locale": "en-US",
    "card": {
      "title": "Verified Credential Expert",
      "issuedBy": "Microsoft",
      "backgroundColor": "#507090",
      "textColor": "#ffffff",
      "logo": {
        "uri": "https://didcustomerplayground.z13.web.core.windows.net/VerifiedCredentialExpert_icon.png",
        "description": "Verified Credential Expert Logo"
      },
      "description": "Use your verified credential to prove to anyone that you know all about verifiable credentials."
    },
    "consent": {
      "title": "Do you want to get your Verified Credential?",
      "instructions": "Sign in with your account to get your card."
    },
    "claims": [
      {
        "claim": "vc.credentialSubject.displayName",
        "label": "Name",
        "type": "String"
      },
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

The JSON rules definition contains two different attestations that instruct the Authenticator to get claim values from two different sources. The issuance request to the Request Service API provides the values for the claims **given\_name** and **family\_name** to satisfy the **idTokenHints** attestation. The user is asked to enter the claim value for **displayName** in the Authenticator during issuance.

```json
{
  "attestations": {
    "idTokenHints": [
        {
        "mapping": [
            {
            "outputClaim": "firstName",
            "required": true,
            "inputClaim": "$.given_name",
            "indexed": false
            },
            {
            "outputClaim": "lastName",
            "required": true,
            "inputClaim": "$.family_name",
            "indexed": false
            }
        ],
        "required": false
        }
    ],
    "selfIssued": {
      "mapping": [
        {
          "outputClaim": "displayName",
          "required": true,
          "inputClaim": "displayName",
          "indexed": false
        }
      ],
      "required": false
    }
  },
  "validityInterval": 2592000,
  "vc": {
    "type": [
      "VerifiedCredentialExpert"
    ]
  }
}
```

## Claims input during issuance

During issuance, Authenticator prompts the user to enter values for the specified claims. User input isn't validated.

![Screenshot of selfIssued claims input.](media/how-to-use-quickstart-multiple/multiple-attestations-issuance.png)

## Claims in issued credential

The issued credentials have three claims in total, where the `First` and `Last name` come from the **id token hint** attestation and the `Name` comes from the **self-issued** attestation.

![Screenshot of claims in issued credential.](media/how-to-use-quickstart-multiple/multiple-attestations-vc.png)

## Configure the samples to issue and verify your custom credential

To configure your sample code to issue and verify your custom credential, you need:

- Your tenant's issuer decentralized identifier (DID).
- The credential type.
- The manifest URL to your credential.

The easiest way to find this information for a custom credential is to go to your credential in the Azure portal. Select **Issue credential**. Then you have access to a text box with a JSON payload for the Request Service API.Replace the placeholder values with your environment's information. The issuer’s DID is the authority value.

![Screenshot of the quickstart custom credential issue.](media/how-to-use-quickstart/quickstart-config-sample-2.png)