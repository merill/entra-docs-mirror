---
layout: Conceptual
title: 'Quickstart: Configure per-app access to private resources - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/quickstart-per-app-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure per-app access to private resources in Global Secure Access.
ms.topic: quickstart
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f93b337c-3d83-c9d8-43b6-180084bcf957
document_version_independent_id: f93b337c-3d83-c9d8-43b6-180084bcf957
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/quickstart-per-app-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/quickstart-per-app-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/quickstart-per-app-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 685a8d51-c4a9-fb37-b659-26a320806208
---

# Quickstart: Configure per-app access to private resources - Global Secure Access | Microsoft Learn

## Overview

This quickstart shows you the steps needed to configure per-app access to private resources. For more information about Global Secure Access, see [What is Global Secure Access?](overview-what-is-global-secure-access)

## Prerequisites

Administrators who interact with **Global Secure Access** features must have the [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference). Some features might also require other roles.

To follow the [Zero Trust principle of least privilege](/en-us/security/zero-trust/), consider using [Privileged Identity Management (PIM)](/en-us/azure/active-directory/privileged-identity-management/pim-configure) to activate just-in-time privileged role assignments.

The product requires licensing. For details, see the licensing section of [What is Global Secure Access?](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Configure per-app access to private resources

Create specific private apps for granular segmented access to private access resources using Microsoft Entra Private Access.

[![Diagram of the Global Secure Access app traffic flow for private resources.](media/quickstart-per-app-access/private-access-diagram-global-secure-access.png)](media/quickstart-per-app-access/private-access-diagram-global-secure-access.png#lightbox)

1. [Configure a private network connector and connector group](how-to-configure-connectors).
2. [Create a private Global Secure Access application](how-to-configure-per-app-access).
3. [Enable the Private Access traffic forwarding profile](how-to-manage-private-access-profile).
4. [Install and configure the Global Secure Access Client on end-user devices](how-to-install-windows-client).

After you complete these steps, users with the Global Secure Access client installed on a Windows device can connect to your private resources through a Global Secure Access app and private network connector.

Optionally:

- [Secure Quick Access applications with Conditional Access policies](how-to-target-resource-private-access-apps).
- [Review the Global Secure Access logs](concept-global-secure-access-logs-monitoring).