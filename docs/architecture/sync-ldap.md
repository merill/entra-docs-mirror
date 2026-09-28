---
layout: Conceptual
title: LDAP synchronization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/sync-ldap
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving LDAP synchronization with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-03-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: d4cd43d5-0967-fd81-c804-6c9e2d446be9
document_version_independent_id: 221094df-742b-6981-a9ab-28d4acf4c382
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/sync-ldap.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/sync-ldap
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/sync-ldap.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d33a6ba7-d9a8-9b85-d9d1-3e2b3ca0f561
---

# LDAP synchronization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Lightweight Directory Access Protocol (LDAP) is a directory service protocol that runs on the TCP/IP stack. It provides a mechanism that you can use to connect to, search, and modify internet directories. Based on a client-server model, the LDAP directory service enables access to an existing directory.

Many companies depend on on-premises LDAP servers to store users and groups for their critical business apps.

Microsoft Entra ID can replace LDAP synchronization with Microsoft Entra Connect. The Microsoft Entra Connect synchronization service performs all operations related to synchronizing identity data between you're on premises environments and Microsoft Entra ID.

## When to use LDAP synchronization

Use LDAP synchronization when you need to synchronize identity data between your on premises LDAP v3 directories and Microsoft Entra ID as illustrated in the following diagram.

![architectural diagram](media/authentication-patterns/ldap-sync.png)

## System components

- **Microsoft Entra ID**: Microsoft Entra ID synchronizes identity information (users, groups) from organization's on-premises LDAP directories via Microsoft Entra Connect.
- **Microsoft Entra Connect**: is a tool for connecting on premises identity infrastructures to Microsoft Entra ID. The wizard and guided experiences help to deploy and configure prerequisites and components required for the connection.
- **Custom Connector**: A Generic LDAP Connector enables you to integrate the Microsoft Entra Connect synchronization service with an LDAP v3 server. It sits on Microsoft Entra Connect.
- **Active Directory**: Active Directory is a directory service included in most Windows Server operating systems. Servers that run Active Directory Services, referred to as domain controllers, authenticate and authorize all users and computers in a Windows domain.
- **LDAP v3 server**: LDAP protocol-compliant directory storing corporate users and passwords used for directory services authentication.

## Implement LDAP synchronization with Microsoft Entra ID

Explore the following resources to learn more about LDAP synchronization with Microsoft Entra ID.

- [Hybrid Identity: Directory integration tools comparison](../identity/hybrid/) describes differences between Microsoft Entra Connect Sync and Microsoft Entra Connect cloud provisioning.
- [Microsoft Entra Connect and Microsoft Entra Connect Health installation roadmap](../identity/hybrid/connect/how-to-connect-install-roadmap) provides detailed installation and configuration steps.
- The [Generic LDAP Connector](/en-us/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericldap) enables you to integrate the synchronization service with an LDAP v3 server.

    Note

    Deploying the LDAP Connector requires an advanced configuration. Microsoft provides this connector with limited support. Configuring this connector requires familiarity with Microsoft Identity Manager and the specific LDAP directory.

    When you deploy this configuration in a production environment, collaborate with a partner such as Microsoft Consulting Services for help, guidance, and support.