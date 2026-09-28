---
layout: Conceptual
title: App support for SMS-based authentication in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-authentication-sms-supported-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn which apps are supported for users to sign in to Microsoft Entra ID using SMS
ms.topic: reference
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: anjusingh
locale: en-us
document_id: 5ee9d7f4-1d8d-adc5-c00b-ddccd0225328
document_version_independent_id: 4eb876ad-f2b6-997f-5413-90205504c34f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-authentication-sms-supported-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-authentication-sms-supported-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-authentication-sms-supported-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 12af9084-ce8d-7588-a8b4-dd84a4cae273
---

# App support for SMS-based authentication in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

SMS-based authentication is available to Microsoft apps integrated with the Microsoft identity platform (Microsoft Entra ID). This article lists the web and mobile apps that support SMS-based authentication.

## Move to modern, phishing-resistant authentication

Important

Microsoft recommends phishing-resistant authentication methods for improved security. Consider migrating users to one of the following methods:

- [Passkeys (FIDO2)](concept-authentication-passkeys-fido2)
- [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-overview)
- [Certificate-based authentication](concept-certificate-based-authentication)

SMS-based authentication is available to Microsoft apps integrated with the Microsoft identity platform (Microsoft Entra ID). The table lists some of the web and mobile apps that support SMS-based authentication. If you would like to add or validate any app, [contact us](https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789).

| App | Web/browser app | Native mobile app |
| --- | --- | --- |
| Office 365- Microsoft Online Services\* | ● |  |
| Microsoft One Note | ● |  |
| Microsoft Teams | ● | ● |
| Company portal | ● | ● |
| My Apps portal | ● | Not available |
| Microsoft Forms | ● | Not available |
| Microsoft Edge | ● |  |
| Microsoft Power BI | ● |  |
| Microsoft Stream | ● |  |
| Microsoft Power Apps | ● |  |
| Microsoft Azure | ● | ● |
| Azure Virtual Desktop | ● |  |

\**SMS sign-in isn't available for office applications, such as Word, Excel, etc., when accessed directly on the web, but is available when accessed through the [Office 365 web app](https://www.office.com)*

The above mentioned Microsoft apps support SMS sign-in is because they use the Microsoft Identity login (`https://login.microsoftonline.com/`), which allows users to enter phone number and SMS code.

## Unsupported Microsoft apps

Microsoft 365 desktop (Windows or Mac) apps and Microsoft 365 web apps (except MS One Note) that are accessed directly on the web don't support SMS sign-in. These apps use the Microsoft Office login (`https://office.live.com/start/*`) that requires a password to sign in. For the same reason, Microsoft Office mobile apps (except Microsoft Teams, Company portal, and Microsoft Azure) don't support SMS sign-in.

| Unsupported Microsoft apps | Examples |
| --- | --- |
| Native desktop Microsoft apps | Microsoft Teams, Microsoft 365 apps, Word, Excel, and so on. |
| Native mobile Microsoft apps (except Microsoft Teams, Company portal, and Microsoft Azure) | Outlook, Edge, Power BI, Stream, SharePoint, Power Apps, Word, and so on. |
| Microsoft 365 web apps (accessed directly on web) | [Outlook](https://outlook.live.com/owa/), [Word](https://office.live.com/start/Word.aspx), [Excel](https://office.live.com/start/Excel.aspx), [PowerPoint](https://office.live.com/start/PowerPoint.aspx) |

## Support for Non-Microsoft apps

To make Non-Microsoft apps compatible with the SMS sign-in feature:

- Integrate Non-Microsoft web apps with Microsoft Entra ID and use Microsoft Entra authentication. Use Security Assertion Markup Language [SAML](../enterprise-apps/add-application-portal-setup-sso) or OpenID Connect [OIDC](../enterprise-apps/add-application-portal-setup-oidc-sso) to integrate with Microsoft Entra SSO.
- Integrate Non-Microsoft on-premises apps with Microsoft Entra ID using [Microsoft Entra application proxy](../app-proxy/application-proxy-add-on-premises-application)
- Integrate Non-Microsoft client apps with [Microsoft identity platform](../../identity-platform/v2-overview)for authentication
    - [Sample app iOS](../../identity-platform/tutorial-v2-ios)
    - [Sample app Android](../../identity-platform/tutorial-v2-android)