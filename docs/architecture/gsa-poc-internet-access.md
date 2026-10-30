---
layout: Conceptual
title: Microsoft Global Secure Access Proof-of-Concept Guidance - Configure Microsoft Entra Internet Access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/gsa-poc-internet-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: global-secure-access
manager: martinco
description: Learn how to deploy and test Microsoft Global Secure Access as a proof of concept with Microsoft Entra Internet Access.
ms.topic: concept-article
ms.date: 2026-02-20T00:00:00.0000000Z
locale: en-us
document_id: 57de6982-5615-3e9e-183f-5738207a5e2d
document_version_independent_id: 57de6982-5615-3e9e-183f-5738207a5e2d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/gsa-poc-internet-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/gsa-poc-internet-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/gsa-poc-internet-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: 72e389ff-1291-abf0-3418-2ddc6f77c6ee
---

# Microsoft Global Secure Access Proof-of-Concept Guidance - Configure Microsoft Entra Internet Access - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Global Secure Access with Microsoft Entra Internet Access, Microsoft Entra Private Access, and the Microsoft traffic profile.

Detailed guidance begins with [Introduction to Microsoft Global Secure Access proof-of-concept guidance](gsa-poc-guidance-intro), continues with [Configure Microsoft Entra Private Access](gsa-poc-private-access), and concludes with this article.

This article helps you to configure Microsoft Entra Internet Access to act as a secure web gateway. This solution enables you to configure policies for filtering web content to allow or block internet traffic. You can then group those policies into security profiles that you apply to your users through Conditional Access policies.

Note

Apply rules and policies in [order of priority](../global-secure-access/concept-internet-access#policy-processing-logic). For detailed guidance, refer to [Policy processing logic](../global-secure-access/concept-internet-access#policy-processing-logic).

## Configure Microsoft Entra Internet Access

To configure Microsoft Entra Internet Access, see [How to configure Global Secure Access web content filtering](../global-secure-access/how-to-configure-web-content-filtering). It provides guidance to perform these high-level steps:

1. Enable internet traffic forwarding.
2. Create a policy for filtering web content.
3. Create a security profile.
4. Link the security profile to a Conditional Access policy.
5. Assign users or groups to the traffic forwarding profile.

## Configure use cases

Configure and test Microsoft Entra Internet Access use cases with web content filtering policies, security profiles, and Conditional Access policies. The following sections provide example use cases with specific guidance.

### Create a baseline profile that applies to all internet traffic routed through the service

Perform the following steps to use a [baseline profile](../global-secure-access/concept-internet-access#policy-processing-logic) to help secure all traffic in your environment without needing to apply Conditional Access policies:

1. [Create a policy for filtering web content](../global-secure-access/how-to-configure-web-content-filtering#create-a-web-content-filtering-policy) that includes rules to allow or block fully qualified domain names (FQDNs) or web categories across your user base. For example, create a rule that blocks the **Social Networking** category to block all social media sites.
2. Link the policy for filtering web content to the [baseline profile](../global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile). In the Microsoft Entra admin center, go to **Global Secure Access** &gt; **Secure** &gt; **Security profiles** &gt; **Baseline profile**.
3. Sign in to your test device and try to access the blocked site.
4. View activity in the [traffic log](../global-secure-access/how-to-view-traffic-logs) to confirm that entries for your target FQDN show as blocked. If necessary, use **Add filter** to filter results on **User principal name** for your test user.

### Block a group from accessing websites based on category

1. [Create a policy for filtering web content](../global-secure-access/how-to-configure-web-content-filtering#create-a-web-content-filtering-policy) that includes rules to block a web category. For example, create a rule that blocks the **Social Networking** category to block all social media sites.
2. [Create a security profile](../global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile) to group and prioritize your policies. Link the policy for filtering web content to this profile.
3. Create a [Conditional Access policy](../global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) to apply the security profile to your users.
4. Sign in to your test device and try to access a blocked site. You should see **DeniedTraffic** for `http` websites and a **Can't reach this page** notification for `https` websites. It can take up to 90 minutes for a newly assigned policy to take effect. It can take up to 20 minutes for changes to an existing policy to take effect.
5. View activity in the [traffic log](../global-secure-access/how-to-view-traffic-logs) to confirm that entries for your target FQDN show as blocked. If necessary, use **Add filter** to filter results on **User principal name** for your test user.

### Block a group from accessing websites based on FQDN

1. [Create a policy for filtering web content](../global-secure-access/how-to-configure-web-content-filtering#create-a-web-content-filtering-policy) that includes rules to block an FQDN (not a URL).
2. [Create a security profile](../global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile) to group and prioritize your policies. Link the policy for filtering web content to this profile.
3. Create a [Conditional Access policy](../global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) to apply the security profile to your users.
4. Sign in to your test device and try to access the blocked FQDN. You should see **DeniedTraffic** for `http` websites and a **Can't reach this page** notification for `https` websites. It can take up to 90 minutes for a newly assigned policy to take effect. It can take up to 20 minutes for changes to an existing policy to take effect.
5. View activity in the [traffic log](../global-secure-access/how-to-view-traffic-logs) to confirm that entries for your target FQDN show as blocked. If necessary, use **Add filter** to filter results on **User principal name** for your test user.

### Allow a user to access a blocked website

1. [Create a policy for filtering web content](../global-secure-access/how-to-configure-web-content-filtering#create-a-web-content-filtering-policy) that includes a rule to allow an FQDN.
2. [Create a security profile](../global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile) to group and prioritize your policies for filtering web content. Give this allowed profile a higher priority than the blocked profile. For example, if the blocked profile is set to priority 500, set the allowed profile to 400.
3. Create a [Conditional Access policy](../global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) to apply the security profile to the users who need access to the blocked FQDN.
4. Sign in to your test device and try to access the allowed FQDN. It can take up to 90 minutes for a newly assigned policy to take effect. It can take up to 20 minutes for changes to an existing policy to take effect.
5. View activity in the [traffic log](../global-secure-access/how-to-view-traffic-logs) to confirm that entries for your target FQDN show as allowed. If necessary, use **Add filter** to filter results on **User principal name** for your test user.

### Enable and manage the Microsoft traffic forwarding profile

A key feature of Microsoft Entra Internet Access is its ability to help secure Microsoft traffic. You can quickly deploy an automatically configured [Microsoft traffic profile](../global-secure-access/concept-microsoft-traffic-profile) that includes traffic forwarding rules. Use these rules to help secure and monitor Microsoft traffic (such as SharePoint Online and Exchange Online) and authentication traffic for any application that's integrated with Microsoft Entra ID. There are [known limitations](../global-secure-access/reference-current-known-limitations#access-controls-limitations).

1. [Enable the Microsoft traffic profile](../global-secure-access/how-to-manage-microsoft-profile).
2. Assign users and groups to the profile.
3. If desired, configure Conditional Access policies to enforce compliant network checks.
4. Sign in to your test device and try to access SharePoint Online and Exchange Online.
5. View activity in the [traffic log](../global-secure-access/how-to-view-traffic-logs) to confirm that Global Secure Access enabled access. Verify in the sign-in logs that **Through Global Secure Access** shows as **Yes**.

### Implement universal tenant restrictions

[Universal tenant restrictions](../global-secure-access/how-to-universal-tenant-restrictions) enable you to control access to external tenants by unmanaged identities on company-managed devices and networks. You can enforce this restriction with Entra ID Tenant Restrictions, by either blocking or allowing all traffic to an external tenant.

This scenario usually requires that you send all of your traffic through a corporate network proxy. With Universal Tenant Restrictions, organizations can apply tenant restrictions policies to users on any device with the Global Secure Access client, without the need to implement VPN and send traffic through a specific proxy, reducing network latency.

After you enable the Microsoft traffic profile, follow these steps to implement universal tenant restrictions:

1. [Set up tenant restrictions v2](/en-us/azure/active-directory/external-identities/tenant-restrictions-v2). If your organization currently uses tenant restrictions v1, review the [guide for migrating to tenant restrictions v2](https://aka.ms/trv2migration).
2. [Enable Universal Tenant Restrictions](../global-secure-access/how-to-universal-tenant-restrictions#enable-universal-tenant-restrictions).
3. Sign in to your test device and use a private browser window to sign in to any application that is protected by Entra ID in a different tenant, using member account credentials from that tenant.

## Troubleshoot

If you have problems with your PoC, these articles can help you with troubleshooting, logging, and monitoring:

- [Global Secure Access FAQ](../global-secure-access/resource-faq)
- [Troubleshoot problems installing the Microsoft Entra private network connector](../global-secure-access/troubleshoot-connectors)
- [Troubleshoot the Global Secure Access client: Diagnostics](../global-secure-access/troubleshoot-global-secure-access-client-advanced-diagnostics)
- [Troubleshoot the Global Secure Access client: Health check tab](../global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check)
- [Troubleshoot a Distributed File System issue with Global Secure Access](../global-secure-access/troubleshoot-distributed-file-system)
- [Global Secure Access logs and monitoring](../global-secure-access/concept-global-secure-access-logs-monitoring)
- [How to use workbooks with Global Secure Access](../global-secure-access/how-to-use-workbooks)