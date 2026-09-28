---
layout: Conceptual
title: Configure Airtable for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/airtable-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Airtable.
ms.topic: how-to
ms.date: 2026-02-25T00:00:00.0000000Z
locale: en-us
document_id: 3ee72578-3212-e186-b5bb-886e3b688720
document_version_independent_id: 39c6e08d-31d0-c60c-16a8-a2f140124b38
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/airtable-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/airtable-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/airtable-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2ea36345-71d2-16cf-d02d-6235ecc7a683
---

# Configure Airtable for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Airtable and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Airtable](https://www.airtable.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Airtable.
- Remove users in Airtable when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Airtable.
- Provision groups and group memberships in Airtable.
- [Single sign-on](airtable-tutorial) to Airtable (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- An Airtable tenant.
- A user account in Airtable with Admin permissions.

## Step 1: Plan your provisioning deployment

- Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
- Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- Determine what data to [map between Microsoft Entra ID and Airtable](../app-provisioning/customize-application-attributes).

## Step 2: Create an Airtable Personal Access Token to authorize provisioning with Microsoft Entra ID.

1. Login to [Airtable Developer Hub](https://airtable.com) as an Admin user, and then navigate to `https://airtable.com/create/tokens`.
2. Select "Personal Access Tokens" from the left hand navigation bar.

    ![Screenshot of Personal Access Token Selection.](media/airtable-provisioning-tutorial/developer-hub-personal-access-token.png)
3. Create a new token with a memorable name such as "AzureAdScimProvisioning".
4. Add the "enterprise.scim.usersAndGroups:manage" scope.

    ![Screenshot of enterprise scim scope addition.](media/airtable-provisioning-tutorial/enterprise-scim-scope.png)
5. Select "Create Token" and copy the resulting token for use in **Step 5** below.

## Step 3: Add Airtable from the Microsoft Entra application gallery

Add Airtable from the Microsoft Entra application gallery to start managing provisioning to Airtable. If you have previously setup Airtable for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Airtable

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Airtable in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Airtable**.

    ![Screenshot of the Airtable link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Airtable Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Airtable. If the connection fails, ensure your Airtable account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Airtable in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Airtable for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Airtable API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Airtable |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | displayName | String |  |  |
    | title | String |  |  |
    | emails[type eq "work"].value | String |  |  |
    | preferredLanguage | String |  |  |
    | name.givenName | String |  | ✓ |
    | name.familyName | String |  | ✓ |
    | name.formatted | String |  |  |
    | addresses[type eq "work"].formatted | String |  |  |
    | addresses[type eq "work"].streetAddress | String |  |  |
    | addresses[type eq "work"].locality | String |  |  |
    | addresses[type eq "work"].region | String |  |  |
    | addresses[type eq "work"].postalCode | String |  |  |
    | addresses[type eq "work"].country | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | phoneNumbers[type eq "mobile"].value | String |  |  |
    | phoneNumbers[type eq "fax"].value | String |  |  |
    | externalId | String |  |  |
    | nickName | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager.value | String |  |  |
    | addresses[type eq "home"].formatted | String |  |  |
    | addresses[type eq "home"].streetAddress | String |  |  |
    | addresses[type eq "home"].locality | String |  |  |
    | addresses[type eq "home"].region | String |  |  |
    | addresses[type eq "home"].postalCode | String |  |  |
    | addresses[type eq "home"].country | String |  |  |
    | addresses[type eq "other"].formatted | String |  |  |
    | addresses[type eq "other"].streetAddress | String |  |  |
    | addresses[type eq "other"].locality | String |  |  |
    | addresses[type eq "other"].region | String |  |  |
    | addresses[type eq "other"].postalCode | String |  |  |
    | addresses[type eq "other"].country | String |  |  |
    | emails[type eq "home"].value | String |  |  |
    | emails[type eq "other"].value | String |  |  |
    | locale | String |  |  |
    | name.honorificPrefix | String |  |  |
    | name.honorificSuffix | String |  |  |
    | name.middleName | String |  |  |
    | name.familyName | String |  |  |
    | phoneNumbers[type eq "home"].value | String |  |  |
    | phoneNumbers[type eq "other"].value | String |  |  |
    | phoneNumbers[type eq "pager"].value | String |  |  |
    | timezone | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |  |
    | userType | String |  |  |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Airtable in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Airtable for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Airtable |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a few users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.