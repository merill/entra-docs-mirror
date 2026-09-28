---
layout: Conceptual
title: SCIM synchronization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/sync-scim
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving SCIM synchronization with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 7d334036-b74e-acb9-f0af-a6e281e907dd
document_version_independent_id: 60fc83b6-9ba2-80f0-d94d-747104cf78df
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/sync-scim.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/sync-scim
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/sync-scim.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 6fea2565-24d7-5ca8-db50-a52b87edd15b
---

# SCIM synchronization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

System for Cross-Domain Identity Management (SCIM) is an open standard protocol for automating the exchange of user identity information between identity domains and IT systems. SCIM ensures that employees added to the Human Capital Management (HCM) system automatically have accounts created in Microsoft Entra ID or Windows Server Active Directory. User attributes and profiles are synchronized between the two systems, updating removing users based on the user status or role change.

SCIM is a standardized definition of two endpoints: a /Users’ endpoint and a /Groups endpoint. It uses common REST verbs to create, update, and delete objects. It also uses a pre-defined schema for common attributes like group name, username, first name, last name, and email. Applications that offer a SCIM 2.0 REST API can reduce or eliminate the pain of working with proprietary user management APIs or products. For example, any SCIM-compliant client can make an HTTP POST of a JSON object to the /Users endpoint to create a new user entry. Instead of needing a slightly different API for the same basic actions, apps that conform to the SCIM standard can instantly take advantage of pre-existing clients, tools, and code.

## Use when:

You want to automatically provision user information from an HCM system to Microsoft Entra ID and Windows Server Active Directory, and then to target systems if necessary.

![architectural diagram](media/authentication-patterns/scim-auth.png)

## Components of system

- **HCM system**: Applications and technologies that enable Human Capital Management process and practices that support and automate HR processes throughout the employee lifecycle.
- **Microsoft Entra provisioning service**: Uses the SCIM 2.0 protocol for automatic provisioning. The service connects to the SCIM endpoint for the application, and uses the SCIM user object schema and REST APIs to automate provisioning and de-provisioning of users and groups.
- **Microsoft Entra ID**: User repository used to manage the lifecycle of identities and their entitlements.
- **Target system**: Application or system that has SCIM endpoint and works with the Microsoft Entra provisioning to enable automatic provisioning of users and groups.

## Implement SCIM with Microsoft Entra ID

- [How provisioning works in Microsoft Entra ID](../identity/app-provisioning/how-provisioning-works)
- [Managing user account provisioning for enterprise apps in the Azure portal](../identity/app-provisioning/configure-automatic-user-provisioning-portal)
- [Build a SCIM endpoint and configure user provisioning with Microsoft Entra ID](../identity/app-provisioning/use-scim-to-provision-users-and-groups)
- [SCIM 2.0 protocol compliance of the Microsoft Entra provisioning service](../identity/app-provisioning/application-provisioning-config-problem-scim-compatibility)