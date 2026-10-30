---
layout: Conceptual
title: Secure on-premises computer accounts with Active Directory - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/service-accounts-computer
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide to help secure on-premises computer accounts, or LocalSystem accounts, with Active Directory
ms.topic: how-to
ms.date: 2023-02-03T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 90b3660b-a58f-3ca4-cfbd-2e98c152912b
document_version_independent_id: dac305e8-8167-7eb6-2e27-6739df590ce8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/service-accounts-computer.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/service-accounts-computer
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/service-accounts-computer.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9bf4ec80-96fc-eade-72e1-89af8d5c97f5
---

# Secure on-premises computer accounts with Active Directory - Microsoft Entra | Microsoft Learn

A computer account, or LocalSystem account, is highly privileged with access to almost all resources on the local computer. The account isn't associated with signed-on user accounts. Services run as LocalSystem access network resources by presenting the computer credentials to remote servers in the format `<domain_name>\\<computer_name>$`. The computer account predefined name is `NT AUTHORITY\SYSTEM`. You can start a service and provide security context for that service.

![Screenshot of a list of local services on a computer account.](media/govern-service-accounts/secure-computer-accounts-image-1.png)

## Benefits of using a computer account

A computer account has the following benefits:

- **Unrestricted local access** - the computer account provides complete access to the machine's local resources
- **Automatic password management** - removes the need for manually changed passwords. The account is a member of Active Directory, and its password is changed automatically. With a computer account, there's no need to register the service principal name.
- **Limited access rights off-machine** - the default access-control list in Active Directory Domain Services (AD DS) permits minimal access to computer accounts. During access by an unauthorized user, the service has limited access to network resources.

## Computer account security-posture assessment

Use the following table to review potential computer-account issues and mitigations.

| Computer-account issue | Mitigation |
| --- | --- |
| Computer accounts are subject to deletion and re-creation when the computer leaves and rejoins the domain. | Confirm the requirement to add a computer to an Active Directory group. To verify computer accounts added to a group, use the scripts in the following section. |
| If you add a computer account to a group, services that run as LocalSystem on that computer get group access rights. | Be selective about computer-account group memberships. Don't make a computer account a member of a domain administrator group. The associated service has complete access to AD DS. |
| Inaccurate network defaults for LocalSystem. | Don't assume the computer account has the default limited access to network resources. Instead, confirm group memberships for the account. |
| Unknown services that run as LocalSystem. | Ensure services that run under the LocalSystem account are Microsoft services, or trusted services. |

## Find services and computer accounts

To find services that run under the computer account, use the following PowerShell cmdlet:

```powershell
Get-WmiObject win32_service | select Name, StartName | Where-Object {($_.StartName -eq "LocalSystem")}
```

To find computer accounts that are members of a specific group, run the following PowerShell cmdlet:

```powershell
Get-ADComputer -Filter {Name -Like "*"} -Properties MemberOf | Where-Object {[STRING]$_.MemberOf -like "Your_Group_Name_here*"} | Select Name, MemberOf
```

To find computer accounts that are members of identity administrators groups (domain administrators, enterprise administrators, and administrators), run the following PowerShell cmdlet:

```powershell
Get-ADGroupMember -Identity Administrators -Recursive | Where objectClass -eq "computer"
```

## Computer account recommendations

Important

Computer accounts are highly privileged, therefore use them if your service requires unrestricted access to local resources, on the machine, and you can't use a managed service account (MSA).

- Confirm the service owner's service runs with an MSA
- Use a group managed service account (gMSA), or a standalone managed service account (sMSA), if your service supports it
- Use a domain user account with the permissions needed to run the service