---
layout: Conceptual
title: Troubleshoot sign in problems in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/troubleshoot-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot common user sign-in problems and errors in Microsoft Entra Domain Services.
ms.topic: troubleshooting
ms.date: 2025-02-19T00:00:00.0000000Z
locale: en-us
document_id: 18703d9f-a884-0eb1-fa9a-62986bfaec91
document_version_independent_id: 89c7c6ff-ef1b-07e8-8b89-4e32d807ee7a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/troubleshoot-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/troubleshoot-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/troubleshoot-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3c5b1c03-3ddd-f0c0-56b5-655246b01c2e
---

# Troubleshoot sign in problems in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

The most common reasons for a user account that can't sign in to a Microsoft Entra Domain Services managed domain include the following scenarios:

- The account isn't synchronized into Domain Services yet.
- Domain Services doesn't have the password hashes to let the account sign in.
- The account is locked out.

Tip

Domain Services can't synchronize in credentials for accounts that are external to the Microsoft Entra tenant. External users can't sign in to the Domain Services managed domain.

## Account isn't synchronized into Domain Services yet

Depending on the size of your directory, it may take a while for user accounts and credential hashes to be available in a managed domain. For large directories, this initial one-way sync from Microsoft Entra ID can take few hours, and up to a day or two. Make sure that you wait long enough before retrying authentication.

For hybrid environments that user Microsoft Entra Connect to synchronize on-premises directory data into Microsoft Entra ID, make sure that you run the latest version of Microsoft Entra Connect and have [configured Microsoft Entra Connect to perform a full synchronization after enabling Domain Services](tutorial-configure-password-hash-sync). If you disable Domain Services and then re-enable, you have to follow these steps again.

If you continue to have issues with accounts not synchronizing through Microsoft Entra Connect, restart the Azure AD Sync Service. From the computer with Microsoft Entra Connect installed, open a command prompt window, then run the following commands:

```console
net stop 'Microsoft Azure AD Sync'
net start 'Microsoft Azure AD Sync'
```

## Domain Services doesn't have the password hashes

Microsoft Entra ID doesn't generate or store password hashes in the format that's required for NTLM or Kerberos authentication until you enable Domain Services for your tenant. For security reasons, Microsoft Entra ID also doesn't store any password credentials in clear-text form. Therefore, Microsoft Entra ID can't automatically generate these NTLM or Kerberos password hashes based on users' existing credentials.

### Hybrid environments with on-premises synchronization

For hybrid environments using Microsoft Entra Connect to synchronize from an on-premises AD DS environment, you can locally generate and synchronize the required NTLM or Kerberos password hashes into Microsoft Entra ID. After you create your managed domain, [enable password hash synchronization to Microsoft Entra Domain Services](tutorial-configure-password-hash-sync). Without completing this password hash synchronization step, you can't sign in to an account using the managed domain. If you disable Domain Services and then re-enable, you have to follow those steps again.

For more information, see [How password hash synchronization works for Domain Services](/en-us/azure/active-directory/hybrid/connect/how-to-connect-password-hash-synchronization#password-hash-sync-process-for-azure-ad-domain-services).

### Cloud-only environments with no on-premises synchronization

Managed domains with no on-premises synchronization, only accounts in Microsoft Entra ID, also need to generate the required NTLM or Kerberos password hashes. If a cloud-only account can't sign in, has a password change process successfully completed for the account after enabling Domain Services?

- **No, the password has not been changed.**
    - [Change the password for the account](tutorial-create-instance#enable-user-accounts-for-azure-ad-ds) to generate the required password hashes, then wait for 15 minutes before you try to sign in again.
    - If you disable Domain Services and then re-enable, each account must follow the steps again to change their password and generate the required password hashes.
- **Yes, the password has been changed.**
    - Try to sign in using the *UPN* format, such as `driley@aaddscontoso.com`, instead of the *SAMAccountName* format like `AADDSCONTOSO\deeriley`.
    - The *SAMAccountName* may be automatically generated for users whose UPN prefix is overly long or is the same as another user on the managed domain. The *UPN* format is guaranteed to be unique within a Microsoft Entra tenant.

## The account is locked out

A user account in a managed domain is locked out when a defined threshold for unsuccessful sign-in attempts has been met. This account lockout behavior is designed to protect you from repeated brute-force sign-in attempts that may indicate an automated digital attack.

By default, if there are 5 bad password attempts in 2 minutes, the account is locked out for 30 minutes.

For more information and how to resolve account lockout issues, see [Troubleshoot account lockout problems in Domain Services](troubleshoot-account-lockout).