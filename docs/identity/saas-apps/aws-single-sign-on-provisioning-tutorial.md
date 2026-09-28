---
layout: Conceptual
title: Configure AWS IAM Identity Center (successor to AWS single sign-on) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/aws-single-sign-on-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to AWS IAM Identity Center.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
locale: en-us
document_id: a63d94b1-c9fe-53e6-959e-790b57d3c3ce
document_version_independent_id: 3a8cb353-6c8d-10a6-9ffd-2cbabb3e74e3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/aws-single-sign-on-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/aws-single-sign-on-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/aws-single-sign-on-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: efb9f009-3294-566a-2ba7-b8f9d783a42f
---

# Configure AWS IAM Identity Center (successor to AWS single sign-on) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both AWS IAM Identity Center (successor to AWS single sign-on) and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [AWS IAM Identity Center](https://console.aws.amazon.com/singlesignon) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in AWS IAM Identity Center
- Remove users in AWS IAM Identity Center when they no longer require access
- Keep user attributes synchronized between Microsoft Entra ID and AWS IAM Identity Center
- Provision groups and group memberships in AWS IAM Identity Center
- [aws singlesign-on document](aws-single-sign-on-tutorial) to AWS IAM Identity Center
- Long lived bearer token authentication supported.

AWS IAM Identity Center is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A SAML connection from your Microsoft Entra account to AWS IAM Identity Center, as described in [Tutorial](aws-single-sign-on-tutorial)

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and AWS IAM Identity Center](../app-provisioning/customize-application-attributes).

## Step 2: Configure AWS IAM Identity Center to support provisioning with Microsoft Entra ID

1. Open the [AWS IAM Identity Center](https://console.aws.amazon.com/singlesignon).
2. Choose **Settings** in the left navigation pane
3. In **Settings**, select Enable in the Automatic provisioning section.

    ![Screenshot of enabling automatic provisioning.](media/aws-single-sign-on-provisioning-tutorial/automatic-provisioning.png)
4. In the Inbound automatic provisioning dialog box, copy and save the **SCIM endpoint** and **Access Token** (visible after selecting Show Token). These values are entered in the **Tenant URL** and **Secret Token** field in the Provisioning tab of your AWS IAM Identity Center application. ![Screenshot of extracting provisioning configurations.](media/aws-single-sign-on-provisioning-tutorial/inbound-provisioning.png)

## Step 3: Add AWS IAM Identity Center from the Microsoft Entra application gallery

Add AWS IAM Identity Center from the Microsoft Entra application gallery to start managing provisioning to AWS IAM Identity Center. If you have previously setup AWS IAM Identity Center for SSO, you can use the same application. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to AWS IAM Identity Center (successor to AWS single sign-on)

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in AWS IAM Identity Center (successor to AWS single sign-on) based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for AWS IAM Identity Center (successor to AWS single sign-on) in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an app owner or [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **AWS IAM Identity Center (successor to AWS single sign-on)**.

    ![Screenshot of the AWS IAM Identity Center (successor to AWS single sign-on) link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your AWS IAM Identity Center (successor to AWS single sign-on) Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to AWS IAM Identity Center (successor to AWS single sign-on). If the connection fails, ensure your AWS IAM Identity Center (successor to AWS single sign-on) account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to AWS IAM Identity Center (successor to AWS single sign-on) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in AWS IAM Identity Center (successor to AWS single sign-on) for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the AWS IAM Identity Center (successor to AWS single sign-on) API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for Filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | displayName | String |  |
    | title | String |  |
    | emails[type eq "work"].value | String |  |
    | preferredLanguage | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | name.formatted | String |  |
    | addresses[type eq "work"].formatted | String |  |
    | addresses[type eq "work"].streetAddress | String |  |
    | addresses[type eq "work"].locality | String |  |
    | addresses[type eq "work"].region | String |  |
    | addresses[type eq "work"].postalCode | String |  |
    | addresses[type eq "work"].country | String |  |
    | phoneNumbers[type eq "work"].value | String |  |
    | externalId | String |  |
    | locale | String |  |
    | timezone | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |
12. Select **groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to AWS IAM Identity Center (successor to AWS single sign-on) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in AWS IAM Identity Center (successor to AWS single sign-on) for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for Filtering |
    | --- | --- | --- |
    | displayName | String | ✓ |
    | externalId | String |  |
    | members | Reference |  |
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Just-in-time (JIT) application access with PIM for groups

With PIM for Groups, you can provide just-in-time access to groups in Amazon Web Services and reduce the number of users that have permanent access to privileged groups in AWS.

**Configure your enterprise application for SSO and provisioning**

1. Add AWS IAM Identity Center to your tenant, configure it for provisioning as described in the article above, and start provisioning.
2. Configure [single sign-on](aws-single-sign-on-provisioning-tutorial) for AWS IAM Identity Center.
3. Create a [group](/en-us/azure/active-directory/fundamentals/how-to-manage-groups) that provides all users access to the application.
4. Assign the group to the AWS IAM Identity Center application.
5. Assign your test user as a direct member of the group created in the previous step, or provide them access to the group through an access package. This group can be used for persistent, non-admin access in AWS.

**Enable PIM for groups**

1. Create a second group in Microsoft Entra ID. This group provides access to admin permissions in AWS.
2. Bring the group under [management in Microsoft Entra PIM](/en-us/azure/active-directory/privileged-identity-management/groups-discover-groups).
3. Assign your test user as [eligible for the group in PIM](/en-us/azure/active-directory/privileged-identity-management/groups-assign-member-owner) with the role set to member.
4. Assign the second group to the AWS IAM Identity Center application.
5. Use on-demand provisioning to create the group in AWS IAM Identity Center.
6. Sign-in to AWS IAM Identity Center and assign the second group the necessary permissions to perform admin tasks.

Now any end user that was made eligible for the group in PIM can get JIT access to the group in AWS by [activating their group membership](/en-us/azure/active-directory/privileged-identity-management/groups-activate-roles#activate-a-role).

**Key considerations**

- How long does it take to have a user provisioned to the application?
    - When a user is added to a group in Microsoft Entra ID outside of activating their group membership using Microsoft Entra ID Privileged Identity Management (PIM):
        - The group membership is provisioned in the application during the next synchronization cycle. The synchronization cycle runs every 40 minutes.
    - When a user activates their group membership in Microsoft Entra ID PIM:
        - The group membership is provisioned in 2 – 10 minutes. When there is a high rate of requests at one time, requests are throttled at a rate of five requests per 10 seconds.
        - For the first five users within a 10-second period activating their group membership for a specific application, group membership is provisioned in the application within 2-10 minutes.
        - For the sixth user and above within a 10-second period activating their group membership for a specific application, group membership is provisioned to the application in the next synchronization cycle. The synchronization cycle runs every 40 minutes. The throttling limits are per enterprise application.
- If the user is unable to access the necessary group in AWS, please review the troubleshooting tips below, PIM logs, and provisioning logs to ensure that the group membership was updated successfully. Depending on how the target application has been architected, it may take additional time for the group membership to take effect in the application.
- You can create alerts for failures using [Azure Monitor](/en-us/entra/identity/app-provisioning/application-provisioning-log-analytics).
- Deactivation is done during the regular incremental cycle. It isn't processed immediately through on-demand provisioning.

## Troubleshooting Tips

### Missing attributes

When provisioning a user to AWS, they're required to have the following attributes

- firstName
- lastName
- displayName
- userName

Users who don't have these attributes fail with the following error

![errorcode](https://user-images.githubusercontent.com/83957767/146811532-8b95a90b-2a32-4094-87a3-1b8180793a66.png)

### Multi-valued attributes

AWS doesn't support the following multi-valued attributes:

- email
- phone numbers

Trying to flow the above as multi-valued attributes results in the following error message

![errorcode2](https://user-images.githubusercontent.com/83957767/146811704-8980c317-aa6b-43ad-bfb8-a17534fcb9d0.png)

There are two ways to resolve this

1. Ensure the user only has one value for phoneNumber/email
2. Remove the duplicate attributes. For example, having two different attributes being mapped from Microsoft Entra ID both mapped to "phoneNumber\_\_\_" on the AWS side would result in the error if both attributes have values in Microsoft Entra ID. Only having one attribute mapped to a "phoneNumber\_\_\_\_ " attribute would resolve the error.

### Invalid characters

Currently AWS IAM Identity Center isn't allowing some other characters that Microsoft Entra ID supports like tab (\t), new line (\n), return carriage (\r), and characters such as " &lt;|&gt;|;|:% ".

You can also check the AWS IAM Identity Center troubleshooting tips [here](https://docs.aws.amazon.com/singlesignon/latest/userguide/azure-ad-idp.html#azure-ad-troubleshooting).