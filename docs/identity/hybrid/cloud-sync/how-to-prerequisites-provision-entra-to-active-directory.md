---
layout: Conceptual
title: Microsoft Entra prerequisites for AD (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-prerequisites-provision-entra-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: mwongerapk
ms.reviewer: marshmacy
ms.subservice: hybrid-cloud-sync
ms.topic: how-to
ms.date: 2026-08-10T00:00:00.0000000Z
description: Prerequisites and license requirements for provisioning users and groups from Microsoft Entra ID to on-premises Active Directory with Microsoft Entra Cloud Sync.
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: 0c83d1e7-a264-3926-3558-8865462220ac
document_version_independent_id: 0c83d1e7-a264-3926-3558-8865462220ac
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-prerequisites-provision-entra-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-prerequisites-provision-entra-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-prerequisites-provision-entra-to-active-directory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: c707526a-c9c5-d92b-af00-b2d487c0999b
---

# Microsoft Entra prerequisites for AD (Preview) - Microsoft Entra ID | Microsoft Learn

This article lists the prerequisites and license requirements for provisioning **users and groups** from Microsoft Entra ID to on-premises Active Directory Domain Services (AD DS) by using Microsoft Entra Cloud Sync. Complete these items before you [configure provisioning](how-to-configure-entra-to-active-directory).

## License requirements

Provisioning to Active Directory uses a configuration-based licensing model.

| Configuration | License required |
| --- | --- |
| **Existing configurations** (created before general availability) | No license change is required. These configurations continue to run under their existing Microsoft Entra ID P1 licensing. |
| First **2** new configurations per tenant | Microsoft Entra ID P1. |
| **More than 2** new configurations per tenant (3–20) | Microsoft Entra ID Governance. |

Note

A maximum of **20** configurations (domains) can be configured per tenant. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## General requirements

- Microsoft Entra account with at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) role.
- On-premises AD DS schema with the *msDS-ExternalDirectoryObjectId* attribute, which is available in Windows Server 2016 and later.
- Provisioning agent with build version [1.1.2334.0](reference-version-history#1123340) or later.

Note

The permissions to the service account are assigned during clean install only. If you're upgrading from the previous version, permissions need to be assigned manually by using PowerShell:

```powershell
$credential = Get-Credential
Set-AADCloudSyncPermissions -PermissionType UserGroupCreateDelete -TargetDomain "FQDN of domain" -EACredential $credential
```

If the permissions are set manually, assign Read, Write, Create, and Delete all properties for all descendant Groups and User objects. These permissions aren't applied to AdminSDHolder objects by default. For more information, see [Microsoft Entra provisioning agent gMSA PowerShell cmdlets](how-to-gmsa-cmdlets#grant-permissions-to-a-specific-domain).

The provisioning agent and the sync client also have their own requirements:

- Install the provisioning agent on a domain-joined server. We recommend Windows Server 2025 or Windows Server 2022. You can use older Windows Server versions that are in extended support, but support for this configuration might require a [paid support program](/en-us/lifecycle/policies/fixed#extended-support).
- The provisioning agent must be able to communicate with one or more domain controllers on ports TCP/389 (LDAP) and TCP/3268 (Global Catalog).
    - Global Catalog lookup is required to filter out invalid membership references.
- Microsoft Entra Connect Sync with build version [2.2.8.0](../connect/reference-connect-version-history#2280)or later.
    - Required to support on-premises user membership synchronized using Microsoft Entra Connect Sync.
    - Required to synchronize `AD DS:user:objectGUID` to `AAD DS:user:onPremisesObjectIdentifier`.

## User provisioning prerequisites (preview)

If you provision users to AD DS, ensure that the applications they use support Kerberos. Applications that collect the user's password and perform an LDAP bind aren't supported for cloud-managed users because there's no AD DS password to present.

To give cloud-managed users passwordless access to on-premises Kerberos resources, configure the passwordless method your organization uses. For Windows Hello for Business, configure [cloud Kerberos trust](/en-us/windows/security/identity-protection/hello-for-business/deploy/hybrid-cloud-kerberos-trust). For FIDO2 security keys, follow [Passwordless security key sign-in to on-premises resources](/en-us/entra/identity/authentication/howto-authentication-passwordless-security-key-on-premises). Microsoft Entra ID issues a partial TGT that the client exchanges with an on-premises domain controller for a full AD TGT.

## More information

Consider the following points when you provision to AD DS:

- Group membership written to AD DS includes only members that have an AD DS account. Those members can be on-premises synchronized users, cloud-managed users that Cloud Sync provisions to AD DS because they're in scope of user provisioning, or other cloud-created security groups. A cloud-managed user that has no AD DS account is skipped.
- On-premises synchronized users must have the *onPremisesObjectIdentifier* attribute set on their account.
- The *onPremisesObjectIdentifier* must match a corresponding *objectGUID* in the target AD DS environment.
- An on-premises user *objectGUID* attribute can be synchronized to a cloud user *onPremisesObjectIdentifier* attribute by using either sync client.
- Only global Microsoft Entra ID tenants can provision from Microsoft Entra ID to AD DS. Tenants such as B2C aren't supported.
- The provisioning job runs on a recurring schedule.

Note

The preview of Group Writeback v2 in Microsoft Entra Connect Sync is deprecated and no longer supported. If you use Group Writeback v2, move your sync client to Microsoft Entra Cloud Sync. If you provision Microsoft 365 groups to AD DS, you can keep using Group Writeback v1.