---
layout: Conceptual
title: Configure GroupTalk for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/grouptalk-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to GroupTalk.
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
locale: en-us
document_id: a808c29f-27e0-de88-4937-f6d3c13e4057
document_version_independent_id: 2a469b64-e344-f08a-4498-2c5d97da57d3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/grouptalk-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/grouptalk-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/grouptalk-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 94f29963-bcc5-ae84-1804-26ce47a2f922
---

# Configure GroupTalk for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both GroupTalk and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [GroupTalk](https://www.grouptalk.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in GroupTalk
- Remove users in GroupTalk when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and GroupTalk
- Provision groups and group memberships in GroupTalk
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
        - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
        - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
        - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in GroupTalk with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and GroupTalk](../app-provisioning/customize-application-attributes).

## Step 2: Configure GroupTalk to support provisioning with Microsoft Entra ID

1. Reach out to GroupTalk Support at support@grouptalk.com with the **Tenant name** and **ID** you would like to integrate with Microsoft Entra ID.
2. When you've been notified that the necessary setup for your Microsoft Entra integration is ready, login to GroupTalk Admin and navigate to your Organization view.
3. A Microsoft Entra Integration configuration item should be visible. Select it to verify the **Tenant name** and **ID** to obtain a **JWT (Secret Token)**.
4. The GroupTalk Tenant URL is `https://api.grouptalk.com/api/scim/`. The **Tenant URL** and the **Secret Token** retrieved in the previous step is entered in the Provisioning tab of your GroupTalk application.

## Step 3: Add GroupTalk from the Microsoft Entra application gallery

Add **GroupTalk** from the Microsoft Entra application gallery to start managing provisioning to GroupTalk.

1. Select the **Sign up for GroupTalk** button, which will route you to the GroupTalk administrative application.
2. If you're already logged in to GroupTalk, logout to get to the login screen. Select the Microsoft Entra ID tab, and select the **Sign in** button.

    ![GroupTalk](media/grouptalk-provisioning-tutorial/login.png)
3. Login with your AD Administrative account, and accept the GroupTalk application's access rights. You get an error message after this is done indicating the user isn't present. This is expected since your user isn't provisioned to GroupTalk yet but you have now added GroupTalk to your tenant.
4. Go back to the Azure portal and verify that **GroupTalk** is now added to your Enterprise Applications.

Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to GroupTalk

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for GroupTalk in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **GroupTalk**.

    ![The GroupTalk link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your GroupTalk Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to GroupTalk. If the connection fails, ensure your GroupTalk account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to GroupTalk in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in GroupTalk for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the GroupTalk API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | phoneNumbers[type eq "mobile"].value | String | ✓ |
    | emails[type eq "work"].value | String | ✓ |
    | active | Boolean |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | externalId | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |
    | urn:ietf:params:scim:schemas:extension:grouptalk:2.0:User:label1 | String |  |
    | urn:ietf:params:scim:schemas:extension:grouptalk:2.0:User:label2 | String |  |
    | urn:ietf:params:scim:schemas:extension:grouptalk:2.0:User:label3 | String |  |
    | urn:ietf:params:scim:schemas:extension:grouptalk:2.0:User:label4 | String |  |
    | urn:ietf:params:scim:schemas:extension:grouptalk:2.0:User:label5 | String |  |
12. Review the group attributes that are synchronized from Microsoft Entra ID to GroupTalk in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in GroupTalk for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | displayName | String | ✓ |
    | members | Reference |  |
    | externalId | String |  |
    | urn:ietf:params:scim:schemas:extension:grouptalk:2.0:Group:description | String |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.