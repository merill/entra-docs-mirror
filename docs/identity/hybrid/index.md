---
layout: Landing
title: Hybrid identity documentation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/
summary: Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location. We call this hybrid identity.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: mwongerapk
description: Integrate your on-premises directories with Microsoft Entra ID. This allows you to provide a common identity for your users for Microsoft 365, Azure, and SaaS applications integrated with Microsoft Entra ID.
ms.collection: na
ms.date: 2026-08-10T00:00:00.0000000Z
ms.topic: landing-page
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: 93f9804f-d547-4472-a528-9b8272700db8
document_version_independent_id: 8123e042-c55b-782c-720e-ec24058d731d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: landing
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/index.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 228fe8d7-a086-3fed-52ce-34b19840b3f5
---

# Hybrid identity documentation

Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location. We call this hybrid identity.

## About Hybrid Identity

### Overview

- [What is hybrid identity?](whatis-hybrid-identity)
- [What is provisioning?](what-is-provisioning)
- [What is inter-directory provisioning?](what-is-inter-directory-provisioning)

## Getting started

### Get started

- [Common scenarios](common-scenarios)
- [Choose the right sync client](common-scenarios)
- [Steps to start](get-started)

## Manage your deployment

### Get started

- [Install your sync tool](install)
- [Configure synchronization](configure)
- [Configure account settings](accounts)
- [Migrate your sync tool](cloud-sync/migrate-azure-ad-connect-to-cloud-sync)

## Manage users and groups

### Get started

- [Provision users on-demand](on-demand-provision)
- [Scheduling imports](connect/how-to-connect-sync-feature-scheduler)
- [Prevent accidental deletions](accidental-deletes)

## Provision - Active Directory to Microsoft Entra ID

### Get started

- [Integrate a single AD forest with a single Microsoft Entra tenant](cloud-sync/tutorial-single-forest)
- [Integrate an existing forest and a new forest with a single Microsoft Entra tenant](cloud-sync/tutorial-existing-forest)
- [Configuration - AD to Microsoft Entra ID](cloud-sync/how-to-configure)
- [Attribute mapping - AD to Microsoft Entra ID](cloud-sync/how-to-attribute-mapping)
- [Directory extensions and custom attributes - AD to Microsoft Entra ID](cloud-sync/custom-attribute-mapping)
- [Supported topologies - AD to Microsoft Entra ID](cloud-sync/plan-cloud-sync-topologies)

## Provision - Microsoft Entra ID to Active Directory

### Get started

- [Provision groups to Active Directory using Microsoft Entra Cloud Sync](group-writeback-cloud-sync)
- [Govern on-premises Active Directory based apps (Kerberos) using Microsoft Entra ID Governance](cloud-sync/govern-on-premises-groups)
- [Supported topologies - Microsoft Entra ID to AD](cloud-sync/plan-cloud-sync-topologies)
- [Configuration - Microsoft Entra ID to AD (preview)](cloud-sync/how-to-configure-entra-to-active-directory)
- [Scenario - Provisioning users and groups to AD (preview)](cloud-sync/tutorial-users-groups-provisioning-walkthrough)
- [Using directory extensions when provisioning to AD](cloud-sync/tutorial-directory-extension-group-provisioning)
- [Provisioning to Active Directory FAQ](cloud-sync/reference-provision-to-active-directory-faq)

## Migrations

### Get started

- [Migrate to Microsoft Entra Cloud Sync from Connect sync](cloud-sync/migrate-azure-ad-connect-to-cloud-sync)
- [Migrate Microsoft Entra Connect Sync group writeback V2 to Microsoft Entra Cloud Sync](cloud-sync/migrate-group-writeback)