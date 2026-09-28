---
layout: Conceptual
title: Certificate signing options in a SAML token - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/certificate-signing-options
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to use advanced certificate signing options in the SAML token for preintegrated apps in Microsoft Entra ID
ms.topic: concept-article
ms.date: 2025-07-10T00:00:00.0000000Z
ms.reviewer: saumadan
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 8aac55fa-1799-ee74-543d-4f1477c024a0
document_version_independent_id: 44e91059-fd03-ea15-5568-a708979b56f7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/certificate-signing-options.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/certificate-signing-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/certificate-signing-options.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8e4d43b8-82c0-8336-bca3-223bd0794c52
---

# Certificate signing options in a SAML token - Microsoft Entra ID | Microsoft Learn

Today Microsoft Entra ID supports thousands of preintegrated applications in the Microsoft Entra App Gallery. Over 500 of the applications support single sign-on by using the [Security Assertion Markup Language (SAML)](https://wikipedia.org/wiki/Security_Assertion_Markup_Language) 2.0 protocol, such as the [NetSuite](https://azuremarketplace.microsoft.com/marketplace/apps/aad.netsuite) application. When a customer authenticates to an application through Microsoft Entra ID by using SAML, Microsoft Entra ID sends a token to the application (via an HTTP POST). The application then validates and uses the token to sign in the customer instead of prompting for a username and password. These SAML tokens are signed with the unique certificate generated in Microsoft Entra ID and by specific standard algorithms.

Microsoft Entra ID uses some of the default settings for the gallery applications. The default values are set up based on the application's requirements.

In Microsoft Entra ID, you can set up certificate signing options and the certificate signing algorithm.

## Certificate signing options

Microsoft Entra ID supports three certificate signing options:

- **Sign SAML assertion**. This default option is set for most of the gallery applications. If you select this option, Microsoft Entra ID as an Identity Provider (IdP) signs the SAML assertion and certificate with the [X.509](https://wikipedia.org/wiki/X.509) certificate of the application.
- **Sign SAML response**. If you select this option, Microsoft Entra ID as an IdP signs the SAML response with the X.509 certificate of the application.
- **Sign SAML response and assertion**. If you select this option, Microsoft Entra ID as an IdP signs the entire SAML token with the X.509 certificate of the application.

## Certificate signing algorithms

Microsoft Entra ID supports two signing algorithms, or secure hash algorithms (SHAs), to sign the SAML response:

- **SHA-256**. Microsoft Entra ID uses this default algorithm to sign the SAML response. It's the newest algorithm and is more secure than SHA-1. Most of the applications support the SHA-256 algorithm. If an application supports only SHA-1 as the signing algorithm, you can change it. Otherwise, we recommend that you use the SHA-256 algorithm for signing the SAML response.
- **SHA-1**. This algorithm is older, and is less secure than SHA-256. If an application supports only this signing algorithm, you can select this option in the **Signing Algorithm** drop-down list. Microsoft Entra ID then signs the SAML response with the SHA-1 algorithm.

## Prerequisites

To change an application's SAML certificate signing options and the certificate signing algorithm, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, Application Administrator.

## Change certificate signing options and signing algorithm

To change an application's SAML certificate signing options and the certificate signing algorithm:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results.

Next, change the certificate signing options in the SAML token for that application:

1. In the left pane of the application overview page, select **Single sign-on**.
2. If the **Set up Single Sign-On with SAML** page appears, go to step 5.
3. If the **Set up Single Sign-On with SAML** page doesn't appear, select **Change single sign-on modes**.
4. In the **Select a single sign-on method** page, select **SAML**. If **SAML** isn't available, the application doesn't support SAML, and you might ignore the rest of this procedure and article.
5. In the **Set up Single Sign-On with SAML** page, find the **SAML Signing Certificate** heading, and select the **Edit** icon (a pencil). The **SAML Signing Certificate** page appears.
6. In the **Signing Option** drop-down list, choose **Sign SAML response**, **Sign SAML assertion**, or **Sign SAML response and assertion**. Descriptions of these options appear earlier in this article in the Certificate signing options.
7. In the **Signing Algorithm** drop-down list, choose **SHA-1** or **SHA-256**. Descriptions of these options appear earlier in this article in the Certificate signing algorithms section.
8. If you're satisfied with your choices, select **Save** to apply the new SAML signing certificate settings. Otherwise, select the **X** to discard the changes.