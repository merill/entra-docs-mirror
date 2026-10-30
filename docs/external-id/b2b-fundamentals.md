---
layout: Conceptual
title: Microsoft Entra B2B best practices and recommendations - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/b2b-fundamentals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn best practices and recommendations for business-to-business (B2B) guest user access in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2025-05-07T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
locale: en-us
document_id: 4a40d1d9-4f4f-4389-27f6-298eccc3c69b
document_version_independent_id: e7fb480b-de99-e06f-5e22-58dd9b78785b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/b2b-fundamentals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/b2b-fundamentals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/b2b-fundamentals.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2e8b6387-7bfe-4e27-b795-a9ae80707eef
---

# Microsoft Entra B2B best practices and recommendations - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article contains recommendations and best practices for business-to-business (B2B) collaboration in Microsoft Entra External ID.

Important

The [email one-time passcode feature](one-time-passcode) is now turned on by default for all new tenants and for any existing tenants where you haven't explicitly turned it off. When this feature is turned off, the fallback authentication method is to prompt invitees to create a Microsoft account.

## B2B recommendations

| Recommendation | Comments |
| --- | --- |
| Consult Microsoft Entra guidance for securing your collaboration with external partners | Learn how to take a holistic governance approach to your organization's collaboration with external partners by following the recommendations in [Securing external collaboration in Microsoft Entra ID and Microsoft 365](../architecture/secure-external-access-resources). |
| Carefully plan your cross-tenant access and external collaboration settings | Microsoft Entra External ID gives you a flexible set of controls for managing collaboration with external users and organizations. You can allow or block all collaboration, or configure collaboration only for specific organizations, users, and apps. Before configuring settings for cross-tenant access and external collaboration, take a careful inventory of the organizations you work and partner with. Then determine if you want to enable [B2B direct connect](b2b-direct-connect-overview) or [B2B collaboration](what-is-b2b) with other Microsoft Entra tenants. |
| Restrict guest user access to the directory | By default, guest users have limited access to your Microsoft Entra directory. They can manage their own profile and see some information about other users, groups, and apps. You can further restrict access so that guests can see only their own profile information. Learn more about [default guest permissions](../fundamentals/users-default-permissions) and how to configure [external collaboration settings](external-collaboration-settings-configure). |
| Determine who can invite guests | By default, all users in your organization, including B2B collaboration guest users, can invite external users to B2B collaboration. If you want to limit the ability to send invitations, you can turn invitations on or off for everyone, or limit invitations to certain roles by configuring [external collaboration settings](external-collaboration-settings-configure). |
| Use tenant restrictions to control how external accounts are used on your networks and managed devices. | With tenant restrictions, you can prevent your users from using accounts they've created in unknown tenants or accounts they've received from external organizations. We recommend you disallow these accounts and use B2B collaboration instead. |
| For an optimal sign-in experience, federate with identity providers | Whenever possible, federate directly with identity providers to allow invited users to sign in to your shared apps and resources without having to create Microsoft Accounts (MSAs) or Microsoft Entra accounts. You can use the [Google federation feature](google-federation) to allow B2B guest users to sign in with their Google accounts. Or, you can use the [SAML/WS-Fed identity provider feature](direct-federation) to set up federation with any organization whose identity provider (IdP) supports the SAML 2.0 or WS-Fed protocol. |
| Use the Email one-time passcode feature for B2B guests who can’t authenticate by other means | The [Email one-time passcode](one-time-passcode) feature authenticates B2B guest users when they can't be authenticated through other means like Microsoft Entra ID, a Microsoft account (MSA), or Google federation. When the guest user redeems an invitation or accesses a shared resource, they can request a temporary code, which is sent to their email address. Then they enter this code to continue signing in. |
| Add company branding to your sign-in page | You can customize your sign-in page so it's more intuitive for your B2B guest users. See how to [add company branding to sign in and Access Panel pages](../fundamentals/how-to-customize-branding). |
| Add your privacy statement to the B2B guest user redemption experience | You can add the URL of your organization's privacy statement to the first time invitation redemption process so that an invited user must consent to your privacy terms to continue. See [How-to: Add your organization's privacy info in Microsoft Entra ID](../fundamentals/properties-area). |
| Use the bulk invite (preview) feature to invite multiple B2B guest users at the same time | Invite multiple guest users to your organization at the same time by using the bulk invite preview feature in the Azure portal. This feature lets you upload a CSV file to create B2B guest users and send invitations in bulk. See [Tutorial for bulk inviting B2B users](tutorial-bulk-invite). |
| Enforce Conditional Access policies for Microsoft Entra multifactor authentication | We recommend enforcing MFA policies on the apps you want to share with partner B2B users. This way, MFA will be consistently enforced on the apps in your tenant regardless of whether the partner organization is using MFA. See [Conditional Access for B2B collaboration users](authentication-conditional-access). If you have a close business relationship with an organization and you've verified their MFA practices, you can configure cross-tenant access settings to accept their MFA claims ([learn more](cross-tenant-access-overview#organizational-settings)). |
| Use authentication strength Conditional Access policies for guests | Authentication strength is a Conditional Access control that lets you define a specific combination of multifactor authentication (MFA) methods that an external Microsoft Entra user must complete to access your resources. It works together with MFA trust settings in your cross-tenant access settings to determine where and how the external user must perform MFA. See [Authentication strength policies for external users](authentication-conditional-access#authentication-strength-policies-for-external-users) |
| If you’re enforcing device-based Conditional Access policies, use exclusion lists to allow access to B2B users | If device-based Conditional Access policies are enabled in your organization, B2B guest user devices will be blocked because they’re not managed by your organization. You can create exclusion lists containing specific partner users to exclude them from the device-based Conditional Access policy. See [Conditional Access for B2B collaboration users](authentication-conditional-access). |
| Use a tenant-specific URL when providing direct links to your B2B guest users | As an alternative to the invitation email, you can give a guest a direct link to your app or portal. This direct link must be tenant-specific, meaning it must include a tenant ID or verified domain so the guest can be authenticated in your tenant, where the shared app is located. See [Redemption experience for the guest user](redemption-experience). |
| When developing an app, use UserType to determine guest user experience | If you're developing an application and you want to provide different experiences for tenant users and guest users, use the UserType property. The UserType claim isn't currently included in the token. Applications should use the Microsoft Graph API to query the directory for the user to get their UserType. |
| Change the UserType property *only* if the user’s relationship to the organization changes | Although it’s possible to use PowerShell to convert the UserType property for a user from Member to Guest (and vice-versa), you should change this property only if the relationship of the user to your organization changes. See [Properties of a B2B guest user](user-properties). |
| Find out if your environment will be affected by Microsoft Entra directory limits | Microsoft Entra B2B is subject to Microsoft Entra service directory limits. For details about the number of directories a user can create and the number of directories to which a user or guest user can belong, see [Microsoft Entra service limits and restrictions](../identity/users/directory-service-limits-restrictions). |
| Manage the B2B account lifecycle with the Sponsor feature | A sponsor is a user or group responsible for their guest users. For more details about this new feature see [Sponsor field for B2B users](b2b-sponsors). |