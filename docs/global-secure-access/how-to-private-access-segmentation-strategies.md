---
layout: Conceptual
title: Private Access segmentation strategies for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-private-access-segmentation-strategies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn best practices for transitioning from VPN replacement with Quick Access to per-application segmentation using Microsoft Entra Private Access.
ms.topic: how-to
ms.date: 2026-03-17T00:00:00.0000000Z
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: f62feb47-ab7a-a766-d585-a72f9c4d7137
document_version_independent_id: f62feb47-ab7a-a766-d585-a72f9c4d7137
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-private-access-segmentation-strategies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-private-access-segmentation-strategies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-private-access-segmentation-strategies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: f2387ee2-0be6-a4b5-5496-ff507026d42e
---

# Private Access segmentation strategies for Global Secure Access - Global Secure Access | Microsoft Learn

Microsoft Entra Private Access provides a path from traditional VPN solutions to granular, per-application access. Many organizations begin by replacing their VPN with [Quick Access](how-to-configure-quick-access), which provides broad connectivity to corporate resources. The next step is to segment that broad access into individual applications so that each user only reaches the resources they need.

This article walks through the recommended strategy for transitioning from Quick Access to per-application segmentation, using [Application Discovery](how-to-application-discovery) to inform your segmentation decisions.

Per-application segmentation aligns with the broader Zero Trust principle of network segmentation and software-defined perimeters. For wider context and planning guidance, see:

- [Secure networks with Zero Trust: Network segmentation and software-defined perimeters](/en-us/security/zero-trust/deploy/networks#1-network-segmentation-and-software-defined-perimeters)
- [Microsoft Zero Trust](https://zerotrust.microsoft.com/)
- [Zero Trust Workshop: Network segmentation guidance (NET_012)](https://microsoft.github.io/zerotrustassessment/docs/workshop-guidance/network/NET_012)

## Prerequisites

- A Microsoft Entra tenant onboarded to [Microsoft Entra Private Access](concept-private-access).
- A Microsoft Entra tenant configured with [Quick Access](how-to-configure-quick-access).
- Users actively accessing resources through Quick Access so that Application Discovery has traffic data to analyze.
- One of the following roles: [Global Secure Access Administrator](reference-role-based-permissions#global-secure-access-administrator) or [Application Administrator](reference-role-based-permissions#application-administrator).

## Understand the segmentation journey

The transition from VPN to per-application segmentation follows a phased approach:

| Phase | Description |
| --- | --- |
| **Phase 1: VPN modernization** | Deploy Quick Access with broad IP ranges and wildcard FQDNs to replicate VPN-level connectivity. Users can access the same resources they reached through the VPN, and you can decommission the VPN. |
| **Phase 2: Discovery** | Use Application Discovery to analyze traffic patterns and understand which applications users are accessing through Quick Access. Identify the most-used application segments and the users who access them. |
| **Phase 3: Segmentation** | Create individual [per-app access](how-to-configure-per-app-access) enterprise applications for high-value or sensitive resources. Assign only the users and groups that require access to each application. |
| **Phase 4: Governance** | Apply [Conditional Access](how-to-target-resource-private-access-apps) to your segmented applications, manage access with [Microsoft Entra ID Governance](/en-us/entra/id-governance/identity-governance-overview), and continue to monitor access patterns. |

Tip

Don't attempt to segment all applications at once. Start with the most critical or most-used applications identified through Application Discovery, then expand your segmentation over time.

## Phase 1: Modernize your VPN with Quick Access

If you haven't already, [configure Quick Access](how-to-configure-quick-access) with the IP ranges and FQDNs that your VPN currently provides access to. Quick Access gives users broad connectivity similar to a VPN but through Microsoft Entra Private Access.

Most customers also configure [Private DNS](concept-private-name-resolution) at this stage so users can reach internal resources by name. Configure your private DNS suffixes alongside Quick Access to replicate the name resolution behavior that users expect from a VPN.

At this stage, all users who are assigned to Quick Access can reach any resource within the defined ranges. This broad access is intentional — it ensures a smooth transition from VPN without disrupting user productivity.

## Phase 2: Discover application access patterns

After users have been accessing resources through Quick Access, use Application Discovery to understand traffic patterns.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](reference-role-based-permissions#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Application Discovery**.
3. Review the discovered application segments, sorted by the number of users.

Focus on identifying:

- **High-traffic applications** — Application segments with the most users and transactions. These are strong candidates for early segmentation because they have the highest impact.
- **Sensitive applications** — Resources such as financial systems, HR platforms, or administrative tools that should be restricted to specific teams. For example, only the finance team should access SAP, and only HR staff should reach the HR management system.
- **Application groupings** — Multiple application segments that belong to the same application. A single application might span several FQDNs, IP addresses, or ports. For example, Active Directory Domain Services (AD DS) for a specific site might include multiple domain controllers across several TCP and UDP ports.

For detailed guidance on interpreting Application Discovery data, see [Application Discovery for Global Secure Access](how-to-application-discovery).

## Phase 3: Segment access by application

After you identify the applications to segment, create individual enterprise applications for each one.

### Create per-app applications from discovered segments

1. In the **Application Discovery** table, select one or more application segments that correspond to the application you want to segment.
2. Select **Add to new application**.
3. Enter a descriptive **Name** for the application and select the appropriate **Connector Group**.
4. Review the application segments and add or remove segments as needed.
5. Select **Save**.

For complete steps, see [Create a new application](how-to-application-discovery#create-a-new-application) in the Application Discovery article.

### Assign users and groups with least privilege

After you create the application, restrict access to only the users who need it:

1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
2. Select the application you created.
3. Under **Users and groups**, remove broad assignments inherited from Quick Access.
4. Add only the specific users or groups that need access to this application.

For example:

| Application | Assigned groups |
| --- | --- |
| SAP Finance Portal | Finance team, Accounting team |
| HR Management System | HR team, People managers |
| Engineering wiki | Engineering team |
| AD DS — Contoso HQ | All domain-joined users at HQ |

Important

When you move an application segment from Quick Access to a specific enterprise application, all traffic to that segment follows the new application's configuration. No traffic to the segmented application goes through Quick Access, even if the segment remains within the ranges defined by Quick Access. Verify that the correct users are assigned before you segment to avoid access disruptions.

### Move both FQDNs and the IP addresses they resolve to

If you use Private DNS, be aware of how FQDN-based and IP-based segments interact during segmentation:

- When you move an FQDN to an enterprise application, only traffic that's addressed to that FQDN (and resolved through Private DNS) follows the new application's configuration.
- Traffic that the client sends directly to the IP address — for example, traffic generated after a local DNS resolution, or traffic from a process that uses cached IPs — continues to match Quick Access if that IP is still within a Quick Access range.

To ensure all traffic to a segmented application follows its enterprise application configuration:

1. Add the FQDNs *and* the IP addresses or ranges that the application resolves to into the new enterprise application.
2. Remove those same IP addresses or ranges from Quick Access so the application's configuration is the only match for that traffic.

### Prioritize which applications to segment first

Consider this order when deciding which applications to segment first:

1. **High-sensitivity, low-user-count applications** — These are the easiest to segment because they have a small, well-defined audience and the highest security benefit. Examples: administrative tools, financial systems.
2. **High-traffic, well-defined applications** — Applications with many users but a clear audience. Examples: department-specific portals.
3. **Infrastructure services** — Services like AD DS or DNS that many users depend on. These require careful planning because they often span multiple segments and protocols.

## Phase 4: Apply Conditional Access

After you create segmented applications, apply Conditional Access policies to each one individually — something that isn't possible with broad VPN or Quick Access connectivity. Common policies include:

- **Require MFA** for sensitive applications such as financial or HR systems.
- **Require compliant devices** for applications that handle confidential data.
- **Block access from risky sign-ins** using Microsoft Entra ID Protection signals.

For most environments, the recommended baseline is to apply the Conditional Access guidance in [Apply Conditional Access to Private Access apps](how-to-target-resource-private-access-apps) consistently across your segmented applications. Avoid creating many individual, app-specific policies unless a specific use case requires it — broad, well-tested policies are easier to operate and audit than dozens of one-off configurations. Reserve app-specific policies for cases where the data sensitivity, regulatory requirements, or user population of an application genuinely differs from the rest of your environment.

## Govern access and continue monitoring

Segmentation isn't a one-time activity. After you segment applications, use governance and ongoing monitoring to keep access aligned with business need.

### Govern access with Microsoft Entra ID Governance

Manage who has access to your segmented enterprise applications by using [Microsoft Entra ID Governance](/en-us/entra/id-governance/identity-governance-overview):

- Use [access packages](/en-us/entra/id-governance/entitlement-management-overview) to bundle related Private Access enterprise applications and grant access through self-service requests with approval workflows.
- Configure [access reviews](/en-us/entra/id-governance/access-reviews-overview) so application owners regularly recertify who needs access.
- Use [lifecycle workflows](/en-us/entra/id-governance/what-are-lifecycle-workflows) to automatically remove access when users change roles or leave the organization.

This approach scales segmentation: instead of manually managing user and group assignments on each enterprise application, owners request access through packages and reviews keep assignments accurate over time.

### Continue monitoring

Regularly review Application Discovery to:

- Identify new applications that users are accessing through Quick Access.
- Detect changes in usage patterns that suggest new segmentation opportunities.
- Verify that segmented applications have the correct user assignments.

Over time, move more application segments out of Quick Access and into individually managed enterprise applications.

## Should you remove Quick Access entirely?

Quick Access isn't designed to be removed entirely after segmentation is complete. It's expected to remain in place even in mature deployments, for the following reasons:

- **Catch-all for unsegmented traffic** — Quick Access continues to serve traffic for resources you haven't segmented yet, including newly discovered applications surfaced by Application Discovery.
- **Private DNS host** — Private DNS suffixes are typically configured on Quick Access. Keeping Quick Access in place preserves consistent name resolution for users, even as individual applications are pulled into their own enterprise applications.
- **Recommended fallback segments** — Some application segments — for example, broad infrastructure ranges or services that aren't well-suited to per-app segmentation — are intentionally left in Quick Access.

When segmentation is mature, Quick Access typically retains:

- Private DNS configuration.
- Recommended infrastructure or fallback application segments.
- A user assignment that matches the population that still needs broad access (often a subset of the original VPN-replacement assignment, not all users).

Treat the goal as *minimizing* the scope of Quick Access — narrowing its assignments and segments — rather than removing it entirely.