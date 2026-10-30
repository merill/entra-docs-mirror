---
layout: Conceptual
title: Use a group managed service account with Microsoft Entra Cloud Sync  - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/gmsa-cloud-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This document details using a gMSA account with cloud sync
ms.topic: how-to
ms.date: 2025-09-29T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 5124f7d2-27b8-63fb-81ef-743817cc1c10
document_version_independent_id: 5124f7d2-27b8-63fb-81ef-743817cc1c10
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/gmsa-cloud-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/gmsa-cloud-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/gmsa-cloud-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: aec4c5c9-bc21-538b-dc78-279926256c68
---

# Use a group managed service account with Microsoft Entra Cloud Sync  - Microsoft Entra ID | Microsoft Learn

A group Managed Service Account is a managed domain account that provides automatic password management, simplified service principal name (SPN) management, the ability to delegate the management to other administrators, and also extends this functionality over multiple servers. Microsoft Entra Cloud Sync supports and uses a gMSA for running the agent. You can choose to allow the installer to create a new account or specify a custom account. You'll be prompted for administrative credentials during setup, in order to create this account or set permissions if using a custom account. If the installer creates the account, the account appears as `domain\provAgentgMSA$`. For more information on a gMSA, see [group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

## Prerequisites for gMSA

- The Active Directory schema in the gMSA domain's forest needs to be updated to Windows Server 2012 or later.
- [PowerShell RSAT modules](/en-us/windows-server/remote/remote-server-administration-tools) on a domain controller.
- At least one domain controller in the domain must be running Windows Server 2012 or later.
- A domain-joined server that runs Windows Server 2022, Windows Server 2019, or Windows Server 2016 for the agent installation.

## Permissions set on a gMSA account (ALL permissions)

When the installer creates the gMSA account, it sets **ALL** of the permissions on the account. The following tables detail these permissions

### MS-DS-Consistency-Guid

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Write property mS-DS-ConsistencyGuid | Descendant user objects |
| Allow | &lt;gmsa account&gt; | Write property mS-DS-ConsistencyGuid | Descendant group objects |

If the associated forest is hosted in a Windows Server 2016 environment, it includes the following permissions for NGC keys and STK keys.

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Write property msDS-KeyCredentialLink | Descendant user objects |
| Allow | &lt;gmsa account&gt; | Write property msDS-KeyCredentialLink | Descendant device objects |

### Password Hash Sync

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Replicating Directory Changes | This object only (Domain root) |
| Allow | &lt;gmsa account&gt; | Replicating Directory Changes All | This object only (Domain root) |

### Password Writeback

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Reset Password | Descendant User objects |
| Allow | &lt;gmsa account&gt; | Write property lockoutTime | Descendant User objects |
| Allow | &lt;gmsa account&gt; | Write property pwdLastSet | Descendant User objects |
| Allow | &lt;gmsa account&gt; | Unexpire Password | This object only (Domain root) |

### Group Writeback

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Generic Read/Write | All attributes of object type group and subobjects |
| Allow | &lt;gmsa account&gt; | Create/Delete child object | All attributes of object type group and subobjects |
| Allow | &lt;gmsa account&gt; | Delete/Delete tree objects | All attributes of object type group and subobjects |

### Exchange Hybrid Deployment

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Read/Write all properties | Descendant User objects |
| Allow | &lt;gmsa account&gt; | Read/Write all properties | Descendant InetOrgPerson objects |
| Allow | &lt;gmsa account&gt; | Read/Write all properties | Descendant Group objects |
| Allow | &lt;gmsa account&gt; | Read/Write all properties | Descendant Contact objects |

### Exchange Mail Public Folders

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Read all properties | Descendant PublicFolder objects |

### UserGroupCreateDelete (CloudHR)

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | &lt;gmsa account&gt; | Generic write | All attributes of object type group and subobjects |
| Allow | &lt;gmsa account&gt; | Create/Delete child object | All attributes of object type group and subobjects |
| Allow | &lt;gmsa account&gt; | Generic write | All attributes of object type user and subobjects |
| Allow | &lt;gmsa account&gt; | Create/Delete child object | All attributes of object type user and subobjects |

## Using a custom gMSA account

If you're creating a custom gMSA account, the installer will set the **ALL** permissions on the custom account.

For steps on how to upgrade an existing agent to use a gMSA account see [group Managed Service Accounts](how-to-install#group-managed-service-accounts).

For more information on how to prepare your Active Directory for group Managed Service Account, see [group Managed Service Accounts Overview](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).