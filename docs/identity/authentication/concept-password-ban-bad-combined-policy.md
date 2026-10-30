---
layout: Conceptual
title: Combined password policy and check for weak passwords in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-password-ban-bad-combined-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about the combined password policy and check for weak passwords in Microsoft Entra ID
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: tilarso
locale: en-us
document_id: 61301762-ff5c-3768-8274-51bf50b3c912
document_version_independent_id: 48dce508-46ac-d1bb-8a2e-84775236e62c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-password-ban-bad-combined-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-password-ban-bad-combined-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-password-ban-bad-combined-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: df6e0144-57ce-da32-c09f-f5b6f9101ce0
---

# Combined password policy and check for weak passwords in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Beginning in October 2021, Microsoft Entra validation for compliance with password policies also includes a check for [known weak passwords](concept-password-ban-bad) and their variants. This article explains details about the password policy criteria checked by Microsoft Entra ID.

## Microsoft Entra password policies

A password policy is applied to all user and admin accounts that are created and managed directly in Microsoft Entra ID. You can [ban weak passwords](concept-password-ban-bad) and define parameters to [lock out an account](howto-password-smart-lockout) after repeated bad password attempts. Other password policy settings can't be modified.

The Microsoft Entra password policy doesn't apply to user accounts synchronized from an on-premises AD DS environment using Microsoft Entra Connect unless you enable CloudPasswordPolicyForPasswordSyncedUsersEnabled. If CloudPasswordPolicyForPasswordSyncedUsersEnabled and password writeback are enabled, Microsoft Entra password expiration policy applies, but the on-premises password policy takes precedence for length, complexity, and so on.

The following Microsoft Entra password policy requirements apply for all passwords that are created, changed, or reset in Microsoft Entra ID. Requirements are applied during user provisioning, password change, and password reset flows. You can't change these settings except as noted.

| Property | Requirements |
| --- | --- |
| Characters allowed | Uppercase characters (A - Z)Lowercase characters (a - z)Numbers (0 - 9)Symbols:- @ # $ % ^ & \* - \_ ! + = [ ] { } | \ : ' , . ? / ` ~ " ( ) ; &lt; &gt;- blank space |
| Characters not allowed | Unicode characters. Note: For Microsoft Entra External ID tenants, Unicode characters are allowed if the user is created by using Microsoft Graph API or Self-Service Sign-Up. |
| Password length | Passwords require- A minimum of 8 characters- A maximum of 256 characters |
| Password complexity | Passwords require three out of four of the following categories:- Uppercase characters- Lowercase characters- Numbers - Symbols Note: Password complexity check isn't required for Education tenants. |
| Password not recently used | When a user changes their password, the new password shouldn't be the same as the current password. |
| Password isn't banned by [Microsoft Entra Password Protection](concept-password-ban-bad) | The password can't be on the global list of banned passwords for Microsoft Entra Password Protection, or on the customizable list of banned passwords specific to your organization. |

## Password expiration policies

Password expiration policies are unchanged but they're included in this article for completeness. Those assigned at least the [User Administrator](../role-based-access-control/permissions-reference#user-administrator) role can use the [Microsoft Graph PowerShell cmdlets](/en-us/powershell/microsoftgraph/) to set user passwords not to expire.

Note

By default, only passwords for user accounts that aren't synchronized through Microsoft Entra Connect can be configured to not expire. For more information about directory synchronization, see [Connect AD with Microsoft Entra ID](../hybrid/connect/how-to-connect-password-hash-synchronization#password-expiration-policy).

You can also use PowerShell to remove the never-expires configuration, or to see user passwords that are set to never expire.

The following expiration requirements apply to other providers that use Microsoft Entra ID for identity and directory services, such as Microsoft Intune and Microsoft 365.

| Property | Requirements |
| --- | --- |
| Password expiry duration (Maximum password age) | Default value: **90** days.The value is configurable by using the [Update-MgDomain](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/update-mgdomain) cmdlet from the Microsoft Graph PowerShell module. |
| Password expiry (Let passwords never expire) | Default value: **false** (indicates that password's have an expiration date).The value can be configured for individual user accounts by using the [Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser) cmdlet. |