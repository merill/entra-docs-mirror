---
layout: Conceptual
title: Microsoft Entra Agent ID default inactivity policy - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/agent-default-inactivity-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: jawoods
ms.author: jawoods
ms.service: entra-id-governance
manager: dougeby
description: Configure the default Microsoft Entra Agent ID inactivity policy to disable inactive agent identities automatically
ms.topic: how-to
ms.date: 2026-10-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: cc89c21d-cc3b-ff53-47bd-ac68e0288157
document_version_independent_id: cc89c21d-cc3b-ff53-47bd-ac68e0288157
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/agent-default-inactivity-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../agent-id/toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/agent-default-inactivity-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/agent-default-inactivity-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 36819af4-dc90-2534-2a43-47169bce41fb
---

# Microsoft Entra Agent ID default inactivity policy - Microsoft Entra ID Governance | Microsoft Learn

To ensure the security and manageability of agent identities for Microsoft customers, Microsoft Entra Agent ID provides a default inactivity policy to all tenants. This policy identifies inactive agent identities, notifies relevant users, and then proceeds to disable the identity if no new activity is detected. Organizations can use this default policy to clean up inactive agent identities regardless of their licensing status.

The Agent ID default inactivity policy allows only limited customization. Customers who want to create custom lifecycle policies using additional policy rules and customization should ensure they have the appropriate license. More details here: [Agent lifecycle policies](/en-us/entra/id-governance/agent-lifecycle-policies)

Important

Agent ID lifecycle policies are in preview. Preview features are provided without a service-level agreement and aren't recommended for production workloads. Certain features might not be supported or might have limited capabilities.

## Prerequisites

### License requirements

No license is required to use the Agent ID default inactivity policy.

### Roles

One of the following roles:

- [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator)
- [AI Administrator](../identity/role-based-access-control/permissions-reference#ai-administrator)
- [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator)

## Enable the Agent ID default inactivity policy

Enable the default inactivity policy to notify owners and sponsors of inactive agent identities, then disable and delete the identities if the agents remain inactive.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using one of the supported roles listed above.
2. Browse to **ID Governance** &gt; **Lifecycle Workflows** &gt; **Lifecycle Policies** &gt; **Agent ID (Preview)**.
3. Select **Default Agent Identity Inactivity Lifecycle Policy**.
4. Select the **Policy Configuration** tab.
5. Toggle **Enable policy**.
6. Review the configuration, and then select **Save**.

Once the policy is enabled, Microsoft Entra Agent ID periodically evaluates the agent identities within its scope. When an agent identity has been inactive for 60 days, the identity enters the notification and enforcement process.

## Microsoft Entra Agent ID default policy behavior

Agent identities that are inactive and subject to the default inactivity policy will move through the following stages. The actions and timeframes are not customizable for default policy users.

| Days inactive | Action |
| --- | --- |
| 60 days | Notify the agent identity's sponsors and owners |
| 90 days | Disable the agent identity |
| 455 days | Delete the agent identity |

To return an agent to an active state, a user should interact with the agent or otherwise cause it to take action. Users cannot freely retain inactive agents that are subject to the inactivity policy without making them active.

Once an agent has been disabled or deleted, it can only be recovered by an owner or administrator. Sponsors are not authorized to reenable or restore agent identities.

## Configure the Agent ID default inactivity policy

Administrators can configure the default inactivity policy's scope and set fallback notification recipients.

### Policy scope

The default inactivity policy supports two scopes: **All Agent IDs** and **All Agent IDs except selected**.

- **All Agent IDs**: All agent identities are subject to the policy.
- **All Agent IDs except selected**: The admin can choose specific identities to exclude from the policy. These identities can remain inactive indefinitely.

Use the **All Agent IDs except selected** option if your organization needs to ensure that seasonal agents, limited-use agents, or other agents that aren't usually active won't be disabled.

To exclude specific agent identities from the policy, choose **All Agent IDs except selected**. Then, choose **+ Select Agent IDs**, select the needed agent identities in the list that appears, and then choose **Select**. Select **Save** to save the changes to the policy.

### Fallback notification recipients

Notifications inform accountable representatives when an agent identity has been inactive for at least 60 days. When sponsors or owners are available for the agent identity, they will be notified. If no sponsor or owner is present, the system will notify any fallback recipients provided by the administrator.

To provide a fallback recipient, enter one or more email addresses separated by spaces, commas, or semicolons and then select **Save**. Note that group mailboxes are supported.

## Policy priority

Customers with appropriate licenses can create multiple agent identity lifecycle policies with different scopes, rules, and actions. Policy priority determines which policy applies when an agent identity is included in more than one policy.

The default inactivity policy is always the last policy applied. Any active custom policies take precedence.

To learn more, see [Microsoft Entra Agent ID lifecycle policies](agent-lifecycle-policies).