---
layout: Conceptual
title: How Conditional Access Authentication Strengths Work for External Users - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-strength-external-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how admins can use authentication strength requirements for external users in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: namkedia, inbarc
locale: en-us
document_id: 02d04fb2-960d-995e-82c7-9a91fec68668
document_version_independent_id: 02d04fb2-960d-995e-82c7-9a91fec68668
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-strength-external-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-strength-external-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-strength-external-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 64551016-0f57-3788-a26a-26af74004452
---

# How Conditional Access Authentication Strengths Work for External Users - Microsoft Entra ID | Microsoft Learn

Authentication strengths are especially useful for restricting external access to sensitive apps in your organization. They can enforce specific authentication methods, such as phishing-resistant methods, for external users.

When you apply a Conditional Access authentication strength policy to external Microsoft Entra users, the policy works together with multifactor authentication (MFA) trust settings in your cross-tenant access settings to determine where and how the external user must perform MFA. A Microsoft Entra user authenticates in their home Microsoft Entra tenant. When the user accesses your resource, Microsoft Entra ID applies the policy and checks if you enabled MFA trust.

Note

Enabling MFA trust is optional for business-to-business (B2B) collaboration but is *required* for [B2B direct connect](../../external-id/b2b-direct-connect-overview#multifactor-authentication-mfa).

In external user scenarios, the authentication methods that can satisfy authentication strengths vary, depending on whether the user is completing MFA in the home tenant or the resource tenant. The following table indicates the allowed methods in each tenant. If a resource tenant opts to trust claims from external Microsoft Entra organizations, the resource tenant for MFA accepts only the claims listed in the table's "Home tenant" column. If the resource tenant disables MFA trust, the external user must complete MFA in the resource tenant by using one of the methods listed in the "Resource tenant" column.

| Authentication method | Home tenant | Resource tenant |
| --- | --- | --- |
| Text message as second factor | ✅ | ✅ |
| Voice call | ✅ | ✅ |
| Microsoft Authenticator push notification | ✅ | ✅ |
| Microsoft Authenticator phone sign-in | ✅ |  |
| OATH software token | ✅ | ✅ |
| OATH hardware token | ✅ |  |
| FIDO2 security key | ✅ |  |
| Windows Hello for Business | ✅ |  |
| Certificate-based authentication | ✅ |  |

For more information about how to set authentication strengths for external users, see [Require multifactor authentication strengths for external users](../conditional-access/policy-guests-mfa-strength).

## User experience for external users

A Conditional Access authentication strength policy works together with [MFA trust settings](../../external-id/cross-tenant-access-settings-b2b-collaboration) in your cross-tenant access settings. First, a Microsoft Entra user authenticates with their own account in the home tenant. When the user tries to access your resource, Microsoft Entra ID applies the Conditional Access authentication strength policy and checks if you enabled MFA trust:

- **If MFA trust is enabled**: Microsoft Entra ID checks the user's authentication session for a claim that indicates MFA was fulfilled in the user's home tenant. See the preceding table for authentication methods that are acceptable for MFA when they're completed in an external user's home tenant.

    If the session contains a claim that indicates the MFA policies are already met in the user's home tenant, and the methods satisfy the authentication strength requirements, the user is allowed access. Otherwise, Microsoft Entra ID presents the user with a challenge to complete MFA in the home tenant by using an acceptable authentication method.
- **If MFA trust is disabled**: Microsoft Entra ID presents the user with a challenge to complete MFA in the resource tenant by using an acceptable authentication method. See the preceding table for authentication methods that are acceptable for MFA by an external user.