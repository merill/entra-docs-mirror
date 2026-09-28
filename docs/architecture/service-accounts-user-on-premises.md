---
layout: Conceptual
title: Secure user-based service accounts in Active Directory - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/service-accounts-user-on-premises
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn how to locate, assess, and mitigate security issues for user-based service accounts
ms.topic: how-to
ms.date: 2023-02-09T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 5e81a15f-3dc0-4e7e-2395-dcb3a9033414
document_version_independent_id: 9d9fb864-d27c-8dab-bc11-3dcdacb03d95
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/service-accounts-user-on-premises.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/service-accounts-user-on-premises
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/service-accounts-user-on-premises.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: b1207767-ac43-91d4-f1f2-50a0db2da8e2
---

# Secure user-based service accounts in Active Directory - Microsoft Entra | Microsoft Learn

On-premises user accounts were the traditional approach to help secure services running on Windows. Today, use these accounts if group managed service accounts (gMSAs) and standalone managed service accounts (sMSAs) aren't supported by your service. For information about the account type to use, see [Securing on-premises service accounts](service-accounts-on-premises).

You can investigate moving your service an Azure service account, such as a managed identity or a service principal.

Learn more:

- [What are managed identities for Azure resources?](../identity/managed-identities-azure-resources/overview)
- [Securing service principals in Microsoft Entra ID](service-accounts-principal)

You can create on-premises user accounts to provide security for services and permissions the accounts use to access local and network resources. On-premises user accounts require manual password management, like other Active Directory (AD) user accounts. Service and domain administrators are required to maintain strong password management processes to help keep accounts secure.

When you create a user account as a service account, use it for one service. Use a naming convention that clarifies it's a service account, and the service it's related to.

## Benefits and challenges

On-premises user accounts are a versatile account type. User accounts used as service accounts are controlled by policies governing user accounts. Use them if you can't use an MSA. Evaluate whether a computer account is a better option.

The challenges of on-premises user accounts are summarized in the following table:

| Challenge | Mitigation |
| --- | --- |
| Password management is manual and leads to weaker security and service downtime | - Ensure regular password complexity and that changes are governed by a process that maintains strong passwords - Coordinate password changes with a service password, which helps reduce service downtime |
| Identifying on-premises user accounts that are service accounts can be difficult | - Document service accounts deployed in your environment - Track the account name and the resources they can access - Consider adding the prefix svc to user accounts used as service accounts |

## Find on-premises user accounts used as service accounts

On-premises user accounts are like other AD user accounts. It can be difficult to find the accounts, because no user account attribute identifies it as a service account. We recommend you create a naming convention for user accounts uses as service accounts. For example, add the prefix svc to a service name: svc-HRDataConnector.

Use some of the following criteria to find service accounts. However, this approach might not find accounts:

- Trusted for delegation
- With service principal names
- With passwords that never expire

To find the on-premises user accounts used for services, run the following PowerShell commands:

To find accounts trusted for delegation:

```PowerShell

Get-ADObject -Filter {(msDS-AllowedToDelegateTo -like '*') -or (UserAccountControl -band 0x0080000) -or (UserAccountControl -band 0x1000000)} -prop samAccountName,msDS-AllowedToDelegateTo,servicePrincipalName,userAccountControl | select DistinguishedName,ObjectClass,samAccountName,servicePrincipalName, @{name='DelegationStatus';expression={if($_.UserAccountControl -band 0x80000){'AllServices'}else{'SpecificServices'}}}, @{name='AllowedProtocols';expression={if($_.UserAccountControl -band 0x1000000){'Any'}else{'Kerberos'}}}, @{name='DestinationServices';expression={$_.'msDS-AllowedToDelegateTo'}}

```

To find accounts with service principal names:

```PowerShell

Get-ADUser -Filter * -Properties servicePrincipalName | where {$_.servicePrincipalName -ne $null}

```

To find accounts with passwords that never expire:

```PowerShell

Get-ADUser -Filter * -Properties PasswordNeverExpires | where {$_.PasswordNeverExpires -eq $true}

```

You can audit access to sensitive resources, and archive audit logs to a security information and event management (SIEM) system. By using Azure Log Analytics or Microsoft Sentinel, you can search for and analyze service accounts.

## Assess on-premises user account security

Use the following criteria to assess the security of on-premises user accounts used as service accounts:

- Password management policy
- Accounts with membership in privileged groups
- Read/write permissions for important resources

### Mitigate potential security issues

See the following table for potential on-premises user account security issues and their mitigations:

| Security issue | Mitigation |
| --- | --- |
| Password management | - Ensure password complexity and password change are governed by regular updates and strong password requirements - Coordinate password changes with a password update to minimize service downtime |
| The account is a member of privileged groups | - Review group membership - Remove the account from privileged groups - Grant the account rights and permissions to run its service (consult with service vendor) - For example, deny sign-in locally or interactive sign-in |
| The account has read/write permissions to sensitive resources | - Audit access to sensitive resources - Archive audit logs to a SIEM: Azure Log Analytics or Microsoft Sentinel - Remediate resource permissions if you detect undesirable access levels |

## Secure account types

Microsoft doesn't recommend use of on-premises user accounts as service accounts. For services that use this account type, assess if it can be configured to use a gMSA or an sMSA. In addition, evaluate if you can move the service to Azure to enable use of safer account types.