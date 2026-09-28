---
layout: Conceptual
title: Configure uniFLOW Online for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/uniflow-online-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: beatrizd
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to uniFLOW Online.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: b4794afa-b8c5-75f5-f8ff-92fe3bb9c0ed
document_version_independent_id: 09b50f8b-e632-673b-a168-0c8e11f4621f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/uniflow-online-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/uniflow-online-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/uniflow-online-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 60535965-4164-8623-bcba-956980bba2fb
---

# Configure uniFLOW Online for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both uniFLOW Online and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to [uniFLOW Online](https://www.uniflowonline.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in uniFLOW Online.
- Disable users in uniFLOW Online.
- Remove users in uniFLOW Online when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and uniFLOW Online.
- [Single sign-on](uniflow-online-tutorial) to uniFLOW Online (recommended).
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- An administrator account with uniFLOW Online.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and uniFLOW Online](../app-provisioning/customize-application-attributes).

## Step 2: Configure uniFLOW Online to support provisioning with Microsoft Entra ID

- In a different web browser window, sign in to uniFLOW Online website as an administrator.
- Select **Extensions** tab **&gt; Identity Providers &gt; Configure identity providers**.
- Select **Add identity provider**. On the **ADD IDENTITY PROVIDER**section, perform the following steps:
    - Enter the **Display name** .
    - For **Provider type**, select **WS-Federation** option from the dropdown.
    - For **WS-Federation type**, select **Microsoft Entra ID** option from the dropdown.
    - Select **Save**.
- Enable the Advanced Administrative View within your user Profile settings by navigating to **Profile settings &gt; Administrator view** and setting it to **Advanced**.
- The provisioning tab will now be available within the Identity Provider configuration.
- Select **Enable Provisioning**when you're ready to set up user provisioning in your company's Microsoft Entra ID.
    - **Provisioning tenant URL** (only displayed once after **Provisioning** is enabled): You need this URL when setting up provisioning in your Microsoft Entra application.
    - **Provisioning secret token** (only displayed once after **Provisioning** is enabled): You need this token when setting up provisioning in your Microsoft Entra application.

## Step 3: Add uniFLOW Online from the Microsoft Entra application gallery

Add uniFLOW Online from the Microsoft Entra application gallery to start managing provisioning to uniFLOW Online. If you have previously setup uniFLOW Online for SSO you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to uniFLOW Online

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for uniFLOW Online in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **uniFLOW Online**.

    ![Screenshot of the uniFlow Online link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your uniFLOW Online Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to uniFLOW Online. If the connection fails, ensure your uniFLOW Online account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to uniFLOW Online in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in uniFLOW Online for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the uniFLOW Online API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by uniFLOW Online |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | externalId | String | ✓ | ✓ |
    | emails[type eq "work"].value | String | ✓ |  |
    | active | Boolean |  | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | displayName | String |  |  |
    | title | String |  |  |
    | addresses[type eq "work"].streetAddress | String |  |  |
    | title | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | urn:ietf:params:scim:schemas:extension:uniFLOWOnline:2.0:User:cardNumber | String |  |  |
    | urn:ietf:params:scim:schemas:extension:uniFLOWOnline:2.0:User:cardRegistrationCode | String |  |  |
    | urn:ietf:params:scim:schemas:extension:uniFLOWOnline:2.0:User:localUsername | String |  |  |
    | urn:ietf:params:scim:schemas:extension:uniFLOWOnline:2.0:User:pin | String |  |  |
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.