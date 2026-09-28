---
layout: Conceptual
title: Configure Amazon Business for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/amazon-business-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Amazon Business.
ms.topic: how-to
ms.date: 2026-02-20T00:00:00.0000000Z
locale: en-us
document_id: 9a5d2103-3bf5-d7ac-0876-3c5f7ffcd274
document_version_independent_id: c9ffa8a7-569d-676f-d8aa-6aeba2ff950d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/amazon-business-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/amazon-business-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/amazon-business-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e827e51a-a5dd-cd6e-902f-78574e14daf4
---

# Configure Amazon Business for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Amazon Business and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Amazon Business](https://www.amazon.com/b2b/info/amazon-business?layout=landing) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Amazon Business.
- Remove users in Amazon Business when they don't require access anymore.
- Assign Amazon Business roles to user.
- Keep user attributes synchronized between Microsoft Entra ID and Amazon Business.
- Provision groups and group memberships in Amazon Business.
- [Single sign-on](amazon-business-tutorial) to Amazon Business (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- An Amazon Business account.
- A user account in Amazon Business with Admin permissions (Admin on all Legal Entity groups in your Amazon Business account).

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Amazon Business](../app-provisioning/customize-application-attributes).

## Step 2: Configure Amazon Business to support provisioning with Microsoft Entra ID

Before configuring and enabling the provisioning service, you need to identify a default group for both users and groups. We recommend you to

- Follow the principle of least privilege by having REQUISITIONER only permissions for the default users group.
- Follow the group naming convention referenced in the following section for ease of referencing the groups throughout this document.
    - Default SCIM Parent Group
        - This is the root of your SCIM directory in AmazonBusiness. All SCIM groups are placed directly under this default group. You can select an existing group as the default SCIM parent group.
    - Default SCIM Users Group
        - Users who are assigned to your Amazon Business app is placed into this group by default with a Requisitioner role. It's recommended to have this group at the same level as the Default SCIM Parent Group.
        - If a user is provisioned without a group assignment, they'll be placed into this group by default with a Requisitioner role.
        - Any deactivated user remains in this group. Hence, it's recommended to not use any role other than Requisitioner for this group.

Note

- The Default SCIM Parent Group can be the same as the default group selected for your SSO configuration.
- The Default SCIM Parent Group can be a Legal Entity group. Choosing Legal Entity as the default group is recommended if you have different invoicing templates set up for different groups in your AB Account.
- We currently support enabling SCIM for only one Legal Entity in an Amazon Business account.

Once your Default SCIM Groups have been identified, go to your Amazon Business account &gt; Business Settings &gt; Identity Management (SCIM) page, enter the details and select Activate. It's necessary to complete this step before proceeding to the next step.

## Step 3: Add Amazon Business from the Microsoft Entra application gallery

Add Amazon Business from the Microsoft Entra application gallery to start managing provisioning to Amazon Business. If you have previously setup Amazon Business for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Amazon Business

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Amazon Business based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Amazon Business in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Amazon Business**.

    ![Screenshot of the Amazon Business link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, input your Amazon Business Tenant URL, Authorization Endpoint. Select **Test Connection** to ensure Microsoft Entra ID can connect to Amazon Business. If the connection fails, ensure your Amazon Business account has Admin permissions and try again.

    ![Screenshot of Token.](media/amazon-business-provisioning-tutorial/test-connection.png)

    For **Tenant URL** and **Authorization endpoint** values, use the following table.

    | Country/region | Tenant URL | Authorization endpoint |
    | --- | --- | --- |
    | Canada | https://na.business-api.amazon.com/scim/v2/ | https://www.amazon.ca/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | Germany | https://eu.business-api.amazon.com/scim/v2/ | https://www.amazon.de/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | Spain | https://eu.business-api.amazon.com/scim/v2/ | https://www.amazon.es/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | France | https://eu.business-api.amazon.com/scim/v2/ | https://www.amazon.fr/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | GB/UK | https://eu.business-api.amazon.com/scim/v2/ | https://www.amazon.co.uk/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | India | https://eu.business-api.amazon.com/scim/v2/ | https://www.amazon.in/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | Italy | https://eu.business-api.amazon.com/scim/v2/ | https://www.amazon.it/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | Japan | https://jp.business-api.amazon.com/scim/v2/ | https://www.amazon.co.jp/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | Mexico | https://na.business-api.amazon.com/scim/v2/ | https://www.amazon.com.mx/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | US | https://na.business-api.amazon.com/scim/v2/ | https://www.amazon.com/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
    | Australia | https://jp.business-api.amazon.com/scim/v2/ | https://www.amazon.com.au/b2b/abws/oauth?state=1&redirect\_uri=https://portal.azure.com/TokenAuthorize&applicationId=amzn1.sp.solution.ee27ec8c-1ee9-4c6b-9e68-26bdc37479d3 |
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select users.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Amazon Business in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Amazon Business for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Amazon Business API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Amazon Business |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | emails[type eq "work"].value | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | externalId | String |  |  |
    | roles | List of appRoleAssignments [appRoleAssignments] |  |  |
12. Select **groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Amazon Business in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Amazon Business for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Amazon Business |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Feature limitations

- Flat structure is created on the Amazon Business account, that is, all pushed groups are at the same level under the Default SCIM Group. Nested structure/hierarchy isn't supported.
- Group names are same in Azure and Amazon Business account.
- As new groups are created on the Amazon Business Account, Admins need to reconfigure the business settings (for example, turning on purchasing, updating shared settings, adding guided buying policies, and so on) for the new groups as needed.
- Deleting old Groups / removing users from old groups in Amazon Business results in losing visibility into orders placed with that old Group, hence it's recommended to
    - Not delete the old groups/assignments, and
    - Turn off purchasing for the old groups.
- Email / Username Update - Updating email and / or username via SCIM isn't supported at this time.
- Password Sync - Password sync isn't supported.
- SSO Requirement - While the Amazon Business app allows the activation of SCIM provisioning without SSO, provisioned users require SSO Authentication in order to access Amazon Business.
- Multi-Legal Entity (MLE) accounts - We currently don't support enabling SCIM for more than one Legal Entity in an Amazon Business Account.
- When provisioning a group with the same name as already existing one in Amazon Business, these groups are automatically linked (new group is created in Amazon Business).

## Troubleshooting tips

- If Amazon Business administrators have only logged in using SSO or don’t know their passwords, they can use the forgot password flow to reset their password and then sign in to Amazon Business.
- If Admin and Requisitioner roles have already been applied to customer in a group, assigning Finance or Tech roles won't result in updates on Amazon Business side.
- Customers with MASE accounts (Multiple Account Same Email) who delete one of their accounts can see errors that account doesn't exist when provisioning new users for short amount of time (24-48 hours).
- Customers can't be removed immediately via Provision on Demand. Provisioning must be turned on and the removal happens 40 mins after the action is taken.