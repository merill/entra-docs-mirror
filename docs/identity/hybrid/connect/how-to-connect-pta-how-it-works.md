---
layout: Conceptual
title: 'Microsoft Entra Connect: Pass-through Authentication - How it works - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta-how-it-works
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how Microsoft Entra pass-through authentication works
keywords: Azure AD Connect Pass-through Authentication, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: bca93908-e200-5f75-b129-d38c06fe321a
document_version_independent_id: 40b2e0a9-8365-6232-242c-63b6a1102e52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta-how-it-works.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta-how-it-works
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta-how-it-works.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a43bd89b-439c-cf8d-4f5e-b19b6c837002
---

# Microsoft Entra Connect: Pass-through Authentication - How it works - Microsoft Entra ID | Microsoft Learn

This article is an overview of how Microsoft Entra pass-through authentication works. For deep technical and security information, see the [Security deep dive](how-to-connect-pta-security-deep-dive) article.

## How does Microsoft Entra pass-through authentication work?

Note

As a pre-requisite for Pass-through Authentication to work, users need to be provisioned into Microsoft Entra ID from on-premises Active Directory using Microsoft Entra Connect. Pass-through Authentication does not apply to cloud-only users.

When a user tries to sign in to an application secured by Microsoft Entra ID, and if Pass-through Authentication is enabled on the tenant, the following steps occur:

1. The user tries to access an application, for example, [Outlook Web App](https://outlook.office365.com/owa/).
2. If the user isn't already signed in, the user is redirected to the Microsoft Entra ID **User Sign-in** page.
3. The user enters their username into the Microsoft Entra sign-in page, and then selects the **Next** button.
4. The user enters their password into the Microsoft Entra sign-in page, and then selects the **Sign in** button.
5. Microsoft Entra ID, on receiving the request to sign in, places the username and password (encrypted by using the public key of the Authentication Agents) in a queue.
6. An on-premises Authentication Agent retrieves the username and encrypted password from the queue. Note that the Agent doesn't frequently poll for requests from the queue, but retrieves requests over a pre-established persistent connection.
7. The agent decrypts the password by using its private key.
8. The agent validates the username and password against Active Directory by using standard Windows APIs, which is a similar mechanism to what Active Directory Federation Services (AD FS) uses. The username can be either the on-premises default username, usually `userPrincipalName`, or another attribute configured in Microsoft Entra Connect (known as `Alternate ID`).
9. The on-premises Active Directory domain controller (DC) evaluates the request and returns the appropriate response (success, failure, password expired, or user locked out) to the agent.
10. The Authentication Agent, in turn, returns this response back to Microsoft Entra ID.
11. Microsoft Entra ID evaluates the response and responds to the user as appropriate. For example, Microsoft Entra ID either signs the user in immediately or requests for Microsoft Entra multifactor authentication.
12. If the user sign-in is successful, the user can access the application.

The following diagram illustrates all the components and the steps involved:

![Pass-through Authentication](media/how-to-connect-pta-how-it-works/pta2.png)