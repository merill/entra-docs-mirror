---
layout: Conceptual
title: Catalog Access Reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/catalog-access-reviews
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes what Catalog Access Reviews are, how to create one, and how to complete a review for one.
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 0690baf3-0fcd-2513-cca8-01aeb287f1fb
document_version_independent_id: 0690baf3-0fcd-2513-cca8-01aeb287f1fb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/catalog-access-reviews.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/catalog-access-reviews
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/catalog-access-reviews.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 861c92f8-632f-5aa2-2ac1-8ae49e24846d
---

# Catalog Access Reviews - Microsoft Entra ID Governance | Microsoft Learn

Catalog access reviews in Microsoft Entra ID Governance enable organizations to simplify how reviewers can review user access to multiple resource types, such as groups, applications, and custom disconnected resources at once. This helps ensure only the right people retain access, while enabling managers and resource owners to review access efficiently through a multi-stage process.

## License requirements

This feature requires Microsoft Entra ID Governance or Microsoft Entra Suite subscriptions, for your organization's users. For more information, see the articles of each capability for more details. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Add resources to catalog

To enable access reviews across multiple resources in a single reviewer experience, you must first add those resources to a catalog. Groups, applications, and custom data provided resources are currently the three resources that can be reviewed through a catalog. To add resources to a catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) or catalog creator, and as the owner or administrator of the resources.
2. Browse to **Entitlement management** &gt; **Catalogs**.
3. On the catalogs screen, select an existing catalog or select **New Catalog** to create a new one.
4. On the catalog overview page, select **Resources** &gt; **Add resources**.
5. To review memberships of groups or teams, select **Groups and Teams** and choose the groups you want to include in the catalog. To review app role assignments, select **Applications** and choose the applications you want to include in the catalog.

    Note

    In catalog access reviews, only groups, applications, and [custom data provided resources](custom-data-resource-access-reviews) are supported.
6. With the resources selected, select **Add** to save them in the catalog.
7. To enable the review to also include data from custom data providers, select **Custom Data Provided Resource**, and provide the name and description of the resource. For more information, see [custom data provided resource](custom-data-resource-access-reviews).

For more information on creating a catalog and adding resources, see [Create and manage a catalog of resources](entitlement-management-catalog-create). &gt; [!NOTE] &gt; Changes made within 12 hours before an access review starts such as adding users or resources may not be reflected in that review .

## Create a catalog access review

Once you add resources to a catalog, you can create a catalog access review so that reviewers can review access across all of these resources at once for the users they manage. To create a catalog access review, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access Reviews** &gt; **New access review**.
3. On the Access reviews template screen, select **Review users access across multiple resource types within a catalog** to select the **catalog review template**. ![Screenshot of the access review templates page.](media/catalog-access-reviews/access-review-templates.png)
4. Enter [basic information](create-access-review) about the workflow and select **Next**.
5. On the **resources** tab, select the catalog where you added the resources and select **Next**.
6. On the **Reviewers and schedule** tab, choose reviewers.
7. Optionally, you can configure [multi-stage reviews](using-multi-stage-reviews), where the resource owners (group or application owners) serve as secondary reviewers.
8. Configure **reviewer experience** options (email notifications, reminders, justification requirements) and **completion settings**.
9. Select **Create** to finalize the access review.

You can also create an access review programmatically using Microsoft Graph. For more information, see [Create a single stage access review on a catalog](/en-us/graph/api/accessreviewset-post-definitions?view=graph-rest-beta&amp;tabs=http&amp;preserve-view=true#example-6-create-a-single-stage-access-review-on-a-catalog).

## Upload data from custom data resources

If you have added custom data provided resources to the catalog, then you must upload the data while the review instance is initializing. For more information, see [custom data resource access review](custom-data-resource-access-reviews).

## Completing a catalog access review

When the catalog access review is created, reviewers receive an email notification that directs them to the myaccess portal. They can also directly navigate to the My Access portal where they can view their direct report's access to all resources in the catalog.

To complete a catalog access review, follow these steps:

1. Sign in to the My Access portal at https://myaccess.microsoft.com as the reviewer of the users you want to complete the catalog access review for.
2. In the left menu, select **Access reviews** to see a list of access reviews pending approval.
3. Select the **Multi-resource** tab to see a list of pending catalog access reviews.
4. For each access item, choose **Approve** or **Deny**, and provide a justification if required.
5. Select **Submit** to record your decisions.

On the review end date, all decisions, except those for custom disconnected resources, are automatically applied.