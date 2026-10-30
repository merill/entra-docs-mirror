---
layout: Conceptual
title: 'Tutorial: Govern and monitor applications - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/tutorial-govern-monitor
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to govern and monitor an application in Microsoft Entra ID, including access reviews and integrating logs with Azure Monitor.
ms.topic: tutorial
ms.date: 2024-12-04T00:00:00.0000000Z
ms.reviewer: saibandaru
ms.custom: enterprise-apps
locale: en-us
document_id: 05d57cf6-5bdb-2f1a-9895-3263c8f7b43b
document_version_independent_id: 79ec4cad-2d40-725e-6353-8058e813a06d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/tutorial-govern-monitor.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/tutorial-govern-monitor
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/tutorial-govern-monitor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a0e92f42-4e8f-12c9-ac6f-b6bda2517fb8
---

# Tutorial: Govern and monitor applications - Microsoft Entra ID | Microsoft Learn

The IT administrator at Fabrikam has added and configured an application from the [Microsoft Entra application gallery](overview-application-gallery). They also made sure that access can be managed and that the application is secure by using the information in [Tutorial: Manage application access and security](tutorial-manage-access-security). They now need to understand the resources that are available to govern and monitor the application.

Using the information in this tutorial, an administrator of the application learns how to:

- Create an access review
- Access the audit logs
- Access the sign-ins
- Send logs to Azure Monitor

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Identity Governance Administrator, Privileged Role Administrator, Cloud Application Administrator, or Application Administrator.
- An enterprise application that has been configured in your Microsoft Entra tenant.

## Create an access review

The administrator wants to make sure that users or guests have appropriate access. They decide to ask users of the application to participate in an access review and recertify or attest to their need for access. When the access review is finished, they can then make changes and remove access from users who no longer need it. For more information, see [Manage user and guest user access with access reviews](../../id-governance/manage-access-review).

To create an access review:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **ID Governance** &gt; **Access reviews**.
3. Select **New access review** to create a new access review.
4. In **Select what to review**, select **Applications**.
5. Select **+ Select application(s)**, select the application, and then choose **Select**.
6. Now you can select a scope for the review. Your options are:
    - **Guest users only** - This option limits the access review to only the Microsoft Entra B2B guest users in your directory.
    - **All users** - This option scopes the access review to all user objects associated with the resource. Select **All users**.
7. Select **Next: Reviews**.
8. In the **Specify reviewers** section, in the Select reviewers box, select **Selected user(s) or group(s)**, select **+ Select reviewers**, and then select the user account that is assigned to the application.
9. In the **Specify recurrence of review**section, specify the following selections:
    - **Duration (in days)** - Accept the default value of **3**.
    - **Review recurrence** - select **One time**.
    - **Start date** - Accept today's date as the start date.
10. Select **Next: Settings**.
11. In the **Upon completion settings** section, you can specify what happens after the review finishes. Select **Auto apply results to resource**.
12. Select **Next: Review + Create**.
13. Name the access review. Optionally, give the review a description. The name and description are shown to the reviewers.
14. Review the information and select **Create**.

### Start the access review

The access review starts in a few minutes and it appears in your list with an indicator of its status.

By default, Microsoft Entra ID sends an email to reviewers shortly after the review starts. If you choose not to have Microsoft Entra ID send the email, be sure to inform the reviewers that an access review is waiting for them to complete. You can show them the instructions for how to review access to groups or applications. If your review is for guests to review their own access, show them the instructions for how to review access for themselves to groups or applications.

If you've assigned guests as reviewers and they haven't accepted their invitation to the tenant, they won't receive an email from access reviews. They must first accept the invitation before they can begin reviewing.

### View the status of an access review

You can track the progress of access reviews as they're completed.

1. Go to **ID Governance** &gt; **Access reviews**.
2. In the list, select the access review you created.
3. On the **Overview** page, check the progress of the access review.

The **Results** page provides information on each user under review in the instance, including the ability to Stop, Reset, and Download results. To learn more, check out the [Complete an access review of groups and applications in Microsoft Entra access reviews](../../id-governance/complete-access-review) article.

## Access the audit logs

The Microsoft Entra audit logs capture a wide variety of activities within your tenant. These logs provide valuable insights into the activities you need to monitor. For more information, see [Audit logs in Microsoft Entra ID](../monitoring-health/concept-audit-logs).

To access the audit logs, go to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.

The audit logs capture activities that fall under the following categories. This list is not exhaustive. For a full list of the audit log categories and activities, see [Audit log activities](../monitoring-health/reference-audit-activities).

- Password reset activity
- Password reset registration activity
- Self-service groups activity
- Office365 Group Name Changes
- Account provisioning activity
- Password rollover status
- Account provisioning errors

## Access the sign-in logs

The Microsoft Entra sign-in logs capture interactive, non-interactive, managed identity, and service principal sign-ins. For more information, see [Sign-in logs in Microsoft Entra ID](../monitoring-health/concept-sign-ins).

To access the sign-in logs, go to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.

You also can view application sign-in information from the Enterprise applications area. The sign-in logs open the same logs from **Monitoring & health** &gt; **Sign-in logs**, but the filter is already set to the selected application. The **Usage & insights** report also summarizes sign-in activity for the application.

## Send logs to Azure Monitor

The Microsoft Entra activity logs only store information for seven days for Microsoft Entra ID Free and 30 days for Microsoft Entra ID P1/P2. Depending on your needs, you might require extra storage to back up the activity logs data.

Using Azure Monitor logs, you can retain the data for longer and enable powerful analysis tools, such as visualization and alerts. For more information about integrating logs with Azure Monitor logs, see [Integrate Microsoft Entra logs with Azure Monitor](../monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).

To send logs to Azure Monitor, you need a Log Analytics workspace. Once that's created, you configure diagnostic settings to integrate with Log Analytics. There are cost considerations associated with integrating logs with Azure Monitor and Log Analytics, so review this section of [Microsoft Entra activity logs in Azure Monitor](../monitoring-health/concept-log-monitoring-integration-options-considerations#cost-considerations) before proceeding.

With a Log Analytics workspace configured:

1. Select **Diagnostic settings**, and then select **Add diagnostic setting**. You can also select Export Settings from the Audit Logs or Sign-ins page to get to the diagnostic settings configuration page.
2. Choose the logs you want to stream, select the **Send to Log Analytics workspace** option, and complete the fields.
3. Select **Save**.

After about 15 minutes, verify that events are streamed to your Log Analytics workspace.