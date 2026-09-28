---
layout: Conceptual
title: Disable pass-through authentication by using Microsoft Entra Connect or PowerShell - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta-disable-do-not-configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how to disable pass-through authentication by using the Microsoft Entra Connect Do Not Configure feature or by using PowerShell.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 7c2367c9-7da4-f611-1409-0a0c34ef5516
document_version_independent_id: 16dc4773-99da-784f-bf93-7b7eb7560852
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta-disable-do-not-configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta-disable-do-not-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta-disable-do-not-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 925ccd96-6441-611d-0225-b2407c3da601
---

# Disable pass-through authentication by using Microsoft Entra Connect or PowerShell - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to disable pass-through authentication by using Microsoft Entra Connect or PowerShell.

## Prerequisites

Before you begin, ensure that you have the following prerequisite.

- A Windows machine with pass-through authentication agent version 1.5.1742.0 or later installed. Any earlier version might not have the requisite cmdlets for completing this operation.

    If you don't already have an agent, you can install it.

    1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
    2. Download the latest Auth Agent.
    3. Install the feature by running either of the following commands.
        - `.\AADConnectAuthAgentSetup.exe`
        - `.\AADConnectAuthAgentSetup.exe ENVIRONMENTNAME=<identifier>`
            Important

            If you're using the Azure Government cloud, pass in the ENVIRONMENTNAME parameter with the following value:

            | Environment Name | Cloud |
            | --- | --- |
            | AzureUSGovernment | US Gov |
- An Azure Hybrid Identity Administrator account for running the PowerShell cmdlets.

## Use Microsoft Entra Connect

If you're using pass-through authentication with Microsoft Entra Connect, and it's set to **Do not configure**, you can disable the setting.

Note

If you already have password hash synchronization enabled, disabling pass-through authentication will result in a tenant fallback to password hash synchronization.

## Use PowerShell

In a PowerShell session, run the following cmdlets:

1. PS C:\Program Files\Microsoft Azure AD Connect Authentication Agent&gt; `Import-Module .\Modules\PassthroughAuthPSModule`
2. `Get-PassthroughAuthenticationEnablementStatus`
3. `Disable-PassthroughAuthentication`