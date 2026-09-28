---
layout: Conceptual
title: Manage agent identity blueprints in the Microsoft Entra admin center - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/manage-agent-blueprint
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to manage agent identity blueprints in the Microsoft Entra admin center, including viewing permissions, managing credentials, and configuring owners and sponsors.
ms.date: 2026-04-27T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: alamaral
locale: en-us
document_id: 429adc79-5a59-d730-4372-f3b897478ebc
document_version_independent_id: 429adc79-5a59-d730-4372-f3b897478ebc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/manage-agent-blueprint.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/manage-agent-blueprint
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/manage-agent-blueprint.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: d96e2771-fba7-fffc-2f15-750be41f2938
---

# Manage agent identity blueprints in the Microsoft Entra admin center - Microsoft Entra Agent ID | Microsoft Learn

The Microsoft Entra admin center allows you to view all agent identity blueprint principals in your tenant. You can search, filter, sort, and manage blueprint principals including their credentials, permissions, and owners.

## Navigate to the agent identity blueprint list

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent blueprints**.
3. Select a blueprint principal to open its management page.

## Search and filter blueprints

1. Enter the **name** or **object ID** of the blueprint principal in the search box.
2. To look up a blueprint by its **Blueprint Application ID**, select **Add filters** and add the **Blueprint App ID** filter.
3. You can further refine the list using filters based on various criteria.

## Select viewing options

To customize your view, select **Choose columns** to configure which columns are shown. The available columns are:

| Column Name | Description | Sortable | Filterable | Special notes |
| --- | --- | --- | --- | --- |
| **Name** | Display name of the agent identity blueprint principal | ✓ | ✓ | Primary search field; clickable to view details of the agent identity blueprint principal |
| **Agent identities** | The number of child agent identities created by the agent blueprint principal | ✗ | ✗ | Select this to see a list of linked child agent identities for that agent identity blueprint principal |
| **Status** | Current operational state (Active, or Disabled) | ✓ | ✓ |  |
| **Blueprint Application ID** | Unique identifier for the agent identity blueprint of this agent identity blueprint principal | ✗ | ✓ |  |
| **Object ID** | Unique identifier for agent blueprint principal | ✗ | ✓ |  |

## View linked agent identities

View the agent identities that were created from a blueprint.

1. From the blueprint's management page, select **Linked agent identities** from the left menu.
2. The list shows each linked identity with its **Name**, **Status**, **View Access** link, and **Owners and Sponsors**.
3. Select an identity name to navigate to its detail page.
4. Use **Add filters** to refine the list.

## View granted permissions

Review the permissions assigned to a blueprint principal, organized by consent type.

1. From the blueprint's management page, select **Granted permissions** under **Access**.
2. Select the **Admin consent** tab to view permissions granted through administrator consent, or select the **User consent** tab to view permissions granted through user consent.
3. The list shows the **API name**, **Claim value**, **Permission**, **Type**, **Granted through**, and **Granted by** for each permission entry.

## View the manifest

To view or edit the raw JSON manifest for the agent identity blueprint, select **Manifest** under **Developer settings** from the blueprint's management page.

Note

The manifest editor is currently in preview.

## Manage credentials

Configure the credentials that agent identities use to authenticate. The credentials page has three tabs for different credential types.

[![Screenshot of the blueprint credentials page showing three tabs for certificates, client secrets, and federated credentials.](media/manage-agent-blueprint/blueprint-credentials-page.png)](media/manage-agent-blueprint/blueprint-credentials-page.png#lightbox)

Important

To best align with Zero Trust principles, use federated credentials or certificates instead of client secrets.

### Upload a certificate

1. From the blueprint's management page, select **Credentials** under **Developer settings**.
2. Select the **Certificates** tab.
3. Select **Upload certificate**.
4. Browse to and select the certificate file, and optionally add a description.
5. Select **Add**.

### Create a client secret

1. From the blueprint's management page, select **Credentials** under **Developer settings**.
2. Select the **Client secrets** tab.
3. Select **New client secret**.
4. Enter a **Description** for the secret.
5. Select an expiration period under **Expires**. For custom expiration, set the **Start** and **End** dates.
6. Select **Add**.
7. Copy the secret **Value** immediately. The value isn't displayed again after you leave the page.

Note

Your tenant policy might limit the maximum lifetime for client secrets.

### Add a federated credential

Federated credentials use workload identity federation to establish trust between Microsoft Entra and external identity providers without storing secrets. For more information about these scenarios and how workload identity federation works, see [Workload identity federation](/en-us/entra/workload-id/workload-identity-federation).

Take the following steps to add a federated credential for an agent identity blueprint principal.

1. From the blueprint's management page, select **Credentials** under **Developer settings**.
2. Select the **Federated credentials** tab.
3. Select **Add credential**.
4. Under **Federated credential scenario**, select a scenario:
    - **Managed Identity** — Configure a managed identity to get tokens and access resources across tenants.
    - **GitHub Actions deploying Azure resources** — Configure a GitHub workflow to get tokens and deploy to Azure.
    - **Kubernetes accessing Azure resources** — Configure a Kubernetes service account to get tokens and access Azure resources.
    - **Other issuer** — Configure an identity managed by an external OpenID Connect provider.
5. Complete the required fields for the selected scenario.
6. Select **Add**.

## Manage owners and sponsors

Owners and sponsors help establish governance for your blueprint. From the **Owners and sponsors** page in the left menu, you can manage ownership for both the agent blueprint and the agent blueprint principal.

For detailed steps on adding, removing, and managing owners and sponsors, see [Add and manage owners and sponsors for agent identities and blueprints](manage-owners-sponsors-agents).

## View audit and sign-in logs

You can view logs for both the agent blueprint principal and the blueprint itself from the blueprint's management page.

### Agent blueprint principal activity

The agent blueprint principal supports both audit and sign-in logs:

- To view administrative actions taken on the blueprint principal, select **Audit logs** from the left menu under **Agent blueprint principal activity**.
- To view sign-in activity for the blueprint principal, select **Sign-in logs** from the left menu under **Agent blueprint principal activity**. For more information, see [view sign-in logs for agents](sign-in-audit-logs-agents).

### Agent blueprint activity

The agent blueprint supports only audit logs:

- To view administrative actions related to the blueprint configuration, select **Audit logs** from the left menu under **Agent blueprint activity**.

## Disable an agent identity blueprint principal

To disable an agent identity blueprint principal, select the **Disable** button in the command bar at the top of the blueprint's overview page. A confirmation dialog appears warning that existing agent identities created from this blueprint **will no longer be able to authenticate**. Confirm the action to proceed.