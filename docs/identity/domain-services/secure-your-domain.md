---
layout: Conceptual
title: Secure Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/secure-your-domain
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to disable weak ciphers, old protocols, and NTLM password hash synchronization for a Microsoft Entra Domain Services managed domain.
ms.assetid: 6b4665b5-4324-42ab-82c5-d36c01192c2a
ms.topic: how-to
ms.date: 2025-03-14T00:00:00.0000000Z
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: 1ca07bf8-d285-e7ae-aaf1-a9292bbdf75c
document_version_independent_id: 7694cb10-8eb6-397d-2cbb-4e249556b88d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/secure-your-domain.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/secure-your-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/secure-your-domain.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c3d5b5d0-38ab-5dc0-7bbf-4f9b2d2b7ef1
---

# Secure Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

By default, Microsoft Entra Domain Services enables the use of ciphers such as NTLM v1 and TLS v1. These ciphers may be required for some legacy applications, but are considered weak and should be disabled if you don't need them. If you have on-premises hybrid connectivity using Microsoft Entra Connect, you can also disable the synchronization of NTLM password hashes.

This article shows you how to harden a managed domain by using settings such as:

- Disable NTLM v1 and TLS v1 ciphers
- Disable NTLM password hash synchronization
- Disable Kerberos RC4 encryption (on the pathway to deprecation)
- Enable Kerberos armoring
- LDAP signing
- LDAP channel binding

## Prerequisites

To complete this article, you need the following resources:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
    - You need [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) and [Groups Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#groups-administrator) Microsoft Entra roles in your tenant to modify security settings for a managed domain.
    - You need [Domain Services Contributor](/en-us/azure/role-based-access-control/built-in-roles#domain-services-contributor) Azure role to modify security settings for a managed domain.

## Use Security settings to harden your domain

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Entra Domain Services**.
3. Choose your managed domain, such as *aaddscontoso.com*.
4. On the left-hand side, select **Security settings**.
5. Click **Enable** or **Disable** for the following settings:

    - **TLS 1.2 Only Mode**
    - **NTLM v1 Authentication**
    - **NTLM Password Synchronization**
    - **Kerberos RC4 Encryption**
    - **Kerberos Armoring**
    - **LDAP Signing**
    - **LDAP Channel Binding**

    ![Screenshot of Security settings to disable weak ciphers and NTLM password hash sync](media/secure-your-domain/security-settings.png)

## Disable Kerberos RC4 encryption

RC4 encryption for Kerberos is on the pathway to deprecation. Windows security updates related to [CVE-2026-20833](https://www.cve.org/CVERecord?id=CVE-2026-20833) shift default Kerberos KDC behavior to AES-first and reduce RC4 usage in phases. Unless you have workloads, devices, or services that are explicitly dependent on RC4, you should disable RC4 from your managed domain's security settings.

### Deprecation timeline

| Phase | Date | Behavior |
| --- | --- | --- |
| Initial deployment | January 13, 2026 | Updates introduce audit signals and preparation controls. |
| Enforcement (manual rollback available) | April 2026 | Default Kerberos KDC behavior shifts to AES-first. RC4-dependent scenarios can start failing unless explicitly configured. |
| Enforcement (final) | July 2026 | Updates remove rollback support and keep enforcement enabled. |

For more details, see [How to manage Kerberos KDC usage of RC4 for service account ticket issuance changes related to CVE-2026-20833](https://support.microsoft.com/en-us/topic/how-to-manage-kerberos-kdc-usage-of-rc4-for-service-account-ticket-issuance-changes-related-to-cve-2026-20833-1ebcda33-720a-4da8-93c1-b0496e1910dc).

### Turn off RC4 in the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Entra Domain Services**.
3. Choose your managed domain, such as *aaddscontoso.com*.
4. On the left-hand side, select **Security settings**.
5. Set **Kerberos RC4 Encryption** to **Disabled**.
6. Select **Save**.

### Turn off RC4 with PowerShell

To disable RC4 using PowerShell, set the `KerberosRc4Encryption` property to `Disabled`:

```powershell
$securitySettings = @{"DomainSecuritySettings"=@{"KerberosRc4Encryption"="Disabled"}}
Set-AzResource -Id $DomainServicesResource.ResourceId -Properties $securitySettings -ApiVersion "2021-03-01" -Verbose -Force
```

Warning

Before you disable RC4, verify that no workloads, devices, or service accounts depend on RC4 encryption. You can identify RC4 dependencies by enabling [security audits](security-audit-events) and monitoring Kerberos ticket event IDs **4768** and **4769**. For workloads that temporarily require RC4, configure the affected service account **msDS-SupportedEncryptionTypes** value to include RC4 as documented in the [CVE-2026-20833 support article](https://support.microsoft.com/en-us/topic/how-to-manage-kerberos-kdc-usage-of-rc4-for-service-account-ticket-issuance-changes-related-to-cve-2026-20833-1ebcda33-720a-4da8-93c1-b0496e1910dc).

## Assign Azure Policy compliance for TLS 1.2 usage

In addition to **Security settings**, Microsoft Azure Policy has a **Compliance** setting to enforce TLS 1.2 usage. The policy has no impact until it is assigned. When the policy is assigned, it appears in **Compliance**:

- If the assignment is **Audit**, the compliance will report if the Domain Services instance is compliant.
- If the assignment is **Deny**, the compliance will prevent a Domain Services instance from being created if TLS 1.2 is not required and prevent any update to a Domain Services instance until TLS 1.2 is required.

![Screenshot of Compliance settings](media/secure-your-domain/policy-tls.png)

## Audit NTLM failures

While disabling NTLM password synchronization will improve security, many applications and services are not designed to work without it. For example, connecting to any resource by its IP address, such as DNS Server management or RDP, will fail with Access Denied. If you disable NTLM password synchronization and your application or service isn’t working as expected, you can check for NTLM authentication failures by enabling security auditing for the **Logon/Logoff** &gt; **Audit Logon** event category, where NTLM is specified as the **Authentication Package** in the event details. For more information, see [Enable security audits for Microsoft Entra Domain Services](security-audit-events).

## Use PowerShell to harden your domain

If needed, [install and configure Azure PowerShell](/en-us/powershell/azure/install-azure-powershell). Make sure that you sign in to your Azure subscription using the [Connect-AzAccount](/en-us/powershell/module/Az.Accounts/Connect-AzAccount) cmdlet.

Also if needed, [install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation). Make sure that you sign in to your Microsoft Entra tenant using the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph) cmdlet.

To disable weak cipher suites and NTLM credential hash synchronization, sign in to your Azure account, then get the Domain Services resource using the [Get-AzResource](/en-us/powershell/module/az.resources/get-azresource) cmdlet:

Tip

If you receive an error using the [Get-AzResource](/en-us/powershell/module/az.resources/get-azresource) command that the *Microsoft.AAD/DomainServices* resource doesn't exist, [elevate your access to manage all Azure subscriptions and management groups](/en-us/azure/role-based-access-control/elevate-access-global-admin).

```powershell
Login-AzAccount

$DomainServicesResource = Get-AzResource -ResourceType "Microsoft.AAD/DomainServices"
```

Next, define *DomainSecuritySettings* to configure the following security options:

1. Disable NTLM v1 support.
2. Disable the synchronization of NTLM password hashes from your on-premises AD.
3. Disable TLS v1.
4. Disable Kerberos RC4 Encryption.
5. Enable Kerberos Armoring.

Important

Users and service accounts can't perform LDAP simple binds if you disable NTLM password hash synchronization in the Domain Services managed domain. If you need to perform LDAP simple binds, don't set the *"SyncNtlmPasswords"="Disabled";* security configuration option in the following command.

```powershell
$securitySettings = @{"DomainSecuritySettings"=@{"NtlmV1"="Disabled";"SyncNtlmPasswords"="Disabled";"TlsV1"="Disabled";"KerberosRc4Encryption"="Disabled";"KerberosArmoring"="Enabled"}}
```

Finally, apply the defined security settings to the managed domain using the [Set-AzResource](/en-us/powershell/module/az.resources/set-azresource) cmdlet. Specify the Domain Services resource from the first step, and the security settings from the previous step.

```powershell
Set-AzResource -Id $DomainServicesResource.ResourceId -Properties $securitySettings -ApiVersion "2021-03-01" -Verbose -Force
```

It takes a few moments for the security settings to be applied to the managed domain.

Important

After you disable NTLM, perform a full password hash synchronization in Microsoft Entra Connect to remove all the password hashes from the managed domain. If you disable NTLM but don't force a password hash sync, NTLM password hashes for a user account are only removed on the next password change. This behavior could allow a user to continue to sign in if they have cached credentials on a system where NTLM is used as the authentication method.

Once the NTLM password hash is different from the Kerberos password hash, fallback to NTLM won't work. Cached credentials also no longer work if the VM has connectivity to the managed domain controller.