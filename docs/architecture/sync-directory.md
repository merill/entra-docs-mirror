---
layout: Conceptual
title: Directory synchronization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/sync-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving directory synchronization with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-03-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 26e11a5f-8b0e-b3be-de91-0928a9a84b56
document_version_independent_id: a360a5a1-da96-a131-f214-bf7ea8e0cd06
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/sync-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/sync-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/sync-directory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: c1d88de1-fcbe-6c28-01eb-d2730a8b234c
---

# Directory synchronization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Many organizations have a hybrid infrastructure that encompasses both on-premises and cloud components. Synchronizing users' identities between local and cloud directories lets users access resources with a single set of credentials.

Synchronization is the process of

- creating an object based on certain conditions,
- keeping the object updated, and
- removing the object when conditions are no longer met.

On-premises provisioning involves provisioning from on-premises sources (such as Active Directory) to Microsoft Entra ID.

## When to use directory synchronization

Use directory synchronization when you need to synchronize identity data from your on premises Active Directory environments to Microsoft Entra ID as illustrated in the following diagram.

![architectural diagram](media/authentication-patterns/dir-sync-auth.png)

## System components

- **Microsoft Entra ID**: Synchronizes identity information from organization's on premises directory via Microsoft Entra Connect.
- **Microsoft Entra Connect**: A tool for connecting on premises identity infrastructures to Microsoft Entra ID. The wizard and guided experiences help you to deploy and configure prerequisites and components required for the connection (including sync and sign on from Active Directories to Microsoft Entra ID).
- **Active Directory**: Active Directory is a directory service that is included in most Windows Server operating systems. Servers that run Active Directory Domain Services (AD DS) are called domain controllers. They authenticate and authorize all users and computers in the domain.

Microsoft designed [Microsoft Entra Connect cloud sync](../identity/hybrid/cloud-sync/what-is-cloud-sync) to meet and accomplish your hybrid identity goals for synchronization of users, groups, and contacts to Microsoft Entra ID. Microsoft Entra Connect cloud sync uses the Microsoft Entra cloud provisioning agent instead of the Microsoft Entra Connect application.

## Implement directory synchronization with Microsoft Entra ID

Explore the following resources to learn more about directory synchronization with Microsoft Entra ID.

- [What is identity provisioning with Microsoft Entra ID?](../identity/hybrid/what-is-provisioning)Provisioning is the process of creating an object based on certain conditions, keeping the object up-to-date and deleting the object when conditions are no longer met. On-premises provisioning involves provisioning from on premises sources (like Active Directory) to Microsoft Entra ID.
- [Hybrid Identity: Directory integration tools comparison](../identity/hybrid/) describes differences between Microsoft Entra Connect Sync and Microsoft Entra Connect cloud provisioning.
- [Microsoft Entra Connect and Microsoft Entra Connect Health installation roadmap](../identity/hybrid/connect/how-to-connect-install-roadmap) provides detailed installation and configuration steps.