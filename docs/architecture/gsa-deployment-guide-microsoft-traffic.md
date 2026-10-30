---
layout: Conceptual
title: Microsoft Global Secure Access deployment guide for Microsoft Traffic - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/gsa-deployment-guide-microsoft-traffic
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: global-secure-access
manager: martinco
description: Deploy and verify Microsoft Global Secure Access for Microsoft Traffic
customer intent: As a Microsoft Partner, I want to deploy Microsoft Traffic as a Proof of Concept in my production or test environment.
ms.topic: how-to
ms.date: 2025-01-06T00:00:00.0000000Z
locale: en-us
document_id: e30210fa-b15d-04d8-0250-912e098ab7f6
document_version_independent_id: e30210fa-b15d-04d8-0250-912e098ab7f6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/gsa-deployment-guide-microsoft-traffic.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/gsa-deployment-guide-microsoft-traffic
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/gsa-deployment-guide-microsoft-traffic.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: be9bdac6-3115-371b-b3c6-ca32a9d2989d
---

# Microsoft Global Secure Access deployment guide for Microsoft Traffic - Microsoft Entra | Microsoft Learn

[Microsoft Global Secure Access](../global-secure-access/overview-what-is-global-secure-access) converges network, identity, and endpoint access controls for secure access to any app or resource from any location, device, or identity. It enables and orchestrates access policy management for corporate employees. You can continuously monitor and adjust, in real time, user access to your private apps, Software-as-a-Service (SaaS) apps, and Microsoft endpoints. Continuous monitoring and adjusting helps you to appropriately respond to permission and risk level changes as they occur.

The Microsoft traffic forwarding profile enables you to control and manage internet traffic that is specific to Microsoft endpoints even when users work from remote locations. It helps you to:

- Protect against data exfiltration.
- Reduce risk of token theft and replay attacks.
- Correlate device source IP address with activity logs to improve threat hunting efficiencies.
- Ease access policy management without a list of egress IP addresses.

The guidance in this article helps you to test and deploy the Microsoft traffic profile in your production environment. [Microsoft Global Secure Access deployment guide introduction](gsa-deployment-guide-intro) provides guidance on how to initiate, plan, execute, monitor, and close your Global Secure Access deployment project.

## Identify and plan for key use cases

Before you enable Microsoft Entra Secure Access Essentials, determine what you want it to do for you. Understand your use cases to decide which features to deploy. The following table recommends configurations based on use cases.

| Use case | Recommended configuration |
| --- | --- |
| Prevent users and groups from using your organization's devices to sign in to unauthorized Entra ID tenants. | Configure universal tenant restrictions. |
| Ensure users connect and authenticate only with the Global Secure Access secure network tunnel to reduce risk of token theft/replay for Microsoft 365 and all Enterprise applications. | Configure compliant network check in Conditional Access policies. |
| Maximize threat hunting success and efficiencies. | Configure Source IP restoration (Preview) and [Use enriched Microsoft 365 logs](../global-secure-access/how-to-view-enriched-logs). |

After you determine which capabilities you require for your use cases, include feature deployment in your implementation.

## Test and deploy Microsoft traffic profile

At this point, you completed the initiate and plan stages of your Global Secure Access deployment project. You understand what you need to implement for whom. You defined the users to enable in each wave. You have a schedule for each wave's deployment. You have met [licensing requirements](../global-secure-access/overview-what-is-global-secure-access#licensing-overview). You're ready to enable Microsoft traffic profile.

1. Create end user communications to set expectations and provide an escalation path.
2. Create a roll-back plan that defines the circumstances and procedures for when you remove Global Secure Access client from a user device or disable the traffic forwarding profile.
3. [Create a Microsoft Entra group](../fundamentals/how-to-manage-groups) that includes your pilot users.
4. Send end user communications.
5. Enable the [Microsoft traffic forwarding profile](../global-secure-access/how-to-manage-microsoft-profile) and assign your pilot group to it.
6. If you plan to maximize your threat hunting success and efficiency, configure [Source IP restoration](../global-secure-access/how-to-source-ip-restoration).
7. Create Conditional Access policies that require [compliant network](../global-secure-access/how-to-compliant-network) checks to your pilot group if it's a planned use case.
8. Configure [universal tenant restrictions](../global-secure-access/how-to-universal-tenant-restrictions) if it's a planned use case.
9. Deploy the [Global Secure Access client for Windows](../global-secure-access/how-to-install-windows-client) on devices for your pilot group to test.
10. Have your pilot users test your configuration.
11. View sign-in logs to ensure that pilot users are connecting to Microsoft endpoints using Global Secure Access.
12. Verify compliant network check by pausing Global Secure Access agent and then attempting to access SharePoint.
13. Verify tenant restrictions by attempting to sign into a different tenant.
14. Verify Source IP restoration by comparing the IP address in the sign-in log of a successful connection to SharePoint Online when connecting with Global Secure Access agent running vs. disabled to ensure they're the same. 
    Note

    You must disable any Conditional Access policy that enforces the compliant network check for this verification.

Update your configuration to address any issues. Repeat the test. Implement roll-back plans if needed. Iterate changes to your end user communications and deployment plan if needed.

After you complete your pilot, you have a repeatable process to proceed with each wave of users in your production deployment.

1. Identify the groups that contain your wave's users.
2. Notify your support team of the wave's schedule and its included users.
3. Send the wave's end user communications.
4. Assign the wave's groups to the Microsoft traffic forwarding profile.
5. Deploy the Global Secure Access Client on the wave's users' devices.
6. Create or update Conditional Access policies to enforce your use case requirements on the wave's relevant groups.
7. As needed, iterate changes to your end user communications and deployment plan.