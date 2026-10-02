---
layout: Conceptual
title: Reset a user's password - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/users-reset-password-azure-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Instructions about how to reset a user's password using Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-08-27T00:00:00.0000000Z
ms.reviewer: jeffsta
ms.custom: ge-structured-content-pilot, sfi-image-nochange
locale: en-us
document_id: d85a9cdc-b09a-979c-8711-c04222f57d08
document_version_independent_id: fe414258-573c-ac73-8f58-8d9429329337
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/users-reset-password-azure-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/users-reset-password-azure-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/users-reset-password-azure-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 93412fb2-ad59-83f9-f4cb-b5b75a4f7327
---

# Reset a user's password - Microsoft Entra | Microsoft Learn

## Overview

Administrators can reset a user's password if the user forgets the password, if the user gets locked out, or if the user never received a password.

Note

If you're not an administrator and you need instructions on how to reset your own work or school password, see [Reset your work or school password](https://support.microsoft.com/account-billing/reset-your-work-or-school-password-using-security-info-23dde81f-08bb-4776-ba72-e6b72b9dda9e).

Unless your tenant is the home directory for a user, you can't reset their password. This means that if your user is signing in to your organization using an account from another organization, a Microsoft account, or a Google account, you also can't reset their password.

If your user has a source of authority as Windows Server Active Directory, you can only reset the password if you turned on password writeback and the user domain is managed. Changing the user password for federated domains isn't supported. In this case, change the user password in the on-premises Active Directory.

If your user has a source of authority as External Microsoft Entra ID, you can't reset the password. Only the user, or an administrator in that tenant, can reset the password.

## Prerequisites

You must have at least the [Password Administrator](../identity/role-based-access-control/permissions-reference#password-administrator) role to reset a user's password. Other roles can reset passwords for a limited set of users. For more information, see [Who can reset passwords](../identity/role-based-access-control/privileged-roles-permissions#who-can-reset-passwords).

## To reset a password

Follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Password Administrator](../identity/role-based-access-control/permissions-reference#password-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select the user that needs the reset, then select **Reset password**.

    The **Alain Charon - Profile** page appears with the **Reset password** option.

    [![Screenshot of the User's profile page, with Reset password option highlighted.](media/users-reset-password-azure-portal/user-profile-reset-password-link.png)](media/users-reset-password-azure-portal/user-profile-reset-password-link.png#lightbox)
4. In the **Reset password** page, select **Reset password**.

    Note

    When you're using Microsoft Entra ID, Microsoft Entra ID autogenerates a temporary password for the user. When using Active Directory on-premises, you create the password for the user.
5. Copy the password and give it to the user. The user must change the password during the next sign-in process.

Note

The temporary password never expires. The next time the user signs in, the password still works, regardless of how much time has passed since the temporary password was generated.

Important

If an administrator can't reset the user's password, and the Application Event Logs on the Microsoft Entra Connect server has error code hr=80231367, review the user's attributes in Active Directory. If the attribute **AdminCount** is set to 1, this prevents an administrator from resetting the user's password. The attribute **AdminCount** must be set to 0, for administrators to reset the user's password.