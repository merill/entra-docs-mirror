---
layout: Conceptual
title: How to access Azure SQL with a service endpoint using Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-use-with-azure-sql-service-endpoint
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure direct connectivity between your virtual network and Azure SQL using service endpoints with Microsoft Entra Private Access for secure database access.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: e7f9f5c8-0f31-0555-7c9a-c28a40636e37
document_version_independent_id: e7f9f5c8-0f31-0555-7c9a-c28a40636e37
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-use-with-azure-sql-service-endpoint.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-use-with-azure-sql-service-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-use-with-azure-sql-service-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/20ed8455-bc18-4537-87a4-83784e7b2a39
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/9a7f703b-30bb-4d62-9eb4-97213f571849
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 5b069f09-0cda-1d8b-1451-389addc9a5bc
---

# How to access Azure SQL with a service endpoint using Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

## Overview

Access Azure services using Microsoft Entra Private Access with a virtual network service endpoint. The combination provides direct connectivity using an optimal network route. A virtual network service endpoint lets you limit network access to Azure service resources and remove access from the internet. Service endpoints provide a direct connection between your virtual network and supported Azure services. You use your virtual networks private address space to access the Azure services.

To learn more about virtual networks, see [What is Azure Virtual Network?](/en-us/azure/virtual-network/virtual-networks-overview).

This article shows you how to access Azure SQL with a service endpoint using Microsoft Entra Private Access.

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing.
    - The [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) role to manage the Global Secure Access features.
    - The [Conditional Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#conditional-access-administrator) to create and interact with Conditional Access policies.
- Azure SQL Server configured with service endpoint
- Microsoft Entra private network connector deployed in the service endpoint subnet. To learn how to deploy a connector, see [How to configure private network connectors for Microsoft Entra Private Access and Microsoft Entra application proxy](how-to-configure-connectors). To learn more about connectors, see [Understand the Microsoft Entra private network connector](concept-connectors). To learn more about connector groups, see [Understand Microsoft Entra private network connector groups](concept-connector-groups).

## Change Azure SQL Server connection policy to proxy

Since users are connecting from outside Azure, your Azure SQL server should have a connection policy of `proxy`. The `proxy` policy establishes the Transmission Control Protocol (TCP) session via the Azure SQL Database gateway and all subsequent packets flow via the gateway. 

To set the policy to `proxy`:

1. Sign in to the Azure portal and navigate to your SQL server.
2. In the left hand navigation under **Security**, select **Networking**.
3. On the **Connectivity** tab, set **Connection Policy** to `Proxy`.
4. Select **Save**.

[![Screenshot showing the connectivity tab on the networking page within Security section.](media/how-to-use-with-azure-sql-service-endpoint/networking-connectivity.png)](media/how-to-use-with-azure-sql-service-endpoint/networking-connectivity.png#lightbox)

## Create a Global Secure Access application for the Azure SQL server

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
3. Select **New application**.
4. Choose the right connector group with the connector deployed in the service endpoint subnet.
5. Select **Add application segment**:
    - Destination type: `FQDN`
    - Fully Qualified Domain Name (FQDN): `<fqdn of the SQL server>`. For example, `contosodbserver1.database.windows.net`.
    - Ports: `1433`
    - Protocol: `TCP`
6. Select **Apply** to add the application segment.
7. Select **Save** to save the application.
8. Assign users to the application.

## Validate the configuration

Ensure connectivity to the SQL server works from the connector machine. The connector is deployed on the service endpoint subnet.

Check connectivity to the SQL server from outside the service endpoint subnet. Computers that don't have the Global Secure Access client installed should fail. Computers that have the Global Secure Access client installed should succeed.