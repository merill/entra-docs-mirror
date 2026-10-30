---
layout: Conceptual
title: Configure UiPath for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/uipath-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to UiPath.
ms.topic: how-to
ms.date: 2026-04-14T00:00:00.0000000Z
locale: en-us
document_id: 87a69374-b966-82d5-662c-88e07190ff04
document_version_independent_id: 87a69374-b966-82d5-662c-88e07190ff04
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/uipath-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/uipath-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/uipath-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3cf858a6-7c63-ef43-d7cf-743ccda452bd
---

# Configure UiPath for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both UiPath and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users to [UiPath](https://www.UiPath.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in UiPath
- Remove users in UiPath when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and UiPath
- [Single sign-on](../enterprise-apps/add-application-portal-setup-oidc-sso) to UiPath (recommended).
- Client Credentials Authentication authentication supported.

Note

UiPath currently supports user provisioning only. Group provisioning isn't supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in UiPath with Admin permissions.

## Step 1: Plan your provisioning deployment

- Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
- Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- Determine what data to [map between Microsoft Entra ID and UiPath](../app-provisioning/customize-application-attributes).

## Step 2: Configure UiPath to support provisioning with Microsoft Entra ID

1. Sign in to [UiPath Automation Cloud](https://cloud.uipath.com) with an account that has admin permissions in your UiPath organization.
2. In the left-hand menu, select **Admin**, then navigate to **Security Settings** &gt; **Authentication settings**.
3. Ensure the Microsoft Entra directory integration is configured and shows **Active** status.

    ![Screenshot shows the Microsoft Entra ID integration card with Active status.](media/uipath-provisioning-tutorial/integration-active.png)
4. Scroll down to the **Directory integration details** section and select **Enable SCIM**.

    ![Screenshot shows the Directory integration details section with the Enable SCIM button.](media/uipath-provisioning-tutorial/enable.png)
5. In the **Configure SCIM directory integration** dialog, select one of the following SCIM authorization methods supported by Microsoft Entra ID:

    - **OAuth client credentials grant** (Recommended)
    - **Long-lived bearer token**

    ![Screenshot shows the Configure SCIM directory integration dialog with authorization method options.](media/uipath-provisioning-tutorial/configure.png)
6. Select **Configure**. The **SCIM is enabled!** confirmation screen displays the connection details you need to configure in Microsoft Entra ID.

    **For Bearer token:**

    - **SCIM URL** : The endpoint URL for the SCIM connector.
    - **Bearer token** : The secret token to authenticate requests.

    ![Screenshot shows the SCIM enabled confirmation with Bearer token details and attribute mappings.](media/uipath-provisioning-tutorial/bearer-token.png)

    **For OAuth client credentials grant:**

    - **SCIM URL** : The endpoint URL for the SCIM connector.
    - **OAuth application ID** : The client identifier for the OAuth application.
    - **OAuth secret** : The client secret for the OAuth application.

    ![Screenshot shows the SCIM enabled confirmation with OAuth client credentials details and attribute mappings.](media/uipath-provisioning-tutorial/secret-token.png)

    Copy these values, you need them later in this tutorial.

    Note

    Leave this browser tab open. Don't select **I have completed identity provider configuration** until you have completed the steps in Step 5.
7. After completing the Microsoft Entra ID configuration in Step 5, return to UiPath and select **I have completed identity provider configuration**. The Directory integration details section now confirms SCIM provisioning and deprovisioning are active.

    ![Screenshot shows the Directory integration details after SCIM is configured, with Manage SCIM and Remove SCIM buttons.](media/uipath-provisioning-tutorial/configured.png)

## Step 3: Add UiPath from the Microsoft Entra application gallery

Add UiPath from the Microsoft Entra application gallery to start managing provisioning to UiPath. If you have previously setup UiPath for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to UiPath

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in UiPath based on user assignments in Microsoft Entra ID.

### Configure automatic user provisioning for UiPath in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an app owner or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot shows the enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **UiPath**.

    ![Screenshot shows the UiPath link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot shows the provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of new configuration.](common/application-provisioning.png)
6. In the connection details, enter the values obtained from Step 2 based on your chosen authorization method:

    **For OAuth2 client credentials grant (Recommended):**

    - **Tenant URL** — Enter the **SCIM URL** from Step 2 (for example, `https://cloud.uipath.com/{orgId}/identity_/api/scim/v2`).
    - **Token endpoint** — Enter your UiPath organization's token exchange endpoint (for example, `https://cloud.uipath.com/{org-name}/identity_/connect/token`).
    - **Client identifier** — Enter the **OAuth application ID** from Step 2.
    - **Client secret** — Enter the **OAuth secret** from Step 2.

    **For Bearer authentication:**

    - **Tenant URL** — Enter the **SCIM URL** from Step 2 (for example, `https://cloud.uipath.com/{orgId}/identity_/api/scim/v2`).
    - **Secret token** — Enter the **Bearer token** from Step 2.

    Select **Test Connection** to ensure Microsoft Entra ID can connect to UiPath. If the connection fails, verify the values entered match those provided in Step 2 and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to UiPath in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in UiPath for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the UiPath API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by UiPath |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | externalId | String | ✓ | ✓ |
    | displayName | String |  | ✓ |
    | title | String |  |  |
    | emails[type eq "work"].value | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | addresses[type eq "work"].locality | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
12. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.