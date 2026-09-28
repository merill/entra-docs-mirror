---
layout: Conceptual
title: Complete an access review of groups & applications - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/complete-access-review
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to complete an access review of group members or application access in Microsoft Entra access reviews.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 92b6e44f-9a0e-1930-b007-4d9e26537aa7
document_version_independent_id: f4bb0402-3ac9-7109-cd84-8f575f14acdc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/complete-access-review.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/complete-access-review
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/complete-access-review.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 89aa2adc-c0c6-7ed3-1427-fdf5ad9662b5
---

# Complete an access review of groups & applications - Microsoft Entra ID Governance | Microsoft Learn

As an administrator, you [create an access review of groups or applications](create-access-review) and reviewers [perform the access review](perform-access-review). This article describes how to see the results of the access review and apply them.

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Prerequisites

- Microsoft Entra ID P2 or Microsoft Entra ID Governance
- At least the role of User Administrator or Identity Governance Administrator to manage access reviews on groups and applications. Users who have at least the Privileged Role Administrator role can manage reviews of role-assignable groups, see: [Use Microsoft Entra groups to manage role assignments](../identity/role-based-access-control/groups-concept)
- Security readers have read access.

For more information, see: [License requirements](access-reviews-overview#license-requirements).

## View the status of an access review

Follow these steps to track the progress of access reviews as they complete.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access Reviews**.
3. In the list, select an access review.

    On the **Overview** page, you can see the progress of the **Current** instance of the review. If there isn't an active instance open at the time, you see information on the previous instance. No access rights are changed in the directory until the review is completed.

    ![Review of All company group](media/complete-access-review/all-company-group.png)

    All blades under **Current** are only viewable during the duration of each review instance.

    Note

    While the **Current** access review only shows information about the active review instance, you can get information about reviews yet to take place in the **Series** under the **View status of multi-stage review (preview)** section.

    The Results page provides more information on each user under review in the instance, including the ability to Stop, Reset, and Download results.

    ![Review guest access across Microsoft 365 groups](media/complete-access-review/all-company-group-results.png)

    If you're viewing an access review that reviews guest access across Microsoft 365 groups, the Overview pane lists each group in the review.

    ![review guest access across Microsoft 365 groups](media/complete-access-review/review-guest-access-across-365-groups.png)

    Select a group to see the progress of the review on that group, also to Stop, Reset, Apply, and Delete.

    ![review guest access across Microsoft 365 groups in detail](media/complete-access-review/progress-group-review.png)
4. If you want to stop an access review before it reaches the scheduled end date, select the **Stop** button.

    When you stop a review, reviewers can no longer provide responses. You can't restart a review after it's stopped.

    Note

    The Stop option is only available for a specific review instance, not for the entire recurring review series. To stop a recurring review series, you can edit the series and update the **End** option to the desired date when you want the series to stop. This change prevents any future review instances from being created beyond the updated end date.
5. If you're no longer interested in the access review, you can delete it by clicking the **Delete** button.

### View status of multi-stage review (preview)

To see the status and stage of a multi-stage access review:

1. Select the multi-stage review you want to check the status of or see what stage it's in.
2. Select **Results** on the left nav menu under **Current**.
3. On the results page, under **Status**, you can see which stage the multi-stage review is in. The next stage of the review won't become active until the duration specified during the access review setup passes.
4. If a decision is made, but the review duration for this stage hasn't expired yet, you can select **Stop current stage** button on the results page. This will trigger the next stage of review.

## Retrieve the results

To view the results for a review, select the **Results** page. To view just a user's access, in the Search box, type the display name or user principal name of a user whose access was reviewed.

![Retrieve results for an access review](media/complete-access-review/retrieve-results.png)

To view the results of a completed instance of an access review that is recurring, select **Review history**, then select the specific instance from the list of completed access review instances, based on the instance's start and end date. The results of this instance can be obtained from the **Results** page. Recurring access reviews provide a continuous view of access to resources that might need to be updated more often than one-time access reviews.

To retrieve the results of an access review, both in-progress or completed, select the **Download** button. The resulting CSV file can be viewed in Excel or in other programs that open UTF-8 encoded CSV files.

### Retrieve the results programmatically

You can also retrieve the results of an access review using Microsoft Graph or PowerShell.

You'll first need to locate the [instance](/en-us/graph/api/resources/accessreviewinstance) of the access review. If the [accessReviewScheduleDefinition](/en-us/graph/api/resources/accessReviewScheduleDefinition) is a recurring access review, instances represent each recurrence. A review that doesn't recur has exactly one instance. Instances also represent each unique group being reviewed in the schedule definition. If a schedule definition reviews multiple groups, each group has a unique instance for each recurrence. Every instance contains a list of decisions that reviewers can take action on, with one decision per identity being reviewed.

Once you identify the instance, to retrieve the decisions using Graph, call the Graph API to [list decisions from an instance](/en-us/graph/api/accessreviewinstance-list-decisions). If the instance is a multi-stage review, call the Graph API to [list decisions from a multi-stage access review](/en-us/graph/api/accessreviewstage-list-decisions). The caller must be either a user in an appropriate role with an application that has the delegated `AccessReview.Read.All` or `AccessReview.ReadWrite.All` permission, or an application with the `AccessReview.Read.All` or `AccessReview.ReadWrite.All` application permission. For more information, see the tutorial for how to [review a security group](/en-us/graph/tutorial-accessreviews-securitygroup).

You can also retrieve the decisions in PowerShell with the `Get-MgIdentityGovernanceAccessReviewDefinitionInstanceDecision` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module. The default page size of this API is 100 decision items.

## Apply the changes

If **Auto apply results to resource** was enabled based on your selections in **Upon completion settings**, autoapply executes once a review instance completes, or earlier if you manually stop the review.

If **Auto apply results to resource** wasn't enabled for the review, navigate to **Review History** under **Series** after the review duration ends or the review was stopped early, and select on the instance of the review you’d like to Apply.

![Apply access review changes](media/complete-access-review/apply-changes.png)

Select **Apply** to manually apply the changes. If a user's access was denied in the review, when you select **Apply**, Microsoft Entra ID removes their membership or application assignment.

![Apply access review changes button](media/complete-access-review/apply-changes-button.png)

The status of the review changes from **Completed** through intermediate states such as **Applying** and finally to state **Result applied**. You should expect to see denied users, if any, being removed from the group membership or application assignment in a few minutes.

Manually or automatically applying results doesn't have an effect on a group that originates in an on-premises directory. If you want to change a group that originates on-premises, download the results and apply those changes to the representation of the group in that directory.

Note

Some denied users are unable to have results applied to them. Scenarios where this could happen include:

- Reviewing members of a synced on-premises Windows Server AD group: If the group is synced from on-premises Windows Server AD, the group can't be managed in Microsoft Entra ID and therefore membership can't be changed.
- Reviewing a resource (role, group, application) with nested groups assigned: For users who have membership through a nested group, we won't remove their membership to the nested group and therefore they'll retain access to the resource being reviewed.
- User not found / other errors can also result in an apply result not being supported.
- Reviewing the members of mail enabled group: The group can't be managed in Microsoft Entra ID, so membership can't be changed.
- Reviewing an Application that uses group assignment won't remove the members of those groups, so they'll retain the existing access from the group relationship for the application assignment

Note

Access review decisions don't change membership in dynamic groups. These groups are managed by rules, and users remain members as long as they match the rule conditions.

## Actions taken on denied guest users in an access review

On review creation, the creator can choose between two options for denied guest users in an access review.

- Denied guest users can have their access to the resource removed. This setting is the default.
- The denied guest user can be blocked from signing in for 30 days, then deleted from the tenant. During the 30-day period the guest user is able to be restored access to the tenant by an administrator. After the 30-day period is completed, if the guest user hasn't been granted access to the resource again, they're removed from the tenant permanently. In addition, using the Microsoft Entra admin center, a Global Administrator can explicitly [permanently delete a recently deleted user](../fundamentals/users-restore) before that time period is reached. Once a user is permanently deleted, the data about that guest user is removed from active access reviews. Audit information about deleted users remains in the audit log.

### Actions taken on denied B2B direct connect users

Denied B2B direct connect users and teams lose access to all shared channels in the Team.