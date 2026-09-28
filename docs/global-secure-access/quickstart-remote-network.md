---
layout: Conceptual
title: 'Quickstart: Create a remote network, apply Conditional Access, and review the logs - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/quickstart-remote-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to Create a remote network, apply Conditional Access, and review the logs in Global Secure Access.
ms.topic: quickstart
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 71688f8a-c580-25bb-3961-05bd61a9321f
document_version_independent_id: 71688f8a-c580-25bb-3961-05bd61a9321f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/quickstart-remote-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/quickstart-remote-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/quickstart-remote-network.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 681c12db-079e-afc0-5779-494fef773f52
---

# Quickstart: Create a remote network, apply Conditional Access, and review the logs - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Internet Access isolates the traffic for Microsoft applications and resources, such as Exchange Online and SharePoint Online. Users can access these resources by connecting to the Global Secure Access client or through a remote network, such as in a branch office location.

This quickstart shows you the steps needed to create a remote network and start acquiring Microsoft traffic. For more information about Global Secure Access, see [What is Global Secure Access?](overview-what-is-global-secure-access)

## Prerequisites

Administrators who interact with **Global Secure Access** features must have the [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference). Some features might also require other roles.

To follow the [Zero Trust principle of least privilege](/en-us/security/zero-trust/), consider using [Privileged Identity Management (PIM)](/en-us/azure/active-directory/privileged-identity-management/pim-configure) to activate just-in-time privileged role assignments.

The product requires licensing. For details, see the licensing section of [What is Global Secure Access?](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Create a remote network, apply Conditional Access, and review the logs

[![Diagram of the Microsoft Entra Internet Access traffic flow with remote networks and Conditional Access.](media/quickstart-remote-network/internet-access-remote-networks-option.png)](media/quickstart-remote-network/internet-access-remote-networks-option.png#lightbox)

1. [Create a remote network](how-to-manage-remote-networks).
2. [Target the Microsoft traffic profile with Conditional Access policy](how-to-target-resource-microsoft-profile).
3. [Review the Global Secure Access logs](concept-global-secure-access-logs-monitoring).

After you complete these optional steps, users can connect to Microsoft services without the Global Secure Access client if they're connecting through the remote network you created *and* if they meet the conditions you added to the Conditional Access policy.