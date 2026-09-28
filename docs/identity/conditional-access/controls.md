---
layout: Conceptual
title: Custom controls in Microsoft Entra Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/controls
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how custom controls in Microsoft Entra Conditional Access work.
ms.topic: concept-article
ms.date: 2026-05-19T00:00:00.0000000Z
ms.reviewer: gkinasewitz
ms.custom: sfi-image-nochange
locale: en-us
document_id: e03d33c6-c60b-153c-bf76-a127be502170
document_version_independent_id: 7bbf1dc5-bd91-d03a-7939-439bfbee85c9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/controls.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/controls
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/controls.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ff2a3908-414a-9100-6002-9bbe8508f699
---

# Custom controls in Microsoft Entra Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

Custom controls are a preview capability of Microsoft Entra ID. When you use custom controls, users are redirected to a compatible service to meet authentication requirements outside of Microsoft Entra ID. To meet this control, a user's browser redirects to the external service, performs any required authentication, and then redirects back to Microsoft Entra ID. Microsoft Entra ID verifies the response and, if the user is successfully authenticated or validated, the user continues in the Conditional Access flow.

Important

Custom controls are deprecated. Adding new custom controls and editing existing custom controls will not be allowed starting September 2026. Full retirement is scheduled for early 2027. Start planning your migration now. For more information, see the [External MFA GA announcement](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/external-mfa-in-microsoft-entra-id-is-now-generally-available/4488926).

For more information, see [Manage external MFA in Microsoft Entra ID](../authentication/how-to-authentication-external-method-manage).

## Creating custom controls

Caution

Custom controls **can't** be used with:

- Microsoft Entra ID Protection's automation requiring multifactor authentication
- Microsoft Entra self-service password reset (SSPR)
- Satisfying multifactor authentication claim requirements
- Sign-in frequency controls
- Privileged Identity Manager (PIM)
- Intune device enrollment
- Cross-tenant trusts
- Joining devices to Microsoft Entra ID.

Custom controls work with a limited set of approved authentication providers. To create a custom control, first contact the provider you want to use. Each non-Microsoft provider has its own process and requirements to sign up, subscribe, or join the service, and to indicate that you want to integrate with Conditional Access. At that point, the provider gives you a block of data in JSON format. This data allows the provider and Conditional Access to work together for your tenant, creates the new control and defines how Conditional Access can tell if your users have successfully performed verification with the provider.

Copy the JSON data and paste it into the related textbox. Don't change the JSON unless you fully understand the change you're making. Changing the JSON might break the connection between the provider and Microsoft, potentially locking you and your users out of your accounts.

The option to create a custom control is located in the **Manage** section of the **Conditional Access** page.

![Custom controls interface in Conditional Access](media/controls/custom-controls-conditional-access.png)

Selecting **New custom control** opens a page with a textbox for the JSON data of your control.

![New custom control](media/controls/new-custom-controls-conditional-access.png)

## Deleting custom controls

To delete a custom control, ensure that it isn't being used in any Conditional Access policy. Then follow these steps:

1. Go to the Custom controls list.
2. Select … .
3. Select **Delete**.

## Editing custom controls

To edit a custom control, delete the current control and create a new one with the updated information.

## Known limitations

Custom controls can't be used with Microsoft Entra ID Protection's automation requiring Microsoft Entra multifactor authentication, Microsoft Entra self-service password reset (SSPR), satisfying multifactor authentication claim requirements, with sign-in frequency controls, to elevate roles in Privileged Identity Manager (PIM), as part of Intune device enrollment, for cross-tenant trusts, or when joining devices to Microsoft Entra ID.