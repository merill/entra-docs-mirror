---
layout: Conceptual
title: 'Microsoft Entra Connect cloud provisioning agent: Automatic upgrade - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-automatic-upgrade
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the built-in automatic upgrade feature in the Microsoft Entra Connect cloud provisioning agent.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: c00b19d2-b6f0-cb12-b1b3-66f19ab70eb0
document_version_independent_id: be18a118-49a4-47a5-b890-7c12ebb42581
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-automatic-upgrade.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-automatic-upgrade
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-automatic-upgrade.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 69627f58-a7c6-f3c2-dcfe-aec498c58894
---

# Microsoft Entra Connect cloud provisioning agent: Automatic upgrade - Microsoft Entra ID | Microsoft Learn

Making sure your Microsoft Entra Connect cloud provisioning agent installation is always up to date is easy with the automatic upgrade feature.

The agent is installed here: "Program files\Azure AD Connect Provisioning Agent\AADConnectProvisioningAgent.exe"

To verify your version, right-click the executable and select properties and then details.

![Agent file version](media/how-to-automatic-upgrade/agent-1.png)

The agent updater is installed here: "Program files\Azure AD Connect Provisioning Agent Updater\AzureADConnectAgentUpdater.exe"

To verify your version, right-click the executable and select properties and then details.

![Agent updater version](media/how-to-automatic-upgrade/agent-2.png)

## Uninstall the agent

To remove the agent, go to **Uninstall or change a program** and uninstall the following:

- **Microsoft Entra Connect Agent Updater**
- **Microsoft Entra Provisioning Agent**
- **Microsoft Entra Provisioning Agent Package**

![Agent removal](media/how-to-automatic-upgrade/agent-3.png)