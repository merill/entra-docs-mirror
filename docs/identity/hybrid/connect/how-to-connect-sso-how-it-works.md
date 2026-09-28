---
layout: Conceptual
title: 'Microsoft Entra Connect: Seamless Single Sign-On - How it works - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sso-how-it-works
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how the Microsoft Entra seamless single sign-on feature works.
keywords: what is Azure AD Connect, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: d8bb630d-3c70-4eb6-57ff-c1cb2d43cf76
document_version_independent_id: 0ea6e768-c503-ef66-8337-40607909f6a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sso-how-it-works.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sso-how-it-works
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sso-how-it-works.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 6655d8ae-a218-3585-fc6e-276dcb314e46
---

# Microsoft Entra Connect: Seamless Single Sign-On - How it works - Microsoft Entra ID | Microsoft Learn

This article gives you technical details into how the Microsoft Entra seamless single sign-on (Seamless SSO) feature works.

## How does Seamless SSO work?

This section has three parts to it:

1. The setup of the Seamless SSO feature.
2. How a single user sign-in transaction on a web browser works with Seamless SSO.
3. How a single user sign-in transaction on a native client works with Seamless SSO.

### How does set up work?

Seamless SSO is enabled using Microsoft Entra Connect as shown [here](how-to-connect-sso-quick-start). While enabling the feature, the following steps occur:

- A computer account (`AZUREADSSOACC`) is created in your on-premises Active Directory (AD) in each AD forest that you synchronize to Microsoft Entra ID (using Microsoft Entra Connect).
- In addition, a number of Kerberos service principal names (SPNs) are created for use during the Microsoft Entra sign-in process.
- The computer account's Kerberos decryption key is shared securely with Microsoft Entra ID. If there are multiple AD forests, each computer account will have its own unique Kerberos decryption key.

Important

The `AZUREADSSOACC` computer account needs to be strongly protected for security reasons. Only Domain Admins should be able to manage the computer account. Ensure that Kerberos delegation on the computer account is disabled, and that no other account in Active Directory has delegation permissions on the `AZUREADSSOACC` computer account.. Store the computer account in an Organization Unit (OU) where they are safe from accidental deletions and where only Domain Admins have access. The Kerberos decryption key on the computer account should also be treated as sensitive. We highly recommend that you [roll over the Kerberos decryption key](how-to-connect-sso-faq) of the `AZUREADSSOACC` computer account at least every 30 days.

Important

Seamless SSO supports the following Kerberos encryption types: `AES256_HMAC_SHA1`, `AES128_HMAC_SHA1`, and `RC4_HMAC_MD5`. For enhanced security, Microsoft recommends configuring the `AzureADSSOAcc$` account to use `AES256_HMAC_SHA1` or another AES-based encryption type instead of RC4. The configured encryption type is stored in the `msDS-SupportedEncryptionTypes` attribute of the account in Active Directory Domain Services (AD DS).

Starting with the July 2026 Windows Server update, the default Kerberos encryption type in AD DS will change from RC4 to AES-256. Organizations that continue to use RC4 may experience authentication or Seamless SSO issues after this update is applied. To help ensure uninterrupted SSO access, Microsoft recommends migrating the `AzureADSSOAcc$` account to AES-256 as soon as possible.

If the `AzureADSSOAcc$` account is currently configured to use `RC4_HMAC_MD5` and you plan to switch to an AES-based encryption type, you must first roll over the Kerberos decryption key for the `AzureADSSOAcc$` account, as described in the [FAQ documentation](how-to-connect-sso-faq). Failing to roll over the key before changing the encryption type can prevent Seamless SSO from functioning correctly.

Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses integrated Windows authentication (IWA).

### How does sign-in on a web browser with Seamless SSO work?

The sign-in flow on a web browser is as follows:

1. The user tries to access a web application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.
2. If the user isn't already signed in, the user is redirected to the Microsoft Entra sign-in page.
3. The user types in their user name into the Microsoft Entra sign-in page.

    Note

    For [certain applications](how-to-connect-sso-faq), steps 2 & 3 are skipped.
4. Using JavaScript in the background, Microsoft Entra ID challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.
5. The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACC` computer account (which represents Microsoft Entra ID).
6. Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.
7. The browser forwards the Kerberos ticket it acquired from Active Directory to Microsoft Entra ID.
8. Microsoft Entra ID decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.
9. After evaluation, Microsoft Entra ID either returns a token back to the application or asks the user to perform additional proofs, such as multifactor authentication.
10. If the user sign-in is successful, the user is able to access the application.

The following diagram illustrates all the components and the steps involved.

![Seamless Single Sign On - Web app flow](media/how-to-connect-sso-how-it-works/sso2.png)

Seamless SSO is opportunistic. This means that if it fails, the sign-in experience falls back to its regular behavior. In that case, the user needs to enter their password to sign in.

### How does sign-in on a native client with Seamless SSO work?

The sign-in flow on a native client is as follows:

1. The user tries to access a native application (for example, the Outlook client) from a domain-joined corporate device inside your corporate network.
2. If the user isn't already signed in, the native application retrieves the username of the user from the device's Windows session.
3. The app sends the username to Microsoft Entra ID, and retrieves your tenant's WS-Trust MEX endpoint. This WS-Trust endpoint is used exclusively by the Seamless SSO feature, and isn't a general implementation of the WS-Trust protocol on Microsoft Entra ID.
4. The app then queries the WS-Trust MEX endpoint to see if integrated authentication endpoint is available. The integrated authentication endpoint is used exclusively by the Seamless SSO feature.
5. If step 4 succeeds, a Kerberos challenge is issued.
6. If the app is able to retrieve the Kerberos ticket, it forwards it up to Microsoft Entra integrated authentication endpoint.
7. Microsoft Entra ID decrypts the Kerberos ticket and validates it.
8. Microsoft Entra ID signs the user in, and issues a SAML token to the app.
9. The app then submits the SAML token to Microsoft Entra ID OAuth2 token endpoint.
10. Microsoft Entra ID validates the SAML token and issues an access token, a refresh token for the specified resource, and an ID token to the app.
11. The user gets access to the app's resource.

The following diagram illustrates all the components and the steps involved.

![Seamless Single Sign On - Native app flow](media/how-to-connect-sso-how-it-works/sso14.png)