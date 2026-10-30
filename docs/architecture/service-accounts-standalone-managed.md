---
layout: Conceptual
title: Secure standalone managed service accounts - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/service-accounts-standalone-managed
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn when to use, how to assess, and to secure standalone managed service accounts (sMSAs)
ms.topic: concept-article
ms.date: 2023-02-08T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: b05be319-b505-e269-72aa-5223dfc59bf4
document_version_independent_id: 77601032-bc8d-2cca-9213-58e1a93d7d4d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/service-accounts-standalone-managed.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/service-accounts-standalone-managed
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/service-accounts-standalone-managed.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 13dea504-d8b2-485c-d907-e74b8efcb258
---

# Secure standalone managed service accounts - Microsoft Entra | Microsoft Learn

Standalone managed service accounts (sMSAs) are managed domain accounts that help secure services running on a server. They can't be reused across multiple servers. sMSAs have automatic password management, simplified service principal name (SPN) management, and delegated management to administrators.

In Active Directory (AD), sMSAs are tied to a server that runs a service. You can find accounts in the Active Directory Users and Computers snap-in in Microsoft Management Console.

Note

Managed service accounts were introduced in Windows Server 2008 R2 Active Directory Schema, and they require Windows Server 2008 R2, or a later version.

## sMSA benefits

sMSAs have greater security than user accounts used as service accounts. They help reduce administrative overhead:

- Set strong passwords - sMSAs use 240 byte, randomly generated complex passwords
    - The complexity minimizes the likelihood of compromise by brute force or dictionary attacks
- Cycle passwords regularly - Windows changes the sMSA password every 30 days.
    - Service and domain administrators don’t need to schedule password changes or manage the associated downtime
- Simplify SPN management - SPNs are updated if the domain functional level is Windows Server 2008 R2. The SPN is updated when you:
    - Rename the host computer account
    - Change the host computer domain name server (DNS) name
    - Use PowerShell to add or remove other sam-accountname or dns-hostname parameters
    - See, [Set-ADServiceAccount](/en-us/powershell/module/activedirectory/set-adserviceaccount)

## Using sMSAs

Use sMSAs to simplify management and security tasks. sMSAs are useful when services are deployed to a server and you can't use a group managed service account (gMSA).

Note

You can use sMSAs for more than one service, but it's recommended that each service has an identity for auditing.

If the software creator can’t tell you if the application uses an MSA, test the application. Create a test environment and ensure it accesses required resources.

Learn more: [Managed Service Accounts: Understanding, Implementing, Best Practices, and Troubleshooting](/en-us/archive/blogs/askds/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting)

### Assess sMSA security posture

Consider the sMSA scope of access as part of the security posture. To mitigate potential security issues, see the following table:

| Security issue | Mitigation |
| --- | --- |
| sMSA is a member of privileged groups | - Remove the sMSA from elevated privileged groups, such as Domain Admins - Use the least-privileged model  - Grant the sMSA rights and permissions to run its services - If you're unsure about permissions, consult the service creator |
| sMSA has read/write access to sensitive resources | - Audit access to sensitive resources - Archive audit logs to a security information and event management (SIEM) program, such as Azure Log Analytics or Microsoft Sentinel  - Remediate resource permissions if an undesirable access is detected |
| By default, the sMSA password rollover frequency is 30 days | Use group policy to tune the duration, depending on enterprise security requirements. To set the password expiration duration, go to:Computer Configuration&gt;Policies&gt;Windows Settings&gt;Security Settings&gt;Security Options. For domain member, use **Maximum machine account password age**. |

### sMSA challenges

Use the following table to associate challenges with mitigations.

| Challenge | Mitigation |
| --- | --- |
| sMSAs are on a single server | Use a gMSA to use the account across servers |
| sMSAs can't be used across domains | Use a gMSA to use the account across domains |
| Not all applications support sMSAs | Use a gMSA, if possible. Otherwise, use a standard user account or a computer account, as recommended by the creator |

## Find sMSAs

On a domain controller, run DSA.msc, and then expand the managed service accounts container to view all sMSAs.

To return all sMSAs and gMSAs in the Active Directory domain, run the following PowerShell command:

`Get-ADServiceAccount -Filter *`

To return sMSAs in the Active Directory domain, run the following command:

`Get-ADServiceAccount -Filter * | where { $_.objectClass -eq "msDS-ManagedServiceAccount" }`

## Manage sMSAs

To manage your sMSAs, you can use the following AD PowerShell cmdlets:

`Get-ADServiceAccount``Install-ADServiceAccount``New-ADServiceAccount``Remove-ADServiceAccount``Set-ADServiceAccount``Test-ADServiceAccount``Uninstall-ADServiceAccount`

## Move to sMSAs

If an application service supports sMSAs, but not gMSAs, and you're using a user account or computer account for the security context, see[Managed Service Accounts: Understanding, Implementing, Best Practices, and Troubleshooting](/en-us/archive/blogs/askds/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting).

If possible, move resources to Azure and use Azure managed identities, or service principals.