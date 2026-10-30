---
layout: Conceptual
title: Microsoft Entra multifactor authentication overview - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-howitworks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how Microsoft Entra multifactor authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: michmcla
locale: en-us
document_id: a586047b-a3f3-9cc7-5408-e06f81c1ff99
document_version_independent_id: 5a6f9e74-2859-6f44-1ec4-9fada1441df5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-mfa-howitworks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-mfa-howitworks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-mfa-howitworks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: 18d13106-6571-2683-1ee7-d7e8c8bb124e
---

# Microsoft Entra multifactor authentication overview - Microsoft Entra ID | Microsoft Learn

Multifactor authentication is a process in which users are prompted during the sign-in process for an additional form of identification, such as a code on their cellphone or a fingerprint scan.

If you only use a password to authenticate a user, it leaves an insecure vector for attack. If the password is weak or has been exposed elsewhere, an attacker could be using it to gain access. When you require a second form of authentication, security is increased because this additional factor isn't something that's easy for an attacker to obtain or duplicate.

![Conceptual image of the various forms of multifactor authentication.](media/concept-mfa-howitworks/methods.png)

Microsoft Entra multifactor authentication works by requiring two or more of the following authentication methods:

- Something you know, typically a password.
- Something you have, such as a trusted device that's not easily duplicated, like a phone or hardware key.
- Something you are - biometrics like a fingerprint or face scan.

Microsoft Entra multifactor authentication can also further secure password reset. When users register themselves for Microsoft Entra multifactor authentication, they can also register for self-service password reset in one step. Administrators can choose forms of secondary authentication and configure challenges for MFA based on configuration decisions.

You don't need to change apps and services to use Microsoft Entra multifactor authentication. The verification prompts are part of the Microsoft Entra sign-in, which automatically requests and processes the MFA challenge when needed.

Note

The prompt language is determined by browser locale settings. If you use custom greetings but don’t have one for the language identified in the browser locale, English is used by default. Network Policy Server (NPS) will always use English by default, regardless of custom greetings. English is also used by default if the browser locale can't be identified.

![MFA sign-in screen.](media/concept-mfa-howitworks/sign-in-screen.png)

## Available verification methods

When users sign in to an application or service and receive an MFA prompt, they can choose from one of their registered forms of additional verification. Users can access [My Profile](https://myprofile.microsoft.com) to edit or add verification methods.

The following additional forms of verification can be used with Microsoft Entra multifactor authentication:

- Microsoft Authenticator
- Authenticator Lite (in Outlook)
- Windows Hello for Business
- Passkey (FIDO2)
- Passkey in Microsoft Authenticator
- QR code
- Certificate-based authentication (when configured for multifactor authentication)
- External MFA
- Temporary Access Pass (TAP)
- OATH hardware token (preview)
- OATH software token
- SMS
- Voice call

## How to enable and use Microsoft Entra multifactor authentication

You can use [security defaults](../../fundamentals/security-defaults) in Microsoft Entra tenants to quickly enable Microsoft Authenticator for all users. You can enable Microsoft Entra multifactor authentication to prompt users and groups for additional verification during sign-in.

For more granular controls, you can use [Conditional Access](../conditional-access/overview) policies to define events or applications that require MFA. These policies can allow regular sign-in when the user is on the corporate network or a registered device but prompt for additional verification factors when the user is remote or on a personal device.

![Diagram that shows how Conditional Access works to secure the sign-in process.](media/tutorial-enable-azure-mfa/conditional-access-overview.png)