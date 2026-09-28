---
layout: Conceptual
title: Configure Asana for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/asana-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Asana.
ms.topic: how-to
ms.date: 2026-02-26T00:00:00.0000000Z
locale: en-us
document_id: 7a630935-6d99-85d7-04ec-232d58246a8a
document_version_independent_id: 8e3e2d98-a1e2-7080-fc04-0eea42e9a7b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/asana-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/asana-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/asana-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e8440e63-95c8-2f09-be1c-c24b6939c539
---

# Configure Asana for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to do in both Asana and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Asana](https://www.asana.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Asana.
- Remove users in Asana when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Asana.
- Provision groups and group memberships in Asana.
- [Single sign-on](asana-tutorial) to Asana (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An Asana tenant with an [Enterprise](https://www.asana.com/pricing) plan or better enabled
- A user account in Asana with admin permissions

Note

Microsoft Entra provisioning integration relies on the [Asana API](https://asana.com/developers/api-reference/users), which is available to Asana.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Asana](../app-provisioning/customize-application-attributes).

## Step 2: Configure Asana to support provisioning with Microsoft Entra ID

Tip

To enable SAML-based single sign-on for Asana, follow the instructions provided. Single sign-on can be configured independently of automatic provisioning, although these two features complement each other.

### Generate Service Account token in Asana

1. Sign in to [Asana](https://app.asana.com/-/login) by using your admin account.
2. Select the profile photo from the top bar, and select **Admin Console**.
3. Select the Apps tab from with your admin console.
4. Select Service accounts.
5. Select **Add Service Account** and perform the following steps.

    ![Screenshot of Service Account Token.](media/asana-provisioning-tutorial/service.png)

    1. Update **Name** and **Description** as needed.
    2. Under the **Permission scopes** section, select **Scoped permissions** and **User provisioning (SCIM)**. Ensure the following permission scopes are selected:
        - Users: Read
        - Users: Create and modify
        - Teams: Read
        - Teams: Create and modify
    3. Select **Save Changes**.
6. Copy the token.

## Step 3: Add Asana from the Microsoft Entra application gallery

Add Asana from the Microsoft Entra application gallery to start managing provisioning to Asana. If you have previously setup Asana for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Asana

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and groups in Asana based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Asana in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Asana**.

    ![Screenshot of the Asana link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Asana Tenant URL and Secret Token provided by Asana. Select **Test Connection** to ensure Microsoft Entra ID can connect to Asana. If the connection fails, contact Asana to check your account setup.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

![Screenshot of Provisioning properties.](common/provisioning-properties.png)

1. Select **Attribute Mapping** in the left panel and select **users**.
2. Review the user attributes that are synchronized from Microsoft Entra ID to Asana in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Asana for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Asana API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Asana |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | name.formatted | String |  |  |
    | title | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |  |
    | addresses[type eq "work"].country | String |  |  |
    | addresses[type eq "work"].region | String |  |  |
    | addresses[type eq "work"].locality | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |  |
3. Select **Groups**.
4. Review the group attributes that are synchronized from Microsoft Entra ID to Asana in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Asana for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Asana |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
5. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
6. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
7. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change log

- 11/06/2021 - Dropped support for **externalId, name.givenName and name.familyName**. Added support for **preferredLanguage , title and urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department**. Enabled **Group Provisioning**.
- 05/23/2023 - Dropped support for **preferredLanguage** Added support for **urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager**.
- 09/07/2023 - Added support for **addresses[type eq "work"].locality, addresses[type eq "work"].region, addresses[type eq "work"].country, phoneNumbers[type eq "work"].value, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization and urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division**.