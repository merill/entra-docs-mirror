---
layout: Conceptual
title: 'Quickstart: Install the Windows client to acquire Microsoft traffic - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/quickstart-install-client
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to Install the Windows client to acquire Microsoft traffic in Global Secure Access.
ms.topic: quickstart
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0b268c46-d891-922a-8325-e2717bc25e1a
document_version_independent_id: 0b268c46-d891-922a-8325-e2717bc25e1a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/quickstart-install-client.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/quickstart-install-client
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/quickstart-install-client.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 24c34086-5c0c-f699-ca4d-f414d5d4558e
---

# Quickstart: Install the Windows client to acquire Microsoft traffic - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Internet Access isolates the traffic for Microsoft applications and resources, such as Exchange Online and SharePoint Online. Users can access these resources by connecting to the Global Secure Access client or through a remote network, such as in a branch office location.

This quickstart shows you the steps needed to install the client and start acquiring Microsoft traffic. For more information about Global Secure Access, see [What is Global Secure Access?](overview-what-is-global-secure-access)

## Prerequisites

Administrators who interact with **Global Secure Access** features must have the [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference). Some features might also require other roles.

To follow the [Zero Trust principle of least privilege](/en-us/security/zero-trust/), consider using [Privileged Identity Management (PIM)](/en-us/azure/active-directory/privileged-identity-management/pim-configure) to activate just-in-time privileged role assignments.

The product requires licensing. For details, see the licensing section of [What is Global Secure Access?](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Install the client to acquire Microsoft traffic

[![Diagram of the basic Microsoft Entra Internet Access traffic flow.](media/quickstart-install-client/internet-access-basic-option.png)](media/quickstart-install-client/internet-access-basic-option.png#lightbox)

1. [Enable the Microsoft traffic forwarding profile](how-to-manage-microsoft-profile).
2. [Install and configure the Global Secure Access Client on end-user devices](how-to-install-windows-client).
3. [Enable universal tenant restrictions](how-to-universal-tenant-restrictions).
4. [Enable enhanced Global Secure Access signaling and Conditional Access](how-to-compliant-network).

After you complete these four steps, users with the Global Secure Access client installed on their Windows device can securely access Microsoft resources from anywhere. Conditional Access policy requires users to use the Global Secure Access client or a configured remote network, when they access Exchange Online and SharePoint Online.