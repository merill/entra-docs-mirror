---
layout: Conceptual
title: Create and manage downloadable access review history report - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/access-reviews-downloadable-review-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Using Microsoft Entra access reviews, you can download a review history for access reviews in your organization.
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 706805d0-10bf-a3aa-5c86-b3099dd8af3b
document_version_independent_id: 54485263-aebd-fed6-820c-3f4824742a6a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/access-reviews-downloadable-review-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/access-reviews-downloadable-review-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/access-reviews-downloadable-review-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 81d53938-0e6f-968b-35c0-1e0b2ab3ef34
---

# Create and manage downloadable access review history report - Microsoft Entra ID Governance | Microsoft Learn

With access reviews, you can create a downloadable review history to help your organization gain more insight. The report pulls the decisions taken by reviewers when a report is created. These reports can be constructed to include specific access reviews, for a specific time frame, and can be filtered to include different review types and review results.

## Who can access and request review history

Review history and request review history are available for any user if they're authorized to view access reviews. To see which roles can view and create access reviews, see [What resource types can be reviewed?](deploy-access-reviews#what-resource-types-can-be-reviewed). Least privilege roles that can create history reports include Privileged Role Administrator, Identity Governance Administrator, User Administrator, Security Reader, Global Reader, and Security Administrator role.

## How to create a review history report

**Prerequisite role:** All users authorized to view access reviews

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access Reviews** &gt; **Review History**.
3. Select **New report**.
4. Specify a review start and end date.
5. Select the review types and review results you want to include in the report.

    ![Access Reviews - Access Review History Report - Create](media/access-reviews-downloadable-review-history/create-review-history.png)
6. Then select **Create** to create an Access Review History Report.

## How to download review history reports

Once a review history report is created, you can download it. All reports that are created are available for download for 30 days in CSV format.

1. Select **Review History** under **Identity Governance**. All review history reports that you created are available.
2. Select the report you wish to download.

## What is included in a review history report?

The reports provide details on a per-user basis showing the following information:

| Element name | Description |
| --- | --- |
| AccessReviewId | Review object ID |
| AccessReviewSeriesId | Object ID of the review series, if the review is an instance of a recurring review. If the review is one time, the value is an empty GUID. |
| ReviewType | Review types include group, application, Microsoft Entra role, Azure role, and access package. |
| ResourceDisplayName | Display Name of the resource being reviewed |
| ResourceId | ID of the resource being reviewed |
| ReviewName | Name of the review |
| CreatedDateTime | Creation datetime of the review |
| ReviewStartDate | Start date of the review |
| ReviewEndDate | End date of the review |
| ReviewStatus | Status of the review. For all review statuses, see the access review status table [here](create-access-review) |
| OwnerId | Reviewer owner ID |
| OwnerName | Reviewer owner name |
| OwnerUPN | Reviewer owner User Principal Name |
| PrincipalId | ID of the principal being reviewed |
| PrincipalName | Name of the principal being reviewed |
| PrincipalUPN | User Principal Name of the user being reviewed |
| PrincipalType | Type of the principal. Options include user, group, and service principal |
| ReviewDate | Date of the review |
| ReviewResult | Review results include Deny, Approve, and Not reviewed |
| Justification | Justification for review result provided by reviewer |
| ReviewerId | Reviewer ID |
| ReviewerName | Reviewer Name |
| ReviewerUPN | Reviewer User Principal Name |
| ReviewerEmailAddress | Reviewer email address |
| AppliedByName | Name of the user who applied the review result |
| AppliedByUPN | User Principal Name of the user who applied the review result |
| AppliedByEmailAddress | Email address of the user who applied the review result |
| AppliedDate | Date when the review result was applied |
| AccessRecommendation | System recommendations include Approve, Deny, and No Info |
| SubmissionResult | Review result submission statuses include Applied and Not Applied. |