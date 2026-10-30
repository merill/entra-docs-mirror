---
layout: Conceptual
title: Certificate-based authentication with federation on iOS - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/certificate-based-authentication-federation-ios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about the supported scenarios and the requirements for configuring certificate-based authentication for Microsoft Entra ID in solutions with iOS devices
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ropc-nochange
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
locale: en-us
document_id: bc28fed5-f6ab-481c-26cc-cde205b96e82
document_version_independent_id: dd651a08-3713-db8f-c535-6bfc9efd6e81
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/certificate-based-authentication-federation-ios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/certificate-based-authentication-federation-ios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/certificate-based-authentication-federation-ios.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: e7efa4a7-e2b0-d929-5747-974f527fa9b9
---

# Certificate-based authentication with federation on iOS - Microsoft Entra ID | Microsoft Learn

To improve security, iOS devices can use certificate-based authentication (CBA) to authenticate to Microsoft Entra ID using a client certificate on their device when connecting to the following applications or services:

- Office mobile applications such as Microsoft Outlook and Microsoft Word
- Exchange ActiveSync (EAS) clients

Using certificates eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.

## Microsoft mobile applications support

| Apps | Support |
| --- | --- |
| Azure Information Protection app | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Company Portal | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Microsoft Teams | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Office (mobile) | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| OneNote | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| OneDrive | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Outlook | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Power BI | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Skype for Business | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Word / Excel / PowerPoint | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |
| Yammer | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-ios/ic195031.png) |

## Requirements

To use CBA with iOS, the following requirements and considerations apply:

- The device OS version must be iOS 9 or above.
- Microsoft Authenticator is required for Office applications on iOS.
- An identity preference must be created in the macOS Keychain that includes the authentication URL of the AD FS server. For more information, see [Create an identity preference in Keychain Access on Mac](https://support.apple.com/guide/keychain-access/create-an-identity-preference-kyca6343b6c9/mac).

The following Active Directory Federation Services (AD FS) requirements and considerations apply:

- The AD FS server must be enabled for certificate authentication and use federated authentication.
- The certificate needs to have to use Enhanced Key Usage (EKU) and contain the UPN of the user in the *Subject Alternative Name (NT Principal Name)*.

## Configure AD FS

For Microsoft Entra ID to revoke a client certificate, the AD FS token must have the following claims. Microsoft Entra ID adds these claims to the refresh token if they're available in the AD FS token (or any other SAML token). When the refresh token needs to be validated, this information is used to check the revocation:

- `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>` - add the serial number of your client certificate
- `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>` - add the string for the issuer of your client certificate

As a best practice, you also should update your organization's AD FS error pages with the following information:

- The requirement for installing the Microsoft Authenticator on iOS.
- Instructions on how to get a user certificate.

For more information, see [Customizing the AD FS sign in page](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950%28v=ws.11%29).

## Use modern authentication with Office apps

Some Office apps with modern authentication enabled send `prompt=login` to Microsoft Entra ID in their request. By default, Microsoft Entra ID translates `prompt=login` in the request to AD FS as `wauth=usernamepassworduri` (asks AD FS to do U/P Auth) and `wfresh=0` (asks AD FS to ignore SSO state and do a fresh authentication). If you want to enable certificate-based authentication for these apps, modify the default Microsoft Entra behavior.

To update the default behavior, set the '*PromptLoginBehavior*' in your federated domain settings to *Disabled*. You can use the [New-MgDomainFederationConfiguration](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/new-mgdomainfederationconfiguration) cmdlet to perform this task, as shown in the following example:

```powershell
New-MgDomainFederationConfiguration -DomainId <domain> -PromptLoginBehavior "disabled"
```

## Support for Exchange ActiveSync clients

On iOS 9 or later, the native iOS mail client is supported. To determine if this feature is supported for all other Exchange ActiveSync applications, contact your application developer.