---
layout: Conceptual
title: Multi-organizational on-premises Exchange mailbox migration for Hosters using Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/parallel-hybrid-migration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id-governance
manager: pmwongera
description: Scenario that describes how Hosters can do a multi-organizational mailbox migration with hybrid identity.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
locale: en-us
document_id: 55553e12-e9cd-88a7-79b3-4b1b4ed8b08d
document_version_independent_id: 55553e12-e9cd-88a7-79b3-4b1b4ed8b08d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/parallel-hybrid-migration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/parallel-hybrid-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/parallel-hybrid-migration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 48cf435b-fc86-77ae-ba22-63df75579548
---

# Multi-organizational on-premises Exchange mailbox migration for Hosters using Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

Parallel multi-organizational mailbox migration can be performed from on-premises Exchange Server to Microsoft 365 cloud / Exchange Online using Microsoft Entra Connect. This method offers the following benefits:

- No downtime.
- Password synchronization for end-users.
- Removes the need to reconfigure Outlook desktop apps on end-users devices post-migration.

## Overview

Some companies have unique Active Directory architectures, in which they support several smaller organizations with the same forest. An example is an on-premises Exchange Server hosting company.

These companies face challenges in migrating mailboxes from on-premises to cloud using Microsoft's migration tools. These companies often need to look for third party solutions to run migrations.

This scenario provides a solution using existing Microsoft toolset to set up Hybrid configurations and subsequent mailbox migrations.

[![Diagram of the parallel hybrid migration scenario.](media/parallel-hybrid-migration/parallel-hybrid-1.png)](media/parallel-hybrid-migration/parallel-hybrid-1.png#lightbox)

## Prerequisites

- For each tenant you're migrating to, there needs to be one Microsoft Entra Connect server.
- You should create virtual machines for each of the Microsoft Entra Connect servers and they need to be domain joined.
- Users in your on-premises Active Directory should be in their own organizational unit (OU).
- Each Microsoft Entra Connect Server has its synchronization rules scoped to individual OUs.
- All of the migrating tenants primary domains must be added and verified in Microsoft 365.
- You should be familiar with [Exchange hybrid deployments](/en-us/exchange/exchange-hybrid).
- Ensure that you meet the [Microsoft Entra Connect prerequisites](how-to-connect-install-prerequisites).
- Ensure that you meet the [prerequisites for the Hybrid Configuration Wizard](/en-us/exchange/hybrid-deployment-prerequisites).

## Parallel Hybrid Migration

The following outlines the steps for the multi-organizational on-premises Exchange mailbox migration with Microsoft Entra Connect using a parallel hybrid environment. Each step must be completed for each tenant that you're migrating to.

### Step 1 - Microsoft Entra Connect

1. On each of the [virtual machines](/en-us/windows-server/virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v?tabs=hyper-v-manager) that were created, [download](https://www.microsoft.com/download/details.aspx?id=47594) Microsoft Entra Connect.
2. Install Microsoft Entra Connect using [custom settings](how-to-connect-install-custom).
3. Configure scoping to the source [on-premises Organizational Unit](how-to-connect-sync-configure-filtering#organizational-unitbased-filtering) that corresponds to the tenant you're synchronizing Microsoft Entra Connect with.

    [![Screenshot of scoping OU.](media/parallel-hybrid-migration/scope-1.png)](media/parallel-hybrid-migration/scope-1.png#lightbox)
4. Enable **Exchange Hybrid deployment** and **Password hash synchronization**

    [![Screenshot of optional features.](media/parallel-hybrid-migration/features-1.png)](media/parallel-hybrid-migration/features-1.png#lightbox)
5. Follow the [post installation tasks](how-to-connect-post-installation) for Microsoft Entra Connect.
6. Verify all of the users are synchronized to the target tenant.

### Step 2 - Hybrid Configuration Wizard

Once you've configured the Microsoft Entra Connect servers and synchronization has completed, use the following steps to download and configure the Exchange Hybrid Configuration Wizard.

1. On each of the virtual machines, [download](https://aka.ms/hybridwizard) and install the [Hybrid Configuration Wizard](/en-us/exchange/hybrid-deployment/deploy-hybrid).
2. On the installation, select [Minimal Hybrid](/en-us/exchange/mailbox-migration/use-minimal-hybrid-to-quickly-migrate).

    [![Screenshot of minimal hybrid.](media/parallel-hybrid-migration/minimal-hybrid-1.png)](media/parallel-hybrid-migration/minimal-hybrid-1.png#lightbox)

For additional information on Exchange Hybrid, see [Exchange hybrid deployments](/en-us/exchange/exchange-hybrid)

### Step 3 - Exchange Administrative Center

1. In [Exchange Admin Center](/en-us/exchange/exchange-admin-center), go to Migration and select the users to be migrated. You can access the EAC using the URL https://admin.exchange.microsoft.com/
2. [Migrate users](/en-us/exchange/troubleshoot/move-or-migrate-mailboxes/migrate-data-with-admin-center).
3. Complete migration batches after mailboxes are fully transferred.

Note

An endpoint should be created at the last step of the Hybrid Configuration Wizard and should be available to create migration batch in the Exchange Admin Center. If not, create an endpoint manually.

Note

Once user provisioning is completed by Microsoft Entra Connect, all users in the organization should be available as MailUser in the Exchange Admin Center and can be selected when creating migration batches.

### Step 4 - Uninstall Hybrid Configuration Wizard and Microsoft Entra Connect

Once you finish the migration, you can uninstall the HCW and Microsoft Entra Connect on the virtual server. At this point you can remove the server from the domain and turn it off.

### Step 5 - Repeat for each tenant

Once you finish the steps for migration, repeat the steps for all of your remaining tenants.