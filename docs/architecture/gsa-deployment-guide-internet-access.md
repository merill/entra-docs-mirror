---
layout: Conceptual
title: Microsoft Global Secure Access Deployment Guide for Microsoft Entra Internet Access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/gsa-deployment-guide-internet-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: global-secure-access
manager: martinco
description: Learn how to deploy Microsoft Global Secure Access for Microsoft Entra Internet Access
customer intent: As a Microsoft Partner, I want to deploy Microsoft Entra Internet Access as a Proof of Concept in my production or test environment.
ms.topic: how-to
ms.date: 2025-01-06T00:00:00.0000000Z
locale: en-us
document_id: fda499a7-dd91-79ed-3b21-8e7710466298
document_version_independent_id: fda499a7-dd91-79ed-3b21-8e7710466298
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/gsa-deployment-guide-internet-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/gsa-deployment-guide-internet-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/gsa-deployment-guide-internet-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: dfd23633-351b-63d9-5f71-96625dc74141
---

# Microsoft Global Secure Access Deployment Guide for Microsoft Entra Internet Access - Microsoft Entra | Microsoft Learn

[Microsoft Global Secure Access](../global-secure-access/overview-what-is-global-secure-access) converges network, identity, and endpoint access controls for secure access to any app or resource from any location, device, or identity. It enables and orchestrates access policy management for corporate employees. You can continuously monitor and adjust, in real time, user access to your private apps, Software-as-a-Service (SaaS) apps, and Microsoft endpoints. This solution helps you to appropriately respond to permission and risk level changes as they occur.

With Microsoft Entra Internet Access, you can control and manage internet access for enterprise users with managed devices when they work locally or remotely. It helps you to:

- Protect your enterprise users and managed devices from malicious internet traffic and malware infection.
- Stop users from accessing sites based on web category or fully qualified domain name.
- Collect internet usage data for reports and support investigations.

The guidance in this article helps you to test and deploy [Microsoft Entra Internet Access](../global-secure-access/concept-internet-access) in your production environment. [Microsoft Global Secure Access deployment guide introduction](gsa-deployment-guide-intro) provides guidance on how to initiate, plan, execute, monitor, and close your Global Secure Access deployment project.

## Identify and plan for key use cases

Before you enable Microsoft Entra Internet Access, plan for what you want it to do for you. Understand use cases, such as the following, to decide which features to deploy.

- Define a baseline policy that applies to all internet access traffic routed through the service.
- Prevent specific users and groups from using managed devices to access websites by category (such as Alcohol and Tobacco or Social Media). Microsoft Entra Internet Access provides more than 60 categories from which you can choose.
- Prevent users and groups from using managed devices to access specific fully qualified domain names (FQDN).
- Configure override policies to allow groups of users to access sites that your web filtering rules would otherwise block.
- Extend the capabilities of Microsoft Entra Internet Access to entire networks, including devices that are not running the Global Secure Access client
    - [Simulate remote network connectivity using a remote virtual wide-area network (vWAN)](../global-secure-access/how-to-create-remote-network-vwan)
    - [Simulate remote network connectivity using an Azure virtual network gateway (VNG)](../global-secure-access/how-to-simulate-remote-network)

After you understand the capabilities you require in your use cases, create an inventory to associate your users and groups with these capabilities. Understand which users and groups to block or allow access to which web categories and FQDNs. Include rule prioritization for each user group.

## Test and deploy Microsoft Entra Internet Access

At this point, you completed initiate and plan stages of your Secure Access Services Edge (SASE) deployment project. You understand what you need to implement for whom. You defined which users to enable in each wave. You have a schedule for each wave's deployment. You have met [licensing requirements](../global-secure-access/overview-what-is-global-secure-access#licensing-overview). You're ready to enable Microsoft Entra Internet Access.

1. Complete the Global Secure Access [prerequisites](../global-secure-access/quickstart-access-admin-center#prerequisites).
2. [Create a Microsoft Entra group](../fundamentals/how-to-manage-groups) that includes your pilot users.
3. Enable the Microsoft Entra Internet access and Microsoft traffic forwarding profiles. Assign your pilot group to each profile.

Note

Microsoft traffic is a subset of internet traffic that has its own dedicated tunnel gateway. For optimal performance, enable Microsoft Traffic with Internet access traffic profile.

1. Create end user communications to set expectations and provide an escalation path.
2. Create a roll-back plan that defines the circumstances and procedures for when you remove Global Secure Access client from a user device or disable the traffic forwarding profile.
3. Send end user communications.
4. Deploy the [Global Secure Access client for Windows](../global-secure-access/how-to-install-windows-client) on devices for your pilot group to test.
5. Configure remote networks using [vWAN](../global-secure-access/how-to-create-remote-network-vwan) or [VNG](../global-secure-access/how-to-simulate-remote-network) if in scope.
6. Configure [web content filtering policies](../global-secure-access/how-to-configure-web-content-filtering#create-a-web-content-filtering-policy) to allow or block categories or FQDNs based on the use cases that you defined during planning.

    - Block by category: define a rule that blocks one of many predefined, managed categories
    - Block by FQDN: define a rule that blocks an FQDN that you specify
    - Override: define a rule that allows a web category or FQDN that you specify
7. Create [security profiles](../global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile) that group and prioritize your web content filtering policies based on your plan.

    - Baseline profile: use Baseline profile feature to group web content filtering policies that apply to all users by default.
    - Security profiles: create security profiles to group web content filtering policies that apply to a subset of users.
8. Create and link [Conditional Access policies](../global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) to apply your security profiles to your pilot group. The default Baseline profile doesn't require a Conditional Access policy.
9. Have your pilot users test your configuration.
10. Confirm activity in the [Global Secure Access Traffic logs](../global-secure-access/how-to-view-traffic-logs).
11. Update your configuration to address any issues and repeat the test. Use roll-back plan if needed.
12. As needed, iterate changes to your end user communications and deployment plan.

After your pilot is complete, you have a repeatable process to understand how to proceed with each wave of users in your production deployment.

1. Identify the groups that contain your wave of users.
2. Notify the support team of the scheduled wave and its included users.
3. Send prepared end user communications according to your plan.
4. Assign the groups to the Microsoft Entra Internet Access traffic forwarding profile.
5. Deploy the Global Secure Access Client on the devices the users in this wave.
6. If needed, create and configure more web content filtering policies to allow or block categories or FQDNs based on the use cases that you defined in your plan.
7. If needed, create more security profiles that group and prioritize your web content filtering policies based on your plan.
8. Create Conditional Access policies to apply new security profiles to the relevant groups in this wave or add the new groups of users to existing Conditional Access policies for existing security profiles.
9. Update your configuration. Test again to address issues. If needed, initiate roll-back plan.
10. As needed, iterate changes in your end user communications and deployment plan.