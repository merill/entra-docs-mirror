---
layout: Conceptual
title: Entra Agent ID lifecycle policies - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/agent-lifecycle-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: chiragdayani
ms.author: chiragdayani
ms.service: entra-id-governance
manager: dougeby
description: Configure Microsoft Entra Agent ID lifecycle policies to automate lifecycle management of agent identities
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-10-06T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 03a6118d-c730-6376-bcc8-9977f98b5274
document_version_independent_id: 03a6118d-c730-6376-bcc8-9977f98b5274
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/agent-lifecycle-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/agent-lifecycle-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/agent-lifecycle-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
platformId: 3b69e8e8-bbe9-f3fc-3712-354bec72bc04
---

# Entra Agent ID lifecycle policies - Microsoft Entra ID Governance | Microsoft Learn

AI agent adoption is accelerating, resulting in a growing number of agent identities with access to critical resources. Without clear lifecycle controls, these identities can persist beyond their usefulness and introduce security risk. Keeping agent identities around when they are no longer needed can lead to security incidents, as forgotten identities can become easy targets for attackers, while agent identities without clear accountability may continue to retain access indefinitely. As organizations deploy more AI agents, these risks become amplified. Security and identity administrators therefore need automated lifecycle management to avoid agent proliferation to manage unmonitored, inactive and orphaned agent identities

Important

Agent ID lifecycle policy is in preview. Preview features are provided without a service-level agreement and aren't recommended for production workloads. Certain features might not be supported or might have limited capabilities.

## Prerequisites

### License requirements

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

### Roles

One of the following roles:

- [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator)
- [AI Administrator](../identity/role-based-access-control/permissions-reference#ai-administrator)

## Create an agent lifecycle policy

Create a policy to define which agent identities should be evaluated and what happens when an agent identity doesn't meet an enabled rule.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator) or [AI Administrator](../identity/role-based-access-control/permissions-reference#ai-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle Workflows** &gt; **Lifecycle Policies** &gt; **Agent IDs**.
3. Select **New policy**.
4. Enter a unique policy name and description.
5. Enable the lifecycle policy.
6. Select the scope of agent identities that needs to be governed by the policy.
7. Configure one or more lifecycle rules:
    - Periodic reconfirmation
    - Minimum sponsor requirement
    - Inactivity monitoring
8. Choose a policy action and, if needed, configure a grace period.
9. Review the notification behavior.
10. Optionally, add one or more fallback recipients to receive lifecycle notifications when an agent identity has no accountable representative, such as a sponsor or owner.
11. Review the configuration, and then select **Save**.
12. If multiple Agent ID lifecycle policies exist, configure the policy priority.

After you create the policy, our system periodically evaluates the agent identities within its scope. When an agent identity violates any enabled lifecycle policy rule, the identity enters the configured notification and enforcement process.

## Configure lifecycle rules

Each Agent ID lifecycle policy can contain one or more rules. Configure the rules that represent your organization's requirements for continued use and accountability.

### Configure periodic reconfirmation

Use periodic reconfirmation to verify that an agent identity is still needed.

1. Enable **Periodic reconfirmation**.
2. Configure the reconfirmation frequency i.e. how often sponsor or owner must re-confirm that the agent identity is still required (between 30 and 730 days).

If the agent identity isn't reconfirmed within the configured timeframe, the configured policy actions trigger so that the accountable representatives can take action via the Manage Agents experience (`https://myaccount.microsoft.com/agents`)

### Configure minimum sponsor requirements

Use the minimum sponsor requirement to ensure that each agent identity has clear accountability.

1. Enable **Minimum sponsor requirement**.
2. Specify the minimum number of sponsors required for each agent identity.

If an agent identity has fewer than the configured number of sponsors, the configured policy actions trigger, so that the available accountable representatives can take action to add / update the sponsors via the Manage Agents experience (`https://myaccount.microsoft.com/agents`), to ensure the agent identity is not disabled / deleted. In case the agent identity has no accountability, then the fallback recipient is notified.

### Configure inactivity monitoring

Use inactivity monitoring to identify stale and unused agent identities.

1. Enable **Inactivity monitoring**.
2. Specify the inactivity duration.
3. Define how long an agent identity can remain inactive before the configured policy actions are triggered.

If an agent identity has been inactive for more than the configured duration i.e. no tokens have been issued for the identity during that time, the configured policy actions trigger, so that the accountable representatives can take appropriate action.

## Configure policy actions

Policy actions define what actions can be taken when an agent identity does not satisfy the policy requirements

| Action | Result |
| --- | --- |
| **Disable** | Disables the agent identity and prevents future sign-ins or usage. |
| **Delete** | Soft Deletes the agent identity. |
| **Disable and delete** | Disables the agent identity immediately and then deletes it after the configurable grace period. |

1. Select the action that should be taken for the agent identities which do not fulfill the organizational policy rules.
2. If you select **Disable and delete**, specify the number of days when delete action triggers after the disablement is completed.
3. To give accountable representatives time to remediate a policy violation, enable the grace period and specify its duration.
4. Review the selected action before you create or update the policy.

## Configure notifications

Notifications inform accountable representatives which lifecycle policy rule was violated by an agent identity and which policy action will be triggered if the required action is not executed.

1. Review the notifications sent to sponsors, owners, or other accountable representatives.
2. Add one or more fallback recipients when notifications need to reach someone if an agent identity has no sponsor or owner.
3. Confirm that the notification schedule gives recipients enough time to remediate the violation before the disable / delete action is triggered.

If the violation isn't remediated within the configured timeframe, Lifecycle Workflows automatically executes the policy action.

## Set policy priority

You can create multiple agent identity lifecycle policies with different scopes, rules, and actions. Policy priority determines which policy applies when an agent identity is included in more than one policy.

1. Open the list of agent identity lifecycle policies.
2. Review policies with overlapping agent identity scopes.
3. Move the policy that should take precedence above the other matching policies.
4. Review the scopes again before you enable broad enforcement.

The highest-priority matching policy applies to the agent identity.

## Verify the policy

Validate the policy with a limited set of test agent identities before you apply it broadly.

1. Select **Specific agents** as the policy scope.
2. Add a small set of test agent identities.
3. For periodic reconfirmation testing, use the minimum allowed frequency of 30 days.
4. Confirm that sponsors or other configured recipients receive the expected notifications.
5. In the [Manage Agents experience](https://myaccount.microsoft.com/agents), verify that a sponsor can reconfirm/ extend, or disable the agent identity.
6. Any unremediated violation results in the configured policy action after the applicable timeframe and grace period.

## How policy enforcement works

Lifecycle policy uses the following process to evaluate and enforce an agent identity lifecycle policy:

1. **Scope evaluation:** identifies the agent identities included in the policy scope.
2. **Rule evaluation:** evaluates each enabled policy rule. An agent identity becomes noncompliant when it violates any enabled rule.
3. **Notification:** notifies the applicable sponsors, owners, or fallback recipients.
4. **Enforcement:** If the violation isn't remediated within the configured timeframe, Lifecycle Workflows disables, deletes, or disables and then deletes the agent identity according to the policy configuration.

| Rule violation | Notification recipient | Action Required |
| --- | --- | --- |
| Reconfirmation overdue | Sponsor or owner or fallback recipient | Disable if no longer needed or reconfirm that the agent identity is still required by clicking on 'Extend' in Manage Agents experience |
| Minimum sponsor requirement not met | Sponsor or owner or fallback recipient | Update sponsors in Manage Agents experience |
| Inactive beyond the configured threshold | Sponsor or accountable representative | Disable if no longer needed or make it active by interacting with it |