---
layout: Conceptual
title: Passwordless authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-passwordless
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Microsoft Entra ID enables integration with passwordless authentication protocols that include certificate-based authentication, passwordless security key sign-in, Windows Hello for Business, and passwordless sign-in with Microsoft Authenticator.
ms.topic: concept-article
ms.date: 2023-03-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: dc4d06b7-bd93-9d5f-d0de-792a2db083a5
document_version_independent_id: 0b258433-46ae-95e3-b864-f63c38c65556
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-passwordless.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-passwordless
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-passwordless.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/798bd9d1-9cc5-4fc7-b0e5-8699d1f6ce2a
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b5dc5f65-34a8-4bfc-9917-97d1e20c88b2
platformId: 3b192678-2587-e8fb-dfba-d3c4bd61499e
---

# Passwordless authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Microsoft Entra ID enables integration with the following passwordless authentication protocols.

- [Overview of Microsoft Entra certificate-based authentication](../identity/authentication/concept-certificate-based-authentication): Microsoft Entra certificate-based authentication (CBA) enables customers to allow or require users to authenticate directly with X.509 certificates against their Microsoft Entra ID for applications and browser sign-in. This feature enables customers to adopt phishing resistant authentication and authenticate with an X.509 certificate against their Public Key Infrastructure (PKI).
- [Enable passwordless security key sign-in](../identity/authentication/howto-authentication-passwordless-security-key): For enterprises that use passwords and have a shared PC environment, security keys provide a seamless way for workers to authenticate without entering a username or password. Security keys provide improved productivity for workers, and have better security. This article explains how to sign in to web-based applications with your Microsoft Entra account using a FIDO2 security key.
- [Windows Hello for Business Overview](/en-us/windows/security/identity-protection/hello-for-business/): Windows Hello for Business replaces passwords with strong two-factor authentication on devices. This authentication consists of a type of user credential that is tied to a device and uses a biometric or PIN.
- [Enable passwordless sign-in with Microsoft Authenticator](../identity/authentication/howto-authentication-passwordless-phone): Microsoft Authenticator can be used to sign in to any Microsoft Entra account without using a password. Microsoft Authenticator uses key-based authentication to enable a user credential that is tied to a device, where the device uses a PIN or biometric. Windows Hello for Business uses a similar technology. Microsoft Authenticator can be used on any device platform, including mobile. Microsoft Authenticator can be used with any app or website that integrates with Microsoft Authentication Libraries.