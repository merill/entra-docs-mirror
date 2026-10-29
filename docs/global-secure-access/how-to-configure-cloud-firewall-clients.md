---
layout: Conceptual
title: Configure cloud firewall for Global Secure Access clients (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-cloud-firewall-clients
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure cloud firewall for traffic from Global Secure Access clients and verify Allow and Block decisions in Microsoft Entra Internet Access.
ms.topic: how-to
ms.subservice: entra-internet-access
ms.date: 2026-10-27T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-generated
locale: en-us
document_id: 3a43881b-7d8a-5f30-170f-8779a96ef844
document_version_independent_id: 3a43881b-7d8a-5f30-170f-8779a96ef844
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-cloud-firewall-clients.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-cloud-firewall-clients
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-cloud-firewall-clients.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
platformId: 57fa8e1e-8806-33eb-a33e-b57170072a15
---

# Configure cloud firewall for Global Secure Access clients (preview) - Global Secure Access | Microsoft Learn

Cloud firewall in Microsoft Entra Internet Access helps you control outbound network access by applying **Allow** or **Block** rules to internet traffic. Use cloud firewall to restrict access to specific destinations, ports, and protocols.

This article describes how to create a cloud firewall policy for traffic from Global Secure Access clients, configure rules, apply the policy through a security profile, and verify traffic decisions.

For branch-office traffic forwarded through a remote network, see [Configure cloud firewall for remote networks](how-to-configure-cloud-firewall).

## Understand traffic acquisition and enforcement

Traffic forwarding and cloud firewall policies serve different purposes:

- **Traffic acquisition** determines which connections are forwarded to Global Secure Access.
- **Cloud firewall enforcement** determines whether forwarded connections are allowed or blocked.

Configure both layers for the traffic you want to protect. Creating a firewall rule doesn't configure the Internet Access profile to acquire that traffic.

The **Default Acquire** policy acquires TCP traffic on ports 80 and 443. To protect other ports or UDP traffic, configure acquisition for the required destinations, ports, and protocols. For more information, see [Manage the Internet Access profile](how-to-manage-internet-access-profile).

Acquisition rules don't override traffic bypass exclusions. For broader acquisition, see [Acquire traffic with wildcard destinations](how-to-manage-internet-access-profile#acquire-traffic-with-wildcard-destinations-preview). Wildcard acquisition and firewall destination matching are separate settings.

Traffic routed through Private Access takes precedence over Internet Access and isn't evaluated by Internet Access cloud firewall rules.

## Prerequisites

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role.
- A [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role to create the Conditional Access policy used to assign a security profile.
- The required Microsoft Entra Internet Access licensing. See [What is Global Secure Access?](overview-what-is-global-secure-access).
- An enabled [Internet Access traffic forwarding profile](how-to-manage-internet-access-profile), configured to acquire the traffic you intend to filter.
- A supported Global Secure Access client installed on the devices you want to protect.

For client installation instructions, see [Windows](how-to-install-windows-client), [macOS](how-to-install-macos-client), [iOS](how-to-install-ios-client), and [Android](how-to-install-android-client).

## Configure acquisition for the examples

The following configuration acquires the traffic used in this article's examples. It isn't an all-port acquisition configuration.

1. Browse to **Global Secure Access &gt; Connect &gt; Traffic forwarding**.
2. Open the Internet Access traffic forwarding profile's acquisition rules.
3. Keep **Default Acquire** enabled for TCP traffic on ports 80 and 443, including the FQDN examples.
4. Expand **Custom Acquire** and select **Add rule** to configure the following additional rules.
5. Enable **Custom Acquire** and save your changes.

| Destination type | Destination | Ports | Protocol | Purpose |
| --- | --- | --- | --- | --- |
| IP subnet | `0.0.0.0/0` | `8080,8081` | TCP | Acquire traffic to any IPv4 destination on the example nonstandard TCP ports. |
| IP subnet | `0.0.0.0/0` | `3478,19302` | UDP | Acquire traffic to any IPv4 destination on the example UDP service ports. |

[![Screenshot showing Custom Acquire rules for IPv4 TCP ports 8080 and 8081 and UDP ports 3478 and 19302, with Default Acquire enabled for TCP ports 80 and 443.](media/how-to-configure-cloud-firewall-clients/acquisition-rules.png)](media/how-to-configure-cloud-firewall-clients/acquisition-rules.png#lightbox)

The `0.0.0.0/0` destination covers all IPv4 destinations, but only on the configured ports and protocol. It doesn't acquire all traffic or include IPv6. You can use more specific destinations when broad acquisition isn't required.

## Plan your firewall rules

Define the destinations, ports, and protocols that your policy needs to allow or block before applying it. You can enable, disable, update, or delete individual rules.

The policy-level default action is **Allow**. Traffic that doesn't match a rule is allowed by the policy. To block traffic, create an explicit **Block** rule rather than setting a policy-level default Block action.

New rules default to action **Allow** and status **Disabled**. You can change a rule's action to **Allow** or **Block** and its status to **Enabled** or **Disabled**.

Rules have unique priorities within a policy. A lower number has a higher priority. Configured matching conditions within a rule are combined using logical AND: traffic must satisfy all configured conditions to match the rule. Conditions set to **Not set** are ignored.

Important

Prepare and review your rules before linking the policy to an active security profile. A broad Block rule can interrupt internet access. Verify required exceptions and maintain a recovery path before enforcement.

## Create a cloud firewall policy

The **Cloud firewall policies** page lists saved policies and their default actions. The preview banner identifies client cloud firewall policies as a preview feature.

[![Screenshot showing the Cloud firewall policies page, Create firewall policy command, a sample policy with default Allow action, and the client preview banner.](media/how-to-configure-cloud-firewall-clients/cloud-firewall-policies.png)](media/how-to-configure-cloud-firewall-clients/cloud-firewall-policies.png#lightbox)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access &gt; Secure &gt; Cloud firewall policies**.
3. Select **Create firewall policy**.
4. On the **Basics** tab, enter a **Name** and **Description**, and select **Next**.
5. On the **Policy settings** tab, review the default **Allow** action and select **Next**.
6. On **Review and create**, review your settings and select **Create**.

## Add firewall rules

1. Open the cloud firewall policy.
2. Under **Rules**, select **+ Add rule**.
3. Enter a **Name** and **Description**.
4. Assign a unique priority.
5. Configure the source and destination matching conditions, ports, and protocol for your scenario.
6. Set the **Action** to **Allow** or **Block**.
7. Review the rule settings, set **Status** to **Enabled** when you're ready to enforce the rule, and save your changes.

The policy's **Rules** page shows each rule's priority, action, and status. Review the **Status** column rather than relying on a description to determine whether a rule is enabled.

[![Screenshot showing firewall rule priorities, descriptions, actions, and statuses, with Allow-Cisco-Web enabled at priority 400 and Block-Cisco-Web disabled at priority 410.](media/how-to-configure-cloud-firewall-clients/firewall-rules.png)](media/how-to-configure-cloud-firewall-clients/firewall-rules.png#lightbox)

### Example: Allow a destination on a nonstandard TCP port

To allow an application to connect to a specific IPv4 destination on TCP port 8080, configure the destination matching conditions as follows:

| Setting | Value |
| --- | --- |
| IPv4 | **Selected IPv4**, with the public test endpoint's address. |
| FQDNs | **Not set**. |
| Protocols | **Selected protocols**, with TCP. |
| Ports | **Selected ports**, with `8080`. |
| Action | **Allow**. |

The screenshot uses `40.65.90.178` as the sample destination. Replace it with a test endpoint you control.

[![Screenshot showing destination IPv4 40.65.90.178, TCP port 8080, and the Allow action in a cloud firewall rule.](media/how-to-configure-cloud-firewall-clients/allow-ip-tcp-8080.png)](media/how-to-configure-cloud-firewall-clients/allow-ip-tcp-8080.png#lightbox)

To compare Allow and Block behavior on different ports, create a separate **Block** rule for the same destination on TCP port `8081`. The TCP 8080 Allow rule doesn't match TCP 8081, and an unmatched connection isn't evidence of an explicit Block.

Ensure acquisition covers both ports, and use an endpoint that responds on both ports before applying the Block rule. These screenshots illustrate rule configuration; they don't establish that a service is currently available at the sample address.

### Example: Allow or block an FQDN

Use the following destination matching conditions for the sample `www.cisco.com` rule:

| Setting | Value |
| --- | --- |
| IPv4 | **Not set**. |
| FQDNs | **Selected FQDNs**, with `www.cisco.com`. |
| Protocols | **Selected protocols**, with TCP. |
| Ports | **Selected ports**, with `80,443`. |
| Action | **Allow** or **Block**, depending on the example state. |

The Allow example uses **Allow-Cisco-Web** at priority `400`, with status **Enabled** and a description of the intended TCP traffic.

[![Screenshot showing the Allow-Cisco-Web rule with its corrected description, priority 400, and Enabled status.](media/how-to-configure-cloud-firewall-clients/allow-fully-qualified-domain-name-rule-settings.png)](media/how-to-configure-cloud-firewall-clients/allow-fully-qualified-domain-name-rule-settings.png#lightbox)

In the destination matching settings, select the FQDN and ports and set the action to **Allow**.

[![Screenshot showing destination FQDN www.cisco.com, TCP ports 80 and 443, and the Allow action.](media/how-to-configure-cloud-firewall-clients/allow-fully-qualified-domain-name.png)](media/how-to-configure-cloud-firewall-clients/allow-fully-qualified-domain-name.png#lightbox)

The Block example uses **Block-Cisco-Web** at priority `410`. Its status is **Disabled** in the sample configuration so that it remains an alternative to the enabled Allow rule.

[![Screenshot showing the Block-Cisco-Web rule with its corrected description, priority 410, and Disabled status.](media/how-to-configure-cloud-firewall-clients/block-fully-qualified-domain-name-rule-settings.png)](media/how-to-configure-cloud-firewall-clients/block-fully-qualified-domain-name-rule-settings.png#lightbox)

Use the same destination matching conditions with the action set to **Block**.

[![Screenshot showing destination FQDN www.cisco.com, TCP ports 80 and 443, and the Block action.](media/how-to-configure-cloud-firewall-clients/block-fully-qualified-domain-name.png)](media/how-to-configure-cloud-firewall-clients/block-fully-qualified-domain-name.png#lightbox)

Important

Treat the Allow and Block examples as alternative states. In the rules overview, **Allow-Cisco-Web** is enabled at priority `400`, and **Block-Cisco-Web** is disabled at priority `410`. Before testing the Block state, disable the matching Allow rule and enable the Block rule. Enabling the lower-priority Block rule alone doesn't override the matching higher-priority Allow rule. Review other matching rules before testing.

The client FQDN example relies on the **Default Acquire** rules for TCP ports 80 and 443. You don't need duplicate Custom Acquire entries for this example's hostname when that traffic is already acquired.

Note

The rule editor states that FQDNs don't work with remote networks for Internet Access. This example applies to client traffic, not the remote-network scenario.

#### FQDN matching and direct-IP connections

FQDN rules depend on the destination name available when cloud firewall evaluates the connection. If a direct-IP connection has no associated destination FQDN, an FQDN rule doesn't match it. An applicable IP rule or the policy's default action can determine the result instead.

Learning a hostname later from TLS Server Name Indication (SNI) doesn't cause cloud firewall to re-evaluate the earlier decision. Don't rely on an FQDN Block rule alone to prevent direct-IP access to the same server. Configure IP restrictions when your policy requires them.

### Example: Filter UDP traffic

To restrict a UDP service, configure a rule for the service's destination and UDP port. Select **UDP** and the required **Allow** or **Block** action. For example, use UDP port `19302` for a test service and UDP port `3478` for a separate control service.

The acquisition example includes both UDP ports. Use an application-level request and response to validate UDP behavior. A TCP connectivity test doesn't validate UDP enforcement.

### Control QUIC traffic on UDP port 443

You can configure cloud firewall rules to **Allow** or **Block** UDP traffic on destination port `443`. Use these rules to control QUIC traffic that uses UDP port 443.

To block this traffic, configure a rule for the intended destinations with protocol **UDP**, destination port `443`, and action **Block**. Cloud firewall can block acquired QUIC traffic that matches this rule. The rule matches UDP traffic on port 443, not only QUIC.

Ensure the Internet Access traffic forwarding profile acquires UDP port `443` for those destinations. The acquisition screenshot in this article doesn't include UDP port 443; add the appropriate **Custom Acquire** rule for this scenario. **Default Acquire** on TCP port 443 doesn't acquire UDP port 443.

Important

The preview supports QUIC acquisition and blocking, but not end-to-end QUIC forwarding. You can configure **Allow** for UDP port 443, but this doesn't enable supported end-to-end QUIC connectivity. Global Secure Access client gaps remain even when the firewall rule allows the traffic.

## Apply the policy through a security profile

After configuring the rules, link the cloud firewall policy to a security profile. Use Conditional Access to assign that profile to the intended users and groups.

### Link the firewall policy to a security profile

1. Browse to **Global Secure Access &gt; Secure &gt; Security profiles**.
2. Create a profile, or open and edit the profile intended for these users.
3. In the profile's linked policies, select **Link a policy** and select the existing cloud firewall policy.
4. Add the policy to the profile, enable the policy link, and save the profile.
5. Review the security profile's priority relative to other profiles that can apply to the same users.

### Assign the profile through Conditional Access

1. Sign in as a **Conditional Access Administrator**.
2. Browse to **Entra ID &gt; Conditional Access &gt; Policies** and select **New policy**.
3. Enter a name, and select the intended users or groups under **Assignments**.
4. Under **Target resources**, select **All internet resources with Global Secure Access**.
5. Under **Session**, select **Use Global Secure Access security profile** and select the profile linked to your cloud firewall policy.
6. Review the assignments and settings. Enable the policy when you're ready to enforce it, and select **Create**.

Start with a limited test group before expanding the assignment. A report-only Conditional Access policy doesn't enforce the firewall configuration.

### Understand security profile selection

Cloud firewall evaluates the firewall policy of one selected security profile, rather than combining the firewall policies from all matching profiles. The highest-priority applicable profile has the lowest priority number. Its firewall policy's default action makes that evaluation terminal.

If none of the applicable security profiles contains a firewall policy, cloud firewall uses the baseline profile.

## Update or remove rules

- To update a rule, open the policy, edit the rule, and save your changes.
- To stop enforcing a rule without deleting it, set its status to **Disabled**.
- To delete a rule, use the trash bin icon in the rule's **Actions** column.

## Verify the configuration

1. Confirm that the test connection is acquired by the Internet Access traffic forwarding profile. For Windows client traffic, use **Advanced diagnostics** to check acquisition.
2. Make a new connection to a destination covered by a firewall rule.
3. Confirm that the observed result matches the rule's action.
4. Browse to **Global Secure Access &gt; Monitor &gt; Traffic logs** and open **Connections**.
5. Find the connection using the test time, destination, port, and protocol. Review the recorded decision and associated security profile, policy, and rule information where available.
6. Test an unrelated destination or port to confirm that the policy hasn't affected traffic outside the intended scope.

For UDP, use a service that returns a verifiable response. A timeout alone doesn't establish that the firewall blocked the connection. Correlate the request with a logged Block decision.

For more information, see [Global Secure Access network traffic logs](how-to-view-traffic-logs).

## Troubleshoot unexpected results

| Symptom | What to check |
| --- | --- |
| Traffic isn't affected by a rule. | Confirm acquisition, rule status, policy link status, profile applicability, and matching conditions. |
| TCP on ports 80 and 443 is acquired, but another port or UDP isn't. | Check the acquisition configuration for the required destination, port, and protocol. |
| A different rule is associated with the connection. | Review overlapping rules, priorities, and the destination information in the connection log. |
| A UDP request times out. | Verify that the service responds without the Block rule, correlate the request with a connection log, and test an unaffected control destination. |
| QUIC fails despite an Allow rule for UDP port 443. | Confirm acquisition and the matching firewall decision. The preview supports QUIC acquisition and blocking, not end-to-end QUIC forwarding. |
| A hostname Block rule doesn't stop direct-IP access. | Check whether a destination FQDN was available for that connection. Review matching IP rules and the policy's default Allow action. |
| Policy changes don't appear to apply. | Allow for the policy propagation interval and retry with a new connection. |

## Preview considerations

The Internet Access traffic forwarding profile doesn't acquire DNS traffic in this preview, including with wildcard acquisition rules. Cloud firewall therefore doesn't support filtering DNS traffic. FQDN-based firewall rules match connections to named destinations; they don't filter DNS queries.

The examples in this article cover IPv4 traffic over TCP and UDP. The `0.0.0.0/0` acquisition destination doesn't include IPv6, and these instructions don't configure IPv6 protection.

QUIC acquisition and blocking are supported; end-to-end QUIC forwarding isn't supported in this preview. FQDN rules require a destination name at the time of the firewall decision and don't replace IP-based restrictions.