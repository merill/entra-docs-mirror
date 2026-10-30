---
layout: Conceptual
title: How to access an Azure Storage account behind Azure Private Link using Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-use-private-link-with-private-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure Microsoft Entra Private Access to securely connect remote users to Azure Storage accounts through Azure Private Link. Covers prerequisites, Quick Access application setup, and connectivity verification.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 489b8c82-8a6d-25fc-a95a-bd36b612c01d
document_version_independent_id: 489b8c82-8a6d-25fc-a95a-bd36b612c01d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-use-private-link-with-private-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-use-private-link-with-private-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-use-private-link-with-private-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cd61cd-9ecf-429b-b494-91576c41f8e4
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://authoring-docs-microsoft.poolparty.biz/devrel/a9a12e3a-5d9d-4197-ad96-b826bc774b60
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/c4bdb33a-5524-4b66-b162-03f5621d7902
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://authoring-docs-microsoft.poolparty.biz/devrel/6dfd60ec-b0d6-48ef-9c74-057162ea03fb
platformId: f38a9f82-bdf4-0bfc-7b45-a95c5d6983f4
---

# How to access an Azure Storage account behind Azure Private Link using Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Private Access lets you extend the security features of Azure Private Link to remote and on-premises users. Extending the security features brings modern authentication features, such as Conditional Access, to the front of Azure Platform as a Service (PaaS) resources.

Azure Private Link lets you access Azure PaaS Services such as Azure Storage and Azure SQL Database. Azure Private Link also lets you access your Azure hosted services and partner services over a private endpoint in your virtual network. The result is that resources like virtual machines (VMs) can privately and securely communicate with Private Link resources.

For more information about Azure Private Link, see [What is Azure Private Link?](/en-us/azure/private-link/private-link-overview).

This article shows you how to use Microsoft Entra Private Access to access an Azure Storage account behind Azure Private Link.

[![Diagram showing the architecture of Azure Private Link using Microsoft Entra Private Access.](media/how-to-use-private-link-with-private-access/architecture-diagram.png)](media/how-to-use-private-link-with-private-access/architecture-diagram.png#lightbox)

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing.
    - The [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) role to manage the Global Secure Access features.
    - The [Conditional Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#conditional-access-administrator) to create and interact with Conditional Access policies.
- Set up a storage account behind Azure Private Link. To learn how to set up a storage account in Azure Private Link, see [Tutorial: Connect to a storage account using an Azure Private Endpoint](/en-us/azure/private-link/tutorial-private-endpoint-storage-portal). To learn more about private endpoints in Azure Private Link, see [What is a private endpoint?](/en-us/azure/private-link/private-endpoint-overview).
- Deploy a Microsoft Entra private network connector in a private virtual network. To learn how to deploy a connector, see [How to configure private network connectors for Microsoft Entra Private Access and Microsoft Entra application proxy](how-to-configure-connectors). To learn more about connectors, see [Understand the Microsoft Entra private network connector](concept-connectors). To learn more about connector groups, see [Understand Microsoft Entra private network connector groups](concept-connector-groups). To learn more about Azure Virtual Network, see [What is Azure Virtual Network?](/en-us/azure/virtual-network/virtual-networks-overview).

## Create a Global Secure Access application for the Azure storage account

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
3. Select **New application**.
4. Choose the right connector group with the connector deployed in the private virtual network.
5. Select **Add application segment**:
    - Destination type: `FQDN`
    - Fully Qualified Domain Name (FQDN): `<fqdn of the storage account>`. For example, `storage1.blob.core.windows.net`.
    - Ports: `443`
    - Protocol: `TCP`
6. Select **Apply** to add the application segment.
7. Select **Save** to save the application.
8. Assign users to the application.

[![Screenshot showing network access properties.](media/how-to-use-private-link-with-private-access/network-access-properties.png)](media/how-to-use-private-link-with-private-access/network-access-properties.png#lightbox)

## Validate the configuration

Ensure connectivity to the storage account works from the connector machine. The connector is deployed on the same private virtual network.

Check connections to the storage account from outside the private virtual network. Computers that don't have the Global Secure Access client installed should fail. Computers that have the Global Secure Access client installed should succeed.