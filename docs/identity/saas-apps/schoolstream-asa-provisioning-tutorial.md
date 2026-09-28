---
layout: Conceptual
title: Configure SchoolStream ASA for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/schoolstream-asa-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to SchoolStream ASA.
ms.topic: how-to
ms.date: 2026-03-20T00:00:00.0000000Z
locale: en-us
document_id: cb9f0599-fc86-8bc8-d347-f04ae36221ea
document_version_independent_id: 893c52bf-5d1c-03c3-f038-9fd2cc39ef60
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/schoolstream-asa-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/schoolstream-asa-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/schoolstream-asa-provisioning-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/440fefb2-823b-44b8-a593-35604cde23b7
- https://authoring-docs-microsoft.poolparty.biz/devrel/9f747546-6aa0-47b1-90d7-ee9646fdb207
- https://authoring-docs-microsoft.poolparty.biz/devrel/bad69977-db6a-44f3-b752-d2bee7de49ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1b2df129-9f07-41b8-9038-0761a41d8a21
- https://authoring-docs-microsoft.poolparty.biz/devrel/c49cc9cb-c0e4-4c7c-8e26-9ab61f52e8b0
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31d7aff-61be-45e2-a324-a578cf0c3360
platformId: b0c1de27-4145-c447-adeb-a766100eb391
---

# Configure SchoolStream ASA for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both SchoolStream ASA and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [SchoolStream ASA](https://www.ssk12.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in SchoolStream ASA
- Remove users in SchoolStream ASA when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and SchoolStream ASA.
- Provision groups and group memberships in SchoolStream ASA.
- [Single sign-on](../enterprise-apps/add-application-portal-setup-oidc-sso) to SchoolStream ASA (recommended).
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A SchoolStream Website. Please contact [SchoolStream support](mailto:support@rtresponse.com) if you don't have one.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and SchoolStream ASA](../app-provisioning/customize-application-attributes).

## Step 2: Configure SchoolStream ASA to support provisioning with Microsoft Entra ID

1. Contact [SchoolStream support](mailto:support@rtresponse.com) to request SchoolStream ASA integration, you need to provide your **Microsoft Entra tenant Id** and your **SchoolStream Website URL**.
2. You get your **Secret Token** and SchoolStream ASA **Tenant URL** after SchoolStream has mapped your SchoolStream Website and Microsoft Entra tenant ID.

## Step 3: Add SchoolStream ASA from the Microsoft Entra application gallery

To start managing provisioning to SchoolStream ASA in your Microsoft Entra ID, you need to add SchoolStream ASA from the Microsoft Entra application gallery.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Browse Microsoft Entra Gallery** section, type **SchoolStream ASA** in the search box.
4. Select **SchoolStream ASA** from results panel and then **Sign up for the app**. Wait a few seconds while the app is added to your tenant.

If you have previously setup SchoolStream ASA for SSO you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to SchoolStream ASA

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in SchoolStream ASA based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for SchoolStream ASA in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **SchoolStream ASA**.

    ![The SchoolStream ASA link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. If you're configuring provisioning for the first time, select **Get started**.
6. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
7. In the **Tenant URL** field, input your SchoolStream ASA Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to SchoolStream ASA. If the connection fails, ensure your SchoolStream ASA account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
8. Select **Create** to create your configuration.
9. Select **Properties** on the **Overview** page.
10. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. In the **Mappings** section, select **Provision Microsoft Entra users**.
12. Select **Add New Mapping** at the bottom.
13. In the dialog **Edit Attribute**:

    - In the **Mapping type** field, select **Direct** from the dropdown,
    - In the **Source attribute** field, select **extensionAttribute1** from the dropdown,
    - Enter your **Microsoft Entra tenant Id** in the field **Default value if null(optional)**,
    - In the **Target attribute** field, select **urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization** from the dropdown,
    - In the **Match objects using this attribute** field, select **No** from the dropdown,
    - In the **Apply this mapping** field, select **Always** from the dropdown,
    - Select **OK**.

        ![Edit Attribute](media/schoolstream-asa-provisioning-tutorial/add-mappings-attribute.png)
14. Review the user attributes that are synchronized from Microsoft Entra ID to SchoolStream ASA in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in SchoolStream ASA for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the SchoolStream ASA API supports filtering users based on that attribute.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | displayName | String |  |
    | emails[type eq "work"].value | String |  |
    | preferredLanguage | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | name.formatted | String |  |
    | phoneNumbers[type eq "mobile"].value | String |  |
    | externalId | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |
15. Select **Groups**.
16. Review the group attributes that are synchronized from Microsoft Entra ID to SchoolStream ASA in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in SchoolStream ASA for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | displayName | String | ✓ |
    | members | Reference |  |
    | externalId | String |  |
17. Select the **Save** button to commit any changes. You can go back to the **Application** tab and select **Edit provisioning** to continue.
18. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
19. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
20. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change log

- 09/24/2020 - Group provisioning got enabled.