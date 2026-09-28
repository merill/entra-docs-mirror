---
layout: Conceptual
title: 'Microsoft Entra Connect: Seamless single sign-on - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes Microsoft Entra seamless single sign-on and how it allows you to provide true single sign-on for corporate desktop users inside your corporate network.
keywords: what is Azure AD Connect, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 3d4a028c-c19d-bc2d-a021-2da38afff08d
document_version_independent_id: a3604972-b194-71be-32b8-0c34b027fae1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 63a7f2c8-af7d-e12b-d981-545465326648
---

# Microsoft Entra Connect: Seamless single sign-on - Microsoft Entra ID | Microsoft Learn

## What is Microsoft Entra seamless single sign-on?

Microsoft Entra seamless single sign-on (Microsoft Entra seamless SSO) automatically signs users in when they are on their corporate devices connected to your corporate network. When enabled, users don't need to type in their passwords to sign in to Microsoft Entra ID, and usually, even type in their usernames. This feature provides your users easy access to your cloud-based applications without needing any additional on-premises components.

Seamless SSO can be combined with either the [Password Hash Synchronization](how-to-connect-password-hash-synchronization) or [Pass-through Authentication](how-to-connect-pta) sign-in methods. Seamless SSO is *not* applicable to Active Directory Federation Services (ADFS).

![Seamless single sign-on](media/how-to-connect-sso/sso1.png)

## SSO via primary refresh token vs. Seamless SSO

For Windows 10, Windows Server 2016, and later versions, it’s recommended to use SSO via primary refresh token (PRT). For Windows 7 and Windows 8.1, it’s recommended to use Seamless SSO. Seamless SSO needs the user's device to be domain-joined, but it isn't used on Windows 10 [Microsoft Entra joined devices](../../devices/concept-directory-join) or [Microsoft Entra hybrid joined devices](../../devices/concept-hybrid-join). SSO on Microsoft Entra joined, Microsoft Entra hybrid joined, and Microsoft Entra registered devices works based on the [Primary Refresh Token (PRT)](../../devices/concept-primary-refresh-token)

SSO via PRT works once devices are registered with Microsoft Entra ID for Microsoft Entra hybrid joined, Microsoft Entra joined or personal registered devices via Add Work or School Account. For more information on how SSO works with Windows 10 using PRT, see: [Primary Refresh Token (PRT) and Microsoft Entra ID](../../devices/concept-primary-refresh-token)

## Key benefits

- *Great user experience*
    - Users are automatically signed into both on-premises and cloud-based applications.
    - Users don't have to enter their passwords repeatedly.
- *Easy to deploy & administer*
    - No additional components needed on-premises to make this work.
    - Works with any method of cloud authentication - [Password Hash Synchronization](how-to-connect-password-hash-synchronization) or [Pass-through Authentication](how-to-connect-pta).
    - Can be rolled out to some or all your users using Group Policy.
    - Register non-Windows 10 devices with Microsoft Entra ID without the need for any AD FS infrastructure. This capability needs you to use version 2.1 or later of the [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).

## Feature highlights

- Sign-in username can be either the on-premises default username (`userPrincipalName`) or another attribute configured in Microsoft Entra Connect (`Alternate ID`). Both use cases work because Seamless SSO uses the `securityIdentifier` claim in the Kerberos ticket to look up the corresponding user object in Microsoft Entra ID.
- Seamless SSO is an opportunistic feature. If it fails for any reason, the user sign-in experience goes back to its regular behavior - that is, the user needs to enter their password on the sign-in page.
- If an application (for example, `https://myapps.microsoft.com/contoso.com`) forwards a `domain_hint` (OpenID Connect) or `whr` (SAML) parameter - identifying your tenant, or `login_hint` parameter - identifying the user, in its Microsoft Entra sign-in request, users are automatically signed in without them entering usernames or passwords.
- Users also get a silent sign-on experience if an application (for example, `https://contoso.sharepoint.com`) sends sign-in requests to Microsoft Entra ID's endpoints set up as tenants - that is, `https://login.microsoftonline.com/contoso.com/<..>` or `https://login.microsoftonline.com/<tenant_ID>/<..>` - instead of Microsoft Entra ID's common endpoint - that is, `https://login.microsoftonline.com/common/<...>`.
- Sign out is supported. This allows users to choose another Microsoft Entra account to sign in with, instead of being automatically signed in using Seamless SSO automatically.
- Microsoft 365 Win32 clients (Outlook, Word, Excel, and others) with versions 16.0.8730.xxxx and above are supported using a non-interactive flow. For OneDrive, you have to activate the [OneDrive silent config feature](https://techcommunity.microsoft.com/t5/Microsoft-OneDrive-Blog/Previews-for-Silent-Sync-Account-Configuration-and-Bandwidth/ba-p/120894) for a silent sign-on experience.
- It can be enabled via Microsoft Entra Connect.
- It's a free feature, and you don't need any paid editions of Microsoft Entra ID to use it.
- It's supported on web browser-based clients and Office clients that support [modern authentication](/en-us/microsoft-365/enterprise/modern-auth-for-office-2013-and-2016) on platforms and browsers capable of Kerberos authentication:

| OS\Browser | Internet Explorer | Microsoft Edge\*\*\*\* | Google Chrome | Mozilla Firefox | Safari |
| --- | --- | --- | --- | --- | --- |
| Windows 10/11 | Yes\* | Yes | Yes | Yes\*\*\* | N/A |
| Windows 8.1 | Yes\* | Yes\*\*\*\* | Yes | Yes\*\*\* | N/A |
| Windows 8 | Yes\* | N/A | Yes | Yes\*\*\* | N/A |
| Windows Server 2012 R2 or above | Yes\*\* | Yes\*\*\*\* | Yes | Yes\*\*\* | N/A |
| Mac OS X | N/A | N/A | Yes\*\*\* | Yes\*\*\* | Yes\*\*\* |

Note

Microsoft Edge legacy is no longer supported

\*Requires Internet Explorer version 11 or later. ([Beginning August 17, 2021, Microsoft 365 apps and services won't support Internet Explorer 11](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-365-apps-say-farewell-to-internet-explorer-11-and/ba-p/1591666).)

\*\*Requires Internet Explorer version 11 or later. Disable Enhanced Protected Mode.

\*\*\*Requires [additional configuration](how-to-connect-sso-quick-start#browser-considerations).

\*\*\*\*Microsoft Edge based on Chromium