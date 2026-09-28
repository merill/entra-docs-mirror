---
layout: Conceptual
title: Verified helpdesk with Microsoft Entra Verified ID - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/helpdesk-with-verified-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: A design pattern describing how to verify in helpdesk scenarios
services: decentralized-identity
ms.topic: concept-article
ms.date: 2024-12-13T00:00:00.0000000Z
locale: en-us
document_id: a0c7bd53-316a-968e-95db-7b897349fb79
document_version_independent_id: a0c7bd53-316a-968e-95db-7b897349fb79
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/helpdesk-with-verified-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/helpdesk-with-verified-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/helpdesk-with-verified-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/54fcef21-b24a-4ef4-9c4a-a525c23ee9a3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ab60220-e56b-41ff-a8bf-45b8d7ab716f
platformId: cc79142b-aa58-19f3-9fab-fe205fa2b088
---

# Verified helpdesk with Microsoft Entra Verified ID - Microsoft Entra Verified ID | Microsoft Learn

## Overview

An ongoing challenge for helpdesk is verifying the identity of callers seeking help, especially in remote interactions via phone, chat, or email. Traditional methods such as personally identifiable information (PII) and knowledge-based authentication are no match for today’s sophisticated attackers, who use phishing, social engineering, and even AI-powered voice cloning to bypass defenses. The consequences are serious: under pressure, helpdesk agents may unintentionally expose sensitive data or authorize fraudulent actions.

## The way forward: Stronger and phish-resistant authentication

To defend against these evolving threats without compromising user experience, organizations must adopt modern verification strategies built for today’s threat landscape. This includes:

- Phish-resistant authentication (for example, passkeys)
- AI-driven fraud detection to flag anomalous behavior
- Zero Trust principles enforcing strict identity checks
- Enterprise-grade identity validation—without relying on PII.

Microsoft offers solutions that enable admins to enhance security without sacrificing user experience. Organizations can adopt the two key patterns:

1. Strong Authentication: Users authenticate with their existing corporate credentials before requesting helpdesk support. User is prompted to present strong phish-resistant credentials before they're granted access to resources. Microsoft platform offers solutions like Azure Communication Services that supports multichannel communication APIs for adding voice, video, chat, text messaging/SMS, email, and more to all your applications. [Azure Communication Services (ACS)](https://azure.microsoft.com/products/communication-services/?msockid=27ae7d5196f463891a416cf192f46589#Features-3) supports a security pattern where users visit a URL to initiate a direct, encrypted voice/video/chat session with a helpdesk via an ACS-integrated app. Authentication is managed using Microsoft Entra ID, and secure ACS tokens ensure controlled access, preventing unauthorized connections.
2. Total loss recovery: In cases where a user has lost all authentication credentials, a secure, policy-driven recovery process is implemented to re-establish access without compromising security. Microsoft Entra Verified ID could help such enterprises add verification processes seamlessly into their existing helpdesk and service desk operations. Upon successful verification, service desk could offer tasks such as password resets, Temporary Access Pass (TAP) provision, MFA (multifactor authentication) onboarding, and account updates, potentially enabling self-service automation. This article explains how to use Microsoft Entra Verified ID for the total loss recovery scenario.

## When to use this pattern

- You have a service desk system with API support.
- Your service desk system allows programmatic integration to query Microsoft Entra ID or any other directory services system to do a reliable matching and updates to user profiles.

## Solution

To deploy verification flows, an enterprise must follow three main steps:

1. Set up Microsoft Entra Verified ID in your Microsoft 365 tenant and enable VerifiedEmployee credential for issuance. Alternatively, an enterprise can also issue Verified ID based on Identity verification flow by working with IDV (Identity Proofing and Verification) partners https://aka.ms/verifiedidisv.
2. Issue Verified ID to your users.
3. Add verification flow to your existing service desk solution.

### Set up Microsoft Entra Verified ID

To set up the Microsoft Entra Verified ID service, follow the instructions for Quick Configuration - [Set up a tenant for Microsoft Entra Verified ID](verifiable-credentials-configure-tenant-quick). Alternatively, customers could use [Advanced set up](verifiable-credentials-configure-tenant) for setting up Verified ID where you as an admin must configure Azure Key Vault, take care of registering your decentralized ID and verifying your domain.

### Get started with issuing VerifiedEmployee Verified ID

1. Create a test user in your [Microsoft Entra tenant](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/%7E/AllUsers/menuId/) and upload a photo of [yourself](https://support.microsoft.com/office/add-your-profile-photo-to-microsoft-365-2eaf93fd-b3f1-43b9-9cdc-bdcd548435b7).
2. Go to [MyAccount](verifiable-credentials-configure-tenant-quick#myaccount-available-now-to-simplify-issuance-of-workplace-credentials), sign in as the test user and issue a VerifiedEmployee credential for the user.

    ![Screenshot of getting started with VerifiedEmployee.](media/helpdesk-with-verified-id/get-started-with-verifiedemployee.png)

You first select who can request issuance of a Verified ID by selecting all users or a specific group of users. Then sign in to https://myaccount.microsoft.com and get your [Face Check](using-facecheck) ready credential using [Microsoft Authenticator](https://www.microsoft.com/security/mobile-authenticator-app).

### Add verification flows to service desk solution

An enterprise can set up Microsoft Entra Verified ID integration by either:

- Add it as an inline process like a `Get Verified` button in the Service desk webapp, follow the steps to add a presentation request to verify Verified ID with Face Check. Steps are mentioned in the link https://aka.ms/verifiedidfacecheck.
- Set up a dedicated web application that could accept Microsoft Entra Verified ID `VerifiedEmployee` with [Face Check](using-facecheck). Use the GitHub [sample](https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet/tree/main/6-woodgrove-helpdesk) to deploy the custom webapp. Select `Deploy to Azure` to deploy the [ARM template](/en-us/azure/azure-resource-manager/templates/) that uses Managed Identity.

    ![Screenshot of Deploy to Azure using ARM template.](media/helpdesk-with-verified-id/deploy-to-azure.png)

An enterprise could add a webhook to send the response of Verified ID verification with [Face Check](using-facecheck) to the ServiceDesk tool. You can refer this example of [adding webhook](/en-us/microsoftteams/platform/webhooks-and-connectors/what-are-webhooks-and-connectors) to a Teams channel. This GitHub sample deploys a verification webapp on Azure using Azure App Service.

An enterprise can add self-service automation services like generate a [Temporary Access Pass](../identity/authentication/howto-authentication-temporary-access-pass) post successful verification of Verified ID taking claims from Verified ID. GitHub [sample](https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet/tree/main/5-onboard-with-tap) explains this self-service automation process.

If you're a **Managed Services provider (MSP)** or **Cloud Solutions Provider (CSP)**, you could also add this pattern to your existing Service Desk process. Deploy the verification flow inline or as a custom web application. For the presentation flow, add the `acceptedIssuers` field in the payload and specify the decentralized identifiers (DIDs) for your customers to verify VerifiedEmployee with Face Check.

```json
...
"requestedCredentials": [ 
  { 
    "type": "VerifiedEmployee", 
    "acceptedIssuers": [ "<authority1>", "<authority2>", "..." ], 
    "configuration": { 
      "validation": { 
        "allowRevoked": false, 
        "validateLinkedDomain": true, 
        "faceCheck": { 
          "sourcePhotoClaimName": "photo", 
          "matchConfidenceThreshold": 70 
        } 
      }
  ...
```

![Sequence diagram of Face Check.](media/helpdesk-with-verified-id/sequence-diagram-of-facecheck.png)