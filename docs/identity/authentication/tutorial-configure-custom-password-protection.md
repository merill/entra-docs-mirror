---
layout: Conceptual
title: Configure custom Microsoft Entra password protection lists - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-configure-custom-password-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: In this tutorial, you learn how to configure custom banned password protection lists for Microsoft Entra ID to restrict common words in your environment.
ms.topic: tutorial
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: rogoya
ms.custom: sfi-image-nochange
locale: en-us
document_id: a425eb90-e161-54c9-3ba8-351ce93296f6
document_version_independent_id: 61ac46d0-cf72-2139-f11a-dd6319b51ff5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/tutorial-configure-custom-password-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/tutorial-configure-custom-password-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/tutorial-configure-custom-password-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0d142674-db8c-bcce-67e6-89b7c4da03cd
---

# Configure custom Microsoft Entra password protection lists - Microsoft Entra ID | Microsoft Learn

Users often create passwords that use common local words such as a school, sports team, or famous person. These passwords are easy to guess, and weak against dictionary-based attacks. To enforce strong passwords in your organization, the Microsoft Entra custom banned password list lets you add specific strings to evaluate and block. A password change request fails if there's a match in the custom banned password list.

In this tutorial you learn how to:

- Enable custom banned passwords
- Add entries to the custom banned password list
- Test password changes with a banned password

## Prerequisites

To complete this tutorial, you need the following resources and privileges:

- A working Microsoft Entra tenant with at least a Microsoft Entra ID P1 or trial license enabled.
    - If needed, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An account with at least the [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) role.
- A non-administrator user with a password you know, such as *testuser*. You test a password change event using this account in this tutorial.
    - If you need to create a user, see [Quickstart: Add new users to Microsoft Entra ID](../../fundamentals/how-to-create-delete-users).
    - To test the password change operation using a banned password, the Microsoft Entra tenant must be [configured for self-service password reset](tutorial-enable-sspr).

## What are banned password lists?

Microsoft Entra ID includes a global banned password list. The contents of the global banned password list isn't based on any external data source. Instead, the global banned password list is based on the ongoing results of Microsoft Entra security telemetry and analysis. When a user or administrator tries to change or reset their credentials, the desired password is checked against the list of banned passwords. The password change request fails if there's a match in the global banned password list. You can't edit this default global banned password list.

To give you flexibility in what passwords are allowed, you can also define a custom banned password list. The custom banned password list works alongside the global banned password list to enforce strong passwords in your organization. Organizational-specific terms can be added to the custom banned password list, such as the following examples:

- Brand names
- Product names
- Locations, such as company headquarters
- Company-specific internal terms
- Abbreviations that have specific company meaning
- Months and weekdays with your company's local languages

When a user attempts to reset a password to something that's on the global or custom banned password list, they see one of the following error messages:

- *Unfortunately, your password contains a word, phrase, or pattern that makes your password easily guessable. Please try again with a different password.*
- *Unfortunately, you can't use that password because it contains words or characters that have been blocked by your administrator. Please try again with a different password.*

The custom banned password list is limited to a maximum of 1000 terms. It's not designed for blocking large lists of passwords. To maximize the benefits of the custom banned password list, review the [custom banned password list concepts](concept-password-ban-bad#custom-banned-password-list) and [password evaluation algorithm overview](concept-password-ban-bad#how-are-passwords-evaluated).

## Configure custom banned passwords

Let's enable the custom banned password list and add some entries. You can add additional entries to the custom banned password list at any time.

To enable the custom banned password list and add entries to it, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods**, then **Password protection**.
3. Set the option for **Enforce custom list** to *Yes*.
4. Add strings to the **Custom banned password list**, one string per line. The following considerations and limitations apply to the custom banned password list:

    - The custom banned password list can contain up to 1000 terms.
    - The custom banned password list is case-insensitive.
    - The custom banned password list considers common character substitution, such as "o" and "0", or "a" and "@".
    - The minimum string length is four characters, and the maximum is 16 characters.

    Specify your own custom passwords to ban, as shown in the following example

    [![Modify the custom banned password list under Authentication methods](media/tutorial-configure-custom-password-protection/enable-configure-custom-banned-passwords-cropped.png)](media/tutorial-configure-custom-password-protection/enable-configure-custom-banned-passwords.png#lightbox)
5. Leave the option for **Enable password protection on Windows Server Active Directory** to *No*.
6. To enable the custom banned passwords and your entries, select **Save**.

It may take several hours for updates to the custom banned password list to be applied.

For a hybrid environment, you can also [deploy Microsoft Entra password protection to an on-premises environment](howto-password-ban-bad-on-premises-deploy). The same global and custom banned password lists are used for both cloud and on-premises password change requests.

## Test custom banned password list

To see the custom banned password list in action, try to change the password to a variation of one that you added in the previous section. When Microsoft Entra ID tries to process the password change, the password is matched against an entry in the custom banned password list. An error is then displayed to the user.

Note

Before a user can reset their password in the web-based portal, the Microsoft Entra tenant must be [configured for self-service password reset](tutorial-enable-sspr). If needed, the user can then [register for SSPR at https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).

1. Go to the **My Apps** page at https://myapps.microsoft.com.
2. In the top-right corner, select your name, then choose **Profile** from the drop-down menu.

    ![Select profile](media/tutorial-configure-custom-password-protection/myapps-profile.png)
3. On the **Profile** page, select **Change password**.
4. On the **Change password** page, enter the existing (old) password. Enter and confirm a new password that's on the custom banned password list you defined in the previous section, then select **Submit**.
5. An error message is returned that tells you the password has been blocked by the administrator, as shown in the following example:

    ![Error message displayed when you try to use a password that's part of the custom banned password list](media/tutorial-configure-custom-password-protection/password-change-error.png)

## Clean up resources

If you no longer want to use the custom banned password list you have configured as part of this tutorial, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods**, then **Password protection**.
3. Set the option for **Enforce custom list** to *No*.
4. To update the custom banned password configuration, select **Save**.