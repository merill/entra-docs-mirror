---
layout: Conceptual
title: Set up Microsoft Entra Verified ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/verified-id-setup-issuance-presentation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: rogulati
ms.author: rogulati
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Configure Microsoft Entra Verified ID in an external tenant, issue credentials, and verify presented credentials in an application.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1026
ms.date: 2026-09-08T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 2a68f980-bf93-d16f-e795-592f53aa815c
document_version_independent_id: 2a68f980-bf93-d16f-e795-592f53aa815c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/verified-id-setup-issuance-presentation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/verified-id-setup-issuance-presentation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/verified-id-setup-issuance-presentation.md
platformId: fd05ffdb-3468-979c-2d23-b566ee3fe545
---

# Set up Microsoft Entra Verified ID - Microsoft Entra External ID | Microsoft Learn

If you're an External ID tenant administrator or developer, use this article to configure Microsoft Entra Verified ID in an external tenant. Before you start, review the prerequisites for Quick setup and the sample application. When you finish, you can create a credential type, issue a credential to a user, and configure an application to request and verify the credential.

Quick setup is the supported setup method for external tenants. It configures signing keys, registers a decentralized identifier (DID), verifies domain ownership, and creates a default Verified Workplace credential.

Important

Advanced setup and Face Check aren't available in external tenants. Quick setup uses a Microsoft-managed shared signing key, supports two issuance and verification requests per second per tenant, and limits credential validity to six months.

## Prerequisites

- A Microsoft Entra External ID tenant with a [registered custom domain](/en-us/entra/identity/users/domains-manage). Without a registered custom domain, there isn't a supported Verified ID setup path for an external tenant.
- The [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator) role to configure Verified ID.
- The [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role if you need to register an application.
- A mobile device with the latest version of Microsoft Authenticator.
- For the .NET sample application, [Git](https://git-scm.com/downloads), [Visual Studio Code](https://code.visualstudio.com/Download) or a similar code editor, [.NET 8.0](https://dotnet.microsoft.com/download/dotnet/8.0), and an [ngrok](https://ngrok.com/) account.

## Set up Verified ID

Use Quick setup to configure Verified ID without deploying Azure Key Vault or managing signing keys.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the Authentication Policy Administrator role.
2. Select **Verified ID**.
3. On the left menu, select **Setup**.
4. Select **Get started**.
5. If your tenant has multiple registered domains, select the domain to use for Verified ID.
6. Wait for setup to finish, and verify that the default workplace credential appears.

Quick setup creates a DID in the format `did:web:verifiedid.entra.microsoft.com:<tenant-id>:<authority-id>`. For more information about Quick setup and the default credential, see [Quick Microsoft Entra Verified ID setup](/en-us/entra/verified-id/verifiable-credentials-configure-tenant-quick).

## Register an application

Register an application so it can get access tokens to call the Verified ID Request Service for issuance and presentation.

1. In the Microsoft Entra admin center, select **Microsoft Entra ID**.
2. Select **Applications** &gt; **App registrations** &gt; **New registration**.
3. Enter a display name for the application.
4. For **Supported account types**, select **Accounts in this organizational directory only**.
5. Select **Register**.
6. On the application page, select **API permissions** &gt; **Add a permission**.
7. Select **APIs my organization uses**.
8. Search for and select **Verifiable Credentials Service Request**.
9. Select **Application permissions**, expand **VerifiableCredential.Create.All**, and select **Add permissions**.
10. Select **Grant admin consent for &lt;your tenant name&gt;**.

You can grant issuance and presentation permissions to separate applications if you need to separate those responsibilities. For the complete registration procedure, see [Register an application in Microsoft Entra ID](/en-us/entra/verified-id/verifiable-credentials-configure-tenant#register-an-application-in-microsoft-entra-id).

## Create a credential type

Create a custom credential with display and rules definitions for the claims that your application issues.

1. Under **Verified ID**, select **Credentials**.
2. Select **Add a credential**.
3. Select **Custom Credential**, and then select **Next**.
4. Enter a credential name.
5. Add the display definition for the credential.
6. Add the rules definition that maps the input claims from your application to the output claims in the credential.
7. Select **Create**.
8. Select **Issue credential** for the credential that you created.
9. Record the authority DID, manifest URL, and tenant ID. You use these values to configure the issuing application.

For a sample display definition, rules definition, and credential, see [Issue Microsoft Entra Verified ID credentials from an application](/en-us/entra/verified-id/verifiable-credentials-configure-issuer).

## Issue a credential

Configure an issuing application to request a credential for a user and add it to the user's Microsoft Authenticator wallet.

1. Download or clone the [.NET sample application](https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet).
2. Configure the sample application with the tenant ID, application client ID, application credential, authority DID, and credential manifest URL that you recorded.
3. Run the sample application and make its callback endpoint available.
4. In the sample application, select **Get Credential**.
5. Scan the QR code with Microsoft Authenticator.
6. Follow the prompts in Microsoft Authenticator to add the credential.
7. Return to the sample application, and verify that it reports a successful issuance.

For the sample configuration and complete testing procedure, see [Issue Microsoft Entra Verified ID credentials from an application](/en-us/entra/verified-id/verifiable-credentials-configure-issuer).

## Configure credential presentation

Configure a relying-party application to request a credential and process the verified claims returned in the callback.

1. In the Microsoft Entra admin center, select **Verified ID** &gt; **Organization settings**.
2. Record the tenant identifier and DID for the verifying organization.
3. Configure the verifier application with its tenant ID, application client ID, application credential, DID authority, and the credential type to request.
4. Create a presentation request for the credential type.
5. Configure the application to receive the authenticated callback and use the verified claims to make its access decision.

The issuer and verifier can use the same tenant or separate organizations and tenants. When they're separate, configure the verifier with its own tenant identifier and DID. For the complete sample configuration, see [Configure Microsoft Entra Verified ID verifier](/en-us/entra/verified-id/verifiable-credentials-configure-verifier).

## Present and verify a credential

Test the presentation request with the credential in Microsoft Authenticator.

1. Run the verifier application and make its callback endpoint available.
2. In the verifier application, select **Verify Credential**.
3. Scan the QR code with Microsoft Authenticator.
4. Review the presentation request, and select **Allow**.
5. Return to the verifier application, and verify that it received the presentation.
6. Confirm that the application uses the verified claims to make the expected access decision.