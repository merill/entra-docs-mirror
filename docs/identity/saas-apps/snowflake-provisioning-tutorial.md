---
layout: Conceptual
title: Configure Snowflake for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/snowflake-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Snowflake.
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
locale: en-us
document_id: b6311c7b-41d1-21d0-c833-f4f290c41e04
document_version_independent_id: 264ebeac-f5c4-e869-a1dd-c7e14494b474
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/snowflake-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/snowflake-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/snowflake-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bedcb7b0-8b48-a764-e64e-ebf1cd2e7a8f
---

# Configure Snowflake for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article demonstrates the steps that you perform in Snowflake and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and deprovision users and groups to [Snowflake](https://www.Snowflake.com/pricing/). For important details on what this service does, how it works, and frequently asked questions, see [What is automated SaaS app user provisioning in Microsoft Entra ID?](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Snowflake
- Remove users in Snowflake when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Snowflake
- Provision groups and group memberships in Snowflake
- Allow [single sign-on](snowflake-tutorial) to Snowflake (recommended)
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- [A Snowflake tenant](https://www.Snowflake.com/pricing/)
- At least one user in Snowflake with the **ACCOUNTADMIN** role.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Snowflake](../app-provisioning/customize-application-attributes).

## Step 2: Configure Snowflake to support provisioning with Microsoft Entra ID

Before you configure Snowflake for automatic user provisioning with Microsoft Entra ID, you need to enable System for Cross-domain Identity Management (SCIM) provisioning on Snowflake.

1. Sign in to Snowflake as an administrator and execute the following from either the Snowflake worksheet interface or SnowSQL.

    ```
    use role accountadmin;
    
     create role if not exists aad_provisioner;
     grant create user on account to role aad_provisioner;
     grant create role on account to role aad_provisioner;
    grant role aad_provisioner to role accountadmin;
     create or replace security integration aad_provisioning
         type = scim
         scim_client = 'azure'
         run_as_role = 'AAD_PROVISIONER';
     select system$generate_scim_access_token('AAD_PROVISIONING');
    ```
2. Use the ACCOUNTADMIN role.

    ![Screenshot of a worksheet in the Snowflake UI with the SCIM access token called out.](media/snowflake-provisioning-tutorial/step-2.png)
3. Create the custom role AAD\_PROVISIONER. All users and roles in Snowflake created by Microsoft Entra ID is owned by the scoped down AAD\_PROVISIONER role.

    ![Screenshot showing the custom role.](media/snowflake-provisioning-tutorial/step-3.png)
4. Let the ACCOUNTADMIN role create the security integration using the AAD\_PROVISIONER custom role.

    ![Screenshot showing the security integrations.](media/snowflake-provisioning-tutorial/step-4.png)
5. Create and copy the authorization token to the clipboard and store securely for later use. Use this token for each SCIM REST API request and place it in the request header. The access token expires after six months and a new access token can be generated with this statement.

    ![Screenshot showing the token generation.](media/snowflake-provisioning-tutorial/step-5.png)

## Step 3: Add Snowflake from the Microsoft Entra application gallery

Add Snowflake from the Microsoft Entra application gallery to start managing provisioning to Snowflake. If you previously set up Snowflake for single sign-on (SSO), you can use the same application. However, we recommend that you create a separate app when you're initially testing the integration. [Learn more about adding an application from the gallery](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Snowflake

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and groups in Snowflake. You can base the configuration on user and group assignments in Microsoft Entra ID.

To configure automatic user provisioning for Snowflake in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Screenshot that shows the Enterprise applications pane.](common/enterprise-applications.png)
3. In the list of applications, select **Snowflake**.

    ![Screenshot that shows a list of applications.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Admin Credentials** section, enter the SCIM 2.0 base URL and authentication token that you retrieved earlier in the **Tenant URL** and **Secret Token** boxes, respectively.

    Note

    The Snowflake SCIM endpoint consists of the Snowflake account URL appended with `/scim/v2/`. For example, if your Snowflake account name is `acme` and your Snowflake account is in the `east-us-2` Azure region, the **Tenant URL** value is `https://acme.east-us-2.azure.snowflakecomputing.com/scim/v2`.
7. Select **Test Connection** to ensure Microsoft Entra ID can connect to Snowflake. If the connection fails, ensure your Snowflake account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
8. Select **Create** to create your configuration.
9. Select **Properties** on the **Overview** page.
10. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to Snowflake in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Snowflake for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | active | Boolean |
    | displayName | String |
    | emails[type eq "work"].value | String |
    | userName | String |
    | name.givenName | String |
    | name.familyName | String |
    | externalId | String |
    | urn:ietf:params:scim:schemas:extension:2.0:User:type [User management - Snowflake Documentation](https://docs.snowflake.com/en/user-guide/admin-user-management#label-user-management-types) | String |

    Note

    Group display name editing is now unlocked. Previously, the group display name in Snowflake could not be changed, preventing customers from editing the mapping. It is now editable.

    Note

    Snowflake supported custom extension user attributes during SCIM provisioning:

    - DEFAULT\_ROLE
    - DEFAULT\_WAREHOUSE
    - DEFAULT\_SECONDARY\_ROLES
    - SNOWFLAKE NAME AND LOGIN\_NAME FIELDS TO BE DIFFERENT

> 
> How to set up Snowflake custom extension attributes in Microsoft Entra SCIM user provisioning is explained [here](https://community.snowflake.com/s/article/HowTo-How-to-Set-up-Snowflake-Custom-Attributes-in-Azure-AD-SCIM-for-Default-Roles-and-Default-Warehouses).
13. Select **Groups**.
14. Review the group attributes that are synchronized from Microsoft Entra ID to Snowflake in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Snowflake for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | displayName | String |
    | members | Reference |
15. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
16. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
17. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector limitations

Snowflake-generated SCIM tokens expire in 6 months. Be aware that you need to refresh these tokens before they expire, to allow the provisioning syncs to continue working.

## Just-in-time (JIT) application access with PIM for Groups

With Privileged Identity Management (PIM) for Groups, you can provide just-in-time access to groups in Snowflake and reduce the number of users who have permanent access to privileged groups in Snowflake.

**Configure your enterprise application for single sign-on (SSO) and provisioning**

To set up persistent, non-admin access in Snowflake, complete these steps:

1. Add Snowflake to your tenant, configure it for provisioning as described in the previous steps of this tutorial, and start provisioning.
2. Configure [single sign-on](snowflake-tutorial) for Snowflake.
3. Create a [group](/en-us/entra/fundamentals/how-to-manage-groups) that provides all users access to the application.
4. Assign the group to the Snowflake application.
5. Assign your test user as a direct member of the group you created for all-user access, or provide access to the group through an access package. This group provides persistent, non-admin access in Snowflake.

**Enable PIM for Groups**

To grant just-in-time admin access, complete these steps:

1. Create a second group in Microsoft Entra ID. This group provides access to admin permissions in Snowflake.
2. Bring the group under [management in Microsoft Entra PIM](/en-us/azure/active-directory/privileged-identity-management/groups-discover-groups).
3. Assign your test user as [eligible for the group in PIM](/en-us/azure/active-directory/privileged-identity-management/groups-assign-member-owner) with the role set to member.
4. Assign the second group to the Snowflake application.
5. Use on-demand provisioning to create the group in Snowflake.
6. Sign in to Snowflake and assign the second group the necessary permissions to perform admin tasks.

Now any end user that was made eligible for the group in PIM can get JIT access to the group in Snowflake by [activating their group membership](/en-us/azure/active-directory/privileged-identity-management/groups-activate-roles#activate-a-role).

**Key considerations**

- How long does it take to have a user provisioned to the application?
    - When a user is added to a group in Microsoft Entra ID outside of activating their group membership using Microsoft Entra Privileged Identity Management (PIM):
        - The group membership is provisioned in the application during the next synchronization cycle. The synchronization cycle runs every 40 minutes.
    - When a user activates their group membership in Microsoft Entra ID PIM:
        - The group membership is provisioned in 2-10 minutes. During periods of high request volume, requests are throttled at a rate of five requests per 10 seconds.
        - For the first five users within a 10-second period activating their group membership for a specific application, group membership is provisioned in the application within 2-10 minutes.
        - For the sixth user and above within a 10-second period activating their group membership for a specific application, group membership is provisioned to the application in the next synchronization cycle. The synchronization cycle runs every 40 minutes. The throttling limits are per enterprise application.
- If the user can't access the necessary group in Snowflake, review the Troubleshooting tips section, PIM logs, and provisioning logs to confirm that the group membership updated successfully. Depending on how the target application is architected, it might take extra time for the group membership to take effect in the application.
- You can create alerts for failures using [Azure Monitor](/en-us/entra/identity/app-provisioning/application-provisioning-log-analytics).
- Deactivation is done during the regular incremental cycle. It isn't processed immediately through on-demand provisioning.

## Troubleshooting tips

The Microsoft Entra provisioning service currently operates under particular [IP ranges](../app-provisioning/use-scim-to-provision-users-and-groups#ip-ranges). If necessary, you can restrict other IP ranges and add these particular IP ranges to the allow list of your application. That technique will allow traffic flow from the Microsoft Entra provisioning service to your application.

## Change log

- 07/21/2020: Enabled soft-delete for all users (via the active attribute).
- 10/12/2022: Updated Snowflake SCIM Configuration.