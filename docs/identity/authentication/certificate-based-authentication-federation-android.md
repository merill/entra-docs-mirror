---
layout: Conceptual
title: Android certificate-based authentication with federation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/certificate-based-authentication-federation-android
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about the supported scenarios and the requirements for configuring certificate-based authentication in solutions with Android devices
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ropc-nochange
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: annaba
locale: en-us
document_id: 745d8871-0559-5824-3d89-6f0b9077ce17
document_version_independent_id: 0dfec7eb-e608-b0b9-93c8-379fdf1eb993
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/certificate-based-authentication-federation-android.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/certificate-based-authentication-federation-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/certificate-based-authentication-federation-android.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: f22ab248-706f-0f28-d0cf-bb7eb7c93aac
---

# Android certificate-based authentication with federation - Microsoft Entra ID | Microsoft Learn

Android devices can use certificate-based authentication (CBA) to authenticate to Microsoft Entra ID using a client certificate on their device when connecting to:

- Office mobile applications such as Microsoft Outlook and Microsoft Word
- Exchange ActiveSync (EAS) clients

Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.

## Microsoft mobile applications support

| Apps | Support |
| --- | --- |
| Azure Information Protection app | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Intune Company Portal | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Microsoft Teams | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| OneNote | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| OneDrive | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Outlook | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Power BI | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Skype for Business | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Word / Excel / PowerPoint | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |
| Yammer | ![Check mark signifying support for this application](media/entra-certificate-based-authentication-android/ic195031.png) |

### Implementation requirements

The device OS version must be Android 5.0 (Lollipop) and above.

A federation server must be configured.

For Microsoft Entra ID to revoke a client certificate, the AD FS token must have the following claims:

- `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>` (The serial number of the client certificate)
- `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>` (The string for the issuer of the client certificate)

Microsoft Entra ID adds these claims to the refresh token if they're available in the AD FS token (or any other SAML token). When the refresh token needs to be validated, this information is used to check the revocation.

As a best practice, you should update your organization's AD FS error pages with the following information:

- The requirement for installing the Microsoft Authenticator on Android.
- Instructions on how to get a user certificate.

For more information, see [Customizing the AD FS Sign-in Pages](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950%28v=ws.11%29).

Office apps with modern authentication enabled send '*prompt=login*' to Microsoft Entra ID in their request. By default, Microsoft Entra ID translates '*prompt=login*' in the request to AD FS as '*wauth=usernamepassworduri*' (asks AD FS to do U/P Auth) and '*wfresh=0*' (asks AD FS to ignore SSO state and do a fresh authentication). If you want to enable certificate-based authentication for these apps, you need to modify the default Microsoft Entra behavior. Set the '*PromptLoginBehavior*' in your federated domain settings to '*Disabled*'. You can use [New-MgDomainFederationConfiguration](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/new-mgdomainfederationconfiguration) to perform this task:

```powershell
New-MgDomainFederationConfiguration -DomainId <domain> -PromptLoginBehavior "disabled"
```

## Exchange ActiveSync clients support

Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported. To determine if your email application does support this feature, contact your application developer.