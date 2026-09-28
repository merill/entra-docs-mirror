---
layout: Conceptual
title: Create verifiable credentials for self-asserted claims - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart-selfissued
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to use a quickstart to create custom credentials for self-issued claims.
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-17T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5966a2ef-d197-43b5-4725-20d64976a5fe
document_version_independent_id: 1d19ee32-6766-8d4f-b2c5-9387b23146e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-use-quickstart-selfissued.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-use-quickstart-selfissued
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-use-quickstart-selfissued.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 5231ad64-6e08-4034-f19a-d721b0fa694d
---

# Create verifiable credentials for self-asserted claims - Microsoft Entra Verified ID | Microsoft Learn

## Overview

A [rules definition](rules-and-display-definitions-model#rulesmodel-type) that uses the [selfIssued attestation](rules-and-display-definitions-model#selfissuedattestation-type) type produces an issuance flow where you're required to manually enter values for the claims in Microsoft Authenticator.

## Create a custom credential with the selfIssued attestation type

In the **Azure portal**, when you select **Add credential**, you get the option to launch two quickstarts. Select **custom credential**, and then select **Next**.

![Screenshot of the Issue credentials quickstart for creating a custom credential.](media/how-to-use-quickstart/quickstart-startscreen.png)

On the **Create a new credential** page, enter the JSON code for the display and the rules definitions. In the **Credential name** box, give the credential a type name. To create the credential, select **Create**.

![Screenshot of the Create a new credential page displaying JSON samples for the display and rules files.](media/how-to-use-quickstart/quickstart-create-new.png)

## Sample JSON display definitions

The JSON display definition is nearly the same, regardless of attestation type. You only have to adjust the labels according to the claims that your verifiable credential has. The expected JSON for the display definitions is the inner content of the displays collection. The JSON is a collection, so if you want to support multiple locales, add multiple entries with a comma as a separator.

```json
{
    "locale": "en-US",
    "card": {
      "title": "Verified Credential Expert",
      "issuedBy": "Microsoft",
      "backgroundColor": "#000000",
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
        "claim": "vc.credentialSubject.companyName",
        "label": "Company",
        "type": "String"
      }
    ]
}
```

## Sample JSON rules definitions

The JSON attestation definition should contain the **selfIssued** name and the claims mapping section. Because the claims are self issued, the value is the same for **outputClaim** and **inputClaim**. The expected JSON for the rules definitions is the inner content of the rules attribute, which starts with the attestation attribute.

```json
{
  "attestations": {
    "selfIssued": {
      "mapping": [
        {
          "outputClaim": "displayName",
          "required": true,
          "inputClaim": "displayName",
          "indexed": true
        },
        {
          "outputClaim": "companyName",
          "required": true,
          "inputClaim": "companyName",
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

During issuance, Authenticator prompts you to enter values for the specified claims. User input isn't validated.

![Screenshot of selfIssued claims input.](media/how-to-use-quickstart-selfissued/selfissued-claims-input.png)

## Configure the samples to issue and verify your custom credential

To configure your sample code to issue and verify your custom credential, you need:

- Your tenant's issuer decentralized identifier (DID).
- The credential type.
- The manifest URL to your credential.

The easiest way to find this information for a custom credential is to go to your credential in the Azure portal. Select **Issue credential**. Then you have access to a text box with a JSON payload for the Request Service API.Replace the placeholder values with your environment's information. The issuer’s DID is the authority value.

![Screenshot of the quickstart custom credential issue.](media/how-to-use-quickstart/quickstart-config-sample-2.png)