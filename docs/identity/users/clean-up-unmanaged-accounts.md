---
layout: Conceptual
title: Clean up unmanaged Microsoft Entra accounts - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/clean-up-unmanaged-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Clean up unmanaged accounts using email one-time password and PowerShell modules in Microsoft Entra ID
ms.date: 2023-05-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro
locale: en-us
document_id: 657eb385-653c-09f5-1680-fc83e7e5e25e
document_version_independent_id: 32231ba2-23ee-e4c2-6ce4-eaf80f7d8ffe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/clean-up-unmanaged-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/clean-up-unmanaged-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/clean-up-unmanaged-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 942252ec-41e3-b5fe-e267-b665aede1248
---

# Clean up unmanaged Microsoft Entra accounts - Microsoft Entra ID | Microsoft Learn

## Overview

Prior to August 2022, Microsoft Entra B2B supported self-service sign-up for email-verified users. With this feature, users create Microsoft Entra accounts, when they verify email ownership. These accounts were created in unmanaged (or viral) tenants: users created accounts with an organization domain, not under IT team management. Access persists after users leave the organization.

To learn more, see [What is self-service sign-up for Microsoft Entra ID?](directory-self-service-signup).

Note

Unmanaged Microsoft Entra accounts via Microsoft Entra B2B were deprecated. As of August 2022, new B2B invitations can't be redeemed. However, invitations prior to August 2022 were redeemable with unmanaged Microsoft Entra accounts.

## Remove unmanaged Microsoft Entra accounts

Use the following guidance to remove unmanaged Microsoft Entra accounts from Microsoft Entra tenants. Tool features help identify viral users in the Microsoft Entra tenant. You can reset the user redemption status.

- Use the sample application in [Azure-samples/Remove-unmanaged-guests](https://github.com/Azure-Samples/Remove-Unmanaged-Guests).
- Use PowerShell cmdlets in [`MSIdentityTools`](https://github.com/AzureAD/MSIdentityTools/wiki/).

### Redeem invitations

After you run a tool, users with unmanaged Microsoft Entra accounts access the tenant, and re-redeem their invitations. However, Microsoft Entra ID prevents users from redeeming with an unmanaged Microsoft Entra account. They can redeem with another account type. Google Federation and SAML/WS-Federation aren't enabled by default. Therefore, users redeem with a Microsoft account (MSA) or email one-time password (OTP). MSA is recommended.

For more information, see [Invitation redemption flow](../../external-id/redemption-experience#invitation-redemption-flow).

## Overtaken tenants and domains

It's possible to convert some unmanaged tenants to managed tenants.

For more information, see [Take over an unmanaged directory as administrator in Microsoft Entra ID](domains-admin-takeover).

Some overtaken domains might not be updated. For example, a missing DNS TXT record indicates an unmanaged state. Implications are:

- For guest users from unmanaged tenants, redemption status is reset. A consent prompt appears.
    - Redemption occurs with the same account.
- The tool might identify unmanaged users as false positives after you reset unmanaged user redemption status.

## Reset redemption with a sample application

Use the sample application on [Azure-Samples/Remove-Unmanaged-Guests](https://github.com/Azure-Samples/Remove-Unmanaged-Guests).

## Reset redemption using `MSIdentityTools` PowerShell module

The `MSIdentityTools` PowerShell module is a collection of cmdlets and scripts, which you use in the Microsoft identity platform and Microsoft Entra ID. Use the cmdlets and scripts to augment PowerShell SDK capabilities. See [microsoftgraph/msgraph-sdk-powershell](https://github.com/microsoftgraph/msgraph-sdk-powershell).

Run the following cmdlets:

- `Install-Module Microsoft.Graph -Scope CurrentUser`
- `Install-Module MSIdentityTools`
- `Import-Module msidentitytools,microsoft.graph`

To identify unmanaged Microsoft Entra accounts, run:

- `Connect-MgGraph -Scope User.Read.All`
- `Get-MsIdUnmanagedExternalUser`

To reset unmanaged Microsoft Entra account redemption status, run:

- `Connect-MgGraph -Scopes User.ReadWriteAll`
- `Get-MsIdUnmanagedExternalUser | Reset-MsIdExternalUser`

To delete unmanaged Microsoft Entra accounts, run:

- `Connect-MgGraph -Scopes User.ReadWriteAll`
- `Get-MsIdUnmanagedExternalUser | Remove-MgUser`

## Resource

The following tool returns a list of external unmanaged users, or viral users, in the tenant.  See [Get-MSIdUnmanagedExternalUser](https://github.com/AzureAD/MSIdentityTools/wiki/Get-MsIdUnmanagedExternalUser).