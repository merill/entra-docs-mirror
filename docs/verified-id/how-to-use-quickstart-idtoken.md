---
layout: Conceptual
title: Create verifiable credentials for ID tokens - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart-idtoken
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to use a quickstart to create custom credentials for ID tokens
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-01-17T00:00:00.0000000Z
locale: en-us
document_id: 2f3b84db-c99a-8e05-cfd9-ca348f91f744
document_version_independent_id: a4a34495-a17b-6cde-cdb4-bd320e3f29a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-use-quickstart-idtoken.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-use-quickstart-idtoken
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-use-quickstart-idtoken.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: 9c0ac92d-43eb-e3bf-94e8-4e1571f7e107
---

# Create verifiable credentials for ID tokens - Microsoft Entra Verified ID | Microsoft Learn

## Overview

A [rules definition](rules-and-display-definitions-model#rulesmodel-type) that uses the [idTokens attestation](rules-and-display-definitions-model#idtokenattestation-type) produces an issuance flow where you're required to do an interactive sign-in to an OpenID Connect (OIDC) identity provider in Microsoft Authenticator. Claims in the ID token that the identity provider returns can be used to populate the issued verifiable credential. The claims mapping section in the rules definition specifies which claims are used.

## Create a custom credential with the idTokens attestation type

In the **Azure portal**, when you select **Add credential**, you get the option to launch two quickstarts. Select **custom credential**, and then select **Next**.

![Screenshot of the issue credentials quickstart for creating a custom credential.](media/how-to-use-quickstart/quickstart-startscreen.png)

On the **Create a new credential** page, enter the JSON code for the display and the rules definitions. In the **Credential name** box, give the credential a type name. To create the credential, select **Create**.

![Screenshot of the Create a new credential page, displaying JSON samples for the display and rules files.](media/how-to-use-quickstart/quickstart-create-new.png)

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
        "claim": "vc.credentialSubject.userName",
        "label": "User name",
        "type": "String"
      },
      {
        "claim": "vc.credentialSubject.displayName",
        "label": "Display name",
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

The JSON attestation definition should contain the **idTokens** name, the [OIDC configuration details](rules-and-display-definitions-model#idtokenattestation-type) (clientId, configuration, redirectUri, and scope) and the claims mapping section. The expected JSON for the rules definitions is the inner content of the rules attribute, which starts with the attestation attribute.

The claims mapping in the following example requires that you configure the token as explained in the Claims in the ID token from the identity provider section.

```json
{
  "attestations": {
    "idTokens": [
      {
        "clientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
        "configuration": "https://didplayground.b2clogin.com/didplayground.onmicrosoft.com/B2C_1_sisu/v2.0/.well-known/openid-configuration",
        "redirectUri": "vcclient://openid/",
        "scope": "openid profile email",
        "mapping": [
          {
            "outputClaim": "userName",
            "required": true,
            "inputClaim": "$.upn",
            "indexed": true
          },
          {
            "outputClaim": "displayName",
            "required": true,
            "inputClaim": "$.name",
            "indexed": false
          },
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

## Application registration

The clientId attribute is the application ID of a registered application in the OIDC identity provider. For Microsoft Entra ID, you create the application by following these steps:

1. In the **Azure portal**, go to **Microsoft Entra ID**.
2. Select **App registrations**, select **New registration**, and then give the app a name.

    If you want only accounts in your tenant to be able to sign in, keep the **Accounts in this directory only** check box selected.
3. In **Redirect URI (optional)**, select **Public client/native (mobile & desktop)**, and then enter **vcclient://openid/**.

If you want to check the claims included in the Microsoft Entra ID token, take the following steps:

1. On the left pane, select **Authentication** &gt; **Add platform** &gt; **Web**.
2. For **Redirect URI**, enter **https://jwt.ms**, and then select **ID Tokens (used for implicit and hybrid flows)**.
3. Select **Configure**.

After you finish testing your ID token, consider removing **https://jwt.ms** and the support for **implicit and hybrid flows**.

**For Microsoft Entra ID**: You can test your app registration and, if you enable support for redirecting to **https://jwt.ms**, you can get an ID token by running the following in your browser:

```http
https://login.microsoftonline.com/<your-tenantId>/oauth2/v2.0/authorize?client_id=<your-appId>&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.ms&scope=openid%20profile&response_type=id_token&prompt=login
```

In the code, replace &lt;your-tenantId&gt; with your tenant ID. To get the extra claims, you need to have **profile** as part of the **scope**.

**For Azure Active Directory B2C**: The app registration process is the same, but B2C has built-in support in the Azure portal for testing your B2C policies via the **Run user flow** functionality.

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

## Claims in the ID token from the identity provider

Claims must exist in the returned identity provider so that they can successfully populate your verifiable credential.

If the claims don't exist, there's no value in the issued verifiable credential. Most OIDC identity providers don't issue a claim in an ID token if the claim has a null value in your profile. Be sure to include the claim in the ID token definition, and ensure that you enter a value for the claim in your user profile.

**For Microsoft Entra ID**: To configure the claims to include in your token, see [Provide optional claims to your app](../identity-platform/optional-claims). The configuration is per application, so this configuration should be for the app that has the application ID specified in the client ID in the rules definition.

To match the display and rules definitions, you should make your application's optionalClaims JSON look like the following example:

```json
"optionalClaims": {
    "idToken": [
        {
            "name": "upn",
            "source": null,
            "essential": false,
            "additionalProperties": []
        },
        {
            "name": "family_name",
            "source": null,
            "essential": false,
            "additionalProperties": []
        },
        {
            "name": "given_name",
            "source": null,
            "essential": false,
            "additionalProperties": []
        },
        {
            "name": "preferred_username",
            "source": null,
            "essential": false,
            "additionalProperties": []
        }
    ],
    "accessToken": [],
    "saml2Token": []
},
```

**For Azure Active Directory B2C**: Configuring other claims in your ID token depends on whether your B2C policy is a *user flow* or a *custom policy*. For information about user flows, see [Set up a sign-up and sign-in flow in Azure Active Directory B2C](/en-us/azure/active-directory-b2c/add-sign-up-and-sign-in-policy?pivots=b2c-user-flow). For information about custom policy, see [Provide optional claims to your app](/en-us/azure/active-directory-b2c/configure-tokens?pivots=b2c-custom-policy#provide-optional-claims-to-your-app).

For other identity providers, see the relevant documentation.

## Configure the samples to issue and verify your custom credential

To configure your sample code to issue and verify your custom credentials, you need:

- Your tenant's issuer decentralized identifier (DID)
- The credential type
- The manifest URL to your credential

The easiest way to find this information for a custom credential is to go to your credential in the Azure portal. Select **Issue credential**. Then you have access to a text box with a JSON payload for the Request Service API. Replace the placeholder values with your environment's information. The issuer’s DID is the authority value.

![Screenshot of the quickstart custom credential issue.](media/how-to-use-quickstart/quickstart-config-sample-2.png)