---
layout: FAQ
title: Microsoft Entra Cloud Sync FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/reference-cloud-sync-faq
summary: >
  <p>Read about frequently asked questions for Microsoft Entra Cloud Sync.</p>
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
ms.date: 2026-03-30T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 42038cf7-555b-5351-0380-b20ac50c4863
document_version_independent_id: 7267c4b4-0770-9fb4-4e45-e8342ca4a850
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/reference-cloud-sync-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/reference-cloud-sync-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/reference-cloud-sync-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: a506f385-8ebe-3f79-6d65-d8372c79b191
---

# Microsoft Entra Cloud Sync FAQ - Microsoft Entra ID | Microsoft Learn

Read about frequently asked questions for Microsoft Entra Cloud Sync.

## How often does cloud sync run?

Password hash synchronization is scheduled every 2-5 minutes. Cloud provisioning synchronization for users and groups is scheduled approximately every 10 to 20 minutes. However, the actual time it takes to provision objects in Microsoft Entra ID depends on the number of changes pending in each sync cycle. Larger volumes of changes may extend the provisioning time, while smaller sets may complete more quickly. Therefore, object sync latency is influenced by both the sync cycle interval and the volume of changes being processed.

## Seeing password hash sync failures on the first run. Why?

This behavior is expected. The failures are due to the user object not present in Microsoft Entra ID. Once the user is provisioned, wait for a couple of runs and confirm that password hash sync no longer has the errors.

## What's the difference between Microsoft Entra Connect Sync and cloud sync?

With Microsoft Entra Connect Sync, provisioning runs on the on-premises sync server. Configuration is stored on the on-premises sync server. With Microsoft Entra Cloud Sync, the provisioning configuration is stored in the cloud and runs in the cloud as part of the Microsoft Entra provisioning service. See the detailed article [What is Microsoft Entra Cloud Sync](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync) for a detailed comparison.

## Can I use cloud sync to sync from multiple Active Directory forests?

Yes. Cloud provisioning can be used to sync from multiple Active Directory forests. In the multi-forest environment, all the references (example, manager) need to be within the domain.

## How is the agent updated?

The agents are auto upgraded by Microsoft. For the IT team, this reduces the burden of having to test and validate new agent versions.

## Can I disable auto upgrade?

There's no supported way to disable auto upgrade.

## Can I change the source anchor for cloud sync?

By default, cloud sync uses ms-ds-consistency-GUID with a fallback to ObjectGUID as source anchor. There's no supported way to change the source anchor.

## I see new service principals with the AD domain name(s) when using cloud sync. Is it expected?

Yes, cloud sync creates a service principal for the provisioning configuration with the domain name as the service principal name. Don't make any changes to the service principal configuration.

## What happens when a synced user is required to change password on next logon?

If password hash sync is enabled in cloud sync and the synced user is required to change password on next logon in on-premises AD, cloud sync doesn't provision the "to-be-changed" password hash to Microsoft Entra ID. Once the user changes the password, the user password hash is provisioned from AD to Microsoft Entra ID.

## Does cloud sync support writeback of ms-ds-consistencyGUID for any object?

No, cloud sync doesn't support writeback of ms-ds-consistencyGUID for any object (including user objects).

## I'm provisioning users using cloud sync. I deleted the configuration. Why do I still see the old synced objects in Microsoft Entra ID?

When you delete the configuration, cloud sync doesn't automatically remove the synced objects in Microsoft Entra ID. To ensure you don't have the old objects, change the scope of the configuration to an empty group or Organizational Units. Once the provisioning runs and cleans up the objects, disable and delete the configuration.

## I uninstalled the cloud sync agent. How long until it's removed from the portal?

When you uninstall or stop a cloud sync agent, the agent isn't removed from the Microsoft Entra admin center immediately. After approximately one hour, the agent shows as **Inactive**. After approximately 10 days, the agent is soft-deleted and no longer appears in the portal. The agent is permanently removed when its certificate expires, which prevents any further interaction with Microsoft services. For more information, see [Agent removal from the portal after uninstall](how-to-configure#agent-removal-from-the-portal-after-uninstall).

## Does cloud sync support Exchange hybrid?

Yes. Cloud sync now supports Exchange hybrid scenarios. For more information, see [Exchange hybrid with cloud sync](exchange-hybrid)

## Can I install the cloud provisioning agent on Windows Server Core?

No, installing the agent on server core isn't supported.

## Can I install the cloud provisioning agent on the same server as Microsoft Entra Connect Sync?

Yes, installing the agent on the same server is supported.

## Can I use a staging server with the cloud provisioning agent?

No, staging servers aren't supported.

## Can I synchronize a Guest user account?

No, synchronizing a guest user account isn't supported.

## If I move a user from an OU that is scoped for cloud sync to an OU that is scoped for Microsoft Entra Connect, what happens?

The user is deleted and recreated. Moving a user from an OU that is scoped for cloud sync is viewed as a delete operation. If the user is moved to an OU that is managed by Microsoft Entra Connect, it will be reprovisioned to Microsoft Entra ID and a new user created.

## If I rename or move the OU that is in scope for the cloud sync filter, what happens to the users that were created in Microsoft Entra ID?

Nothing. The users aren't deleted if the OU is renamed or moved.

## Does Microsoft Entra Cloud Sync support large groups?

Yes. Today we support up to 50,000 group members synchronized using the OU scope filtering.

## Does Microsoft Entra Cloud Sync support nested groups with group scoping?

No. Nested objects beyond the first level aren't included when scoping using security groups. Only use group scope filtering for pilot scenarios, there are limitations to syncing large groups.

## Does the cloud provisioning agent load balance if I have multiple agents installed?

No. Only one agent is ever active.

## Does the cloud provisioning agent require a preferred domain controller list be set?

No. The preferred domain controller list is specified during [agent installation](how-to-install) but it's optional. If no preferred DCs are configured, then the agent uses any available DC in the domain.

## I have a multi-forest environment and the network between the two forests is using NAT (Network Address Translation). Is using Microsoft Entra Cloud Sync between these two forests supported?

No, using Microsoft Entra Cloud Sync over NAT isn't supported because it's dependent on Active Directory which does not support NAT. See [support boundaries for Active Directory over NAT](/en-us/troubleshoot/windows-server/active-directory/support-for-active-directory-over-nat).