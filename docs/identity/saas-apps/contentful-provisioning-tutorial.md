---
layout: Conceptual
title: Configure Contentful for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/contentful-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Contentful.
ms.topic: how-to
ms.date: 2026-04-03T00:00:00.0000000Z
locale: en-us
document_id: fa30548f-c304-06cc-24ce-0ff3cc1424a1
document_version_independent_id: 9fc562ef-c360-fbcf-3a78-cfe3e10df06c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/contentful-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/contentful-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/contentful-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9f4b8fcc-ba57-9da8-af68-7c72c5241eac
---

# Configure Contentful for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to complete in Contentful and in Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Contentful](https://www.contentful.com/) by using the Microsoft Entra provisioning service. For important details about what this service does and how it works, and for frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Contentful
- Remove users in Contentful when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Contentful
- Provision groups and group memberships in Contentful
- [Single sign-on](contentful-tutorial) to Contentful (recommended)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Contentful organization account that has a subscription that supports System for Cross-domain Identity Management (SCIM) provisioning. If you have questions about your organization's subscription, contact [Contentful Support](mailto:support@contentful.com).

## Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Contentful](../app-provisioning/customize-application-attributes).

## Configure Contentful to support provisioning with Microsoft Entra ID

1. In Contentful, create a **Service User** account. All provisioning permissions for Azure are provided through this account. We recommend that you choose **Owner** as the organization role for this account.
2. Sign in to Contentful as the **Service User**.
3. In the left menu, select **Organization settings** &gt; **Access Tools** &gt; **User provisioning**.

    ![Screenshot of the Organization settings menu in Contentful, with User provisioning highlighted under Access Tools.](media/contentful-provisioning-tutorial/access.png)
4. Copy and save the **SCIM URL**. You'll enter this value in the Azure portal, on the **Provisioning** tab of your Contentful application.
5. Select **Generate personal access token**.

    ![Screenshot showing the SCIM URL to generate a personal access token.](media/contentful-provisioning-tutorial/generate.png)
6. In the modal window, enter a name for your personal access token, and then select **Generate**.
7. The SCIM URL and the secret token are generated. Copy and save these values. You'll enter these values on the **Provisioning** tab of your Contentful application.

    ![Screenshot of the Personal access token pane, with C F P A T and the token placeholder name highlighted.](media/contentful-provisioning-tutorial/token.png)

If you have questions while you configure provisioning in the Contentful admin console, contact [Contentful Support](mailto:support@contentful.com).

## Add Contentful from the Microsoft Entra application gallery

To manage provisioning to Contentful, add Contentful from the Microsoft Entra application gallery. If you have previously set up Contentful for single sign-on, you can use the same application. However, we recommend that you create a separate app to initially test the integration. Learn how to [add an application in the gallery](../enterprise-apps/add-application-portal).

## Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Configure automatic user provisioning to Contentful

This section guides you through the steps to set up the Microsoft Entra provisioning service to create, update, and disable users and groups in a test app based on user or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for Contentful in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Screenshot that shows the Enterprise applications menu in the Azure portal, with All applications highlighted.](common/enterprise-applications.png)
3. In the applications list, select **Contentful**.

    ![Screenshot that shows the first 20 results returned in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Provisioning tab highlighted in the Manage section of the left menu.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Contentful Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Contentful. If the connection fails, ensure your Contentful account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Contentful in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Contentful for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Contentful API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | name.givenName | String |  |
    | name.familyName | String |  |
12. In the **Attribute-Mapping** section, review the group attributes that are synced from Microsoft Entra ID to Contentful. The attributes selected as **Matching** properties are used to match the groups in Contentful for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | displayName | String | ✓ |
    | members | Reference |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.