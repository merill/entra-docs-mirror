---
layout: Conceptual
title: 'Quickstart: Configure Quick Access to private resources - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/quickstart-quick-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure Quick Access to private resources in Global Secure Access.
ms.topic: quickstart
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4d07c22d-b19f-cc22-deef-a2ce76a6320a
document_version_independent_id: 4d07c22d-b19f-cc22-deef-a2ce76a6320a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/quickstart-quick-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/quickstart-quick-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/quickstart-quick-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: baa98f94-b61c-3ab1-f3ad-d4825933f9bc
---

# Quickstart: Configure Quick Access to private resources - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Private Access provides a secure, zero-trust access solution for accessing internal resources without requiring a VPN. Configure Quick Access and enable the Private Access traffic forwarding profile to specify the sites and apps you want routed through Microsoft Entra Private Access. At this time, the Global Secure Access client must be installed on end-user devices to use Microsoft Entra Private Access, so that step is included in this section.

This quickstart shows you the steps needed to configure Quick Access to private resources. For more information about Global Secure Access, see [What is Global Secure Access?](overview-what-is-global-secure-access)

Note

Use Quick Access as a transition phase in your Zero Trust journey. After Quick Access has enabled you to replace your VPN, [configure per-app access](quickstart-per-app-access) to achieve application segmentation and per-app granular controls.

## Prerequisites

Administrators who interact with **Global Secure Access** features must have the [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference). Some features might also require other roles.

To follow the [Zero Trust principle of least privilege](/en-us/security/zero-trust/), consider using [Privileged Identity Management (PIM)](/en-us/azure/active-directory/privileged-identity-management/pim-configure) to activate just-in-time privileged role assignments.

The product requires licensing. For details, see the licensing section of [What is Global Secure Access?](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Configure Quick Access to private resources

Set up Quick Access for broader access to your network using Microsoft Entra Private Access.

[![Diagram of the Quick Access traffic flow for private resources.](media/quickstart-quick-access/private-access-diagram-quick-access.png)](media/quickstart-quick-access/private-access-diagram-quick-access.png#lightbox)

1. [Configure a Microsoft Entra private network connector and connector group](how-to-configure-connectors).
2. [Configure Quick Access to your private resources](how-to-configure-quick-access).
3. [Enable the Private Access traffic forwarding profile](how-to-manage-private-access-profile).
4. [Install and configure the Global Secure Access Client on end-user devices](how-to-install-windows-client).

After you complete these four steps, users with the Global Secure Access client installed on a Windows device can connect to private resources, through a Quick Access app and private network connector.