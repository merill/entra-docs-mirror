---
layout: Conceptual
title: Tutorial - Quick setup of your tenant for Microsoft Entra Verified ID - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-tenant-quick
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: In this tutorial, you learn how to quickly configure your tenant to support the Verified ID service.
ms.topic: tutorial
ms.date: 2026-04-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: d71e007d-1acb-61f7-89ca-3dd907f53015
document_version_independent_id: 7a27bfc9-587a-d302-78e5-7513bb97bbbe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/verifiable-credentials-configure-tenant-quick.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/verifiable-credentials-configure-tenant-quick
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/verifiable-credentials-configure-tenant-quick.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: 2aa156dd-2912-8c06-ff42-34c6b6999237
---

# Tutorial - Quick setup of your tenant for Microsoft Entra Verified ID - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Quick Verified ID setup removes several configuration steps an admin needs to complete with a single select on a **Get started** button. The quick setup takes care of signing keys, registering your decentralized ID, and verifying your domain ownership. It also creates a Verified Workplace Credential for you.

In this tutorial, you learn how to use the quick setup to configure your Microsoft Entra tenant to use the verifiable credentials service.

Specifically, you learn how to:

- Configure the Verified ID service using the quick setup.
- Control issuance of Verified Workplace Credentials in MyAccount.

Watch this video to quickly set up your Microsoft Entra tenant to use the verifiable credentials service.

## Prerequisites

- You need the [Authentication Policy Administrator](../identity/role-based-access-control/permissions-reference#authentication-policy-administrator) permission for the directory you want to configure. If you need to perform app registration tasks, you'll also need the [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) permission.
- Ensure that you have a [custom domain registered](../identity/users/domains-manage) for the Microsoft Entra tenant. If you don't have one registered, the setup defaults to the advanced setup experience.

Note

The Quick setup method is currently not supported in EDU Microsoft Entra tenants.

## How Quick Verified ID setup works

- Microsoft manages a shared signing key across multiple tenants within a given region. You no longer need to deploy Azure Key Vault.
- There's a two requests per second (RPS) per tenant limit for issuance and verifications.
- Since it's a shared key, the validityInterval of issued credentials is limited to a maximum of six months.
- Verified ID uses the [custom domain registered](../identity/users/domains-manage) for your Microsoft Entra tenant for domain verification. You no longer need to upload your DID configuration JSON to verify your domain. If you don't have a custom domain registered for your tenant, you can't set up Verified ID using the quick setup method.
- If you have customized your [tenant's branding](../fundamentals/how-to-customize-branding#before-you-begin), the VerifiedEmployee default credential picks up logo and background color from there. If you haven't or prefer other values, you can make changes after setup is complete.
- The Decentralized identifier (DID) gets a name like `did:web:verifiedid.entra.microsoft.com:tenantid:authority-id` and the DID document is discoverable following [did:web specification](https://w3c-ccg.github.io/did-method-web/#create-register).

Note

If the quick setup doesn't meet your requirements, use the [Advanced setup](verifiable-credentials-configure-tenant).

## Set up Verified ID

If you have a custom domain registered for your Microsoft Entra tenant, you see this **Get started** option. If you don't have a custom domain registered, either register it before setting up Verified ID or continue using the [advanced setup](verifiable-credentials-configure-tenant).

![Screenshot that shows how to set up Verifiable Credentials.](media/verifiable-credentials-configure-tenant-quick/verifiable-credentials-getting-started.png)

To set up Verified ID, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with appropriate administrator permissions.
2. Select **Verified ID**.
3. From the left menu, select **Setup**.
4. Select the **Get started** button.
5. If you have multiple domains registered for your Microsoft Entra tenant, select the one you would like to use for Verified ID.

    ![Screenshot that shows how to select domain.](media/verifiable-credentials-configure-tenant-quick/verifiable-credentials-select-domain.png)

When the setup process is complete, you see a default workplace credential available to edit and offer to employees of your tenant on their MyAccount page.

![Screenshot that shows how to set up is completed.](media/verifiable-credentials-configure-tenant-quick/verifiable-credentials-setup-complete.png)

## MyAccount available now to simplify issuance of Workplace Credentials

Issuing Verified Workplace Credentials is now available via [myaccount.microsoft.com](https://myaccount.microsoft.com/). Users can sign in to **MyAccount** using their Microsoft Entra credentials and issue themselves a Verified Workplace Credential via the **Get my Verified ID** option.

![Screenshot that shows issuance via myaccount.](media/verifiable-credentials-configure-tenant-quick/verifiable-credentials-my-account-issue.png)

As an admin, you can either remove the option in MyAccount and create your custom application for issuing Verified Workplace Credentials. You can also select specific groups of users who can use MyAccount to issue credentials for themselves.

![Screenshot that shows controlling issuance via myaccount.](media/verifiable-credentials-configure-tenant-quick/verifiable-credentials-setup-groups.png)

Note

When you have made a configuration change for issuing credentials through My Account, expect some minutes of delay before the change takes effect.

## Register an application in Microsoft Entra ID

If you're planning to use custom credentials or set up your own application for issuing or verifying Verified ID, you need to register an application and grant the appropriate permissions for it. Follow this section in the advanced setup to [register an application](verifiable-credentials-configure-tenant#register-an-application-in-microsoft-entra-id).