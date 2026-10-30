---
layout: Conceptual
title: Create an access review of Azure resource and Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to create an access review of Azure resource and Microsoft Entra roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.custom: pim, sfi-image-nochange
locale: en-us
document_id: abe62ea3-637f-16f7-c519-c2a95a063304
document_version_independent_id: 2c904332-0c2e-4145-a62e-c794c4ca31ec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: dac14205-66c6-90e9-9422-5b9b3e02c751
---

# Create an access review of Azure resource and Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

The need for access to privileged Azure resource and Microsoft Entra roles by your users changes over time. To reduce the risk associated with stale role assignments, you should regularly review access. You can use Microsoft Entra Privileged Identity Management (PIM) to create access reviews for privileged access to Azure resource and Microsoft Entra roles. You can also configure recurring access reviews that occur automatically. This article describes how to create one or more access reviews.

## Prerequisites

Using Privileged Identity Management requires licenses. For more information on licensing, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals) .

For more information about licenses for PIM, see [License requirements to use Privileged Identity Management](../licensing-fundamentals).

To create access reviews for Azure resources, you must be assigned to the [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or the [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) role for the Azure resources. To create access reviews for Microsoft Entra roles, you must be assigned at least the [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator) role.

Using Access Reviews for **Service Principals** requires a Microsoft Entra Workload ID Premium plan in addition to a Microsoft Entra ID P2 or Microsoft Entra ID Governance license.

- Workload Identities Premium licensing: You can view and acquire licenses on the [Workload Identities blade](https://portal.azure.com/#view/Microsoft_Azure_ManagedServiceIdentity/WorkloadIdentitiesBlade) in the Microsoft Entra admin center.

Note

Access reviews capture a snapshot of access at the beginning of each review instance. Any changes made during the review process will be reflected in the subsequent review cycle. Essentially, with the commencement of each new recurrence, pertinent data regarding the users, resources under review, and their respective reviewers is retrieved.

## Create access reviews

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user that is assigned to one of the prerequisite roles.
2. Browse to **ID Governance** &gt; **Privileged Identity Management**.
3. For **Microsoft Entra roles**, select **Microsoft Entra roles**. For **Azure resources**, select **Azure resources**.

    [![Select Identity Governance in the Microsoft Entra admin center screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/identity-governance.png)](media/pim-create-azure-ad-roles-and-resource-roles-review/identity-governance.png#lightbox)
4. For **Microsoft Entra roles**, select **Microsoft Entra roles** again under **Manage**. For **Azure resources**, select the subscription you want to manage.
5. Under Manage, select **Access reviews**, and then select **New** to create a new access review.

    ![Microsoft Entra roles - Access reviews list showing the status of all reviews screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/access-reviews.png)
6. Name the access review. Optionally, give the review a description. The name and description are shown to the reviewers.

    ![Create an access review - Review name and description screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/name-description.png)
7. Set the **Start date**. By default, an access review occurs once. It starts at creation time, and it ends in one month. You can change the start and end dates to have an access review start in the future and last however many days you want.

    ![Start date, frequency, duration, end, number of times, and end date screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/start-end-dates.png)
8. To make the access review recurring, change the **Frequency** setting from **One time** to **Weekly**, **Monthly**, **Quarterly**, **Annually**, or **Semi-annually**. Use the **Duration** slider or text box to specify review duration. For example, the maximum duration that you can set for a monthly review is 27 days, to avoid overlapping reviews.
9. Use the **End** setting to specify how to end the recurring access review series. The series can end in three ways: it runs continuously to start reviews indefinitely, until a specific date, or after a defined number of occurrences completes. You, or another administrator who can manage reviews, can stop the series after creation by changing the date in **Settings**, so that it ends on that date.
10. In the **Users Scope** section, select the scope of the review. For **Microsoft Entra roles**, the first scope option is Users and Groups. Directly assigned users and [role-assignable groups](../../identity/role-based-access-control/groups-concept) are included in this selection. For **Azure resource roles**, the first scope is Users. Groups assigned to Azure resource roles are expanded to display transitive user assignments in the review with this selection. You might also select **Service Principals** to review the machine accounts with direct access to either the Azure resource or Microsoft Entra role.

    ![Users scope to review role membership of screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/users.png)
11. Or, you can create access reviews only for inactive users. In the *Users scope* section, set the **Inactive users (on tenant level) only** to **true**. If the toggle is set to *true*, the scope of the review focuses on inactive users only. Then, specify **Days inactive**. You can specify up to 730 days (two years). Users inactive for the specified number of days are the only users in the review.
12. Under **Review role membership**, select the privileged Azure resource or Microsoft Entra roles to review.

    Note

    Selecting more than one role will create multiple access reviews. For example, selecting five roles will create five separate access reviews.

    ![Review role memberships screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/review-role-membership.png)
13. In **assignment type**, scope the review by how the principal was assigned to the role. Choose **eligible assignments only** to review eligible assignments (regardless of activation status when the review is created) or **active assignments only** to review active assignments. Choose **all active and eligible assignments** to review all assignments regardless of type.

    ![Reviewers list of assignment types screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/assignment-type-select.png)
14. In the **Reviewers** section, select one or more people to review all the users. Or you can select to have the members review their own access.

    ![Reviewers list of selected users or members (self)](media/pim-create-azure-ad-roles-and-resource-roles-review/reviewers.png)

    - **Selected users** - Use this option to designate a specific user to complete the review. This option is available regardless of the scope of the review, and the selected reviewers can review users, groups, and service principals.
    - **Members (self)** - Use this option to have the users review their own role assignments. This option is only available if the review is scoped to **Users and Groups** or **Users**. For **Microsoft Entra roles**, role-assignable groups aren't part of the review when this option is selected.
    - **Manager** – Use this option to have the user’s manager review their role assignment. This option is only available if the review is scoped to **Users and Groups** or **Users**. Upon selecting Manager, you also can specify a fallback reviewer. Fallback reviewers are asked to review a user when the user has no manager specified in the directory. For **Microsoft Entra roles**, role-assignable groups are reviewed by the fallback reviewer if one is selected.

### Upon completion settings

1. To specify what happens after a review completes, expand the **Upon completion settings** section.

    ![Screenshot showing the upon completion settings to auto apply, and choices should reviewer not respond.](media/pim-create-azure-ad-roles-and-resource-roles-review/upon-completion-settings.png)
2. If you want to automatically remove access for users that were denied, set **Auto apply results to resource** to **Enable**. If you want to manually apply the results when the review completes, set the switch to **Disable**.
3. Use the **If reviewers don't respond** list to specify what happens for users that aren't reviewed by the reviewer within the review period. This setting doesn't impact users who were already reviewed.

    - **No change** - Leave user's access unchanged
    - **Remove access** - Remove user's access
    - **Approve access** - Approve user's access
    - **Take recommendations** - Take the system's recommendation on denying or approving the user's continued access
4. Use the **Action to apply on denied guest users** list to specify what happens for guest users that are denied. This setting isn't editable for Microsoft Entra ID and Azure resource role reviews at this time; guest users, like all users, always lose access to the resource if denied.

    ![Upon completion settings - Action to apply on denied guest users screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/action-to-apply-on-denied-guest-users.png)
5. You can send notifications to other users or groups to receive review completion updates. This feature allows for stakeholders other than the review creator to be updated on the progress of the review. To use this feature, select **Select User(s) or Group(s)** and add any users, or groups you want receive completion status notifications.

    ![Upon completion settings - Add additional users to receive notifications screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/upon-completion-settings-additional-receivers.png)

### Advanced settings

1. To configure more settings, expand the **Advanced settings** section.

    ![Advanced settings for show recommendations, require reason on approval, mail notifications, and reminders screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/advanced-settings.png)
2. Set **Show recommendations** to **Enable** to show the reviewers the system recommendations based on the user's access information. Recommendations are based on a 30-day interval period. Users who have logged in the past 30 days are shown with recommended approval of access, while users who haven't logged in are shown with recommended denial of access. These sign-ins are irrespective of whether they were interactive. The last sign-in of the user is also displayed along with the recommendation.
3. Set **Require reason on approval** to **Enable** to require the reviewer to supply a reason for approval.
4. Set **Mail notifications** to **Enable** to have Microsoft Entra ID send email notifications to reviewers when an access review starts, and to administrators when a review completes.
5. Set **Reminders** to **Enable** to have Microsoft Entra ID send reminders of access reviews in progress to reviewers who haven't completed their review.
6. The content of the email sent to reviewers is autogenerated based on the review details, such as review name, resource name, and due date. If you need a way to communicate additional information such as additional instructions or contact information, you can specify these details in the **Additional content for reviewer email** section. These details are included in the invitation and reminder emails sent to assigned reviewers. The highlighted section is where this information is displayed.

    ![Content of the email sent to reviewers with highlights](media/pim-create-azure-ad-roles-and-resource-roles-review/email-info.png)

## Manage the access review

You can track the progress as the reviewers complete their reviews on the **Overview** page of the access review. No access rights are changed in the directory until the review is completed. [![Access reviews overview page showing the details of the access review for Microsoft Entra roles screenshot.](media/pim-create-azure-ad-roles-and-resource-roles-review/access-review-overview.png)](media/pim-create-azure-ad-roles-and-resource-roles-review/access-review-overview.png#lightbox)

After the access review, follow the steps in [Complete an access review of Azure resource and Microsoft Entra roles](pim-complete-roles-and-resource-roles-review) to see and apply the results.

If you're managing a series of access reviews, navigate to the access review, and you find upcoming occurrences in Scheduled reviews, and edit the end date or add/remove reviewers accordingly.

Based on your selections in **Upon completion settings**, auto-apply will be executed after the review's end date or when you manually stop the review. The status of the review changes from **Completed** through intermediate states such as **Applying** and finally to state **Applied**. You should expect to see denied users, if any, being removed from roles in a few minutes.

## Impact of groups assigned to Microsoft Entra roles and Azure resource roles in access reviews

• For **Microsoft Entra roles**, role-assignable groups can be assigned to the role using [role-assignable groups](../../identity/role-based-access-control/groups-concept). When a review is created on a Microsoft Entra role with role-assignable groups assigned, the group name shows up in the review without expanding the group membership. The reviewer can approve or deny access of the entire group to the role. Denied groups lose their assignment to the role when review results are applied.

• For **Azure resource roles**, any security group can be assigned to the role. When a review is created on an Azure resource role with a security group assigned, role reviewers can see a fully expanded view of the group's membership. When a reviewer denies a user that was assigned to the role via the security group, the user won't be removed from the group. This is because a group may be shared with other Azure or non-Azure resources. Administrators must implement the changes resulting from an access denial.

Note

It is possible for a security group to have other groups assigned to it. In this case, only the users assigned directly to the security group assigned to the role will appear in the review of the role.

## Update the access review

After one or more access reviews have been started, you might want to modify or update the settings of your existing access reviews. Here are some common scenarios that you might want to consider:

- **Adding and removing reviewers** - When updating access reviews, you might choose to add a fallback reviewer in addition to the primary reviewer. Primary reviewers may be removed when updating an access review. However, fallback reviewers aren't removable by design.

    Note

    Fallback reviewers can only be added when reviewer type is manager. Primary reviewers can be added when reviewer type is selected user.
- **Reminding the reviewers** - When updating access reviews, you might choose to enable the reminder option under Advanced Settings. Once enabled, users receive an email notification at the midpoint of the review period. Reviewers receive notifications regardless of whether they have completed the review or not.

    ![Screenshot of the reminder option under access reviews settings.](media/pim-create-azure-ad-roles-and-resource-roles-review/reminder-setting.png)
- **Updating the settings** - If an access review is recurring, there are separate settings under "Current" versus under "Series". Updating the settings under "Current" will only apply changes to the current access review while updating the settings under "Series" will update the setting for all future recurrences.

    [![Screenshot of the settings page under access reviews.](media/pim-create-azure-ad-roles-and-resource-roles-review/current-v-series-setting.png)](media/pim-create-azure-ad-roles-and-resource-roles-review/current-v-series-setting.png#lightbox)

Note

Creating Access Reviews for Azure resources using AOBO (Admin On Behalf Of) under the Azure Plan is not supported. If you're a CSP partner managing a customer's subscription via AOBO, you cannot create Access Reviews from your own (partner) tenant.**Workaround**: Have the CSP partner added as a **guest user** in the customer's tenant with the necessary permissions, and create the Access Review **from within the customer's tenant**.