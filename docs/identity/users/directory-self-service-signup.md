---
layout: Conceptual
title: Self-service sign up for email-verified users - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/directory-self-service-signup
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Use self-service sign-up in a Microsoft Entra organization
ms.topic: overview
ms.date: 2024-12-13T00:00:00.0000000Z
ms.reviewer: elkuzmen
ms.custom: sfi-ga-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 06c24fd7-43ce-1445-b734-ffd28410911f
document_version_independent_id: b835d64a-a78a-95d9-11a7-8b93a23944c8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/directory-self-service-signup.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/directory-self-service-signup
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/directory-self-service-signup.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4f9c2c31-b423-289b-b060-5e5ae2e8928f
---

# Self-service sign up for email-verified users - Microsoft Entra ID | Microsoft Learn

## Overview

This article explains how to use self-service sign-up to populate an organization in Microsoft Entra ID, part of Microsoft Entra. If you want to take over a domain name from an unmanaged Microsoft Entra organization, see [Take over an unmanaged tenant as administrator](domains-admin-takeover).

Note

This article covers self-service sign-up for email-verified users in Microsoft Entra ID organizations. For self-service sign-up experiences for external users, such as B2B collaboration users or customers, see [Self-service sign-up in Microsoft Entra External ID](../../external-id/self-service-sign-up-overview).

## Why use self-service sign-up?

- Get customers to services they want faster
- Create email-based offers for a service
- Create email-based sign-up flows that quickly allow users to create identities using their easy-to-remember work email aliases
- A self-service-created Microsoft Entra tenant can be turned into a managed tenant that can be used for other services

## Terms and definitions

- **Self-service sign-up** is the method by which a user signs up for a cloud service and has an identity automatically created for them in Microsoft Entra ID based on their email domain.
- An **unmanaged Microsoft Entra tenant** is the tenant where that identity is created. An unmanaged tenant is a tenant that has no Global Administrator.
- An **email-verified user** is a type of user account in Microsoft Entra ID. A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user. An email-verified user is a regular member of a tenant tagged with creationmethod=EmailVerified.

## Control self-service settings

Admins have two self-service controls today. They can control whether:

- Users can join the tenant via email
- Users can license themselves for applications and services

### Control these capabilities

An admin can configure these capabilities using the following Microsoft Entra cmdlet `Update-MgPolicyAuthorizationPolicy` parameters:

- `allowEmailVerifiedUsersToJoinOrganization` controls whether users can join the tenant by email validation. To join, the user must have an email address in a domain that matches one of the verified domains in the tenant. This setting is applied company-wide for all domains in the tenant. If you set that parameter to $false, no email-verified user can join the tenant.
- `allowedToSignUpEmailBasedSubscriptions` controls the ability for users to perform self-service sign-up. If you set that parameter to $false, no user can perform self-service sign-up.

`allowEmailVerifiedUsersToJoinOrganization` and `allowedToSignUpEmailBasedSubscriptions` are tenant-wide settings that can be applied to a managed or unmanaged tenant. Here's an example where:

- You administer a tenant with a verified domain such as contoso.com.
- You use B2B collaboration from a different tenant to invite a user that doesn't already exist (userdoesnotexist@contoso.com) in the home tenant of contoso.com.
- The home tenant has the `allowedToSignUpEmailBasedSubscriptions` turned on.

If the preceding conditions are true, then a member user is created in the home tenant, and a B2B guest user is created in the inviting tenant.

Note

Office 365 for Education users are currently the only ones who are added to existing managed tenants even when this toggle is enabled

For more information on Flow and Power Apps trial sign-ups, see the following articles:

- [How can I prevent my existing users from starting to use Power BI?](https://support.office.com/article/Power-BI-in-your-Organization-d7941332-8aec-4e5e-87e8-92073ce73dc5#bkmk_preventjoining)
- [Flow in your organization Q&A](/en-us/power-automate/organization-q-and-a)

### How do the controls work together?

These two parameters can be used in conjunction to define more precise control over self-service sign-up. For example, the following command allows users to perform self-service sign-up, but only if those users already have an account in Microsoft Entra ID (in other words, users who would need an email-verified account to be created first can't perform self-service sign-up):

```powershell
Import-Module Microsoft.Graph.Identity.SignIns
connect-MgGraph -Scopes "Policy.ReadWrite.Authorization"
$param = @{
 allowedToSignUpEmailBasedSubscriptions=$true
 allowEmailVerifiedUsersToJoinOrganization=$false
 }
Update-MgPolicyAuthorizationPolicy -BodyParameter $param
```

The following flowchart explains the different combinations for these parameters and the resulting conditions for the tenant and self-service sign-up.

![flowchart of self-service sign up controls.](media/directory-self-service-signup/selfservicesignupcontrols.png)

You can retrieve this setting's details using the PowerShell cmdlet `Get-MgPolicyAuthorizationPolicy`. For more information, see [Get-MgPolicyAuthorizationPolicy](/en-us/powershell/module/microsoft.graph.identity.signins/get-mgpolicyauthorizationpolicy).

```powershell
Get-MgPolicyAuthorizationPolicy | Select-Object AllowedToSignUpEmailBasedSubscriptions, AllowEmailVerifiedUsersToJoinOrganization
```

For more information and examples of how to use these parameters, see [Update-MgPolicyAuthorizationPolicy](/en-us/powershell/module/microsoft.graph.identity.signins/update-mgpolicyauthorizationpolicy?view=graph-powershell-1.0&amp;preserve-view=true).