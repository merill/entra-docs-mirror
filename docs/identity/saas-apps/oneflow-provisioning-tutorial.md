---
layout: Conceptual
title: Configure Oneflow for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/oneflow-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Oneflow.
ms.topic: how-to
ms.date: 2026-04-21T00:00:00.0000000Z
locale: en-us
document_id: fe4579c0-03a4-4980-6a92-4ba619f8f946
document_version_independent_id: 2a01f15c-4766-5388-5ea6-376a260814b9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/oneflow-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/oneflow-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/oneflow-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0e2cad2c-dd15-ace5-fb66-7c6a7c6553e2
---

# Configure Oneflow for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Oneflow and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Oneflow](https://oneflow.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Oneflow.
- Remove users in Oneflow when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Oneflow.
- Provision groups and group memberships in Oneflow.
- [Single sign-on](oneflow-tutorial) to Oneflow (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Oneflow tenant.
- A user account in Oneflow with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Oneflow](../app-provisioning/customize-application-attributes).

## Step 2: Configure Oneflow to support provisioning with Microsoft Entra ID

Use the following information for Step 5-6.

- Tenant URL: `https://api.oneflow.com/scim/v1/`
- Secret Token: The oneflow SCIM token serves as the secret token in provisioning. Please follow the steps provided in this [article](https://developer.oneflow.com/docs/enable-scim-api-extension) for generating a Oneflow SCIM token.

## Step 3: Add Oneflow from the Microsoft Entra application gallery

Add Oneflow from the Microsoft Entra application gallery to start managing provisioning to Oneflow. If you have previously setup Oneflow for SSO you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Oneflow

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Oneflow in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Oneflow**.

    ![Screenshot of the Oneflow link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Oneflow Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Oneflow. If the connection fails, ensure your Oneflow account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Oneflow in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Oneflow for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Oneflow API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Oneflow |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | externalId | String |  |  |
    | emails[type eq "work"].value | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |  |
    | nickName | String |  |  |
    | title | String |  |  |
    | profileUrl | String |  |  |
    | displayName | String |  |  |
    | addresses[type eq "work"].streetAddress | String |  |  |
    | addresses[type eq "work"].locality | String |  |  |
    | addresses[type eq "work"].region | String |  |  |
    | addresses[type eq "work"].postalCode | String |  |  |
    | addresses[type eq "work"].country | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:adSourceAnchor | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:customAttribute1 | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:customAttribute2 | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:customAttribute3 | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:customAttribute4 | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:customAttribute5 | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:distinguishedName | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:domain | String |  |  |
    | urn:ietf:params:scim:schemas:extension:ws1b:2.0:User:userPrincipalName | String |  |  |
12. Review the group attributes that are synchronized from Microsoft Entra ID to Oneflow in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Oneflow for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Oneflow |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | externalId | String | ✓ | ✓ |
    | members | Reference |  |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.