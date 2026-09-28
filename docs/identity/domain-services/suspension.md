---
layout: Conceptual
title: Suspended domains in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/suspension
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn about the different health states for a Microsoft Entra Domain Services managed domain and how to restore a suspended domain.
ms.assetid: 95e1d8da-60c7-4fc1-987d-f48fde56a8cb
ms.topic: how-to
ms.date: 2025-02-19T00:00:00.0000000Z
locale: en-us
document_id: c91c41d1-a869-5507-3cda-3a61b2dd57c6
document_version_independent_id: 23262ca0-06c1-a4f1-1d9e-08434099788d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/suspension.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/suspension
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/suspension.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 7ad277a4-c8fa-dee4-2c34-ca4eb161177b
---

# Suspended domains in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

When Microsoft Entra Domain Services is unable to service a managed domain for a long period of time, it puts the managed domain into a suspended state. If a managed domain remains in a suspended state, it's automatically deleted. To keep your Domain Services managed domain healthy and avoid suspension, resolve any alerts as quickly as you can.

This article explains why managed domains are suspended, and how to recover a suspended domain.

## Overview of managed domain states

Through the lifecycle of a managed domain, there are different states that indicate its health. If the managed domain reports an issue, quickly resolve the underlying cause to stop the state from continuing to degrade.

![The progression of states that a managed domain takes towards suspension](media/entra-domain-services-suspension/suspension-timeline.png)

A managed domain can be in one of the following states:

- Running
- Needs attention
- Suspended
- Deleted

## Running state

A managed domain that's configured correctly and without problems is in the *Running* state. This is the desired state for a managed domain.

### What to expect

- The Azure platform can regularly monitor the health of the managed domain.
- Domain controllers for the managed domain are patched and updated regularly.
- Changes from Microsoft Entra ID are regularly synchronized to the managed domain.
- Regular backups are taken for the managed domain.

## Needs Attention state

A managed domain with one or more issues that need to be fixed is in the *Needs attention* state. The health page for the managed domain lists the alerts, and indicate where there's a problem.

Some alerts are transient and are automatically resolved by the Azure platform. For other alerts, you can fix the issue by following the resolution steps provided. If there's a critical alert, [open an Azure support request](/en-us/azure/active-directory/fundamentals/how-to-get-support) for additional troubleshooting assistance.

One example of an alert is when there's a restrictive network security group. In this configuration, the Azure platform may not be able to update and monitor the managed domain. An alert is generated, and the state changes to *Needs attention*.

For more information, see [How to troubleshoot alerts for a managed domain](troubleshoot-alerts).

### What to expect

When a managed domain is in the *Needs Attention* state, the Azure platform may not be able to monitor, patch, update, or back up data regularly. In some cases, like an invalid network configuration, the domain controllers for the managed domain may be unreachable.

- The managed domain is in an unhealthy state and ongoing health monitoring may stop until the alert is resolved.
- Domain controllers for the managed domain can't be patched or updated.
- Changes from Microsoft Entra ID may not be synchronized to the managed domain.
- Backups for the managed domain may not be taken.
- If you resolve noncritical alerts that are impacting the managed domain, the health should return to the *Running* state.
- Critical alerts are triggered for configuration issues where the Azure platform can't reach the domain controllers. If these critical alerts aren't resolved within 15 days, the managed domain enters the *Suspended* state.

## Suspended state

A managed domain enters the **Suspended** state for one of the following reasons:

- A critical alert isn't resolved within 15 days. A critical alert can be caused by a misconfiguration that blocks access to resources that are needed by Domain Services, such as the alert [AADDS104: Network Error](alert-nsg).
- There's a billing issue with the Azure subscription or the Azure subscription expired.

Managed domains are suspended when the Azure platform can't manage, monitor, patch, or back up the domain. A managed domain stays in a *Suspended* state for 15 days. To maintain access to the managed domain, resolve critical alerts immediately.

### What to expect

The following behavior is experienced when a managed domain is in the *Suspended* state:

- Domain controllers for the managed domain are deprovisioned and aren't reachable within the virtual network.
- Secure LDAP access to the managed domain over the internet, if enabled, stops working.
- There are failures in authenticating to the managed domain, logging on to domain-joined VMs, or connecting over LDAP/LDAPS.
- Backups for the managed domain are no longer taken.
- Synchronization with Microsoft Entra ID stops.

### How do you know if your managed domain is suspended?

You see an [alert](troubleshoot-alerts) on the Domain Services Health page in the Microsoft Entra admin center that notes the domain is suspended. The state of the domain also shows *Suspended*.

### Restore a suspended domain

To restore the health of a managed domain that's in the *Suspended* state, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Domain services**.
2. Choose your managed domain from the list, such as *aaddscontoso.com*, then select **Health**.
3. Select the alert, such as *AADDS503* or *AADDS504*, depending on the cause of suspension.
4. Choose the resolution link that's provided in the alert and follow the steps to resolve it.

You can restore a managed domain from any backup. Any changes that occurred after the backup aren't restored. The date of your last backup is displayed on the **Health** page of the managed domain. Backups for a managed domain are stored for up to 30 days. Backups that are older than 30 days are deleted.

After you resolve alerts when the managed domain is in the *Suspended* state, [open an Azure support request](/en-us/azure/active-directory/fundamentals/how-to-get-support) to return to a healthy state. If there's a backup less than 30 days old, Azure support can restore the managed domain.

## Deleted state

If a managed domain stays in the *Suspended* state for 15 days, it's deleted. This process is unrecoverable.

### What to expect

When a managed domain enters the *Deleted* state, the following behavior is seen:

- All resources and backups for the managed domain are deleted.
- You can't restore the managed domain. You must create a replacement managed domain to reuse Domain Services.
- After it's deleted, you aren't billed for the managed domain.