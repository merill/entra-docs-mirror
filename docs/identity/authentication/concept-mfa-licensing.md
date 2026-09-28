---
layout: Conceptual
title: Microsoft Entra multifactor authentication versions and consumption plans - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-licensing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about the Microsoft Entra multifactor authentication client and different methods and versions available.
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: michmcla
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 27c42da9-c882-b9ad-961f-6a85087fc016
document_version_independent_id: 206f972b-91e0-5528-2ad8-750a7c9c9839
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-mfa-licensing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-mfa-licensing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-mfa-licensing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: c1f749cc-e317-945d-6feb-b61d3e59a0fc
---

# Microsoft Entra multifactor authentication versions and consumption plans - Microsoft Entra ID | Microsoft Learn

To protect user accounts in your organization, multifactor authentication should be used. This feature is especially important for accounts that have privileged access to resources. Basic multifactor authentication features are available to Microsoft 365 and Microsoft Entra ID users and administrators for no extra cost. If you want to upgrade the features for your admins or extend multifactor authentication to the rest of your users with more authentication methods and greater control, you can enable Microsoft Entra multifactor authentication by using Conditional Access. For more information, see [Common Conditional Access policy: Require MFA for all users](../conditional-access/howto-conditional-access-policy-all-users-mfa).

Important

This article details the different ways that Microsoft Entra multifactor authentication can be licensed and used. For specific details about pricing and billing, see the [Microsoft Entra pricing page](https://www.microsoft.com/security/business/microsoft-entra-pricing).

## Available versions of Microsoft Entra multifactor authentication

Microsoft Entra multifactor authentication can be used, and licensed, in a few different ways depending on your organization's needs. All tenants are entitled to basic multifactor authentication features by using security defaults. You may already be entitled to use advanced Microsoft Entra multifactor authentication depending on the license you currently have. For example, the first 50,000 monthly active users in Microsoft Entra External ID can use MFA and other Premium P1 or P2 features for free.

The following table details the different ways to get Microsoft Entra multifactor authentication and some of the features and use cases for each.

| If you're a user of | Capabilities and use cases |
| --- | --- |
| [Microsoft 365 Business Premium](https://www.microsoft.com/microsoft-365/business) and [EMS](https://www.microsoft.com/security/business/enterprise-mobility-security) or [Microsoft 365 E3 and E5](https://www.microsoft.com/microsoft-365/enterprise/compare-office-365-plans) | EMS E3, Microsoft 365 E3, and Microsoft 365 Business Premium includes Microsoft Entra ID P1. EMS E5 or Microsoft 365 E5 includes Microsoft Entra ID P2. You can use the same Conditional Access features noted in the following sections to provide multifactor authentication to users. |
| [Microsoft Entra ID P1](../../fundamentals/get-started-premium) | You can use [Microsoft Entra Conditional Access](../conditional-access/policy-all-users-mfa-strength) to prompt users for multifactor authentication during certain scenarios or events to fit your business requirements. |
| [Microsoft Entra ID P2](../../fundamentals/get-started-premium) | Provides the strongest security position and improved user experience. Adds [risk-based Conditional Access](../conditional-access/policy-risk-based-sign-in) to the Microsoft Entra ID P1 features that adapts to user's patterns and minimizes multifactor authentication prompts. |
| [All Microsoft 365 plans](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans) | Microsoft Entra multifactor authentication can be enabled for all users using [security defaults](../../fundamentals/security-defaults). Management of Microsoft Entra multifactor authentication is through the Microsoft 365 portal. For an improved user experience, upgrade to Microsoft Entra ID P1 or P2 and use Conditional Access. For more information, see [secure Microsoft 365 resources with multifactor authentication](/en-us/microsoft-365/admin/security-and-compliance/set-up-multi-factor-authentication). |
| [Office 365 free](https://www.microsoft.com/microsoft-365/enterprise/compare-office-365-plans)[Microsoft Entra ID Free](../../verified-id/how-to-create-a-free-developer-account) | You can use [security defaults](../../fundamentals/security-defaults) to prompt users for multifactor authentication as needed but you don't have granular control of enabled users or scenarios, but it does provide that additional security step. |

## Feature comparison based on licenses

The following table provides a list of the features that are available in the various versions of Microsoft Entra ID for multifactor authentication. Plan out your needs for securing user authentication, then determine which approach meets those requirements. For example, although Microsoft Entra ID Free provides security defaults that provide Microsoft Entra multifactor authentication where only the mobile authenticator app can be used for the authentication prompt. This approach may be a limitation if you can't ensure the mobile authentication app is installed on a user's personal device. See Microsoft Entra ID Free tier later in this topic for more details.

| Feature | Microsoft Entra ID Free - Security defaults (enabled for all users) | Microsoft Entra ID Free - Global Administrators only | Office 365 | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
| --- | --- | --- | --- | --- | --- |
| Protect Microsoft Entra tenant admin accounts with MFA | ● | ● (*Microsoft Entra Global Administrator* accounts only) | ● | ● | ● |
| Mobile app as a second factor | ● | ● | ● | ● | ● |
| Phone call as a second factor |  |  | ● | ● | ● |
| Text message as a second factor |  | ● | ● | ● | ● |
| Admin control over verification methods |  | ● | ● | ● | ● |
| Fraud alert |  |  |  | ● | ● |
| MFA Reports |  |  |  | ● | ● |
| Custom greetings for phone calls |  |  |  | ● | ● |
| Custom caller ID for phone calls |  |  |  | ● | ● |
| Trusted IPs |  |  |  | ● | ● |
| Remember MFA for trusted devices |  | ● | ● | ● | ● |
| MFA for on-premises applications |  |  |  | ● | ● |
| Conditional Access |  |  |  | ● | ● |
| Risk-based Conditional Access |  |  |  |  | ● |

## Compare multifactor authentication policies

Our recommended approach to enforce MFA is using [Conditional Access](../conditional-access/overview). Review the following table to determine what capabilities are included in your licenses.

| Policy | Security defaults | Conditional Access | Per-user MFA |
| --- | --- | --- | --- |
| **Management** |  |  |  |
| Standard set of security rules to keep your company safe | ● |  |  |
| One-click on/off | ● |  |  |
| Included in Office 365 licensing (See license considerations) | ● |  | ● |
| Pre-configured templates in Microsoft 365 Admin Center wizard | ● | ● |  |
| Configuration flexibility |  | ● |  |
| **Functionality** |  |  |  |
| Exempt users from the policy |  | ● | ● |
| Authenticate by phone call or text message | ● | ● | ● |
| Authenticate by Microsoft Authenticator and Software tokens | ● | ● | ● |
| Authenticate by FIDO2, Windows Hello for Business, and Hardware tokens |  | ● | ● |
| Blocks legacy authentication protocols | ● | ● | ● |
| New employees are automatically protected | ● | ● |  |
| Dynamic MFA triggers based on risk events |  | ● |  |
| Authentication and authorization policies |  | ● |  |
| Configurable based on location and device state |  | ● |  |
| Support for "report only" mode |  | ● |  |
| Ability to completely block users/services |  | ● |  |

## Microsoft Entra ID Free tier

All users in a Microsoft Entra ID Free tenant can use Microsoft Entra multifactor authentication by using security defaults. The mobile authentication app can be used for Microsoft Entra multifactor authentication when using Microsoft Entra ID Free security defaults.

- [Learn more about Microsoft Entra security defaults](../../fundamentals/security-defaults)
- [Enable security defaults for users in Microsoft Entra ID Free](../../fundamentals/security-defaults#enabling-security-defaults)

You enable Microsoft Entra multifactor authentication in one of the following ways, depending on the type of account you use:

- If you use a Microsoft Account, [register for multifactor authentication](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).
- If you aren't using a Microsoft Account, [turn on multifactor authentication for a user or group in Microsoft Entra ID](howto-mfa-userstates).