---
layout: Conceptual
title: Secure autonomous agents with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-autonomous-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: gracenagy
ms.author: gracenagy
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to configure Microsoft Entra Conditional Access policies for autonomous agents that access resources with their own agent identities.
ms.topic: how-to
ms.date: 2026-07-31T00:00:00.0000000Z
ms.reviewer: kvenkit
ms.custom: msecd-doc-authoring-1017
ai-usage: ai-assisted
locale: en-us
document_id: bb81c071-d6b5-c30d-8ea4-8afa59f35db5
document_version_independent_id: bb81c071-d6b5-c30d-8ea4-8afa59f35db5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-autonomous-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-autonomous-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-autonomous-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 73af9332-56a4-c076-915e-b8a4803abc21
---

# Secure autonomous agents with Conditional Access - Microsoft Entra ID | Microsoft Learn

Use Conditional Access to control access for autonomous agents that authenticate with their own agent identity and no signed-in user. This access pattern includes agents that run in the background, respond to events, run on a schedule, or are published for public use without delegated user context.

In this access pattern, the access token's subject is the agent identity. Conditional Access policies therefore target the agent identity, not a user or an agent's user account.

Before you start, review the licensing, role, and agent setup requirements.

## Prerequisites

- A Microsoft Entra ID P1 or P2 license.
- Agent 365 license will soon be required
- At least the [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) role.
- At least one agent identity registered in your tenant.
- The agent uses the [autonomous app OAuth flow](../../agent-id/agent-autonomous-app-oauth-flow).

Important

Before configuring a Conditional Access policy, read the [Conditional Access for agents](agent-id) article. It covers the authentication, service boundaries, and limitations to ensure you cover all scenarios and your corporate data and services are well protected.

## Allow only specific agents to access resources

Create a block policy that excludes approved agent identities or agent identity blueprints. Start in report-only mode so you can review the policy's effect before you enforce it. You can do this by tagging agents and resources with [custom security attributes](/en-us/entra/fundamentals/custom-security-attributes-overview) targeted in your policy, or by manually selecting them using the enhanced object picker.

# [Use the enhanced object picker](#tab/use-the-enhanced-object-picker)
### Create Conditional Access policy using the enhanced object picker

Organizations can create a Conditional Access policy using the enhanced object picker to block all agents except those reviewed and approved by your organization.

The enhanced object picker replaces the previous flat list experience in both the assignment and target resources sections of policy configuration. The new experience is meant to simplify the selection of items you want to scope in the policy.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users, agents or workload identities**.
    1. Under **What does this policy apply to?**, select **Agents**.
        1. Under **Include**, select **All agent identities**.
        2. Under **Exclude**:
            1. Select **Select individual agent identities**.
            2. Using the enhanced object picker, switch between the **All**, **Agent blueprint principals**, and **Agent identities** tabs to select the individual agent blueprints, agent identities, or both that you want to exclude.
            3. Select **Select**.
6. Under **Target resources**:
    1. Under **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Access controls** &gt; **Grant**:
    1. Select **Block**.
    2. Select **Select**.
8. Confirm your settings, and set **Enable policy** to **Report-only**.
9. Select **Create** to create your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

For more information about assignment options and the object picker, see [Target agent identities in Conditional Access policies](howto-target-agent-identities).

# [Use custom security attributes](#tab/use-custom-security-attributes)
### Create Conditional Access policy using custom security attributes

The recommended approach for creating this policy is to create and assign custom security attributes to each agent or agent blueprint, then target those attributes with a Conditional Access policy. This approach uses steps similar to those documented in [Filter for applications in Conditional Access policy](concept-filter-for-applications). You can assign attributes across multiple attribute sets to an agent or cloud application.

#### Create and assign custom attributes

1. Create the custom security attributes:
    1. Create an **Attribute set** named *AgentAttributes*.
    2. Create a **New attribute** named *AgentApprovalStatus* that has **Allow multiple values to be assigned** and **Only allow predefined values to be assigned**selected.
        1. Add the following predefined values: **New**, **In\_Review**, **HR\_Approved**, **Finance\_Approved**, and **IT\_Approved**.
2. Create another attribute set to group resources that your agents are allowed to access:
    1. Create an **Attribute set** named *ResourceAttributes*.
    2. Create a **New attribute** named *Department* that has **Allow multiple values to be assigned** and **Only allow predefined values to be assigned**selected.
        1. Add the following predefined values: **Finance**, **HR**, **IT**, **Marketing**, and **Sales**.
3. Assign the appropriate value to resources that your agent is allowed to access. For example, you might want only agents that are **HR\_Approved** to access resources tagged **HR**.

#### Create Conditional Access policy

After you complete the previous steps, create a Conditional Access policy using custom security attributes to block all agents except those reviewed and approved by your organization.

After you complete the previous steps, create a Conditional Access policy using custom security attributes to block all agents except those reviewed and approved by your organization.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users, agents or workload identities**.
    1. Under **What does this policy apply to?**, select **Agents**.
        1. Under **Include**, select **All agent identities**.
        2. Under **Exclude**:
            1. Select **Select agent identities based on attributes**.
            2. Set **Configure** to **Yes**.
            3. Select the attribute you created earlier, **AgentApprovalStatus**.
            4. Set **Operator** to **Contains**.
            5. Set **Value** to **HR\_Approved**.
            6. Select **Done**.
6. Under **Target resources**:
    1. Under **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Access controls** &gt; **Grant**:
    1. Select **Block**.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to create your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

---

## Block high-risk agent identities

Create a policy that blocks high-risk agent identities, based on [signals from Microsoft Entra ID Protection](/en-us/entra/id-protection/concept-risky-agents), from organizational resources. For details on risk detection types and response actions for agents, see [Identity Protection for agents](/en-us/entra/id-protection/concept-risky-agents). Agent risk is in Preview.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Enter a name for the policy.
5. Under **Assignments**, select **Users, agents or workload identities**.
    1. Under **What does this policy apply to?**, select **Agents**.
        1. Under **Include**, select **All agent identities**.
6. Under **Target resources** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Agent risk (Preview)**, set **Configure** to **Yes**.
    1. Under **Configure agent risk levels needed for policy to be enforced**, select **High**. This guidance is based on Microsoft recommendations and might be different for each organization.
8. Under **Access controls** &gt; **Grant**, select **Block**, and then select **Select**.
9. Set **Enable policy** to **Report-only**.
10. Select **Create**.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

For details about agent risk detections, see [Microsoft Entra ID Protection and agents](../../id-protection/concept-risky-agents).

## Policies for agent user accounts

To create policies for an agent that access resources through its own user account, find agent-user policy guidance in [Secure agents that act as users with Microsoft Entra Conditional Access](policy-agent-user). The article includes the following policies:

- [Block risky agent user accounts](policy-agent-user#block-risky-agent-user-accounts)
- [Require a compliant device](policy-agent-user#require-a-compliant-device)
- [Require a compliant network](policy-agent-user#require-a-compliant-network)