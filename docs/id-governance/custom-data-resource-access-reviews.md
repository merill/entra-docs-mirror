---
layout: Conceptual
title: Include custom data provided resource in the catalog for catalog user Access Reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/custom-data-resource-access-reviews
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
ms.reviewer: jgangadhar
description: Learn how to include custom data provided resource in Microsoft Entra catalogs to create user Access Reviews for disconnected applications.
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 48fc8acd-7bf6-9507-5131-a9fb182f4636
document_version_independent_id: 48fc8acd-7bf6-9507-5131-a9fb182f4636
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/custom-data-resource-access-reviews.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/custom-data-resource-access-reviews
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/custom-data-resource-access-reviews.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 62ce6ac4-c606-d5a8-72af-2eac307df7f7
---

# Include custom data provided resource in the catalog for catalog user Access Reviews - Microsoft Entra ID Governance | Microsoft Learn

Organizations often have applications that aren’t yet integrated with Microsoft Entra but still need to be governed. Using custom data provided resources, you can include these disconnected applications in Microsoft Entra ID access reviews by uploading their access data directly into a catalog.

This capability enables you to run user Access Reviews (UARs) across both Microsoft Entra-connected and custom resources within the same catalog. Reviewers can easily review and certify users’ access in the My Access portal, helping ensure consistent governance, improved visibility, and compliance across all resources whether or not they’re connected to Microsoft Entra.

## License requirements

This feature requires Microsoft Entra ID Governance or Microsoft Entra Suite subscriptions, for your organization's users. For more information, see the articles of each capability for more details. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Create a catalog

If you do not yet have a catalog, then create a new catalog. If you have a catalog already, then continue at the next section.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) or catalog creator.

    Tip

    Users who were assigned to the User Administrator role will no longer be able to create catalogs or manage access packages in a catalog they don't own. If users in your organization were assigned to the User Administrator role to configure catalogs, access packages, or policies in entitlement management, you should instead assign these users the Identity Governance Administrator role.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. Select **New catalog**.
4. Enter a unique name for the catalog and provide a description. Users see this information in an access package's details.
5. Select **Create** to create the catalog.

For more information on creating a catalog and adding resources, see [Create and manage a catalog of resources](entitlement-management-catalog-create).

## Add a custom data provided resource to a catalog

With a catalog created, you can add custom data provided resources to it by doing the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you created in the previous section.
4. On the left menu, select **Resources**.
5. Select **Add resources**.
6. Select the resource type: **custom data provided resource**.

    ![Screenshot of adding resources to a catalog.](media/custom-data-resource-access-reviews/catalog-resources.png)
7. On the **Basics** tab, enter:

    - **Name** – A name for the resource.
    - **Description** – A description for the resource.

    ![Screenshot of entering basic information for the custom data provided resource.](media/custom-data-resource-access-reviews/custom-resource-basic-information.png)
8. Select **Next: Details**.
9. On the **Details** tab, enter:

    - **Subscription** - Select the subscription.
    - **Resource group** - Select the resource group.
    - **Logic app name** - A name for the logic app.

    ![Screenshot of entering the details for the logic app as part of the custom data provided resource.](media/custom-data-resource-access-reviews/custom-resource-details-information.png)
10. Select **Create a logic app** to deploy the new logic app.
11. Select **Save**.
12. Select **Add**.

## Create a User Access Review

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access Reviews** &gt; **new access review**.
3. On the Access reviews template screen, select **Review users access across multiple resource types within a catalog**, and select **catalog review template**. ![Screenshot of the access review templates page.](media/catalog-access-reviews/access-review-templates.png)
4. Enter [basic information](create-access-review) about the workflow and select **Next**.
5. On the **resources** tab, select the catalog where you added the resources and select **Next**.
6. On the **Reviewers and schedule** tab, select reviewers you want to conduct access reviews. Currently only single stage reviews where the managers of the users who the access reviews are for can be set as reviewers.
7. Select **Create**.

You can also create an access review programmatically using Microsoft Graph. For more information, see [Create a single stage access review on a catalog](/en-us/graph/api/accessreviewset-post-definitions?view=graph-rest-beta&amp;tabs=http&amp;preserve-view=true#example-6-create-a-single-stage-access-review-on-a-catalog).

## Logic app integration

![Screenshot of the logic app trigger history.](media/custom-data-resource-access-reviews/logic-app-trigger.png)

The Logic App will receive a notification when the access review is initiated and can be configured to automatically upload custom data for the review. The Logic App will also receive a notification when the review completes and can be configured to set the apply result on the not reviewed or deny decisions. For more information, see [Configuring logic app for uploading and remediating decisions](https://github.com/Azure/azure-quickstart-templates/blob/master/application-workloads/identity-governance/byod-logic-app/README.md).

## Manually upload custom data

After creating the catalog access review, but before uploading your custom data, you must get both the Access Review object ID, and the Access Review instance object ID. To get this information, you'd do the following:

1. Browse to **ID Governance** &gt; **Access Reviews**.
2. Select the catalog access review you created.
3. On the Access Review overview screen, copy the **Object ID**.

    ![Screenshot of finding the access review object ID.](media/custom-data-resource-access-reviews/access-review-object-id.png)
4. Select the current instance of the access review on the access review overview screen.
5. On the access review instance screen, save the instance **Object ID**.

    ![Screenshot of finding the access review instance object ID.](media/custom-data-resource-access-reviews/access-review-instance-object-id.png)

    After copying both the access review object and access review instance object IDs, note that the status of the access review shows as **Initializing**.

    ![Initializing access review status.](media/custom-data-resource-access-reviews/initializing-access-review-status.png)
6. Return to the catalog you created, and select **Resources**.
7. On the resource screen for the catalog, select the custom data access resource you created, and select **Upload custom access data**.

    ![Screenshot of the upload custom access data option.](media/custom-data-resource-access-reviews/upload-custom-access-data.png)
8. On the Upload access data for custom resource screen under **Basics**, enter both the access review object ID, and the Access review instance object ID.

    ![Screenshot of basic information for custom data access.](media/custom-data-resource-access-reviews/upload-access-data-basics.png)
9. Under **Upload files** select up to 10 CSVs to include in the access data and select **Save**.

    ![Screenshot of uploading files to custom access data.](media/custom-data-resource-access-reviews/upload-access-data-files.png)

    Note

    To confirm all CSVs were uploaded successfully, view the [audit logs](entitlement-management-logs-and-reporting).
10. You have **up to two hours** from the time the review enters the *Initializing* state to complete the upload.

Note

Another option to automatically upload files when a review starts is through the use of a logic app: [logic app template](https://github.com/Azure/azure-quickstart-templates/blob/master/application-workloads/identity-governance/byod-logic-app/README.md).

## Manually apply results

When a review is complete, remediation can be set for any decision items for the custom data provided resource that do not have an **Approve** outcome.

1. Browse to **ID Governance** &gt; **Access Reviews**.
2. Select the catalog access review you created.
3. Select the current instance of the access review on the access review overview screen.
4. On results page, you can select one or more decisions to remediate.

    ![Screenshot of selecting decisions to remediate.](media/custom-data-resource-access-reviews/apply-results.png)
5. Select the **Apply results** to set the apply result to **Applied successfully**.

Note

Remediation can only be done for decisions that are for a custom data provided resource and where the outcome is not **Approve**.

## Custom data for access CSV fields

When uploading CSVs to be included in the access data, the following parameters are included in the template:

Note

All columns are mandatory.

| Parameter | Description |
| --- | --- |
| PrincipalId | The **Microsoft Entra ID User ID** of the user whose access needs to be reviewed. This value must match a valid Microsoft Entra user. |
| PrincipalType | Specifies the type of principal. For access reviews this will always be **EntraIdUser**. |
| PermissionId | A unique identifier for the permission in the application that will be reviewed. This helps distinguish between different permissions within the same app. |
| PermissionName | The display name of the permission that the user has in the application. Example: Read, Write, and Admin. |
| PermissionDescription | A brief explanation of what this permission allows within the application. This provides reviewers with context when deciding whether access should be continued. |
| PermissionType | Indicates the category of permission. |
| ScopeId | A unique identifier for the application. |
| ScopeDisplayName | The display name of the application. |
| EntitlementOwners\_Users | A comma separated list of the **Microsoft Entra ID User ID** owners of the permission. |
| EntitlementOwners\_Groups | A comma separated list of the **Microsoft Entra ID Group ID** group owners of the permission. |
| CustomData | Any additional information that could provide more context to a reviewer when making a decision. |

Note

For resource owner reviews, the resource owners are determined from the **EntitlementOwners\_Users** and/or **EntitlementOwners\_Groups** columns and must be specified.

You can also upload custom data via Graph by creating an upload session and then uploading a CSV file. For more information, see [customDataProvidedResourceUploadSession](/en-us/graph/api/resources/customdataprovidedresourceuploadsession?view=graph-rest-beta&amp;preserve-view=true).

## Active review state

At the **Active** stage:

- Reviewers receive an email notification.
- They can sign in to the [My Access portal](https://myaccess.microsoft.com) to view and complete their review decisions.

## Applying stage

In the **Applying** stage, you can get a list of denied users by making the [list decisions](/en-us/graph/api/accessreviewinstance-list-decisions?view=graph-rest-beta&amp;tabs=http&amp;preserve-view=true) API call:

```http
GET https://graph.microsoft.com/beta/identityGovernance/accessReviews/definitions/{access review object ID}/instances/{access review instance object ID}/decisions?$filter=(decision eq 'Deny' and resourceId eq '<custom data provided resource ID>')
```

For each decision item:

Remove access from your own system and then patch each decision item to indicate success or failure for removal by making the [update accessReviewInstanceDecisionItem](/en-us/graph/api/accessreviewinstancedecisionitem-update?view=graph-rest-beta&amp;tabs=http&amp;preserve-view=true) API call:

```http
PATCH https://graph.microsoft.com/beta/identityGovernance/accessReviews/definitions/{access review object ID}/instances/{access review instance object ID}/decisions/{decision ID}
Content-Type: application/json

{
 "applyResult": "AppliedSuccessfully",
 "applyDescription": "ServiceNow ticket created"
}
```

The review transition to the **Applied** state once all the custom data provided decisions have been applied. For example, if you have five decisions that must be made from the data, you must apply using PATCH each of five decision items before the review transitions to **Applied**.

## Review status

As reviewers take actions, the review progresses through several states:

| Review Status | Description |
| --- | --- |
| Initializing | Review instance created; waiting for custom data upload. |
| Active | Reviewers can take decisions in the My Access portal. |
| Applying | Review decisions are being remediated. |
| Applied | All decisions are marked as applied. |

## Timeframes summary

| Action | When | Time limit |
| --- | --- | --- |
| Upload custom data | During *Initializing* | Within two hours. |
| Review decisions | During *Active* | Until the review end date. |
| Apply decisions | During *Applying* | 30 days and review remains in applying status until all decisions are marked as applied. |