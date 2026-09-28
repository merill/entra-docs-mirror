---
layout: Conceptual
title: Rotate the Kerberos server key for Microsoft Entra Kerberos - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/kerberos-server-key-rotation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: pmwongera
description: Learn how to rotate the Microsoft Entra Kerberos server key to maintain security and align with best practices in hybrid identity environments.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: Vimala, vimrang, barclayn
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: 70563b0d-fd3c-914c-505a-2d5a847835e8
document_version_independent_id: 70563b0d-fd3c-914c-505a-2d5a847835e8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/kerberos-server-key-rotation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/kerberos-server-key-rotation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/kerberos-server-key-rotation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: a6b05c6c-9726-49b5-ac33-84fa1680f1bb
---

# Rotate the Kerberos server key for Microsoft Entra Kerberos - Microsoft Entra ID | Microsoft Learn

In hybrid identity environments, Microsoft Entra Kerberos uses a shared Kerberos server key between on-premises Active Directory Domain Services (AD DS) and Microsoft Entra ID. This key encrypts and protects Ticket Granting Tickets (TGTs) issued by Microsoft Entra ID. This article shows you how to rotate the key to maintain security and align with Active Directory best practices.

The key is stored on a dedicated Microsoft Entra Kerberos server object in on-premises Active Directory and securely published to Microsoft Entra ID. This object is logical, not a physical server, and functions like a read-only domain controller (RODC) for Kerberos trust.

## Prerequisites

- The `AzureADHybridAuthenticationManagement` PowerShell module installed.
- Domain admin or equivalent credentials for on-premises AD DS.
- Cloud admin credentials for Microsoft Entra ID.
- A Microsoft Entra Kerberos server object already configured in on-premises Active Directory.

## Understand why key rotation matters

Regular rotation of the Kerberos server key helps:

- Limit the lifetime of cryptographic material.
- Reduce risk if a key is compromised.
- Align with standard Kerberos and Active Directory security practices.

Microsoft recommends rotating the Microsoft Entra Kerberos server key on the same schedule you use for other Active Directory Kerberos (`krbtgt`) keys.

## How key rotation works

Microsoft Entra Kerberos uses a dual-key model to avoid service disruption during rotation:

- **Primary key**: Used for all newly issued Kerberos tickets.
- **Secondary key**: Retains the previous key to validate existing tickets until they naturally expire.

When you rotate the key, the new key becomes the primary key, and the previous primary key is retained as the secondary key. Microsoft Entra ID validates Kerberos tickets by using the primary key while continuing to honor tickets protected by the secondary key. This process doesn't interrupt user access.

## Rotate the Kerberos server key

Use the `Set-AzureADKerberosServer` cmdlet to rotate the key. This command:

- Generates a new Kerberos server key.
- Stores the key on the on-premises Active Directory Kerberos server object.
- Securely publishes the key to Microsoft Entra ID.
- Updates the key version in both environments.

```powershell
Set-AzureADKerberosServer -Domain $domain -CloudCredential $cloudCred -DomainCredential $domainCred -RotateServerKey
```

Warning

There are other tools that could rotate the `krbtgt` keys. However, you must use the `Set-AzureADKerberosServer` cmdlet to rotate the `krbtgt` keys of your Microsoft Entra Kerberos server. This ensures that the keys are updated in both on-premises Active Directory and Microsoft Entra ID.

Important

To fully retire older keys, perform the rotation twice, ensuring that both the original primary and secondary keys have expired.

### Use the -Force parameter

Using `-Force` with `Set-AzureADKerberosServer` allows the command to apply or update Kerberos server configuration without confirmation prompts. This flag ensures consistent, nondisruptive execution while maintaining full security controls.

```powershell
Set-AzureADKerberosServer -Domain $domain -CloudCredential $cloudCred -DomainCredential $domainCred -RotateServerKey -Force
```

Typically, `-Force` is used when:

- Rerunning the command to repair or reconcile configuration.
- Automating Kerberos setup or key management.
- Recovering from partial or failed configuration attempts.
- Ensuring consistent state across environments without manual confirmation.

## When to rotate the key

Microsoft doesn't mandate a fixed rotation interval but recommends aligning with your existing Kerberos security practices. Common approaches include:

- Rotating on the same cadence as Active Directory `krbtgt` keys.
- Rotating as part of scheduled security maintenance windows.
- Rotating immediately after a suspected credential compromise.