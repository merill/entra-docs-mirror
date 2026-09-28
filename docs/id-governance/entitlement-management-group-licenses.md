---
layout: Conceptual
title: Manage the lifecycle of group-based licenses in Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-group-licenses
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This step-by-step tutorial shows how to create an access package for managing group-based licenses in entitlement management.
ms.subservice: entitlement-management
ms.topic: tutorial
ms.date: 2024-07-15T00:00:00.0000000Z
locale: en-us
document_id: 962b0e53-34f1-a664-9111-74fbbee47fda
document_version_independent_id: 5f763fe4-756a-375e-675a-47bdb506b79f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-group-licenses.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-group-licenses
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-group-licenses.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/b8932893-874f-48e4-b2d5-5521fe75a61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/e757ef92-a039-44aa-8ed6-705843b26fea
platformId: bcb87818-90a2-ab23-cd95-c8925281b4d7
---

# Manage the lifecycle of group-based licenses in Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn

With Microsoft Entra ID, you can use groups to manage the [licenses for your applications](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true). You can make the management of these groups even easier by using entitlement management:

- Configure periodic access reviews to ensure only authorized users that need the licenses are in the group.
- Allow other users to request membership to the group.

In this tutorial, you play the role of an IT administrator for Woodgrove Bank. You're asked to create an access package so employees in your organization can easily gain access to Office licenses. (You should already have a group that manages your [Office licenses](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true).) You want to be able to review these group members every year. You also want to allow new employees to request Office licenses, pending manager approval.

To use entitlement management, you must have one of these licenses:

- Microsoft Entra ID P2 or Microsoft Entra ID Governance
- Enterprise Mobility + Security (EMS) E5

For more information, see [License requirements](entitlement-management-overview#license-requirements).

## Step 1: Configure basics for your access package

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, User Administrator, and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page Select **New access package**.
4. On the **Basics** tab, in the **Name** box, enter **Office Licenses**. In the **Description** box, enter **Access to licenses for Office applications**.
5. You can leave **General** in the **Catalog** list.

## Step 2: Configure the resources for your access package

1. Select **Next: Resource roles** to go to the **Resource roles** tab.
2. On this tab, you select the resources and the resource role to include in the access package. In this scenario, select **Groups and Teams** and search for your group that has assigned [Office licenses](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true).
3. In the **Role** list, select **Member**.

## Step 3: Configure requests for your access package

1. Select **Next: Requests** to go to the **Requests** tab.

    On this tab, you create a request policy. A *policy* defines the rules for access to an access package. You create a policy that allows non-guest users in the resource directory to request the access package.
2. In the **Users who can request access** section, select **For users in your directory** and then select **All members (excluding guests)**. These settings make it so that only members of your directory can request Office licenses.
3. Ensure that **Require approval** is set to **Yes**.
4. Leave **Require requestor justification** set to **Yes**.
5. Leave **How many stages** set to **1**.
6. Under **Approver**, select **Manager as approver**. This option allows the requestor's manager to approve the request. You can select a different person to be the fallback approver if the system can't find the manager.
7. Leave **Decision must be made in how many days?** set to **14**.
8. Leave **Require approver justification** set to **Yes**.
9. Under **Enable new requests and assignments**, select **Yes** to enable new users to request the access package as soon as it's created.

## Step 4: Configure requestor information for your access package

1. Select **Next** to go to the **Requestor information** tab.
2. On this tab, you can ask questions to collect more information from the requestor. The questions are shown on the request form and can be either required or optional. In this scenario, you haven't been asked to include requestor information for the access package, so you can leave these boxes empty.

## Step 5: Configure the lifecycle for your access package

1. Select **Next: Lifecycle** to go to the **Lifecycle** tab.
2. In the **Expiration** section, for **Access package assignments expire**, select **Number of days**.
3. In **Assignments expire after**, enter **365**. This box specifies when members who have access to the access package needs to renew their access.
4. You can also configure access reviews, which allow periodic checks of whether the users still need access to the access package. A review can be a self-review performed by the user themselves. Or you can set a user's manager or another person as the reviewer. For more information, see [Access reviews](entitlement-management-access-reviews-create).

    In this scenario, you want all employees to review whether they still need a license for Office each year.

    1. Under **Require access reviews**, select **Yes**.
    2. You can leave **Starting on** set to the current date. This date is when the access review starts. After you create an access review, you can't update its start date.
    3. Under **Review frequency**, select **Annually**, because the review occurs once per year. The **Review frequency** box is where you determine how often the access review runs.
    4. Specify a **Duration (in days)**. The duration box is where you indicate how many days each occurrence of the access review series runs.
    5. Under **Reviewers**, select **Manager**.

## Step 6: Review and create your access package

1. Select **Next: Review + Create** to go to the **Review + Create** tab.

    On this tab, you can review the configuration for your access package before you create it. If there are any problems, you can use the tabs to go to a specific point in the process to make edits.
2. When you're happy with your configuration, select **Create**. After a moment, you should see a notification stating that the access package is created.
3. After the access package is created, you'll see the **Overview** page for the package. You find the **My Access portal link** here. Copy the link and share it with your team so your team members can request the access package to be assigned licenses for Office.

## Step 7: Clean up resources

In this step, you delete the Office Licenses access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Open the **Office Licenses** access package.
4. Select **Resource Roles**.
5. Select the group you added to the access package. On the details pane, select **Remove resource role**. In the message box that appears, select **Yes**.
6. Open the list of access packages.
7. For **Office Licenses**, select the ellipsis button (...) and then select **Delete**. In the message box that appears, select **Yes**.