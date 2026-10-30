---
layout: Conceptual
title: Configure Vbrick Rev Cloud for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/vbrick-rev-cloud-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Vbrick Rev Cloud.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: 1d7258fe-a77c-cb2d-2532-7f2dd791f501
document_version_independent_id: eb5a524a-2e61-fa56-ddb7-adc3e9c1d4e3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/vbrick-rev-cloud-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/vbrick-rev-cloud-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/vbrick-rev-cloud-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b25179ee-e435-823e-70af-0db97f498118
---

# Configure Vbrick Rev Cloud for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Vbrick Rev Cloud and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Vbrick Rev Cloud](https://vbrick.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Vbrick Rev Cloud.
- Remove users in Vbrick Rev Cloud when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Vbrick Rev Cloud.
- Provision groups and group memberships in Vbrick Rev Cloud.
- [Single sign-on](vbrick-rev-cloud-tutorial) to Vbrick Rev Cloud (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Vbrick Rev Cloud tenant.
- A user account in Vbrick Rev Cloud with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Vbrick Rev Cloud](../app-provisioning/customize-application-attributes).

## Step 2: Configure Vbrick Rev Cloud to support provisioning with Microsoft Entra ID

1. Sign in to your **Rev Tenant**. Navigate to **Admin &gt; Security Settings &gt; User Security** in the navigation pane.

    ![Screenshot of Vbrick Rev User Security Settings.](media/vbrick-rev-cloud-provisioning-tutorial/app-navigations.png)
2. Navigate to **Microsoft Entra SCIM** section of the page.

    ![Screenshot of the Vbrick Rev User Security Settings with the Microsoft AD SCIM section called out.](media/vbrick-rev-cloud-provisioning-tutorial/enable-azure-ad-scim.png)
3. Enable **Microsoft Entra SCIM** and select **Generate Token** button. ![Screenshot of the Vbrick Rev User Security Settings with the Microsoft AD SCIM enable.](media/vbrick-rev-cloud-provisioning-tutorial/rev-scim-manage.png)
4. It will open a popup with the **URL** and the **JWT token**. Copy and save the **JWT token** and **URL** for next steps.

    ![Screenshot of the Vbrick Rev User Security Settings with the Scim Token section called out.](media/vbrick-rev-cloud-provisioning-tutorial/copy-token.png)
5. Once you have a copy of the **JWT token** and **URL**, select **OK** to close the popup and then select the **Save** button at the bottom of the settings page to enable SCIM for your tenant.

## Step 3: Add Vbrick Rev Cloud from the Microsoft Entra application gallery

Add Vbrick Rev Cloud from the Microsoft Entra application gallery to start managing provisioning to Vbrick Rev Cloud. If you have previously setup Vbrick Rev Cloud for SSO you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Vbrick Rev Cloud

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for Vbrick Rev Cloud in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Vbrick Rev Cloud**.

    ![Screenshot of the Vbrick Rev Cloud link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of new configuration.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Vbrick Rev Cloud Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Vbrick Rev Cloud. If the connection fails, ensure your Vbrick Rev Cloud account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Vbrick Rev Cloud in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Vbrick Rev Cloud for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Vbrick Rev Cloud API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Vbrick Rev Cloud |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | title | String |  |  |
    | emails[type eq "work"].value | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  | ✓ |
    | name.formatted | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | externalId | String |  | ✓ |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Vbrick Rev Cloud in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Vbrick Rev Cloud for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Vbrick Rev Cloud |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | externalId | String |  | ✓ |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.