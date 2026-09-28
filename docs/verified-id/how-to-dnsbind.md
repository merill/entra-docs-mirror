---
layout: Conceptual
title: Link your domain to your decentralized identifier (DID) - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-dnsbind
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to link your domain to your decentralized identifier (DID).
documentationCenter: ''
ms.topic: how-to
ms.date: 2024-12-18T00:00:00.0000000Z
locale: en-us
document_id: 1c3fee62-d380-c103-c965-c07aa1366f7b
document_version_independent_id: 7f7eb40e-cc87-4f1b-457b-1b5fc23c5849
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-dnsbind.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-dnsbind
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-dnsbind.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c05d4a51-b4a2-09e7-3c9d-1c7393eed62a
---

# Link your domain to your decentralized identifier (DID) - Microsoft Entra Verified ID | Microsoft Learn

## Overview

This article reviews the steps needed to verify your ownership of the domain name you're using for your decentralized identifier (DID).

## Prerequisites

To verify domain ownership to your DID, you need to:

- Complete [Getting started](verifiable-credentials-configure-tenant) and the subsequent [tutorial set](verifiable-credentials-configure-tenant).

## Verify domain ownership and distribute the did-configuration.json file

The domain you verify ownership of to your DID is defined in the [overview section](verifiable-credentials-configure-tenant#set-up-verified-id). The domain needs to be a domain under your control and it should be in the format `https://www.contoso.com/`.

1. From the **Microsoft Entra admin center**, choose the **Verified ID** page.
2. Select **Overview** and from this section, choose **Verify domain ownership**.
3. Select **Verify** for the domain.
4. Copy or download the `did-configuration.json` file.

    ![Screenshot that shows downloading the well-known configuration.](media/how-to-dnsbind/verify-download.png)
5. Host the `did-configuration.json` file at the location specified. For example, if you specified domain `https://www.contoso.com`, the file needs to be hosted at `https://www.contoso.com/.well-known/did-configuration.json`. There can be no other path in the URL except the `.well-known path` name.
6. When `did-configuration.json` is publicly available at the `.well-known/did-configuration.json` URL, verify it by selecting **Refresh verification status**.

    ![Screenshot that shows the verified well-known configuration.](media/how-to-dnsbind/verify-download-verified.png)
7. Test out issuing or presenting with Microsoft Authenticator to validate. Make sure the **Warn about unsafe apps** setting in Authenticator is toggled on. The setting is on by default.

## How can I verify that the verification is working?

The portal verifies that `did-configuration.json` is reachable over the internet and valid when you select **Refresh verification status**. Authenticator doesn't honor HTTP redirects. You should also consider verifying that you can request that URL in a browser to avoid errors like not using HTTPS, a bad TLS/SSL certificate, or the URL not being public. If the `did-configuration.json` file can't be requested anonymously in a browser or via tools such as `curl`, without warnings or errors, the portal can't complete the **Refresh verification status** step either.

Note

If you're experiencing problems refreshing your verification status, you can troubleshoot it by running `curl -Iv https://contoso.com/.well-known/did-configuration.json` on a machine with Ubuntu OS. Windows Subsystem for Linux with Ubuntu also works. If curl fails, refreshing the verification status won't work.

## Why do I need to verify domain ownership of our DID?

A DID starts out as an identifier that isn't anchored to existing systems. A DID is useful because a user or organization can own it and control it. If an entity interacting with the organization doesn't know "who" the DID belongs to, then the DID isn't as useful.

Linking a DID to a domain solves the initial trust problem by allowing any entity to cryptographically verify the relationship between a DID and a domain.

## How does Verified ID link DIDs and domains?

Verified ID follows the [well-known DID configuration](https://identity.foundation/.well-known/resources/did-configuration/) specification to create the link. The verifiable credentials service links your DID and domain. The service includes the domain information that you provided in your DID and generates the well-known configuration file:

1. Verified ID uses the domain information you provide during organization setup to write a service endpoint within the DID document. All parties who interact with your DID can see the domain your DID proclaims to be associated with.

    ```json
    "service": [
      {
        "id": "#linkeddomains",
        "type": "LinkedDomains",
        "serviceEndpoint": {
          "origins": [
            "https://verifiedid.contoso.com/"
          ]
        }
      }
    ]
    ```
2. The verifiable credential service in Verified ID generates a compliant well-known configuration resource that you must host on your domain. The configuration file includes a self-issued verifiable credential of the credential type `DomainLinkageCredential`, signed with your DID, that has an origin of your domain. Here's an example of the configuration file stored at the root domain URL.

    ```json
    {
      "@context": "https://identity.foundation/.well-known/contexts/did-configuration-v0.0.jsonld",
      "linked_dids": [
        "jwt..."
      ]
    }
    ```

## User experience in the wallet

When a user is going through an issuance flow or presenting a verifiable credential, they should know something about the organization and its DID. Authenticator validates a DID's relationship with the domain in the DID document and presents users with two different experiences depending on the outcome.

## Verified domain

Before Authenticator displays a **Verified** icon, a few points must be true:

- The DID signing the self-issued open ID (SIOP) request must have a service endpoint for a linked domain.
- The root domain doesn't use a redirect and uses HTTPS.
- The domain listed in the DID document has a resolvable well-known resource.
- The well-known resource's verifiable credential is signed with the same DID that was used to sign the SIOP that Authenticator used to kick-start the flow.

If all the previously mentioned points are true, then Authenticator displays a verified page and includes the domain that was validated.

![Screenshot that shows a new permission request.](media/how-to-dnsbind/new-permission-request.png)

## Unverified domain

If any of the preceding points aren't true, Authenticator displays a full-page warning indicating that the domain is unverified. The user is warned that they're in the middle of a potential risky transaction and should proceed with caution. They might have chosen to take this route because:

- The DID isn't anchored to a domain.
- The configuration wasn't set up properly.
- The DID that the user is interacting with could be malicious and actually can't prove that they own the domain linked.

It's highly important that you link your DID to a domain that's recognizable to the user.

![Screenshot that shows the unverified domain warning on the Add a credential screen.](media/how-to-dnsbind/add-credential-not-verified-authenticated.png)

## How do I update the linked domain on my DID?

With the web trust system, updating your linked domain isn't supported. You have to opt out and onboard again.

## Linked domain made easy for developers

Note

The DID document must be publicly available for DID registration to succeed.

The easiest way for a developer to get a domain to use for a linked domain is to use the Azure Storage static website feature. You can't control what the domain name is, except that it contains your storage account name as part of its hostname.

To quickly set up a domain to use for a linked domain:

1. Create a storage account. During creation, select **StorageV2** (general-purpose v2 account) and **Locally redundant storage** (LRS).
2. Go to the storage account and select **Static website** on the leftmost menu and enable **Static website**. If you can't see the **Static website** menu item, you didn't create a **V2** storage account.
3. Copy the primary endpoint name that appears after saving. This value is your domain name. It looks something like `https://<your-storageaccountname>.z6.web.core.windows.net/`.

When it's time to upload the `did-configuration.json` file:

1. Go to the storage account and select **Containers** on the leftmost menu. Then select the container named **$web**.
2. Select **Upload** and select the folder icon to find your file.
3. Before you upload, open the **Advanced** section and specify **.well-known** in the **Upload to folder** text box.
4. Upload the file.

You now have your file publicly available at a URL that looks something like `https://<your-storageaccountname>.z6.web.core.windows.net/.well-known/did-configuration.json`.