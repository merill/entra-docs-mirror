---
layout: Conceptual
title: Configure Postman for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/postman-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Postman.
ms.topic: how-to
ms.date: 2026-04-21T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0b8b58fe-6d42-3867-fe55-cd99e82bf520
document_version_independent_id: 4b4dc7e6-b909-5d0b-7ad4-8ead39fd62f0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/postman-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/postman-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/postman-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: aa0d47f0-7994-9cba-0d27-9c41874a7cc9
---

# Configure Postman for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Postman and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Postman](https://www.postman.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Postman.
- Remove users in Postman when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Postman.
- Provision groups and group memberships in Postman.
- [Single sign-on](postman-tutorial) to Postman (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Postman tenant on the [Enterprise plan](https://www.postman.com/pricing/).
- A user account in Postman with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Postman](../app-provisioning/customize-application-attributes).

## Step 2: Configure Postman to support provisioning with Microsoft Entra ID

Before you begin to configure Postman to support provisioning with Microsoft Entra ID, you’ll need to generate a SCIM API token within the Postman Admin Console.

Note

You can visit the page [Postman SCIM provisioning overview](https://learning.postman.com/docs/administration/scim-provisioning/scim-provisioning-overview/#enabling-scim-in-postman), to refer **Enable SCIM provisioning in Postman** steps.

1. Navigate to [Postman Admin Console](https://go.postman.co/home) by logging in to your Postman account.
2. Once you’ve logged in, select **Team** on the right side and select **Team Settings**.
3. Select **Authentication** in the sidebar and then turn on the **SCIM provisioning** toggle.

    ![Screenshot of Postman authentication settings page.](media/postman-provisioning-tutorial/postman-authentication-settings.png)
4. You receive a pop up message asking whether you want to **Turn on SCIM Provisioning**, select **Turn On** to enable SCIM provisioning.

    ![Screenshot of modal to enable SCIM provisioning.](media/postman-provisioning-tutorial/postman-enable-scim-provisioning.png)
5. To **Generate SCIM API Key**, perform the following steps:

    1. Select **Generate SCIM API Key** in the **SCIM provisioning** section.

        ![Screenshot to generate SCIM API key in Postman.](media/postman-provisioning-tutorial/postman-generate-scim-api-key.png)
    2. Enter name of the key and select **Generate**.
    3. Copy your new API key for later use and select **Done**.

    Note

    You can revisit this page to manage your SCIM API keys. If you regenerate an existing API key, you have the option to keep the first key active while you switch over.

    Note

    To continue enabling SCIM provisioning, see [Configuring SCIM with Microsoft Entra ID](https://learning.postman.com/docs/administration/scim-provisioning/configuring-scim-with-azure-ad/). For further information or help configuring SCIM, [contact Postman support](https://www.postman.com/support/).

## Step 3: Add Postman from the Microsoft Entra application gallery

Add Postman from the Microsoft Entra application gallery to start managing provisioning to Postman. If you have previously set up Postman for SSO you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Postman

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Postman in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Postman**.

    ![Screenshot of the Postman link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Provisioning tab for configuring automatic user provisioning.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Postman Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Postman. If the connection fails, ensure your Postman account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page showing notification and deletion settings.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Postman in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Postman for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Postman API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Postman |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | name.givenName | String |  | ✓ |
    | name.familyName | String |  | ✓ |
12. Select **Attribute Mapping** in the left panel and select **group**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Postman in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Postman for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Postman |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.