---
layout: Conceptual
title: Change approval settings for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-approval-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to change approval and requestor information settings for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-26T00:00:00.0000000Z
locale: en-us
document_id: 1be40387-d7c0-48b8-d687-fa36b8727ae8
document_version_independent_id: 1bf72b62-4eca-6c96-b972-ce930cfa73f2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-approval-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-approval-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-approval-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d9b77755-134a-49e7-9a32-bb71c5aeb705
---

# Change approval settings for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

Each access package must have one or more access package assignment policies, before an identity can be assigned access. When an access package is created in the Microsoft Entra admin center, the Microsoft Entra admin center automatically creates the first access package assignment policy for that access package. The policy determines who can request access, and who if anyone must approve access.

As an access package manager, you can change the approval and requestor information settings for an access package at any time by editing an existing policy or adding a new extra policy for requesting access.

This article describes how to change the approval and requestor information settings for an existing access package, through an access package's policy.

## Approval

In the Approval section, you specify whether an approval is required when identities request this access package. The approval settings work in the following way:

- Only one of the selected approvers or fallback approvers needs to approve a request for single-stage approval.
- Only one of the selected approvers from each stage needs to approve a request for multi-stage approval for the request to progress to the next stage.
- If one of the selected approved in a stage denies a request before another approver in that stage approves it, or if no one approves, the request terminates and the identity doesn't receive access.
- The approver can be a specified identity or member of a group, the requestor's Manager, Internal sponsor, or External sponsor depending on who the policy is governing access.

For a demonstration of how to add approvers to a request policy, watch the following video:

For a demonstration of how to add a multi-stage approval to a request policy, watch the following video:

Note

Approvers aren't able to approve their own access package requests.

## Change approval settings of an existing access package assignment policy

Follow these steps to specify the approval settings for requests for the access package through a policy:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access Package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
3. On the Access packages page, open an access package.
4. Either select a policy to edit or add a new policy to the access package

    1. Select **Policies** and then **Add policy** if you want to create a new policy.
    2. Select the policy you wish to edit and then select **edit**.
5. Go to the **Request** tab.
6. To set who can request access for identities, choose either Self, Admin, or Manager.
7. To require users to provide a justification to request the access package, set the **Require requestor justification** toggle to **Yes**.
8. Now determine if requests require single or multi-stage approval. Set the **How many stages** to the number of stages of approval needed.

    ![Access package - Requests - Approval settings](media/entitlement-management-access-package-approval-policy/approval.png)

Use the following steps to add approvers after selecting how many stages you require:

### Single-stage approval

1. Add the **First Approver**:

    If the policy is set to govern access for users in your directory, you can select **Manager as approver**. Or, add a specific user by selecting **Add approvers** after selecting **Choose specific approvers** from the dropdown menu.

    ![Access package - Requests - For users in directory - First Approver](media/entitlement-management-access-package-approval-policy/approval-single-stage-first-approver-manager.png)

    If this policy is set to govern access for users not in your directory, you can select **External sponsor** or **Internal sponsor**. Or, add a specific user by clicking **Add approvers** or groups under Choose specific approvers.

    ![Access package - Requests - For users out of directory - First Approver](media/entitlement-management-access-package-approval-policy/out-directory-first-approver.png)
2. If you selected **Manager** as the first approver, select **Add fallback** to select one, or more users or groups in your directory to be a fallback approver. Fallback approvers receive the request if entitlement management can't find the manager for the user requesting access.

    The manager is found by entitlement management using the **Manager** attribute. The attribute is in the user's profile in Microsoft Entra ID. For more information, see [Add or update a user's profile information using Microsoft Entra ID](../fundamentals/how-to-manage-user-profile-info).
3. If you selected **Choose specific approvers**, select **Add approvers** to choose one, or more, users or groups in your directory to be approvers.
4. In the box under **Decision must be made in how many days?**, specify the number of days that an approver has to review a request for this access package.

    If a request isn't approved within this time period, it's automatically denied. The user has to submit another request for the access package.
5. To require approvers to provide a justification for their decision, set Require approver justification to **Yes**.

    The justification is visible to other approvers and the requestor.

### Multi-stage approval

If you selected a multi-stage approval, you need to add an approver for each extra stage.

1. Add the **Second Approver**:

    If the users are in your directory, add a specific user as the second approver by selecting **Add approvers** under Choose specific approvers.

    ![Access package - Requests - For users in directory - Second Approver](media/entitlement-management-access-package-approval-policy/in-directory-second-approver.png)

    If the users aren't in your directory, select **Internal sponsor** or **External sponsor** as the second approver. After selecting the approver, add the fallback approvers.

    ![Access package - Requests - For users out of directory - Second Approver](media/entitlement-management-access-package-approval-policy/out-directory-second-approver.png)
2. Specify the number of days the second approver has to approve the request in the box under **Decision must be made in how many days?**.
3. Set the Require approver justification toggle to **Yes** or **No**.

    You also can add an extra stage for a three-stage approval process. For example, you might want an employee’s manager to be the first stage approver for an access package. But, one of the resources in the access package contains confidential information. In this case, you could designate the resource owner as a second approver and a security reviewer as the third approver. That allows a security team to have oversight into the process and the ability to, for example, reject a request based on risk criteria not known to the resource owner.
4. Add the **Third Approver**:

    If the users are in your directory, add a specific user as the third approver by clicking **Add approvers** under Choose specific approvers.

    If the users aren't in your directory, you also can select **Internal sponsor** or **External sponsor** as the third approver. After selecting the approver, add the fallback approvers.

    Note

Like the second stage, if the users are in your directory and \*\*Manager as approver\*\* is selected in either the first or second stage of approval, you'll only see an option to select specific approvers for the third stage of approval.

If you want to designate the manager as a third approver, you can adjust your selections in the previous approval stages to ensure that \*\*Manager as approver\*\* isn’t selected. Then, you should see \*\*Manager as approver\*\* as an option in the dropdown.

If the users aren’t in your directory and you haven't selected \*\*Internal sponsor\*\* or \*\*External sponsor\*\* as approvers in previous stages, you'll see them as options for \*\*Third Approver\*\*. Otherwise, you'll only be able to select \*\*Choose specific approvers\*\*.
5. Specify the number of days the third approver has to approve the request in the box under **Decision must be made in how many days?**.
6. Set the Require approver justification toggle to **Yes** or **No**.

### Alternate approvers

You can specify alternate approvers, similar to specifying the primary approvers who can approve requests on each stage. Having alternate approvers help ensure that the requests are approved or denied before they expire (timeout). You can list alternate approvers alongside the primary approver on each stage.

By specifying alternate approvers on a stage, if the primary approvers were unable to approve or deny the request, the pending request gets forwarded to the alternate approvers, per the forwarding schedule you specified during policy setup. They receive an email to approve or deny the pending request.

After the request is forwarded to the alternate approvers, the primary approvers can still approve or deny the request. Alternate approvers use the same My Access site to approve or deny the pending request.

You can list people or groups of people to be approvers and alternate approvers. Ensure that you list different sets of people to be the first, second, and alternate approvers. For example, if you listed Alice and Bob as the first stage approver(s), list Carol and Dave as the alternate approvers. Use the following steps to add alternate approvers to an access package:

1. Under the approver on a stage, select **Show advanced request settings**.

    ![Access package - Policy - Show advanced request settings](media/entitlement-management-access-package-approval-policy/alternate-approvers-click-advanced-request.png)
2. Set **If no action taken, forward to alternate approvers?** toggle to **Yes**.
3. Select **Add alternate approvers** and select the alternate approver(s) from the list.

    ![Access package - Policy - Add Alternate Approvers](media/entitlement-management-access-package-approval-policy/alternate-approvers-add.png)

    If you select Manager as approver for the First Approver, you have an extra option, **Second level manager as alternate approver**, available to choose in the alternate approver field. If you select this option, you need to add a fallback approver to forward the request to in case the system can't find the second level manager.
4. In the **Forward to alternate approver(s) after how many days** box, put in the number of days the approvers have to approve or deny a request. If no approvers have approved or denied the request before the request duration, the request expires (timeout), and the user has to submit another request for the access package.

    Requests can only be forwarded to alternate approvers a day after the request has been initiated. To use alternate approval, the request time-out needs to be at least four days.

## Who can request access

1. After deciding who the access package is for you can designate who can request access for the access package. You can choose Self, Admin, or Manager as those who can request access.

    If you selected **None (administrator direct assignments only)** and you set enable to **No**, then administrators can't directly assign this access package.

    ![Access package - Policy- Enable policy setting](media/entitlement-management-access-package-approval-policy/enable-requests.png)
2. When new requests are enabled, you can specify whether you want to **Allow managers to request on behalf of their employees (preview)**. ![Screenshot of manager approval of request options.](media/entitlement-management-access-package-approval-policy/manager-enable-approval.png)
3. Select **Next**.

## Collect additional requestor information for approval

In order to make sure users are getting access to the right access packages, you can require requestors to answer custom text field or Multiple Choice questions at the time of request. The questions will then be shown to approvers to help them make a decision.

1. Go to the **Requestor information** tab and select the **Questions** sub tab.
2. Type in what you want to ask the requestor, also known as the display string, for the question in the **Question** box.

    ![Access package - Policy- Enable Requestor information setting](media/entitlement-management-access-package-approval-policy/add-requestor-info-question.png)
3. If the community of users who need access to the access package don't all have a common preferred language, then you can improve the experience for users requesting access on myaccess.microsoft.com. To improve the experience, you can provide alternative display strings for different languages. For example, if a user's web browser is set to Spanish, and you have Spanish display strings configured, then those strings are displayed to the requesting user. To configure localization for requests, select **add localization**.

    1. Once in the **Add localizations for question** pane, select the **language code** for the language in which you're localizing the question.
    2. In the language you configured, type the question in the **Localized Text** box.
    3. Once you've added all the localizations needed, select **Save**.

    ![Access package - Policy- Configure localized text](media/entitlement-management-access-package-approval-policy/add-localization-question.png)
4. Select the **Answer format** in which you would like requestors to answer. Answer formats include: *short text*, *Multiple Choice*, and *long text*.

    ![Access package - Policy- Select Edit and localize multiple choice answer format](media/entitlement-management-access-package-approval-policy/answer-format-view-edit.png)
5. If selecting Multiple Choice, select the **Edit and localize** button to configure the answer options.

    1. After selecting Edit and localize the **View/edit question** pane opens.
    2. Type in the response options you wish to give the requestor when answering the question in the **Answer values** boxes.
    3. Type in as many responses as you need.
    4. If you would like to add your own localization for the Multiple Choice options, select the **Optional language code** for the language in which you want to localize a specific option.
    5. In the language you configured, type the option in the Localized text box.
    6. Once you add all of the localizations needed for each Multiple Choice option, select **Save**.

    ![Access package - Policy- Enter multiple choice options](media/entitlement-management-access-package-approval-policy/answer-multiple-choice.png)
6. If you would like to include a syntax check for text answers to questions, you can also specify a custom regex pattern.[![Screenshot of the add regex localization policy.](media/entitlement-management-access-package-approval-policy/add-regex-localization.png)](media/entitlement-management-access-package-approval-policy/add-regex-localization.png#lightbox) If you would like to include a syntax check for text answers to questions, you can also specify a custom regex pattern.
7. To require requestors to answer this question when requesting access to an access package, select the check box under **Required**.
8. Fill out the remaining tabs (for example, Lifecycle) based on your needs.

After you configure requestor information in your access package's policy, can view the requestor's responses to the questions. For guidance on seeing requestor information, see [View requestor's answers to questions](entitlement-management-request-approve#view-requestors-answers-to-questions).