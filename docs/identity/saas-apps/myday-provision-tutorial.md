---
layout: Conceptual
title: Configure myday for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/myday-provision-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to myday.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: d8b8a9e6-2df0-c53d-043d-392d2c75cdee
document_version_independent_id: 14784a3d-b740-bf26-b275-ae070ae790d4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/myday-provision-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/myday-provision-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/myday-provision-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cf50a2a1-3957-1239-37cd-f53b0c55383a
---

# Configure myday for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both myday and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in myday
- Remove users in myday when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and myday
- Provision groups and group memberships in myday
- Single sign-on to myday (recommended)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A user account in myday with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and myday](../app-provisioning/customize-application-attributes).

## Step 2: Configure myday to support provisioning with Microsoft Entra ID

Reach out to your myday representative or the support team to receive the **Tenant URL** and **Secret Token**.

## Step 3: Add myday from the Microsoft Entra application gallery

Add myday from the Microsoft Entra application gallery to start managing provisioning to myday. If you have previously setup myday for Single sign-on (SSO), you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to myday

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for myday in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot shows the Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **myday**.

    ![Screenshot shows the myday link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot shows the Provisioning tab.](common/provisioning.png)
5. Set the **Provisioning Mode** to **Automatic**.

    ![Screenshot shows the Provisioning tab automatic.](common/provisioning-automatic.png)
6. Under the **Admin Credentials** section, input the tenant URL value retrieved earlier in **Tenant URL**. Input the secret Token value retrieved earlier in **Secret Token**. Select **Test Connection** to ensure Microsoft Entra ID can connect to myday. If the connection fails, ensure your myday account has Admin permissions and try again.

    ![Screenshot shows the Tenant URL Token.](common/provisioning-testconnection-tenanturltoken.png)
7. In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot shows the Notification Email.](common/provisioning-notification-email.png)
8. Select **Save**.
9. Under the **Mappings** section, select **Provision Microsoft Entra users**.
10. Review the user attributes that are synchronized from Microsoft Entra ID to myday in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in myday for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the myday API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | userName | String |
    | active | Boolean |
    | displayName | String |
    | title | String |
    | emails[type eq "work"].value | String |
    | preferredLanguage | String |
    | name.givenName | String |
    | name.familyName | String |
    | name.formatted | String |
    | externalId | String |
    | addresses[type eq "work"].country | String |
    | addresses[type eq "work"].locality | String |
    | addresses[type eq "work"].postalCode | String |
    | addresses[type eq "work"].formatted | String |
    | addresses[type eq "work"].region | String |
    | addresses[type eq "work"].streetAddress | String |
    | addresses[type eq "other"].formatted | String |
    | phoneNumbers[type eq "fax"].value | String |
    | phoneNumbers[type eq "mobile"].value | String |
    | phoneNumbers[type eq "work"].value | String |
    | roles[primary eq "True"].display | String |
    | roles[primary eq "True"].type | String |
    | roles[primary eq "True"].value | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |
11. Under the **Mappings** section, select **Provision Microsoft Entra groups**.
12. Review the group attributes that are synchronized from Microsoft Entra ID to myday in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in myday for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | displayName | String |
    | externalId | String |
    | members | Reference |
13. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. To enable the Microsoft Entra provisioning service for myday, change the **Provisioning Status** to **On** in the **Settings** section.

    ![Screenshot shows the Provisioning Status Toggled On.](common/provisioning-toggle-on.png)
15. Define the users and/or groups that you would like to provision to myday by choosing the desired values in **Scope** in the **Settings** section.

    ![Screenshot shows the Provisioning Scope.](common/provisioning-scope.png)
16. When you're ready to provision, select **Save**.

    ![Screenshot shows saving Provisioning Configuration.](common/provisioning-configuration-save.png)

This operation starts the initial synchronization cycle of all users and groups defined in **Scope** in the **Settings** section. The initial cycle takes longer to perform than subsequent cycles, which occur approximately every 40 minutes as long as the Microsoft Entra provisioning service is running.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.