---
layout: Conceptual
title: Tutorial - Manage access to resources in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-first
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Step-by-step tutorial for how to create your first access package using the Microsoft Entra admin center in entitlement management.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: tutorial
ms.date: 2025-06-26T00:00:00.0000000Z
ms.reviewer: markwahl-msft
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 153490a3-43c9-2a0f-73d0-fc7371fb567a
document_version_independent_id: f63bc4c3-3a06-e97a-cdab-c36dae6f5cf0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-first.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-first
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-first.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c0439c36-80e3-415f-8e4c-6951e3f1b136
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/2812d699-d85f-4a7f-839d-44e218b35d24
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 4bb55c1f-735b-d29e-d6de-dcfd33a280c7
---

# Tutorial - Manage access to resources in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

Managing access to all the resources employees need, such as groups, applications, and sites, is an important function for organizations. You want to grant employees the right level of access they need to be productive and remove their access when it's no longer needed.

In this tutorial, you work for Woodgrove Bank as an IT administrator. You've been asked to create a package of resources for a marketing campaign that internal users can use to self-service request. Requests don't require approval and user's access expires after 30 days. For this tutorial, the marketing campaign resources are just membership in a single group, but it could be a collection of groups, applications, or SharePoint Online sites.

![Diagram that shows the scenario overview.](media/entitlement-management-access-package-first/elm-scenario-overview.png)

In this tutorial, you learn how to:

- Create an access package with a group as a resource
- Allow a user in your directory to request access
- Demonstrate how an internal user can request the access package

For a step-by-step demonstration of the process of deploying Microsoft Entra entitlement management, including creating your first access package, view the following video:

This rest of this article uses the Microsoft Entra admin center to configure and demonstrate entitlement management.

## Prerequisites

To use entitlement management, you must have one of the following licenses:

- Microsoft Entra ID P2 or Microsoft Entra ID Governance
- Enterprise Mobility + Security (EMS) E5 license

For more information, see [License requirements](entitlement-management-overview#license-requirements).

## Step 1: Set up users and group

A resource directory has one or more resources to share. In this step, you create a group named **Marketing resources** in the Woodgrove Bank directory that is the target resource for entitlement management. You also set up an internal requestor.

![Diagram that shows the users and groups for this tutorial.](media/entitlement-management-access-package-first/elm-users-groups.png)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
3. [Create two users](../fundamentals/how-to-create-delete-users). Use the following names or different names.

    | Name | Directory role |
    | --- | --- |
    | **Admin1** | At least an Identity Governance Administrator. This user can be the user you're currently signed in. |
    | **Requestor1** | User |
4. [Create a Microsoft Entra security group](/en-us/entra/fundamentals/how-to-manage-groups) named **Marketing resources** with a membership type of **Assigned**. This group is the target resource for entitlement management. The group should be empty of members to start.

## Step 2: Create an access package

An *access package* is a bundle of resources that a team or project needs and is governed with policies. Access packages are defined in containers called *catalogs*. In this step, you create a **Marketing Campaign** access package in the **General** catalog.

![Diagram that describes the relationship between the access package elements.](media/entitlement-management-access-package-first/elm-access-package.png)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open an access package.
4. When opening the access package if you see **Access denied**, ensure that a Microsoft Entra ID P2 or Microsoft Entra ID Governance license is present in your directory.
5. Select **New access package**.

    ![Screenshots that shows how to create an access package.](media/entitlement-management-access-package-first/new-access-packages.png)
6. On the **Basics** tab, type the name *Marketing Campaign* access package and description *Access to resources for the campaign*.
7. Leave the **Catalog** drop-down list set to **General**.

    ![Screenshot showing how to set the basic of the access policy.](media/entitlement-management-access-package-first/new-access-package-basics.png)
8. Select **Next** to open the **Resource roles** tab. On this tab, select the resources and the resource role to include in the access package. You can choose to manage access to groups and teams, applications, and SharePoint Online sites. In this scenario, select **Groups and Teams**.

    ![Screenshot showing how to select groups and teams.](media/entitlement-management-access-package-first/new-access-package-select-resources.png)
9. In the **Select groups** pane, find and select the **Marketing resources** group you created earlier.

    By default, you see groups inside the General catalog. When you select a group outside of the General catalog, which you can see if you check the **See all** check box, it's added to the General catalog.

    ![Screenshot that shows how to select the groups&quot;](media/entitlement-management-access-package-first/resource-roles-select-groups.png)
10. Choose **Select** to add the group to the list.
11. In the **Role** drop-down list, select **Member**. If you select the Owner role, it allows users to add or remove other members or owners. For more information on selecting the appropriate roles for a resource, read [add resource roles](entitlement-management-access-package-resources#add-resource-roles).

    [![Screenshot the shows how to select the member role.](media/entitlement-management-access-package-first/resource-roles.png)](media/entitlement-management-access-package-first/resource-roles.png#lightbox)

    Important

    The [role-assignable groups](../identity/role-based-access-control/groups-concept) added to an access package will be indicated using the Sub Type **Assignable to roles**. For more information, check out the [Create a role-assignable group](../identity/role-based-access-control/groups-create-eligible) article. Keep in mind that once a role-assignable group is present in an access package catalog, administrative users who are able to manage in entitlement management, including users in the Global Administrator role, users in the Identity Governance Administrator role, and catalog owners of the catalog, will be able to control the access packages in the catalog, allowing them to choose who can be added to those groups. If you don't see a role-assignable group that you want to add or you're unable to add it, make sure you have the required Microsoft Entra role and entitlement management role to perform this operation. You might need to ask someone with the required roles add the resource to your catalog. For more information, see [Required roles to add resources to a catalog](entitlement-management-delegate#required-roles-to-add-resources-to-a-catalog).

    Note

    When using [dynamic membership groups](../identity/users/groups-create-rule) you won't see any other roles available besides owner. This is by design. ![Screenshots that shows a dynamic group available roles.](media/entitlement-management-access-package-first/dynamic-group-warning.png)
12. Select **Next** to open the **Requests** tab. On the Requests tab, you create a request policy. A *policy* defines the rules or guardrails to access an access package. You create a policy that allows a specific user in the resource directory to request this access package.
13. In the **Users who can request access** section, select **For users in your directory**, and then select **Specific users and groups**.

    [![Screenshot of the access package requests tab.](media/entitlement-management-access-package-first/new-access-package-requests.png)](media/entitlement-management-access-package-first/new-access-package-requests.png#lightbox)
14. Select **Add users and groups**.
15. In the Select users and groups pane, select the **Requestor1** user you created earlier.

    ![Screenshot of select users and groups.](media/entitlement-management-access-package-first/requests-select-users-groups.png)
16. Choose **Select** to add the user to the list.
17. Scroll down to the **Approval** and **Enable requests** sections.
18. Leave **Require approval** set to **No**.
19. For **Enable requests**, select **Yes** to enable this access package to be requested as soon as it's created.
20. If your organization is set up to receive verified IDs, there's an option to configure an access package to require requestors to provide a verified ID. To learn more, see: [Configure verified ID settings for an access package in entitlement management (Preview)](entitlement-management-verified-id-settings)

    ![Screenshot of the Verified ID picker selection.](media/entitlement-management-access-package-first/verified-id-picker.png)
21. Select **Next** to open the **Requestor information** tab.

    ![Screenshots of the requests tab approval and enable requests settings.](media/entitlement-management-access-package-first/requests-approval-enable.png)
22. On the **Requestor information** tab, you can ask questions to collect more information from the requestor. The questions are shown on the request form and can be either required or optional. You're also able to specify whether or not an employee's manager can request on their behalf, and if approval is required if they do so. If the policy allows managers to request on an employee's behalf, the manager would be answering questions on behalf of the employee, and not themselves. For more information on this option, see: [Request access package on-behalf-of other users(Preview)](entitlement-management-request-behalf). In this scenario, you haven't been asked to include requestor information for the access package, so you can leave these boxes empty. Select **Next** to open the **Lifecycle** tab.
23. On the **Lifecycle** tab, you specify when a user's assignment to the access package expires. You can also specify whether users can extend their assignments. In the **Expiration** section:

    1. Set the **Access package assignments expire** to **Number of days**.
    2. Set the **Assignments expire after** to **30** days.
    3. Leave the **Users can request specific timeline** default value, **Yes**.
    4. Set the **Require access reviews** to **No**.

    ![Screenshot of the access package lifecycle tab](media/entitlement-management-access-package-first/new-access-package-lifecycle.png)
24. Skip the **Custom extensions** step.
25. Select **Next** to open the **Review + Create** tab.
26. On the **Review + Create** tab, select **Create**. After a few moments, you should see a notification that the access package was successfully created.
27. In left menu of the Marketing Campaign access package, select **Overview**.
28. Copy the **My Access portal link**.

    You'll use this link for the next step.

    ![Screenshot that demonstrates how to copy the link to the access policy.](media/entitlement-management-access-package-first/my-access-portal-link.png)

## Step 3: Request access

In this step, you perform the steps as the **internal requestor** and request access to the access package. Requestors submit their requests using a site called the My Access portal. The My Access portal enables requestors to submit requests for access packages, see the access packages they already have access to, and view their request history. When a new guest requests an access package in MyAccess, their preferred language is stamped based on the MyAccess browser language at request time. This enables new guests to receive email communication in a language they understand.

**Prerequisite role:** Internal requestor

1. Sign out of the Microsoft Entra admin center.
2. In a new browser window, navigate to the My Access portal link you copied in the previous step.
3. Sign in to the My Access portal as **Requestor1**.

    You should see the **Marketing Campaign** access package.
4. In the **Business justification** box, type the justification *I'm working on the new marketing campaign*.

    ![Screenshot of the My Access portal listing the access packages.](media/entitlement-management-access-package-first/my-access-access-packages.png)
5. Select **Submit**.
6. In the left menu, select **Request history** to verify that your request was delivered. For more details, select **View**.

    ![Screenshot of the My Access portal request history.](media/entitlement-management-access-package-first/my-access-access-packages-history.png)

## Step 4: Validate that access has been assigned

In this step, you confirm that the **internal requestor** was assigned the access package and that they're now a member of the **Marketing resources** group.

1. Sign out of the My Access portal.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as **Admin1**, which is at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and Access package manager.
3. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
4. Find and select **Marketing Campaign** access package.
5. In the left menu, select **Requests**.

    You should see Requestor1 and the Initial policy with a status of **Delivered**.
6. Select the request to see the request details.

    [![Screenshot of the access package request details.](media/entitlement-management-access-package-first/request-details.png)](media/entitlement-management-access-package-first/request-details.png#lightbox)
7. In the left navigation, select **Entra ID**.
8. Select **Groups** and open the **Marketing resources** group.
9. Select **Members**.

    You should see **Requestor1** listed as a member.

    ![Screenshot shows the requestor one has been added to the marketing resources group.](media/entitlement-management-access-package-first/group-members.png)

## Step 5: Clean up resources

In this step, you remove the changes you made and delete the **Marketing Campaign** access package.

1. In the Microsoft Entra admin center as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) select **ID Governance**.
2. Open the **Marketing Campaign** access package.
3. Select **Assignments**.
4. For **Requestor1**, select the ellipsis (**...**) and then select **Remove access**. In the message that appears, select **Yes**.

    After a few moments, the status will change from Delivered to Expired.
5. Select **Resource roles**.
6. For **Marketing resources**, select the ellipsis (**...**) and then select **Remove resource role**. In the message that appears, select **Yes**.
7. Open the list of access packages.
8. For **Marketing Campaign**, select the ellipsis (**...**) and then select **Delete**. In the message that appears, select **Yes**.
9. In **Identity**, delete any users you created such as **Requestor1** and **Admin1**.
10. Delete the **Marketing resources** group.