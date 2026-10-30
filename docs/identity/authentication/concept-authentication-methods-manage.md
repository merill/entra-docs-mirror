---
layout: Conceptual
title: Manage authentication methods - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-methods-manage
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about the authentication methods policy and different ways to manage authentication methods.
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: jpettere
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7212e5d4-c9ba-0ea3-0ffd-44dfbf9559f4
document_version_independent_id: 0993e970-9eee-9681-98f1-c76f7bd7dd0a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-methods-manage.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-methods-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-methods-manage.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: fb0fabe9-e7cd-8932-936c-5abbcc0cffca
---

# Manage authentication methods - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID allows the use of a range of authentication methods to support a wide variety of sign-in scenarios. For an overview of the available options, see [Authentication methods in Microsoft Entra ID](overview-authentication). Administrators can specifically configure each method to meet their goals for user experience and security. This topic explains how to manage authentication methods for Microsoft Entra ID, and how configuration options affect user sign-in and password reset scenarios.

## Authentication methods policy

The Authentication methods policy is the recommended way to manage authentication methods, including modern methods like passwordless authentication. [Authentication Policy Administrators](../role-based-access-control/permissions-reference#authentication-policy-administrator) can edit this policy to enable authentication methods for all users or specific groups.

Methods enabled in the Authentication methods policy can typically be used anywhere in Microsoft Entra ID, for both authentication and password reset scenarios. The exception is that some methods are inherently limited to use in authentication, such as FIDO2 and Windows Hello for Business, and others are limited to use in password reset, such as security questions. For more control over which methods are usable in a given authentication scenario, consider using the **Authentication Strengths** feature.

Most methods also have configuration parameters to more precisely control how that method can be used. For example, if you enable **Voice calls**, you can also specify whether an office phone can be used in addition to a mobile phone.

Or let's say you want to enable passwordless authentication with Microsoft Authenticator. You can set extra parameters like showing the user sign-in location or the name of the app being signed into. These options provide more context for users when they sign-in and help prevent accidental MFA approvals.

To manage the Authentication methods policy, sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) and browse to **Entra ID** &gt; **Authentication methods** &gt; **Policies**.

![Screenshot of Authentication methods policy.](media/concept-authentication-methods-manage/authentication-methods-policy.png)

Only the [converged registration experience](concept-registration-mfa-sspr-combined) is aware of the Authentication methods policy. Users in scope of the Authentication methods policy but not the converged registration experience won't see the correct methods to register.

## Legacy MFA and SSPR policies

Two other policies, located in **Multifactor authentication** settings and **Password reset** settings, provide a legacy way to manage some authentication methods for all users in the tenant. You can't control who uses an enabled authentication method, or how the method can be used.

Important

In March 2023, we announced the deprecation of managing authentication methods in the legacy multifactor authentication and self-service password reset (SSPR) policies. Beginning September 30, 2025, authentication methods can't be managed in these legacy MFA and SSPR policies. We recommend customers use the manual migration control to migrate to the Authentication methods policy by the deprecation date.

To manage the legacy MFA policy, Browse to **Entra ID** &gt; **Multifactor authentication** &gt; **Getting started** &gt; **Configure** &gt; **Additional cloud-based multifactor authentication settings**.

![Screenshot of MFA service settings.](media/concept-authentication-methods-manage/service-settings.png)

To manage authentication methods for self-service password reset (SSPR), browse to **Entra ID** &gt; **Password reset** &gt; **Authentication methods**. The **Mobile phone** option in this policy allows either voice calls or text message to be sent to a mobile phone. The **Office phone** option allows only voice calls.

![Screenshot of password reset settings.](media/concept-authentication-methods-manage/password-reset.png)

## How policies work together

Settings aren't synchronized between the policies, which allows administrators to manage each policy independently. Microsoft Entra ID respects the settings in all of the policies so a user who is enabled for an authentication method in *any* policy can register and use that method. To prevent users from using a method, it must be disabled in all policies.

Let's walk through an example where a user who belongs to the Accounting group wants to register Microsoft Authenticator. The registration process first checks the Authentication methods policy. If the Accounting group is enabled for Microsoft Authenticator, the user can register it.

If not, the registration process checks the legacy MFA policy. In that policy, any user can register Microsoft Authenticator if one of these settings is enabled for MFA:

- **Notification through mobile app**
- **Verification code from mobile app or hardware token**

If the user can't register Microsoft Authenticator based on either of those policies, the registration process checks the legacy SSPR policy. In that policy too, a user can register Microsoft Authenticator if the user is enabled for SSPR and any of these settings are enabled:

- **Mobile app notification**
- **Mobile app code**

For users who are enabled for **Mobile phone** for SSPR, the independent control between policies can impact sign-in behavior. Where the other policies have separate options for text message and voice calls, the **Mobile phone** for SSPR enables both options. As a result, anyone who uses **Mobile phone** for SSPR can also use voice calls for password reset, even if the other policies don't allow voice calls.

Similarly, let's suppose you enable **Voice calls** for a group. After you enable it, you find that even users who aren't group members can sign-in with a voice call. In this case, it's likely those users are enabled for **Mobile phone** in the legacy SSPR policy or **Call to phone** in the legacy MFA policy.

## Migration between policies

The Authentication methods policy provides a migration guide to help unify administration of all authentication methods. All desired methods can be enabled in the Authentication methods policy if the policy targets intended user groups, or all users. The authentication methods migration guide automates the steps to audit your current policy settings for MFA and SSPR, and consolidate them in the Authentication methods policy. You can access the guide from the [Microsoft Entra admin center](https://entra.microsoft.com) by browsing to **Entra ID** &gt; **Authentication methods** &gt; **Policies**.

![Screenshot of the Authentication methods policy blade with highlighted wizard entry point.](media/how-to-authentication-methods-manage/wizard-entry-point.png)

You can also migrate policy settings manually. The migration has three settings to let you move at your own pace, and avoid problems with sign-in or SSPR during the transition.

After migration is complete, methods in the legacy MFA and SSPR policies can be disabled. You can centralize control over authentication methods for both sign-in and SSPR in a single place, and the legacy MFA and SSPR policies will be disabled.

Note

Security questions can only be enabled today by using the legacy SSPR policy. If you're using security questions, and don't want to disable them, make sure to keep them enabled in the legacy SSPR policy until a migration control is available. You can migrate the remainder of your authentication methods and still manage security questions in the legacy SSPR policy.

To view the migration options, open the Authentication methods policy and click **Manage migration**.

![Screenshot of migration options.](media/concept-authentication-methods-manage/manage-migration.png)

The following table describes each option.

| Option | Description |
| --- | --- |
| Pre-migration | The Authentication methods policy is used only for authentication.Legacy policy settings are respected. |
| Migration in Progress | The Authentication methods policy is used for authentication and SSPR.Legacy policy settings are respected. |
| Migration Complete | Only the Authentication methods policy is used for authentication and SSPR.Legacy policy settings are ignored. |

Tenants are set to either Pre-migration or Migration in Progress by default, depending on their tenant's current state. If you start in Pre-migration, you can move to any of the states at any time. If you started in Migration in Progress, you can move between Migration in Progress and Migration Complete at any time, but won't be allowed to move to Pre-migration. If you move to Migration Complete, and then choose to roll back to an earlier state, we'll ask why so we can evaluate performance of the product.

![Screenshot of reasons for rollback.](media/concept-authentication-methods-manage/reason.png)

Note

After all authentication methods are fully migrated, the following elements of the legacy SSPR policy remain active:

- The **Number of methods required to reset** control: admins can continue to change how many authentication methods must be verified before a user can perform SSPR.
- The SSPR administrator policy: admins can continue to register and use any methods listed under the legacy SSPR administrator policy or methods they're enabled to use in the Authentication methods policy.

In the future, both of these features will be integrated with the Authentication methods policy.

## Known issues and limitations

- In recent updates, we removed the ability to target individual users. Previously targeted users will remain in the policy, but we recommend moving them to a targeted group.
- Registration of an authentication method can fail if many groups are included in the Authentication methods policy or a registration campaign. We recommend consolidating multiple groups into a single group for each authentication method. To maintain registration for users during consolidation, add the new group and remove current groups in the same operation.

    Note

    You might not be able to save updates to the Authentication methods policy if it targets many groups and the policy size exceeds 20 KB. To avoid this limitation, consolidate targeted groups as much as possible.

## Usable and non-usable methods for users

Administrators can view user authentication methods in the Microsoft Entra admin center. Usable methods are listed first, followed by non-usable methods.

Each authentication method can become nonusable for different reasons. For example, a Temporary Access Pass might expire, or a FIDO2 security key might fail attestation. The portal gets updated to explain why the method isn't usable.

Authentication methods that are no longer available due to **Require re-register multifactor authentication** also appear here.