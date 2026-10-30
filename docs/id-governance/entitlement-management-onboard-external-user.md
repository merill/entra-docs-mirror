---
layout: Conceptual
title: Tutorial - Onboard external users to Microsoft Entra ID through an approval process - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-onboard-external-user
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Sammak
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Step-by-step tutorial for how to create an access package for external users requiring approvals in entitlement management.
ms.subservice: entitlement-management
ms.topic: tutorial
ms.date: 2024-07-15T00:00:00.0000000Z
locale: en-us
document_id: 008598cc-9c34-0281-bcfa-a7e5d9555978
document_version_independent_id: 5089bbfa-0699-b3a9-7df0-177595dc1f5a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-onboard-external-user.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-onboard-external-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-onboard-external-user.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/b8932893-874f-48e4-b2d5-5521fe75a61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/e757ef92-a039-44aa-8ed6-705843b26fea
platformId: d47cbbb1-a2fb-eff1-f018-a88bf2c21238
---

# Tutorial - Onboard external users to Microsoft Entra ID through an approval process - Microsoft Entra ID Governance | Microsoft Learn

You can use entitlement management as a way of onboarding external users. This feature allows external users to request access to a set of resources and where you can set up approvals before they gain access to your directory. For external users onboarded through entitlement, you can manage their lifecycle through access packages. When their last access package expires, they are removed from your directory.

In this tutorial, you work for WoodGrove Bank as an IT administrator. You’ve been asked to create an access package to onboard partners from an outside organization that your business group is working with. They need access to a Teams group called **External collaboration**. Approval is needed by an internal sponsor for collaborating organizations. Also, you've been informed that the partner's access needs to expire after 60 days. To use entitlement management, you must have one of the following licenses:

- Microsoft Entra ID P2 or Microsoft Entra ID Governance
- Enterprise Mobility + Security (EMS) E5 license

For more information, see [License requirements](entitlement-management-overview#license-requirements).

## Step 1: Configure basics

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, User Administrator, and Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. When selecting the access package page if you see Access denied, ensure that a Microsoft Entra ID P2 or Microsoft Entra ID Governance license is present in your directory.
4. Select **New access package**.
5. On the **Basics** tab, enter the name **External user package** and description **Access for external users pending approval**.
6. You can leave the **Catalog** drop-down list set to **General**.

## Step 2: Configure resources

1. Select **Next** to open the **Resource roles** tab.

    On this tab, you select the resources and the resource role to include in the access package.
2. Select on **Groups and Teams** and search for your group **External collaboration**.

## Step 3: Configure requests

1. Select **Next** to open the **Requests** tab.

    On this tab, you create a request policy. A *policy* defines the rules or guardrails to access an access package. You create a policy that allows a specific user in the resource directory to request this access package.
2. In the **Users who can request access** section, select **For users not in your directory** and then select **All users (All connected organizations + any new external users)**.
3. Because any user who isn't yet in your directory can view and submit a request for this access package, **Yes** is mandatory for the **Require approval** setting.
4. The following settings allow you to configure how your approvals work for your external users:
5. For **Require requestor justification**, leave this as **Yes**.
6. For **How many stages** leave this as **1**.
7. For Approver scenario, select **Internal sponsor**. This option comes from a configured [Connected Org](entitlement-management-organization) where you can sponsors for specific organizations you're working with. This allows you to set someone specified in the Connected Org from within your organization to be the approver.
8. For **Decision must be made in how many days?** leave this as **14**.
9. For **Require approver justification** leave this as **Yes**.
10. Set **Enable new requests and assignments** to **Yes** to enable this access package to be requested as soon as it's created.

## Step 4: Configure requestor information

1. Select **Next** to open the **Requestor information** tab
2. On this screen, you can ask extra questions to collect more information from your requestor. These questions are shown on their request form and can be set to required or optional. For now you can leave these as empty.

## Step 5: Configure lifecycle

1. Select **Next** to open the **Lifecycle** tab
2. In the **Expiration** section, set **Access package assignment expire** to **Number of days**.
3. Set **Assignment expire after** to **60** days. This field determines when your guest users have to renew their access.
4. You can also configure **Access Reviews** which allows periodic checks of whether the guest still needs access to the access package. A review can be a self-review or you can set specific reviews for this task. For more information, see [Access Reviews](entitlement-management-access-reviews-create).

## Step 6: Review and create your access package

1. Select **Next** to open the **Review + Create** tab.
2. On this screen, you can review the configuration for your access package before creating. If there are any issues, you can use the tabs to navigate to a specific point in the create experience to make edits.
3. When you're happy with your selections, select on **Create**. After a few moments, you should see a notification that the access package was successfully created.
4. Once created, you are brought to the **Overview** page for your access package. You can find the **My Access portal link** and copy the value here. Share this link with your external users and they can go to request this package to start collaborating.

## Step 7: Clean up resources

In this step, you can delete the **External user package** access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Open the **External user package** access package.
4. Select **Resource Roles**.
5. Select the **External collaboration** group you added to this access package, and in the **Details** pane, select **Remove resource role**. In the message that appears, select **Yes**.
6. Open the list of access packages.
7. For **External user package**, select the ellipsis (...) and then select **Delete**. In the message that appears, select **Yes**.