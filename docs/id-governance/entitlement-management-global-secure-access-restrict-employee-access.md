---
layout: Conceptual
title: Use entitlement management and Global Secure Access to restrict employee access to cloud apps - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-global-secure-access-restrict-employee-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how you can use entitlement management and Global Secure Access to restrict employee access to cloud apps.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-05-13T00:00:00.0000000Z
ms.reviewer: jercon
locale: en-us
document_id: 80803022-e860-7b9a-b5e7-593449a9f799
document_version_independent_id: 80803022-e860-7b9a-b5e7-593449a9f799
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-global-secure-access-restrict-employee-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-global-secure-access-restrict-employee-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-global-secure-access-restrict-employee-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 7414052b-7019-2ca2-d757-312bc6a5facb
---

# Use entitlement management and Global Secure Access to restrict employee access to cloud apps - Microsoft Entra ID Governance | Microsoft Learn

The Microsoft Entra Suite provides capabilities to govern who can access restricted websites. Microsoft Entra Internet Access protects access to SaaS apps and entitlement management enables organizations to manage identity and access lifecycle at scale, by automating access request workflows, access assignments, reviews, and expiration.

In this scenario, you set up Global Secure Access and Conditional Access to block access to a specific unauthorized website such as an unsanctioned AI app, while using entitlement management to provide governed access to users who should be exempt from the policy. This scenario is useful for generative AI applications and other web applications that don't support provisioning or federation with Microsoft Entra.

![Screenshot of a diagram showing restricting software as a service app using Conditional Access and Global Secure Access.](media/entra-suite-scenario/restrict-access-saas-app.png)

![Screenshot of a diagram showing granting governed software as a service app using Conditional Access and Global Secure Access.](media/entra-suite-scenario/grant-governed-access-saas-app.png)

## Prerequisites

To complete this scenario, you must have the following prerequisites in your Microsoft Entra tenant:

- Microsoft Entra Suite, or Microsoft Entra ID Governance along with Microsoft Global Secure Access
- Required roles: Conditional Access Administrator, Identity Governance Administrator, and Global Secure Access Administrator
- A Microsoft Entra ID joined device where the Global Secure Access client can be installed.

## Step 1: Set up Global Secure Access

If Global Secure Access isn't already configured, you need to set this up first. Visit [Get started with Global Secure Access](../global-secure-access/quickstart-access-admin-center) for a step-by-step guide. The four steps include:

1. Enable the [Internet Access profile](../global-secure-access/how-to-manage-internet-access-profile) and [Microsoft traffic forwarding profile](../global-secure-access/how-to-manage-microsoft-profile).
2. Install and configure the Global Secure Access Client on end-user devices.

## Step 2: Create a Global Secure Access web content filtering policy

In this step, you create a Global Secure Access web content filtering policy to block access to a specific website. See [How to configure Global Secure Access web content filtering](../global-secure-access/how-to-configure-web-content-filtering).

1. Identify the internet domain that you want to restrict access to and define the process for how users who are blocked should get access. In the following guide, we use a security group to provide users with access.
2. Go to Global Secure Access &gt; Secure &gt; Web content filtering policies and select **Create policy**.
3. Choose a name for the policy and select **Block** as the Action.
4. Under the Policy Rules tab, select “Add rule.” Choose a name, select “fqdn” for Destination type, and enter the destination you would like to block. Select add.
5. Review and create the policy.

## Step 3: Create a Global Secure Access security profile and link the filtering policy

1. Go to Global Secure Access &gt; Secure &gt; Security profiles and select **Create profile**.
2. Choose a profile name, leave “*enabled*” for State, and select a Priority.
3. Under the Link policies tab, choose “*Link a policy*” and select the web content filtering policy.

## Step 4: Create a security group for exempted users

1. Go to Groups and select **New group**.
2. Choose Group type **Security**, enter a group name, and leave membership as **Assigned**.
3. Create the group.

## Step 5: Configure a Conditional Access Policy

Once Global Secure Access is set up, you need to [create a Conditional Access policy](../identity/conditional-access/concept-conditional-access-policies) to restrict access to a specific website.

1. Browse to Protection &gt; Conditional Access &gt; Policies and select **New policy**.
2. Choose a name for the policy.
3. Under Users, select the Include tab and choose **All users**. Select the Exclude tab, choose **Users and groups**, and select the group that you created in Step 4 that is used as an exception group to the policy.
4. Under Target resources, select **All internet resources with Global Secure Access**.
5. Under Session select **Use Global Secure Access security profile**, and select the name of the security profile that you created in Step 3.
6. Under Enable policy select **On**, or leave in Report-only mode for testing.
7. Save the policy.

## Step 6: Create an entitlement management access package to provide governed access to the restricted resource

The last step in the scenario is to create an access package that contains the security group that you specified in Step 4. Users assigned to this access package are assigned to this group, and are exempt from the web content filtering policies that you established.

Like other access packages, you create a policy with rules specifying who can request the package, who must approve, and its lifecycle. Learn more at [Create an access package in entitlement management](entitlement-management-access-package-create).

## Step 7: Test the scenario

Once you complete the previous steps, you're ready to test the scenario.

1. On the Microsoft Entra ID joined device, attempt to visit the site you restricted in Step 2. You should receive a blocking experience for all browsers with a plaintext browser error for HTTP traffic and a "Connection Reset" browser error for HTTPS traffic.
2. In entitlement management, assign the access package you created in Step 5 to the user who is signed in on the Microsoft Entra ID joined device. This assigns the user to the access package which provides access to the security group you created in Step 4. Any required approvals need to be completed before the assignment is completed.
3. On the Microsoft Entra ID joined device, attempt to visit the site you restricted in Step 2. You should now be able to access the site.

Note

It can take up to 60 minutes for the Global Secure Access Policy to take effect.