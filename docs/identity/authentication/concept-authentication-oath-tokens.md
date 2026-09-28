---
layout: Conceptual
title: OATH tokens authentication method - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-oath-tokens
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using OATH tokens in Microsoft Entra ID to help improve and secure sign-in events.
services: active-directory
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: lvandenende
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3580bf07-789b-a9c0-26c2-68d21eb66b70
document_version_independent_id: f61c354b-cac2-c3e2-881a-2f0540bdd8e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-oath-tokens.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-oath-tokens
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-oath-tokens.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 44541dff-2cd5-c14d-360c-e6b81bf6fdf6
---

# OATH tokens authentication method - Microsoft Entra ID | Microsoft Learn

OATH time-based one-time password (TOTP) is an open standard that specifies how one-time password (OTP) codes are generated. OATH TOTP can be implemented using either software or hardware to generate the codes. Microsoft Entra ID doesn't support OATH HOTP, a different code generation standard.

## Software OATH tokens

Software OATH tokens are typically applications such as the Microsoft Authenticator app and other authenticator apps. Microsoft Entra ID generates the secret key, or seed, that's input into the app and used to generate each OTP.

The Authenticator app automatically generates codes when set up to do push notifications so a user has a backup even if their device doesn't have connectivity. Third-party applications that use OATH TOTP to generate codes can also be used.

Some OATH TOTP hardware tokens are programmable, meaning they don't come with a secret key or seed preprogrammed. These programmable hardware tokens can be set up using the secret key or seed obtained from the software token setup flow. Customers can purchase these tokens from the vendor of their choice and use the secret key or seed in their vendor's setup process.

## Hardware OATH tokens (preview)

Microsoft Entra ID supports the use of OATH-TOTP SHA-1 and SHA-256 tokens that refresh codes every 30 or 60 seconds. Customers can purchase these tokens from the vendor of their choice.

Microsoft Entra ID has a new Microsoft Graph API in preview for Azure. Administrators can access Microsoft Graph APIs with least privileged roles to manage tokens in the preview. There aren't any options to manage hardware OATH token in this preview refresh in the Microsoft Entra admin center.

You can continue to manage tokens from the original preview in **OATH tokens** in the Microsoft Entra admin center. On the other hand, you can only manage tokens in the preview refresh by using Microsoft Graph APIs.

Hardware OATH tokens that you add with Microsoft Graph for this preview refresh appear along with other tokens in the admin center. But you can only manage them by using Microsoft Graph.

### Time drift correction

Microsoft Entra ID adjusts time drift of the tokens during activation and every authentication. The following table lists the time adjustment that Microsoft Entra ID makes for tokens during activation and sign in.

| Token refresh interval | Activation time range | Authentication time range |
| --- | --- | --- |
| 30 seconds | +/- 1 day | +/- 1 minute |
| 60 seconds | +/- 2 days | +/- 2 minutes |

### Improvements in the preview refresh

This hardware OATH token preview refresh improves flexibility and security for organizations by removing Global Administrator requirements. Organizations can delegate token creation, assignment, and activation to Privileged Authentication Administrators or Authentication Policy Administrators.

The following table lists the role requirements to manage hardware OATH tokens in the preview refresh.

| Task | Preview refresh role |
| --- | --- |
| Create a new token in the tenant’s inventory. | Authentication Policy Administrator |
| Read a token from the tenant’s inventory; doesn't return the secret. | Authentication Policy Administrator |
| Update a token in the tenant. For example, update manufacturer or module; Secret can't be updated. | Authentication Policy Administrator |
| Delete a token from the tenant’s inventory. | Authentication Policy Administrator |

As part of the preview refresh, end users can also self-assign and activate tokens from their [Security info](https://mysignins.microsoft.com/security-info). In the preview refresh, a token can only be assigned to one user. The following table lists token and role requirements to assign and activate tokens.

| Task | Token state | Role requirement |
| --- | --- | --- |
| Assign a token from the inventory to a user in the tenant. | Assigned | Member (self)Authentication AdministratorPrivileged Authentication Administrator |
| Read the token of the user, doesn't return the secret. | Activated / Assigned (depends if the token was already activated or not) | Member (self)Authentication Administrator (only has restricted Read, not standard Read)Privileged Authentication Administrator |
| Update the token of the user, such as provide current 6-digit code for activation, or change token name. | Activated | Member (self)Authentication AdministratorPrivileged Authentication Administrator |
| Remove the token from the user. The token goes back to the token inventory. | Available (back to the tenant inventory) | Member (self)Authentication AdministratorPrivileged Authentication Administrator |

In the legacy multifactor authentication (MFA) policy, hardware and software OATH tokens can only be enabled together. If you enable OATH tokens in the legacy MFA policy, end users see an option to add **Hardware OATH tokens** in their Security info page.

If you don't want end users to see an option to add **Hardware OATH tokens**, migrate to the Authentication methods policy. In the Authentication methods policy, hardware and software OATH tokens can be enabled and managed separately. For more information about how to migrate to the Authentication methods policy, see [How to migrate MFA and SSPR policy settings to the Authentication methods policy for Microsoft Entra ID](how-to-authentication-methods-manage).

Tenants with a Microsoft Entra ID P1 or P2 license can continue to upload hardware OATH tokens as in the original preview. For more information, see [Upload hardware OATH tokens in CSV format](how-to-mfa-upload-oath-tokens).

For more information about how to enable hardware OATH tokens and Microsoft Graph APIs that you can use to upload, activate, and assign tokens, see [How to manage OATH tokens](how-to-mfa-manage-oath-tokens).

## OATH token icons

Users can add and manage OATH tokens at [Security info](https://aka.ms/mysecurityinfo), or they can select **Security info** from **My account**. Software and hardware OATH tokens have different icons.

| Token registration type | Icon |
| --- | --- |
| OATH software token | ![Software OATH token](media/concept-authentication-methods/software-oath-token-icon.png) |
| OATH hardware token | ![Hardware OATH token](media/concept-authentication-methods/hardware-oath-token-icon.png) |