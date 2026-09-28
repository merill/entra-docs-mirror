---
layout: FAQ
title: Provisioning to Active Directory with Microsoft Entra Cloud Sync FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/reference-provision-to-active-directory-faq
summary: >
  <p>Read about frequently asked questions for provisioning to Active Directory with Microsoft Entra Cloud Sync.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: mwongerapk
description: This document describes frequently asked questions for cloud sync.
ms.topic: faq
ms.date: 2026-08-19T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: e66323a2-ed2b-a9c6-e353-a842e215a16b
document_version_independent_id: e66323a2-ed2b-a9c6-e353-a842e215a16b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/reference-provision-to-active-directory-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/reference-provision-to-active-directory-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/reference-provision-to-active-directory-faq.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: e6b42c31-741a-b3fb-bb28-310733d14647
---

# Provisioning to Active Directory with Microsoft Entra Cloud Sync FAQ - Microsoft Entra ID | Microsoft Learn

Read about frequently asked questions for provisioning to Active Directory with Microsoft Entra Cloud Sync.

## Provisioning users to Active Directory

### Why does a provisioned user keep reverting to the original organizational unit after I change the target container?

This behavior is expected. The default `parentDistinguishedName` expression uses the user's `onPremisesDistinguishedName` attribute when that attribute is populated, and falls back to the constant target container only when it's empty. Because the cloud is the source of authority, the location recorded on the cloud object wins, so changing the target container doesn't move an already-provisioned user, and moving the object manually in Active Directory is reverted on the next sync cycle.

To move the user, either update the target container mapping (which moves every user that matches the mapping rules) or update that user's `onPremisesDistinguishedName` attribute in Microsoft Entra ID. For the steps, see [Move a provisioned user to a different organizational unit](how-to-configure-entra-to-active-directory#move-a-provisioned-user-to-a-different-organizational-unit).

## Provisioning groups to Active Directory

### Does Group Provision to AD in Microsoft Entra Cloud Sync work side-by-side with other Microsoft Entra Connect Sync capabilities?

Yes, You can use Microsoft Entra Cloud Sync solely for Security Group Provisioning to AD while simultaneously using Connect Sync for syncing AD to Microsoft Entra ID. Any cloud security group that includes users synchronized from AD via Microsoft Entra Connect Sync can be provisioned to Active Directory using Microsoft Entra Cloud Sync and Group Provisioning to AD.

For instance, if there are two users (User A and User B) who are Active Directory Domain Services users and have been synchronized with Microsoft Entra Connect Sync to Microsoft Entra ID, you can create a cloud security group in Microsoft Entra ID called SecurityGroup A. This group can then be provisioned back to AD DS using [Microsoft Entra Cloud Sync - Group Provisioning to Active Directory](../group-writeback-cloud-sync).

### I have Microsoft 365 groups that I provision to AD using Group Writeback feature in Microsoft Entra Connect Sync. Will that continue to work?

Yes, when you uninstall or disable Group Writeback V2 from your Connect Sync configuration, it defaults to Group Writeback V1. This default supports the ability to write back all Microsoft 365 groups in Microsoft Entra ID.

### What if I want to disable Group Writeback V1 as well?

When you disable Group Writeback V1, the next full sync deletes all the groups that are written by Microsoft Entra Connect Sync to AD. Cloud Security Groups provisioned using Microsoft Entra Cloud Sync won’t be impacted by this operation.

### Can I continue to use the "Group writeback" field through MS Graph and Microsoft Entra admin center for setting groups in scope for provisioning to AD using Microsoft Entra Cloud Sync?

No, this field isn't currently used for determining the scope of groups being provisioned to AD using Cloud Sync. You have to use the Microsoft Entra Cloud Sync configuration experience in the portal to set scope. For more information, see [Use directory extensions when provisioning to Active Directory](tutorial-directory-extension-group-provisioning).

### If I am following the steps outlined in Migrate Microsoft Entra Connect Sync group writeback V2 to Microsoft Entra Cloud Sync, will this impact my synchronization from Active Directory to Microsoft Entra ID with Microsoft Entra Connect?

No, following the migration steps for moving from group writeback V2 to Microsoft Entra cloud sync will not affect synchronization between AD and Microsoft Entra ID.

## AD user and group enforcement (preview)

### What object types does AD enforcement support?

Users and groups are supported in this preview.

### When I install the provisioning agent, will enforcement be enabled on all of my Active Directory objects?

No. In addition to installing the policy, you must mark each user or group for enforcement. Configure the applicable user or group attribute mapping in provisioning to Active Directory to set the `msDS-ObjectSoa` attribute on the objects you want to protect. Objects without the attribute set aren't enforced.

### Can I define a break-glass account for emergency changes to a protected user or group?

Yes. You can add the security identifier (SID) of an authorized user or group to the policy so that account can make changes to enforced objects when the provisioning service isn't available. For more information, see [Configure AD user and group enforcement](how-to-active-directory-object-enforcement#break-glass-accounts).

### If group A is marked for enforcement, can it be added as a member of group B that isn't marked for enforcement?

Yes. Group A can be added as a member of group B. However, changes to the members of group A can still only be made by the provisioning service.

### What happens if a change is made on a domain controller that doesn't have AD object enforcement enabled?

The change is processed. For full enforcement across the domain, every domain controller must have the feature enabled, either by installing the cumulative Windows Server update plus the matching Group Policy MSI, or by running a Windows Server Insider Preview build that has the feature already enabled.

### How does this feature change the Active Directory role-based access control (RBAC) model?

AD object enforcement is additive to the existing RBAC model. It places another restriction on top of the existing role assignments, without giving any user extra access.

### What role is required to enable the policy?

Domain Admin is required to run the PowerShell script that installs the policy. Run the script on the machine where the Microsoft Entra Cloud Sync provisioning agent is installed.

### How do I see enforcement events in the event log?

To see Audit-mode events, set the Security Diagnostics registry value to **1** on the PDCe. Audited changes then appear in the Directory Services event log on that domain controller. For more information, see [AD and LDS diagnostic event logging](/en-us/troubleshoot/windows-server/active-directory/configure-ad-and-lds-event-logging).