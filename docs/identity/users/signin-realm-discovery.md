---
layout: Conceptual
title: Username lookup during sign-in - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/signin-realm-discovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: How on-screen messaging reflects username lookup during sign-in in Microsoft Entra ID
ms.topic: concept-article
ms.date: 2024-12-17T00:00:00.0000000Z
ms.reviewer: kexia
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: d200ae83-c846-5051-9391-028ec2d3c1f4
document_version_independent_id: 6b32387f-ee24-8fe0-bd39-a338205ab6a0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/signin-realm-discovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/signin-realm-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/signin-realm-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 267144bf-cafe-7d63-bdca-a3f49c8b84c9
---

# Username lookup during sign-in - Microsoft Entra ID | Microsoft Learn

## Overview

The sign-in behavior in Microsoft Entra ID, part of Microsoft Entra, is changing to make room for new authentication methods and improve usability. During sign-in, Microsoft Entra ID determines where a user needs to authenticate. Microsoft Entra ID makes intelligent decisions by reading organization and user settings for the username entered on the sign-in page. This is a step towards a password-free future that enables other credentials like FIDO 2.0.

## Home realm discovery behavior

Traditionally, home realm discovery depended on either the domain provided at sign-in or a Home Realm Discovery policy for legacy applications. For instance, if a Microsoft Entra user entered their username incorrectly but included their organization's domain name, such as "contoso.com," they would still be directed to their organization's credential collection screen. This method didn't allow for customized experiences on an individual user level.

To enhance usability and support a broader range of credentials, Microsoft Entra ID uses a different process. Microsoft Entra ID's username lookup behavior during sign-in intelligently assesses organization-level and user-level settings based on the entered username. If the username is found within the specified domain, the user is directed accordingly; otherwise, the user is redirected to provide their credentials.

Another benefit of this work is improved error messaging. Here are some examples of the improved error messaging when signing in to an application that supports Microsoft Entra users only.

- The username is mistyped or the username hasn't yet been synced to Microsoft Entra ID:

    ![Screenshot of the username is mistyped or not found.](media/signin-realm-discovery/typo-username.png)
- The domain name is mistyped:

    ![Screenshot of the domain name is mistyped or not found.](media/signin-realm-discovery/typo-domain.png)
- User tries to sign in with a known consumer domain:

    ![Screenshot of sign-in with a known consumer domain.](media/signin-realm-discovery/consumer-domain.png)
- The password is mistyped but the username is accurate:

    ![Screenshot of password is mistyped with good username.](media/signin-realm-discovery/incorrect-password.png)

Important

This feature might have an impact on federated domains relying on the old domain-level Home Realm Discovery to force federation. Federated domain support for this new behavior isn't currently available. In the meantime, some organizations have trained their employees to sign in with a username that doesn’t exist in Microsoft Entra ID but contains the proper domain name, because the domain names routes users currently to their organization's domain endpoint. The new sign-in behavior doesn't allow this. The user is notified to correct the user name, and they aren't allowed to sign in with a username that doesn't exist in Microsoft Entra ID. If you or your organization have practices that depend on the old behavior, it's important for organization administrators to update employee sign-in and authentication documentation and to train employees to use their Microsoft Entra username to sign in.

If you have concerns with the new behavior, leave your remarks in the **Feedback** section of this article.