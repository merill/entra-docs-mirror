---
layout: Conceptual
title: Configure Simple In/Out for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/simple-in-out-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Simple In/Out.
ms.topic: how-to
ms.date: 2026-04-16T00:00:00.0000000Z
locale: en-us
document_id: 8a2be98b-2c4a-191e-6c6f-d51debcb15aa
document_version_independent_id: 8a2be98b-2c4a-191e-6c6f-d51debcb15aa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/simple-in-out-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/simple-in-out-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/simple-in-out-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 11563c55-c391-8eb6-0ff0-245f1df874c9
---

# Configure Simple In/Out for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Simple In/Out and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users to [Simple In/Out](https://www.simpleinout.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Simple In/Out.
- Remove users in Simple In/Out when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Simple In/Out.
- [Single sign-on](../enterprise-apps/add-application-portal-setup-oidc-sso) to Simple In/Out (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in Simple In/Out with Admin permissions.

## Step 1: Plan your provisioning deployment

- Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
- Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- Determine what data to [map between Microsoft Entra ID and Simple In/Out](../app-provisioning/customize-application-attributes).

## Step 2: Configure Simple In/Out to support provisioning with Microsoft Entra ID

Any one of your Simple In/Out administrator-level users can configure Single Sign On.

1. In a web browser, head to [simpleinout.com](https://www.simpleinout.com) and sign in with a Simple In/Out administrator's credentials.
2. Select **Settings** in the upper-right.
3. Select **Single Sign On** under the **ENTERPRISE** menu on the left.
4. If you aren't yet on an Enterprise level plan, this settings page will alert you that you need to upgrade your plan in order to use Single Sign On. Follow the link to upgrade your plan if necessary and return to this page.
5. Be sure your provider is set to **Microsoft** and select the **Connect Single Sign On** button.
6. You be asked to confirm that you wish to enable Single Sign On. Select **OK** to confirm.
7. Select **Reveal** on your Recovery Key and store this entire key in a safe place. **IMPORTANT!** If you're ever locked out of your Microsoft accounts and need to disconnect SSO without access, you be required to relay the Recovery Key to Simple In/Out technical support.
8. Select **Reveal** on your Bearer Token and make note of it. You'll need this for Step 5.6.

    - When a new user is provisioned from Microsoft Entra ID to Simple In/Out, Simple In/Out will set that user's role to the default role for your organization. This role will govern the user's permissions inside Simple In/Out. For existing users that may be converted to SSO, Simple In/Out will maintain their existing role.
    - After users are provisioned to Simple In/Out, any administrator-level user can edit a user's role. This is done by selecting a user on the Simple In/Out board, then selecting the **Edit User** button that appears in the user's profile dialog.
    - You can change the default role in Simple In/Out and customize the permissions in the role on Simple In/Out's website.
9. Within Simple In/Out's website, select **Settings** in the upper-right
10. Select **Roles** under the **USERS** menu on the left.
11. Select the **Edit** button associated with your default role as designated by the green checkmark.
12. Any settings can be changed from here and will immediately take effect.

## Step 3: Add Simple In/Out from the Microsoft Entra application gallery

Add Simple In/Out from the Microsoft Entra application gallery to start managing provisioning to Simple In/Out. If you have previously setup Simple In/Out for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Simple In/Out

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in Simple In/Out based on user assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Simple In/Out in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Simple In/Out**.

    ![Screenshot of the Simple In/Out link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Provisioning tab in the application management menu.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Simple In/Out Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Simple In/Out. If the connection fails, ensure your Simple In/Out account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of the Provisioning properties page showing notification and deletion settings.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Simple In/Out in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Simple In/Out for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Simple In/Out API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Simple In/Out |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | displayName | String | ✓ | ✓ |
    | title | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | phoneNumbers[type eq "mobile"].value | String |  |  |
    | phoneNumbers[type eq "fax"].value | String |  |  |
    | externalId | String |  | ✓ |
12. Review the group attributes that are synchronized from Microsoft Entra ID to Simple In/Out in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Simple In/Out for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Simple In/Out |
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