---
layout: Conceptual
title: Migrate to Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/migrate-azure-ad-connect-to-cloud-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to plan a phased migration from Microsoft Entra Connect to Microsoft Entra Cloud Sync, including device synchronization and prerequisite checks.
ms.custom: no-azure-ad-ps-ref, msecd-doc-authoring-1023
ms.topic: how-to
ms.date: 2026-10-06T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ai-usage: ai-assisted
locale: en-us
document_id: fab65962-15ad-f425-ed08-ffe652bea4da
document_version_independent_id: c8292ca0-1831-e004-3741-b2a535dbe520
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/migrate-azure-ad-connect-to-cloud-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/migrate-azure-ad-connect-to-cloud-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/migrate-azure-ad-connect-to-cloud-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d786cb27-ffea-851e-2d27-7f4cfca8b112
---

# Migrate to Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Cloud Sync synchronizes users, groups, and contacts from Active Directory to Microsoft Entra ID by using the Microsoft Entra provisioning agent. When device sync is enabled, Cloud Sync can also synchronize computer objects for Microsoft Entra hybrid join. Use this guide to plan a phased migration from Microsoft Entra Connect to Cloud Sync.

## Steps for migrating from Microsoft Entra Connect to Cloud Sync

Important

During the pilot or coexistence phase, don't remove OUs, domains, groups, users, contacts, or other referenced objects from Microsoft Entra Connect Sync scope. Keep the existing scope configured until objects are fully migrated and you're ready for final cutover. Removing objects from scope before final cutover is unsafe: it can drop references in the Microsoft Entra connector space and export reference deletes (such as group membership removals) to Microsoft Entra ID.

The supported coexistence model is to keep objects in Microsoft Entra Connect Sync scope and use the `cloudNoFlow` and `JoinNoFlow` rules to prevent Microsoft Entra Connect Sync from exporting object adds, object deletes, and non-reference attribute updates. Reference attribute updates, such as `member` and `manager`, can still flow for reference resolution.

You can still migrate in phases, such as by OU or another defined batch. Each batch must remain in Microsoft Entra Connect Sync scope with the no-flow rules applied until that batch is fully migrated and ready for cutover.

| Step | Description |
| --- | --- |
| Choose the best sync tool | Before moving to cloud sync, you should verify that cloud sync is currently the best synchronization tool for you. You can do this task by reviewing the [supported sync scenarios comparison](../common-scenarios). |
| Verify the prerequisites for migrating | This guidance is for users who installed Microsoft Entra Connect by using Express settings. If you synchronize devices for Microsoft Entra hybrid join, include [device sync](device-sync) in your Cloud Sync migration plan. Also verify the [Cloud Sync prerequisites](how-to-prerequisites). |
| Back up your Microsoft Entra Connect configuration | Before making any changes, you should back up your Microsoft Entra Connect configuration. This way, you can rollback. For more information, see [Import and export Microsoft Entra Connect configuration settings](../connect/how-to-connect-import-export-config). |
| Review the migration tutorial | To become familiar with the migration process, review the [Migrate to Microsoft Entra Cloud Sync for an existing synced AD forest](tutorial-pilot-aadc-aadccp) tutorial. This tutorial guides you through the migration process in a sandbox environment. |
| Create or identify an OU for the migration | Create a new OU or identify an existing OU that contains the users you'll test migration on. Keep this OU in Microsoft Entra Connect Sync scope during migration. |
| Move users into new OU (optional) | If you're using a new OU, move the users that are in scope for this pilot into that OU now. Before continuing, let Microsoft Entra Connect Sync pick up the changes so that it's synchronizing them in the new OU. Don't remove the OU or users from Microsoft Entra Connect Sync scope during migration. |
| Run PowerShell on OU | You can run the following PowerShell cmdlet to get the counts of the users that are in the pilot OU. `Get-ADUser -Filter * -SearchBase "<DN path of OU>"` Example: `Get-ADUser -Filter * -SearchBase "OU=Finance,OU=UserAccounts,DC=FABRIKAM,DC=COM"` |
| Stop the scheduler | Before creating new sync rules, you need to stop the Microsoft Entra Connect scheduler. For more information, see [how to stop the scheduler](../connect/how-to-connect-sync-feature-scheduler#stop-the-scheduler). |
| Create the custom sync rules | In the Microsoft Entra Connect Synchronization Rules editor, create an inbound sync rule that sets the `cloudNoFlow` attribute to `True` for users in the OU you created or identified previously. You'll also need an outbound sync rule with a link type of `JoinNoFlow` and a scoping filter that has the `cloudNoFlow` attribute set to `True`. Together, these rules prevent Microsoft Entra Connect Sync from exporting object adds, object deletes, and non-reference attribute updates for the scoped users. Reference attribute updates, such as `member` and `manager`, can still flow for reference resolution. During the pilot or coexistence phase, don't remove the pilot OU, group, domain, or related referenced objects from Microsoft Entra Connect Sync scope. For more information, see the [Migrate to Microsoft Entra Cloud Sync for an existing synced AD forest](tutorial-pilot-aadc-aadccp#create-a-custom-user-inbound-rule) tutorial for how to create these rules. |
| Install the provisioning agent | If you haven't done so, install the provisioning agent. For more information, see [how to install the agent](how-to-install). |
| Configure cloud sync | Once the agent is installed, you need to configure cloud sync. In the configuration, you need to create a scope to the OU that was created or identified previously. For more information, see [Configuring cloud sync](how-to-configure). |
| Verify pilot users are synchronizing and being provisioned | Verify that the users are now being synchronized in the portal. You can use the PowerShell script below to get a count of the number of users that have the on-premises pilot OU in their distinguished name. This number should match the count of users in the previous step. If you create a new user in this OU, verify that it's being provisioned. |
| Start the scheduler | Now that you've verified users are provisioning and synchronizing, you can go ahead and start the Microsoft Entra Connect scheduler. For more information, see [how to start the scheduler](../connect/how-to-connect-sync-feature-scheduler#start-the-scheduler). |
| Schedule your remaining users | Create a phased migration plan for the remaining users, groups, contacts, and related referenced objects. You can migrate in batches, such as by OU, but keep each batch in Microsoft Entra Connect Sync scope with the no-flow rules applied until the batch is fully migrated and ready for cutover. |
| Verify all users are provisioned | As you migrate users, verify that they're provisioning and synchronizing correctly. |
| Stop Microsoft Entra Connect | After you've verified that all objects in the migration scope are provisioned by Microsoft Entra Cloud Sync and their references, such as group memberships and manager relationships, remain intact, you can stop Microsoft Entra Connect Sync for that scope as part of final cutover. Microsoft recommends that you leave the server in a disabled state for a period of time so you can verify that the migration was successful. |
| Verify everything is good | After a period of time, verify that everything is good. |
| Decommission the Microsoft Entra Connect server | Once you've verified everything is good, take the Microsoft Entra Connect server offline. For more information, see [Uninstall Microsoft Entra Connect](../connect/how-to-connect-uninstall). |

## Verify Users script

```PowerShell
# Filename:  VerifyAzureUsers.ps1
# Description: Counts the number of users in Azure that have a specific on-premises distinguished name.
#
# DISCLAIMER:
# Copyright (c) Microsoft Corporation. All rights reserved. This 
# script is made available to you without any express, implied or 
# statutory warranty, not even the implied warranty of 
# merchantability or fitness for a particular purpose, or the 
# warranty of title or non-infringement. The entire risk of the 
# use or the results from the use of this script remains with you.
#
#
#
#

Connect-MgGraph -Scopes "User.Read.All"

#Declare variables

$Users = Get-EntraUser -All:$true -Filter "DirSyncEnabled eq true"
$OU = "OU=Sales,DC=contoso,DC=com"
$counter = 0

#Search users

foreach ($user in $Users) {
  $test = $User.ExtensionProperty
  $DN = $test["onPremisesDistinguishedName"]
  if ($DN -match $OU){$counter++}
}

Write-Host "Total Users found:" + $counter

```

## More information

- [What is provisioning?](../what-is-provisioning)
- [What is Microsoft Entra Cloud Sync?](what-is-cloud-sync)
- [Create a new configuration for Microsoft Entra Cloud Sync](how-to-configure).
- [Migrate to Microsoft Entra Cloud Sync for an existing synced AD forest](tutorial-pilot-aadc-aadccp) ``