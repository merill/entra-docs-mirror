---
layout: Conceptual
title: Configure Gtmhub for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/gtmhub-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Gtmhub.
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1eb3c7a2-ff0b-cb3a-c5ec-ef2086e4a0db
document_version_independent_id: 3da2cd45-def2-9e5c-c801-9cfe5caa7c5c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/gtmhub-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/gtmhub-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/gtmhub-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 29c881b9-ff3f-bdcf-cc92-3a6d4885c954
---

# Configure Gtmhub for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Gtmhub and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Gtmhub](https://www.gtmhub.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Note

Currently, when automatic user provisioning is configured, Microsoft Entra-only automatically de-provisions users and groups to Gtmhub and map users to their respective teams using the Microsoft Entra provisioning service. But in 2021 once SSO is enabled with Gtmhub, users are automatically provisioned when they log in through SSO and is assigned to their respective team.

## Capabilities Supported

- Remove users in Gtmhub when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Gtmhub.
- Map users into their teams automatically and align them.
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- An Enterprise Gtmhub account.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Gtmhub](../app-provisioning/customize-application-attributes).

## Step 2: Configure Gtmhub to support team mapping and user de-provisioning with Microsoft Entra ID

In order to connect your provisioning application to your Gtmhub account you need to issue a SCIM token and compile the tenant URL.

### To issue a new SCIM token:

1. Sign in to your **Gtmhub account**. Navigate to **Settings &gt; Configuration &gt; API Tokens**.

    ![API Tokens tab](media/gtmhub-provisioning-tutorial/api-tokens.png)
2. Select **Issue Token** and select **SCIM**. Enter a name for the token and select the **Generate API Token** button.

    ![Generate Tokens tab](media/gtmhub-provisioning-tutorial/generate-token.png)
3. Once the token is generated you can copy and use it in your Microsoft Entra provisioning application.

    ![Copy Token](media/gtmhub-provisioning-tutorial/token.png)

### To compile the tenant URL:

1. Your tenant URL has to be in the following format:

    `https://app.gtmhub.com/api/v1/scim/azure/{account_id}`
2. If your Gtmhub account is located in the US data center you also have to add the data center to the URL:

    `https://app.us.gtmhub.com/api/v1/scim/azure/{account_id}`
3. To get the account ID go to **Settings** then select the **API Tokens** tab and copy the account ID: ![Account ID](media/gtmhub-provisioning-tutorial/account-id.png)

## Step 3: Add Gtmhub from the Microsoft Entra application gallery

Add Gtmhub from the Microsoft Entra application gallery to start managing provisioning to Gtmhub. If you have previously setup Gtmhub for SSO you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Gtmhub

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Gtmhub in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Gtmhub**.

    ![The Gtmhub link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Gtmhub Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Gtmhub. If the connection fails, ensure your Gtmhub account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Gtmhub in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Gtmhub for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Gtmhub API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | externalId | String | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.