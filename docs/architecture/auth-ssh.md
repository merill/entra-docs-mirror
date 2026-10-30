---
layout: Conceptual
title: SSH authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-ssh
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Get architectural guidance on achieving SSH integration with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ms.subservice: architecture
locale: en-us
document_id: bbc788cf-2460-3a99-a770-796471df0293
document_version_independent_id: b84f1579-fd1b-f0e4-a46a-27ba15a58baa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-ssh.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-ssh
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-ssh.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ba3832af-a2a0-64ba-c2b0-64bf542d1483
---

# SSH authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Secure Shell (SSH) is a network protocol that provides encryption for operating network services securely over an unsecured network. It's commonly used in systems like Unix and Linux. SSH replaces the Telnet protocol, which doesn't provide encryption in an unsecured network.

Microsoft Entra ID provides a virtual machine (VM) extension for Linux-based systems that run on Azure. It also provides a client extension that integrates with the [Azure CLI](/en-us/cli/azure/) and the OpenSSH client.

You can use SSH authentication with Active Directory when you're:

- Working with Linux-based VMs that require remote command-line sign-in.
- Running remote commands in Linux-based systems.
- Securely transferring files in an unsecured network.

## Components of the system

The following diagram shows the process of SSH authentication with Microsoft Entra ID:

![Diagram of Microsoft Entra ID with the SSH protocol.](media/authentication-patterns/ssh-auth.png)

The system includes the following components:

- **User:** The user starts the Azure CLI and the SSH client to set up a connection with the Linux VMs. The user also provides credentials for authentication.
- **Azure CLI:** The user interacts with the Azure CLI to start a session with Microsoft Entra ID, request short-lived OpenSSH user certificates from Microsoft Entra ID, and start the SSH session.
- **Web browser:** The user opens a browser to authenticate the Azure CLI session. The browser communicates with the identity provider (Microsoft Entra ID) to securely authenticate and authorize the user.
- **OpenSSH client:** The Azure CLI (or the user) uses the OpenSSH client to start a connection to the Linux VM.
- **Microsoft Entra ID:** Microsoft Entra authenticates the identity of the user and issues short-lived OpenSSH user certificates to the Azure CLI client.
- **Linux VM:** The Linux VM accepts the OpenSSH user certificate and provides a successful connection.