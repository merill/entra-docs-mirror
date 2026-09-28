---
layout: Conceptual
title: SAM Account Name - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/security-account-name
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: BenMannMicrosoft2
ms.author: benmann
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: SAM Account Name support for Entra Domain Services
ms.topic: concept-article
ms.date: 2026-08-18T00:00:00.0000000Z
locale: en-us
document_id: 583b6467-611f-b16d-b657-e65072a32cf5
document_version_independent_id: 583b6467-611f-b16d-b657-e65072a32cf5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/security-account-name.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/security-account-name
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/security-account-name.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 189ebd9a-b1ac-c9fe-e400-025f9209bc1f
---

# SAM Account Name - Microsoft Entra ID | Microsoft Learn

Enhanced support for synchronizing the security account manager account name (sAMAccountName) with Microsoft Entra Domain Services is now in public preview.

This feature allows sAMAccountName to be populated from the onPremisesSamAccountName attribute in Microsoft Entra ID. Existing managed domains can enable the new synchronization behavior. The feature needs to be enabled.

When enabled, existing hybrid users are updated during synchronization; cloud-only users without an onPremisesSamAccountName value continue to use mailNickname-based generation.

## When is sAMAccountName sync needed?

The security account manager account name (sAMAccountName) attribute stores a user’s legacy logon name in Active Directory Domain Services and is now supported through enhanced synchronization in public preview for Microsoft Entra Domain Services. Applications that use legacy authentication commonly expect this value to be unique, no longer than 20 characters, and free of unsupported special characters. 

Enhanced sAMAccountName synchronization allows organizations with hybrid identities to populate sAMAccountName from onPremisesSamAccountName in Microsoft Entra ID. This helps preserve account-name consistency with on-premises Active Directory and improves compatibility with applications and scripts that depend on existing sAMAccountName values. 

### Prerequisites

- A Microsoft Entra Domain Services managed domain.
- An Enterprise or Premium SKU. The feature is not available with the Standard SKU.
- Users synchronized from on-premises Active Directory must have onPremisesSamAccountName populated in Microsoft Entra ID.
- To change the setting, the administrator must have both the Application Administrator and Groups Administrator roles.

### How sAMAccountName synchronization works

#### Existing managed domains

Existing managed domains continue to use the current behavior until an administrator enables sAMAccountName synchronization from on-premises. 

- **Setting disabled**: Microsoft Entra Domain Services generates sAMAccountName from mailNickname or the user principal name prefix. Truncation and de-duplication are applied when needed to meet legacy constraints.
- **Setting enabled**: Microsoft Entra Domain Services sources sAMAccountName from onPremisesSamAccountName in Microsoft Entra ID for hybrid users. Existing hybrid users are updated during synchronization.

Cloud-only users without an onPremisesSamAccountName value continue to use mailNickname-based sAMAccountName generation. 

#### New managed domains

For new managed domain deployments, enhanced synchronization is enabled by default. The sAMAccountName value for hybrid users is sourced from onPremisesSamAccountName in Microsoft Entra ID. For new domain deployments, samaccountName will need to be enabled, by default it is disabled.

### When to use enhanced synchronization

Consider enabling enhanced synchronization when your organization: 

- Uses hybrid identities and requires the same sAMAccountName values across on-premises Active Directory and Microsoft Entra Domain Services.
- Runs applications, scripts, or authentication workflows that depend on specific sAMAccountName values.
- Is migrating domain-dependent workloads to Azure and wants to preserve existing identity formats.
- Experiences authentication or application errors caused by generated, truncated, duplicated, or mismatched account names.

### Benefits

- **Improved application compatibility:** Applications can continue using established sAMAccountName values without identity-related code changes.
- **Reduced identity drift:** Account names remain consistent across on-premises and managed-domain environments.
- **Simplified migrations:** Existing identity formats can be preserved as workloads move to Azure.
- **Fewer authentication issues:** Administrators can avoid mismatches caused by generating sAMAccountName from mailNickname or the user principal name prefix.

### Before you enable the setting

Enabling the setting changes the sAMAccountName source for existing hybrid users.

Before enabling it: 

- Confirm that onPremisesSamAccountName is populated correctly in Microsoft Entra ID.
- Review applications, scripts, scheduled tasks, and access-control configurations that use sAMAccountName.
- Identify integrations that might depend on the currently generated sAMAccountName value.
- Plan to validate authentication and application access after synchronization completes.

Enable sAMAccountName synchronization from on-premises 

1. Sign in to the Microsoft Entra admin center with an account assigned to both the Application Administrator and Groups Administrator roles.
2. Search for and select Microsoft Entra Domain Services.
3. Select your managed domain.
4. In the left navigation, select Security settings.
5. For sAMAccountName synchronization from on-premises, select Enable.
6. Save the change.

After the setting is enabled, Microsoft Entra Domain Services synchronizes sAMAccountName from onPremisesSamAccountName for existing hybrid users. Cloud-only users without that source attribute continue to use the existing generated behavior. 

### Validate the configuration

1. Select representative hybrid users whose onPremisesSamAccountName values are known.
2. Confirm that their sAMAccountName values in Microsoft Entra Domain Services match the source values in Microsoft Entra ID.
3. Test authentication for applications and scripts that depend on sAMAccountName.

If a user doesn’t receive the expected value, confirm that onPremisesSamAccountName is populated in Microsoft Entra ID and verify that the enhanced synchronization setting is enabled. Enhanced support for synchronizing the Security Account Manager account name (sAMAccountName) with Microsoft Entra Domain Services is now in Public Preview.

This feature allows sAMAccountName to be populated from the onPremisesSamAccountName attribute in Microsoft Entra ID. Existing managed domains can enable the new synchronization behavior, while it is enabled by default for new managed domains.

When enabled, existing hybrid users are updated during synchronization; cloud-only users without an onPremisesSamAccountName value continue to use mailNickname-based generation.

## Security accounts manager account name

The security accounts manager account name (sAMAccountName) attribute stores a user’s legacy logon name in Active Directory Domain Services and is now supported through enhanced synchronization in Public Preview for Microsoft Entra Domain Services. Applications that use legacy authentication commonly expect this value to be unique, no longer than 20 characters, and free of unsupported special characters. 

Enhanced sAMAccountName synchronization allows organizations with hybrid identities to populate sAMAccountName from onPremisesSamAccountName in Microsoft Entra ID. This helps preserve account-name consistency with on-premises Active Directory and improves compatibility with applications and scripts that depend on existing sAMAccountName values. 

### Prerequisites

- A Microsoft Entra Domain Services managed domain.
- An Enterprise or Premium SKU. The feature isn’t available with the Standard SKU.
- Users synchronized from on-premises Active Directory must have onPremisesSamAccountName populated in Microsoft Entra ID.
- To change the setting, the administrator must have both the Application Administrator and Groups Administrator roles.

### How sAMAccountName synchronization works

#### Existing managed domains

Existing managed domains continue to use the current behavior until an administrator enables sAMAccountName synchronization from on-premises. 

- **Setting disabled**: Microsoft Entra Domain Services generates sAMAccountName from mailNickname or the user principal name prefix. Truncation and de-duplication are applied when needed to meet legacy constraints.
- **Setting enabled**: Microsoft Entra Domain Services sources sAMAccountName from onPremisesSamAccountName in Microsoft Entra ID for hybrid users. Existing hybrid users are updated during synchronization.

Cloud-only users without an onPremisesSamAccountName value continue to use mailNickname-based sAMAccountName generation. 

#### New managed domains

For new managed domain deployments, enhanced synchronization is enabled by default. The sAMAccountName value for hybrid users is sourced from onPremisesSamAccountName in Microsoft Entra ID, and this behavior can’t be changed. 

### When to use enhanced synchronization

Consider enabling enhanced synchronization when your organization: 

- Uses hybrid identities and requires the same sAMAccountName values across on-premises Active Directory and Microsoft Entra Domain Services.
- Runs applications, scripts, or authentication workflows that depend on specific sAMAccountName values.
- Is migrating domain-dependent workloads to Azure and wants to preserve existing identity formats.
- Experiences authentication or application errors caused by generated, truncated, duplicated, or mismatched account names.

### Benefits

- **Improved application compatibility:** Applications can continue using established sAMAccountName values without identity-related code changes.
- **Reduced identity drift:** Account names remain consistent across on-premises and managed-domain environments.
- **Simplified migrations:** Existing identity formats can be preserved as workloads move to Azure.
- **Fewer authentication issues:** Administrators can avoid mismatches caused by generating sAMAccountName from mailNickname or the user principal name prefix.

### Before you enable the setting

Enabling the setting changes the sAMAccountName source for existing hybrid users.

Before enabling it: 

- Confirm that onPremisesSamAccountName is populated correctly in Microsoft Entra ID.
- Review applications, scripts, scheduled tasks, and access-control configurations that use sAMAccountName.
- Identify integrations that might depend on the currently generated sAMAccountName value.
- Plan to validate authentication and application access after synchronization completes.

Enable sAMAccountName synchronization from on-premises 

1. Sign in to the Microsoft Entra admin center with an account assigned to both the Application Administrator and Groups Administrator roles.
2. Search for and select Microsoft Entra Domain Services.
3. Select your managed domain.
4. In the left navigation, select Security settings.
5. For sAMAccountName synchronization from on-premises, select Enable.
6. Save the change.

After the setting is enabled, Microsoft Entra Domain Services synchronizes sAMAccountName from onPremisesSamAccountName for existing hybrid users. Cloud-only users without that source attribute continue to use the existing generated behavior. 

### Validate the configuration

1. Select representative hybrid users whose onPremisesSamAccountName values are known.
2. Confirm that their sAMAccountName values in Microsoft Entra Domain Services match the source values in Microsoft Entra ID.
3. Test authentication for applications and scripts that depend on sAMAccountName.
4. If a user doesn’t receive the expected value, confirm that onPremisesSamAccountName is populated in Microsoft Entra ID and verify that the enhanced synchronization setting is enabled.