---
layout: Conceptual
title: 'Tutorial: Set up the Private Network Connector - Microsoft Entra Private Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-private-access-connector-setup
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to install and configure the Private Network Connector for Microsoft Entra Private Access, verify registration, and organize connector groups.
ms.topic: tutorial
ms.date: 2026-03-11T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: aa2daa67-8518-8b2d-555a-d0e7fafba3ee
document_version_independent_id: aa2daa67-8518-8b2d-555a-d0e7fafba3ee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-private-access-connector-setup.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-private-access-connector-setup
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-private-access-connector-setup.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 05783d2f-4630-c4bd-5396-cd0f9b189d8e
---

# Tutorial: Set up the Private Network Connector - Microsoft Entra Private Access | Microsoft Learn

This tutorial establishes the foundation for the remaining Private Access tutorials by confirming your prerequisite setup, installing the Private Network Connector on a server, validating registration in the portal, and moving the connector into a dedicated connector group.

In this tutorial, you learn how to:

- Confirm environment and prerequisites
- Install Private Network Connector software on the server
- Verify connector registration in the Microsoft Entra admin center
- Create a new connector group
- Move the connector out of the default group

## Sample walkthrough video

This video covers most steps across the Private Access tutorials including connector installation, configuration of Quick Access, Private DNS, app segmentation, and client connectivity.

## Background

Before enabling Microsoft Entra Private Access policies, you should validate your test environment and deploy at least one Private Network Connector. The connector is the outbound bridge between Microsoft's service edge and your internal resources.

## Key concepts

Tip

**Why connector setup matters:** The Private Network Connector enables secure access to private resources without exposing inbound ports.

- Connector servers initiate outbound connections to Microsoft.
- Connector groups let you control routing and segment applications by environment.
- Using a dedicated Connector group helps prevent unintended connectivity problems while simplifying future app segmentation and troubleshooting.

### Step 1: Confirm environment and prerequisites

1. Validate your server meets the [minimum requirements](how-to-configure-connectors#windows-server) such as .NET and TLS versions.
2. Confirm the server can access the [required outbound URLs](how-to-configure-connectors#allow-access-to-urls) on ports 80 and 443.
3. Confirm your connector server can reach the target private resource (for example, a file share or internal web app) and can resolve DNS for the target resource.

Important

You need both components before proceeding: (1) a connector server and (2) at least one private resource that the connector server can reach.

### Step 2: Install Private Network Connector software

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as a **Global Secure Access Administrator**.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Connectors and sensors**.
3. Select **Download connector service**.
4. Copy the downloaded package to your connector server (if you didn't download it directly).
5. On the connector server, run the installer with local administrator privileges.
6. Complete sign-in when prompted using an account with the Global Admin role.

Note

You only need Global Admin to register the first Private Network Connector in a tenant. Subsequent connector registrations can be done with the Application Admin role.

1. Wait for installation and registration to complete.
2. Run the Connector Diagnostics to verify proper connectivity and function.
    - Default location is `C:/Program Files/Microsoft Entra Private Network Connector/ConnectorDiagnosticsTool.exe`.

![Screenshot that shows connector health check results with successful connectivity.](media/tutorial-private-access-connector-setup/connector-health-check.png)

### Step 3: Verify connector registration in the Microsoft Entra admin center

1. Return to **Global Secure Access** &gt; **Connect** &gt; **Connectors and sensors**.
2. Confirm your newly installed connector appears in the connector list.
3. Verify connector health/status shows as **Active**.
4. Open the connector details and confirm key metadata such as:
    - Machine Name
    - External IP
    - Version

Note

Newly registered connectors typically become visible in the portal within a couple of minutes but can take up to 10 minutes. Refresh the page if the connector doesn't appear immediately.

### Step 4: Create a new connector group

1. In **Global Secure Access** &gt; **Connect** &gt; **Connectors and sensors**, select **New Connector Group**.
2. Enter a name such as `PA-Tutorial-Connectors`.
3. Open the **Connectors** menu and check the box for the connector you just installed.
4. Select the appropriate Country/Region.
5. Select **Save**.

Tip

You've now moved your new connector out of the default group. Newly added connector servers are always initially added to the default group. For this reason, it's best practice to *not* use it for application traffic. Newly added servers would immediately start serving traffic requests but might not have line of sight to the resource.

Note

Private Network Connectors support multi-geo configuration which allows traffic to be routed using the Microsoft Entra SSE backend that is regionally closer to the application. If you do not specify a Country/Region for the connector group it will use the tenant default which could impact network performance. Note that Quick Access does not support multi-geo and is always routed to the same regional backend as the tenant.

![Diagram that illustrates how Multi-Geo support routes traffic with Microsoft Entra private network connectors.](media/tutorial-private-access-connector-setup/multi-geo-connector-routing.png)

## What you learned

In this exercise, you accomplished the following:

- **Validated your Private Access foundation** - You confirmed server/resource prerequisites.
- **Installed and registered a Private Network Connector** - You established the path for private app access without opening any inbound ports to your network.
- **Verified connector health in the Microsoft Entra admin center** - You confirmed the service can manage and monitor your connector.
- **Implemented connector group organization** - You created a custom connector group and moved the connector out of the Default connector group.

Connector readiness is a hard dependency for successful private resource access in all remaining tutorials.