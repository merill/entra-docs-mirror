---
layout: Conceptual
title: Configure O'Reilly learning platform for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/oreilly-learning-platform-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to O'Reilly learning platform.
ms.topic: how-to
ms.date: 2026-04-13T00:00:00.0000000Z
locale: en-us
document_id: d3f3d3c6-c2fe-36db-6e94-1e0719763de4
document_version_independent_id: 6607d4df-2e6c-318f-540b-5197c7b34b4a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/oreilly-learning-platform-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/oreilly-learning-platform-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/oreilly-learning-platform-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0955e48e-09da-4fc8-7ffe-6a9ae356b9ab
---

# Configure O'Reilly learning platform for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both O'Reilly learning platform and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to [O'Reilly learning platform](https://www.oreilly.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in O'Reilly learning platform.
- Remove users in O'Reilly learning platform when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and O'Reilly learning platform.
- [Single sign-on](oreilly-learning-platform-tutorial) to O'Reilly learning platform (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in O'Reilly learning platform with Admin permissions.
- An O'Reilly learning platform single sign-on (SSO) enabled subscription.

## Step 1: Plan your provisioning deployment

- Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
- Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- Determine what data to [map between Microsoft Entra ID and O'Reilly learning platform](../app-provisioning/customize-application-attributes).

## Step 2: Configure O'Reilly learning platform to support provisioning with Microsoft Entra ID

Before you begin to configure the O'Reilly learning platform to support provisioning with Microsoft Entra ID, you’ll need to generate a SCIM API token within the O’Reilly Admin Console.

1. Navigate to O'Reilly Admin Console by logging in to your O'Reilly account.
2. Once you’ve logged in, select **Admin** in the top navigation and select **Integrations**.
3. Scroll down to the **API tokens** section. Under API tokens, select **Create token** and select the **SCIM API**. Then give your token a name and expiration date, and select Continue. You’ll receive your API key in a pop-up message prompting you to store a copy of it in a secure place. Once you’ve saved a copy of your key, select the checkbox and Continue.
4. You use the O’Reilly SCIM API token in Step 5.

## Step 3: Add O'Reilly learning platform from the Microsoft Entra application gallery

Add O'Reilly learning platform from the Microsoft Entra application gallery to start managing provisioning to O'Reilly learning platform. If you have previously [set up O'Reilly learning platform for SSO](oreilly-learning-platform-tutorial), you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to O'Reilly learning platform

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in O’Reilly learning platform based on user assignments in Microsoft Entra ID.

### To configure automatic user provisioning for O'Reilly learning platform in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **O'Reilly learning platform**.

    ![Screenshot of the O'Reilly learning platform link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your O'Reilly learning platform Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to O'Reilly learning platform. If the connection fails, ensure your O'Reilly learning platform account has the required admin permissions and try again.

    Note

    Enter `https://api.oreilly.com/api/scim/v2` in the **Tenant URL**. If the connection fails, double-check that your token is correct or [contact the O’Reilly platform integration team](mailto:platform-integration@oreilly.com) for help.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to O'Reilly learning platform in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in O'Reilly learning platform for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the O'Reilly learning platform API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by O'Reilly learning platform |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | emails[type eq "work"].value | String |  | ✓ |
    | name.givenName | String |  | ✓ |
    | name.familyName | String |  | ✓ |
    | externalId | String |  | ✓ |
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.