---
layout: Conceptual
title: Configure Secure Web and AI Gateway for Microsoft Copilot Studio agents - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-secure-web-ai-gateway-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure Secure Web and AI Gateway for Microsoft Copilot Studio agents using Global Secure Access.
ms.topic: how-to
ms.date: 2025-11-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d3b4cd39-9c1a-2605-decb-62f5359deea5
document_version_independent_id: d3b4cd39-9c1a-2605-decb-62f5359deea5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-secure-web-ai-gateway-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-secure-web-ai-gateway-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-secure-web-ai-gateway-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://authoring-docs-microsoft.poolparty.biz/devrel/e6f942e8-55a7-4c86-b8e3-7456508ea850
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c389ea6b-b6a0-46df-93a1-1e21f25e19e7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://authoring-docs-microsoft.poolparty.biz/devrel/f1834696-48d6-470d-966b-6ee418881596
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ada1b6-705b-4ed7-aad0-bffd1bd03dfa
platformId: 3ff1afc6-dffb-47d3-9489-16c81a0babf0
---

# Configure Secure Web and AI Gateway for Microsoft Copilot Studio agents - Global Secure Access | Microsoft Learn

Global Secure Access network controls enable you to implement granular access controls for Microsoft Copilot Studio agents. You can apply network security policies including web content filtering, threat intelligence filtering and network file filtering to agent traffic. This capability provides similar security controls for agents that you use for other traffic types in your organization.

Microsoft Entra integrates with Microsoft Copilot Studio to provide network security controls for agent interactions. This integration allows organizations to apply security policies, monitor agent traffic with the Global Secure Access visibility platform, and ensure secure communication between agents and external resources.

## Prerequisites

To configure network security for Copilot Studio agents, you must have:

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID to manage Global Secure Access features.
- A [Power Platform Administrator](/en-us/power-platform/admin/use-service-admin-role-manage-tenant) role to manage Copilot Studio environments.
- A Power Platform environment with Dataverse added to the environment. For more information, see [Create and manage environments in the Power Platform admin center](/en-us/power-platform/admin/create-environment).

## Enable network controls for Copilot Studio agents

To enable network controls for Copilot Studio agents, you must first enable traffic forwarding from these agents in the Power Platform Admin Center.

1. Sign in to the [Power Platform Admin Center](https://admin.powerplatform.microsoft.com) as a [Power Platform Administrator](/en-us/power-platform/admin/use-service-admin-role-manage-tenant).
2. Browse to **Security** &gt; **Identity & access** &gt; **Global Secure Access for Agents**.
3. Select the appropriate environment or environment group and select **Set up**.
4. Enable **Global Secure Access for Agents** for the selection.

[![Screenshot of Power Platform Admin Center showing Global Secure Access for Agents setup page with environment selection and toggle enabled.](media/how-to-secure-web-ai-gateway-agents/screenshot-power-platform-gsa-agents-ui.png)](media/how-to-secure-web-ai-gateway-agents/screenshot-power-platform-gsa-agents-ui.png#lightbox)

Note

After enabling Global Secure Access for Agents in the environment or environment group, any existing Copilot Studio custom connector must be edited and saved to ensure its traffic is routed through Global Secure Access. Custom connectors created afterward automatically use this configuration.

## Create security policies for Copilot Studio agents

After enabling network controls, you can enforce Global Secure Access security policies on agent traffic. You can apply web content filtering, threat intelligence filtering, and other security policies. The following example shows how to configure a web content filtering policy:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Web content filtering policies**.
3. Select **Create policy**.
4. Enter a descriptive name and a description for the policy, then select **Next**.
5. Select **Add rule**.
6. Configure rules based on your security to Copilot Studio agent requirements. For example, block access to `Web repositories`, `Illegal software`, not safe for work (NSFW) sites, and more.
7. Select **Next** to review the policy.
8. Select **Create policy**.

Next, you can create policies like [threat intelligence](how-to-configure-threat-intelligence) to protect agents against malicious destinations or [content policy](how-to-network-content-filtering) to safeguard against unintended data exposure and prevent inline data leaks.

## Link policies to the baseline profile

Group your security policies by linking them to the baseline profile to apply them to Copilot Studio agent traffic. Security profiles linked to Conditional Access policies aren't currently supported for Copilot Studio agents.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
3. Select the **Baseline profile** tab.
4. Select **Edit** to edit the baseline profile rules.
5. Select **Link a policy** and then select **Existing policy**.
6. Select the Copilot Studio agent web repositories policy created earlier and select **Add**.
7. Select **Save** to save the profile changes.

## Monitor and maintain

Regular monitoring and maintenance ensure your security configuration remains effective:

1. **Review traffic logs** regularly for unusual patterns or blocked legitimate traffic. For more information, see [Global Secure Access network traffic logs](how-to-view-traffic-logs).
2. **Update filtering policies** as new services or requirements emerge.
3. **Test policy changes** in a development environment before applying to production.

Note

Configuration changes in the Global Secure Access experience related to web content filtering typically take effect in less than five minutes.

## Known limitations

- The enforcement feature supports only the baseline profile. Network security policies apply per tenant.
- Global Secure Access partner ecosystem integrations, such as third-party Data Loss Prevention (DLP), aren't supported.
- Copilot Studio Bing search network transactions (including knowledge from *public websites* and *Wikipedia*) aren't supported.
- Network requests to Dataverse and Azure SQL knowledge sources aren't supported.
- Network requests to the following custom tools aren't supported: prompt, agent flow, Computer Use, and child agents.
- Network requests to Large Language Model (LLM), either for orchestration or results enhancement, aren't supported.
- Only specific Copilot Studio connectors are supported with network security controls. Refer to the [Copilot Studio documentation](/en-us/power-platform/admin/security/secure-web-ai-gateway-agents) for the list of supported connectors.
- Currently the Agent Name returned in the Global Secure Access traffic logs is the agent's unique *schema name*.