---
layout: Conceptual
title: Configure monday.com for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mondaycom-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to monday.com.
ms.topic: how-to
ms.date: 2026-04-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ca95fea3-9d7b-e504-3c04-0283665a7c39
document_version_independent_id: a767049c-4097-892b-16e7-1b20818c20d1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mondaycom-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mondaycom-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mondaycom-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ee85a389-a916-dc9d-7ba8-cf01230fbf47
---

# Configure monday.com for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both monday.com and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [monday.com](https://www.monday.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in monday.com
- Remove users in monday.com when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and monday.com
- Provision groups and group memberships in monday.com
- [Single sign-on](mondaycom-tutorial) to monday.com (recommended)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
        - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
        - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
        - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- An **Enterprise** monday.com account.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and monday.com](../app-provisioning/customize-application-attributes).

## Step 2: Configure monday.com to support provisioning with Microsoft Entra ID

1. Sign in to [monday.com](https://www.monday.com/). Select your profile picture , on the left navigation pane.
2. Navigate to **Admin &gt; Security**.
3. Select **Open** in the **SCIM** section under the **Login** tab.

![Scim Provisioning Tab](media/mondaycom-provisioning-tutorial/provisioning-tab-monday.png)

1. Select **Generate**. These are the **Tenant URL** and **Secret Token** you need for step 5.

Note

Don't share or save this secret token. You can always generate a new token whenever and wherever it's required.

## Step 3: Add monday.com from the Microsoft Entra application gallery

Add monday.com from the Microsoft Entra application gallery to start managing provisioning to monday.com. If you have previously setup monday.com for SSO you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to monday.com

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for monday.com in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **monday.com**.

    ![The monday.com link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your monday.com Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to monday.com. If the connection fails, ensure your monday.com account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to monday.com in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in monday.com for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the monday.com API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by monday.com |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | userType | String |  |  |
    | displayName | String |  | ✓ |
    | title | String |  |  |
    | locale | String |  |  |
    | timezone | String |  |  |
    | roles | String |  |  |
12. Review the group attributes that are synchronized from Microsoft Entra ID to monday.com in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in monday.com for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by monday.com |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector Limitations

- monday.com only supports the userType "admin" , "guest", "member" and "viewer". The userType "User" isn't supported and is removed in the future.

## Change log

- 1/21/2021 - Added support for core attribute "userType" for users.
- 12/08/2022 - Dropped core user attribute **emails[type eq "work"].value**.Update **userName** , so that it get provisioned **"always"** and not **"only on object creation"**.Removed the mapping for **userType**.Added core user attribute **roles** and it's corresponding mapping.