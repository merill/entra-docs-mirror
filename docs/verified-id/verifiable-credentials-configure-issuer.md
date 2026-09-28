---
layout: Conceptual
title: Tutorial - Issue Microsoft Entra Verified ID credentials from an application - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-issuer
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: In this tutorial, you learn how to issue verifiable credentials by using a sample app.
ms.topic: tutorial
ms.date: 2025-04-30T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: e85be67f-8375-6229-18aa-d687463991f9
document_version_independent_id: c494773d-9fcc-d733-6ddb-935a8e545abd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/verifiable-credentials-configure-issuer.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/verifiable-credentials-configure-issuer
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/verifiable-credentials-configure-issuer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1bf8bf0c-e396-1150-0391-d6fe8d1ba32a
---

# Tutorial - Issue Microsoft Entra Verified ID credentials from an application - Microsoft Entra Verified ID | Microsoft Learn

## Overview

In this tutorial, you run a sample application from your local computer that connects to your Microsoft Entra tenant. Using the application, you're going to issue and verify a verified credential expert card.

In this article, you learn how to:

- Create the verified credential expert card in Azure.
- Gather credentials and environment details to set up the sample application.
- Download the sample application code to your local computer.
- Update the sample application with your verified credential expert card and environment details.
- Run the sample application and issue your first verified credential expert card.
- Verify your verified credential expert card.

The following diagram illustrates the Microsoft Entra Verified ID architecture and the component you configure.

![Diagram that illustrates the Microsoft Entra Verified ID architecture.](media/verifiable-credentials-configure-issuer/verifiable-credentials-architecture.png)

## Prerequisites

- [Set up a tenant for Microsoft Entra Verified ID](verifiable-credentials-configure-tenant).
- To clone the repository that hosts the sample app, install [GIT](https://git-scm.com/downloads).
- [Visual Studio Code](https://code.visualstudio.com/Download), [Visual Studio](https://visualstudio.microsoft.com/downloads/) or similar code editor.
- [.NET 8.0](https://dotnet.microsoft.com/download/dotnet/8.0).
- Download [ngrok](https://ngrok.com/) and sign up for a free account. If you can't use `ngrok` in your organization, read this [FAQ](verifiable-credentials-faq#i-cant-use-ngrok-what-do-i-do).
- A mobile device with the latest version of Microsoft Authenticator.

## Create the verified credential expert card in Azure

In this step, you create the verified credential expert card by using Microsoft Entra Verified ID. After you create the credential, your Microsoft Entra tenant can issue it to users who initiate the process.

1. Sign in to the **Microsoft Entra admin center** with the **Authentication Policy Administrator** role.
2. Select **Verifiable credentials**.
3. After you [set up your tenant](verifiable-credentials-configure-tenant), the **Create credential** page should appear. Alternatively, you can select **Credentials** in the left hand menu and select **+ Add a credential**.
4. In **Create credential**, select **Custom Credential** and select **Next**:

    1. For **Credential name**, enter **VerifiedCredentialExpert**. This name is used in the portal to identify your verifiable credentials. It's included as part of the verifiable credentials contract.
    2. Copy the following JSON and paste it in the **Display definition** textbox

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
    3. Copy the following JSON and paste it in the **Rules definition** textbox

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
                    "indexed": true
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
    4. Select **Create**.

The following screenshot demonstrates how to create a new credential:

![Screenshot that shows how to create a new credential.](media/verifiable-credentials-configure-issuer/how-create-new-credential.png)

## Gather credentials and environment details

Now that you have a new credential, you're going to gather some information about your environment and the credential that you created. You use these pieces of information when you set up your sample application.

1. In Verifiable Credentials, select **Issue credential**.

    ![Screenshot that shows how to select the newly created verified credential.](media/verifiable-credentials-configure-issuer/issue-credential-custom-view.png)
2. Copy the **authority**, which is the Decentralized Identifier, and record it for later.
3. Copy the **manifest** URL. It's the URL that Authenticator evaluates before it displays to the user verifiable credential issuance requirements. Record it for later use.
4. Copy your **Tenant ID**, and record it for later. The Tenant ID is the guid in the manifest URL highlighted in red above.

## Download the sample code

The sample application is available in .NET, and the code is maintained in a GitHub repository. Download the sample code from [GitHub](https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet), or clone the repository to your local machine:

```
git clone https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet.git
```

## Configure the verifiable credentials app

Create a client secret for the registered application that you created. The sample application uses the client secret to prove its identity when it requests tokens.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with appropriate administrator permissions.
2. Select **Microsoft Entra ID**.
3. Go to **Applications** &gt; **App registrations** page.
4. Select the **verifiable-credentials-app** application you created earlier.
5. Select the name to go into the registration details.
6. Copy the **Application (client) ID**, and store it for later.

    ![Screenshot that shows how to copy the app registration ID.](media/verifiable-credentials-configure-issuer/copy-app-id.png)
7. From the main menu, under **Manage**, select **Certificates & secrets**.
8. Select **New client secret**, and do the following:

    1. In **Description**, enter a description for the client secret (for example, **vc-sample-secret**).
    2. Under **Expires**, select a duration for which the secret is valid (for example, six months). Then select **Add**.
    3. Record the secret's **Value**. You'll use this value for configuration in a later step. The secret’s value won't be displayed again, and isn't retrievable by any other means. Record it as soon as it's visible.

At this point, you should have all the required information that you need to set up your sample application.

## Update the sample application

Now you make modifications to the sample app's issuer code to update it with your verifiable credential URL. This step allows you to issue verifiable credentials by using your own tenant.

1. Under the *active-directory-verifiable-credentials-dotnet-main* folder, open Visual Studio Code, and select the project inside the *1-asp-net-core-api-idtokenhint* folder.
2. Under the project root folder, open the *appsettings.json* file. This file contains information about your Microsoft Entra Verified ID environment. Update the following properties with the information that you recorded in earlier steps:

    1. **Tenant ID:** your tenant ID
    2. **Client ID:** your client ID
    3. **Client Secret**: your client secret
    4. **DidAuthority**: Your Decentralized Identifier
    5. **Credential Manifest**: Your manifest URL

    CredentialType is only needed for presentation, so if all you want to do is issuance, it strictly isn't needed.
3. Save the *appsettings.json* file.

The following JSON demonstrates a complete *appsettings.json* file:

```json
{
  "VerifiedID": {
    "Endpoint": "https://verifiedid.did.msidentity.com/v1.0/verifiableCredentials/",
    "VCServiceScope": "3db474b9-6a0c-4840-96ac-1fceb342124f/.default",
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
    "ClientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
    "ClientSecret": "123456789012345678901234567890",
    "CertificateName": "[Or instead of client secret: Enter here the name of a certificate (from the user cert store) as registered with your application]",
    "DidAuthority": "did:web:...your-decentralized-identifier...",
    "CredentialType": "VerifiedCredentialExpert",
    "CredentialManifest":  "https://verifiedid.did.msidentity.com/v1.0/00001111-aaaa-2222-bbbb-3333cccc4444/verifiableCredentials/contracts/VerifiedCredentialExpert"
  }
}
```

## Issue your first verified credential expert card

Now you're ready to issue your first verified credential expert card by running the sample application.

1. From Visual Studio Code, run the *Verifiable\_credentials\_DotNet* project. Or, from your operating system's command line, run:

    ```
    cd active-directory-verifiable-credentials-dotnet\1-asp-net-core-api-idtokenhint
    dotnet build "AspNetCoreVerifiableCredentials.csproj" -c Debug -o .\bin\Debug\net6.
    dotnet run
    ```
2. In another command prompt window, run the following command. This command runs [ngrok](https://ngrok.com/) to set up a URL on 5000, and make it publicly available on the internet.

    ```
    ngrok http 5000
    ```

    Note

    On some computers, you might need to run the command in this format: `./ngrok http 5000`.
3. Open the HTTPS URL generated by ngrok.

    ![Screenshot that shows how to get the ngrok public URL.](media/verifiable-credentials-configure-issuer/ngrok-url.png)
4. From a web browser, select **Get Credential**.

    ![Screenshot that shows how to choose to get the credential from the sample app.](media/verifiable-credentials-configure-issuer/get-credentials.png)
5. Using your mobile device, scan the QR code with the Authenticator app. For more info on scanning the QR code, see the [FAQ section](verifiable-credentials-faq#scanning-the-qr-code).

    ![Screenshot that shows how to scan the QR code.](media/verifiable-credentials-configure-issuer/scan-issuer-qr-code.png)
6. At this time, you see a message warning that this app or website might be risky. Select **Advanced**.

    ![Screenshot that shows how to respond to the warning message.](media/verifiable-credentials-configure-issuer/at-risk.png)
7. At the risky website warning, select **Proceed anyways (unsafe)**. You're seeing this warning because your domain isn't linked to your decentralized identifier (DID). To verify your domain, follow [Link your domain to your decentralized identifier (DID)](how-to-dnsbind). For this tutorial, you can skip the domain registration, and select **Proceed anyways (unsafe).**

    ![Screenshot that shows how to proceed with the risky warning.](media/verifiable-credentials-configure-issuer/proceed-anyway.png)
8. You're prompted to enter a PIN code that is displayed in the screen where you scanned the QR code. The PIN adds an extra layer of protection to the issuance. The PIN code is randomly generated every time an issuance QR code is displayed.

    ![Screenshot that shows how to type the pin code.](media/verifiable-credentials-configure-issuer/enter-verification-code.png)
9. After you enter the PIN number, the **Add a credential** screen appears. At the top of the screen, you see a **Not verified** message (in red). This warning is related to the domain validation warning mentioned earlier.
10. Select **Add** to accept your new verifiable credential.

    ![Screenshot that shows how to add your new credential.](media/verifiable-credentials-configure-issuer/new-verifiable-credential.png)

Congratulations! You now have a verified credential expert verifiable credential.

![Screenshot that shows a newly added verifiable credential.](media/verifiable-credentials-configure-issuer/verifiable-credential-has-been-added.png)

Go back to the sample app. It shows you that a credential successfully issued.

![Screenshot that shows a successfully issued verifiable credential.](media/verifiable-credentials-configure-issuer/credentials-issued.png)

## Verifiable credential names

Your verifiable credential contains **Megan Bowen** for the first name and last name values in the credential. These values were hardcoded in the sample application, and were added to the verifiable credential at the time of issuance in the payload.

In real scenarios, your application pulls the user details from an identity provider. The following code snippet shows where the name is set in the sample application.

```csharp
//file: IssuerController.cs
[HttpGet("/api/issuer/issuance-request")]
public async Task<ActionResult> issuanceRequest()
  {
    ...
    // Here you could change the payload manifest and change the first name and last name.
    payload["claims"]["given_name"] = "Megan";
    payload["claims"]["family_name"] = "Bowen";
    ...
}
```