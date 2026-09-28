---
layout: Conceptual
title: Configure Global Secure Access cloud firewall with remote networks for internet access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-cloud-firewall
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure and use cloud firewall to protect against unauthorized internet access from branch offices using Remote Networks for Internet Access.
ms.topic: how-to
ms.subservice: entra-private-access
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro
ms.reviewer: shkhalid
ai-usage: ai-assisted
locale: en-us
document_id: 51828a2b-42c9-3175-43b6-f6cca0e1d2e6
document_version_independent_id: 51828a2b-42c9-3175-43b6-f6cca0e1d2e6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-cloud-firewall.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-cloud-firewall
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-cloud-firewall.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: c88d0e1c-e2ab-27dc-7fe3-02d38c95fec1
---

# Configure Global Secure Access cloud firewall with remote networks for internet access - Global Secure Access | Microsoft Learn

Global Secure Access cloud firewall protects customers from unauthorized egress access by applying policies on network traffic. Cloud firewall provides centralized management, visibility, and consistent policies for branches.

The current scope is using cloud firewall to enforce policies on Internet traffic from branch offices using Remote Networks for Internet Access.

With cloud firewall, you can:

- Define granular Firewall filtering rules, where you'll define the traffic matching conditions and an action in case the traffic matches.
- Define 5-tuple rules based on source IP, source Port, destination IP, destination Port, and destination Protocol (TCP, UDP).
- Define and enforce an action between **Allow** and **Block**.

## Prerequisites

- Configure [remote networks for internet access](how-to-create-remote-networks).

## Supported scenarios

Cloud firewall supports these scenarios:

| # | **Scenario** |
| --- | --- |
| 1 | Admin can create a cloud firewall policy with default Allow action (can't be changed).The default action is applied to all traffic that does not match any of the rules in the policy. |
| 2 | Admin can add/update rules in a cloud firewall policy and assign priorities to each rule.Rule Matching conditions: In each of these rules, admin can define these traffic matching conditions: source IPv4, source Port, destination IPv4, destination Port, and Protocol (TCP, UDP or both).The action for each rule can be set to **Allow** or **Block**. |
| 3 | Admin can enable or disable an individual cloud firewall policy rule. |
| 4 | Admin can delete an individual cloud firewall policy rule. |
| 5 | Admin can link a cloud firewall policy to the baseline profile for the remote network. |
| 6 | Admin can enable or disable the linked firewall policy to the baseline profile (security profile with priority=65000) |
| 7 | Admin can delete the linked firewall policy with the baseline profile and link another one. |

## Scenario configuration steps

### Create a cloud firewall policy with the default **Allow** action.

1. Sign in to your [Entra admin center](https://entra.microsoft.com/?Microsoft_Azure_Network_Access_isCloudFirewallPolicyEnabled=true&amp;exp.isCloudFirewallPolicyEnabled=true#view/Microsoft_Azure_Network_Access/CloudFirewallPolicy.ReactView).
2. Browse to **Global Secure Access 🡪 Secure 🡪 Cloud firewall policies 🡪 Create firewall policy.**
3. Under the **Basics** tab, provide a **Name** and **Description**, then click **Next &gt;**.
4. Under **Policy settings**, make sure the Default Action is set to **Allow**, then click **Next &gt;**.
5. Under **Review and create**, review the information you've provided, then click **Create**.

[![Screenshot showing the Create firewall policy page in the Entra admin center.](media/how-to-configure-cloud-firewall/create-cloud-firewall-policy.png)](media/how-to-configure-cloud-firewall/create-cloud-firewall-policy.png#lightbox)

### Add or update a cloud firewall rule, assign priority and enable or disable

1. Click on the created firewall policy in the previous step.
2. Under **Rules**, select **+ Add rule**.

[![Screenshot showing the Add rule option in the cloud firewall policy.](media/how-to-configure-cloud-firewall/edit-rules.png)](media/how-to-configure-cloud-firewall/edit-rules.png#lightbox)

1. Configure the 5-tuple rule:

    1. Provide a **Name** and **Description**.
    2. Assign a priority to the rule relevant to other rules in this policy. Rule priority must be greater than or equal to 100 and should be unique within the policy. Lower value means higher priority.
    3. Select Rule settings **Status** to set to **Enable** or **Disable**. Default status is disabled and starting the rule with disabled status is recommended until ready to enforce.
    4. Configure the source and destination matching conditions. Note these important limitations:

        - IPs are defined as IPs, IP ranges, or Classless Inter-Domain Routings (CIDRs).
        - Destination Fully Qualified Domain Names (FQDNs) aren't supported currently so we recommend keeping it at the **Not set** value (default).
    5. Set the **Action** to **Allow** or **Block**.

[![Screenshot showing the cloud firewall rule configuration page.](media/how-to-configure-cloud-firewall/select-action.png)](media/how-to-configure-cloud-firewall/select-action.png#lightbox)

Note

In the rule, source IP, source port, destination IP, destination port, and protocol are logically AND.

For instance, you configure a rule as shown here:

- Source IP = 10.0.0.5
- Source Port = 12345
- Destination IP = 192.168.1.20
- Destination Port = 443
- Protocol = TCP

This firewall rule matches traffic that simultaneously meets the conditions for source IP, source Port, destination Port, destination IP, and Protocol. Not set values (default) in source and destination matching conditions are ignored.

1. (Optional) Update any values in the rule and save them.

### Delete a cloud firewall rule

1. Use the trash bin icon under the **Actions** column to permanently delete any rule.

[![Screenshot showing the delete option for cloud firewall rules.](media/how-to-configure-cloud-firewall/edit-rules-2.png)](media/how-to-configure-cloud-firewall/edit-rules-2.png#lightbox)

Tip

You can also disable the rule if you intend to use the rule in the future rather than deleting it.

### Link a cloud firewall policy to the baseline profile for the remote network

Important

As a best practice, we recommend creating rules in the policy first before linking the policy to the baseline profile. Creating rules in the policy ensures all changes apply collectively. Ensuring collective changes is important if you create a "block-all" rule for the entire branch traffic, then add rules to allow certain traffic. Without following this best practice, you might inadvertently block yourself for all branch traffic.

1. In your [Entra admin center](https://entra.microsoft.com/?Microsoft_Azure_Network_Access_isCloudFirewallPolicyEnabled=true&amp;exp.isCloudFirewallPolicyEnabled=true#view/Microsoft_Azure_Network_Access/CloudFirewallPolicy.ReactView), browse to **Global Secure Access &gt; Secure &gt; Security Profiles &gt; Baseline Profile**.

[![Screenshot showing the navigation to Security Profiles.](media/how-to-configure-cloud-firewall/security-baseline-profile.png)](media/how-to-configure-cloud-firewall/security-baseline-profile.png#lightbox)

1. Click on **Edit profile**, then select **Link policies &gt; + Link a policy** to link an existing cloud firewall policy.

[![Screenshot showing the Link policy option.](media/how-to-configure-cloud-firewall/edit-baseline-policy-link-policies.png)](media/how-to-configure-cloud-firewall/edit-baseline-policy-link-policies.png#lightbox)

Only one cloud firewall policy can be linked to a baseline profile. Linking a cloud firewall policy to a security profile other than the baseline profile won’t have any effect.

### Enable or disable the linked firewall policy to the baseline profile

1. Use the pencil icon to change the State of a linked firewall policy from **enabled** to **disabled** or vice versa.

[![Screenshot showing the enable/disable option for linked firewall policy.](media/how-to-configure-cloud-firewall/edit-baseline-policy.png)](media/how-to-configure-cloud-firewall/edit-baseline-policy.png#lightbox)

### Delete the linked firewall policy and link to another one

1. Use the trash bin icon to permanently delete any policy.
2. Navigate to **+ Link a policy** to link to another policy.

## Known limitations

- The destination FQDN isn't supported in the cloud firewall rule.
- It may take 15-20 minutes for any firewall policy updates to take effect.
- Cloud firewall capability isn't currently supported with Global Secure Access clients.