---
layout: Conceptual
title: Verify your version of cloud sync or connect sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/verify-sync-tool-version
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the steps to verify the version of the provisioning agent or connect sync.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: dfbbfe1a-7192-ae14-764e-1ccbd130545b
document_version_independent_id: 5cba21f3-9f28-ed39-3480-47a676655c6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/verify-sync-tool-version.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/verify-sync-tool-version
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/verify-sync-tool-version.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 37ed3dc4-a740-fb9b-5b30-adcb6e3f7c01
---

# Verify your version of cloud sync or connect sync - Microsoft Entra ID | Microsoft Learn

This article describes the steps to verify the installed version of the provisioning agent and connect sync.

## Verify the provisioning agent

To see what version of the provisioning agent you're using, use the following steps:

Agent verification occurs in the Azure portal and on the local server that runs the agent.

### Verify the agent in the Azure portal

To verify that Microsoft Entra ID registers the agent, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Select **Entra Connect**, and then select **Cloud Sync**.

    [![Screenshot that shows the Get started screen.](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png)](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png#lightbox)
3. On the **Cloud Sync** page, click **Agents** to see the agents that you installed. Verify that the agent appears and that the status is **active**.

### Verify the agent on the local server

To verify that the agent is running, follow these steps:

1. Sign in to the server with an administrator account.
2. Go to **Services**. You can also use *Start/Run/Services.msc* to get to it.
3. Under **Services**, make sure that **Microsoft Azure AD Connect Agent Updater** and **Microsoft Azure AD Connect Provisioning Agent** are present and that the status is **Running**.

    [![Screenshot that shows the Windows services.](../../includes/media/entra-cloud-sync-how-to-verify-installation/windows-services.png)](../../includes/media/entra-cloud-sync-how-to-verify-installation/windows-services.png#lightbox)

### Verify the provisioning agent version

To verify the version of the agent that's running, follow these steps:

1. Go to *C:\Program Files\Microsoft Azure AD Connect Provisioning Agent*.
2. Right-click *AADConnectProvisioningAgent.exe* and select **Properties**.
3. Select the **Details** tab. The version number appears next to the product version.

## Verify connect sync

To see what version of connect sync you're using, use the following steps:

### On the local server

To verify that the agent is running, follow these steps:

1. Sign in to the server with an administrator account.
2. Open **Services** either by navigating to it or by going to *Start/Run/Services.msc*.
3. Under **Services**, make sure that **Microsoft Entra ID Sync** is present and the status is **Running**.

### Verify the connect sync version

To verify the version of the agent that is running, follow these steps:

1. Navigate to 'C:\Program Files\Microsoft Azure AD Connect'
2. Right-click on **AzureADConnect.exe** and select **properties**.
3. Click the **details** tab and the version number ID next to the Product version.