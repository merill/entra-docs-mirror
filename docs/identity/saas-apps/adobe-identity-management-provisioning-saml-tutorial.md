---
layout: Conceptual
title: Configure Adobe Identity Management (SAML) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/adobe-identity-management-provisioning-saml-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Adobe Identity Management (SAML).
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
locale: en-us
document_id: 74baca5e-21fc-ea27-b3ba-c71c6b672216
document_version_independent_id: 74baca5e-21fc-ea27-b3ba-c71c6b672216
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/adobe-identity-management-provisioning-saml-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/adobe-identity-management-provisioning-saml-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/adobe-identity-management-provisioning-saml-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 65968dfb-89b9-1793-4d2d-004e4b71e649
---

# Configure Adobe Identity Management (SAML) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Adobe Identity Management (SAML) and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to Adobe Identity Management (SAML) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Adobe Identity Management (SAML).
- Remove users in Adobe Identity Management (SAML) when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Adobe Identity Management (SAML).
- Provision groups and group memberships in Adobe Identity Management (SAML).
- [Single sign-on](adobe-identity-management-tutorial) to Adobe Identity Management (SAML) (recommended).

Adobe Identity Management (SAML) is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A federated directory in the [Adobe Admin Console](https://adminconsole.adobe.com/) with verified domains.
- Review the [Adobe documentation](https://helpx.adobe.com/enterprise/using/add-azure-sync.html#add-sync) on user provisioning

Note

If your organization uses the User Sync Tool or a UMAPI integration, you must first pause the integration. Then, add Microsoft Entra automatic provisioning to automate user management. Once Microsoft Entra automatic provisioning is configured and running, you can completely remove the User Sync Tool or UMAPI integration.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Adobe Identity Management (SAML)](../app-provisioning/customize-application-attributes).

## Step 2: Configure Adobe Identity Management (SAML) to support provisioning with Microsoft Entra ID

1. Log in to [Adobe Admin Console](https://adminconsole.adobe.com/). Navigate to **Settings &gt; Directory Details &gt; Sync**.
2. Select **Add Sync**.

    ![Screenshot shows to add.](media/adobe-identity-management-provisioning-saml-tutorial/add-sync.png)
3. Select **Sync users from Microsoft Azure** and select **Next**.

    ![Screenshot that shows 'Sync users from Microsoft Entra ID' selected.](media/adobe-identity-management-provisioning-saml-tutorial/sync-users.png)
4. Copy and save the **Tenant URL** and the **Secret token**. These values are entered in the **Tenant URL** and **Secret Token** fields in the Provisioning tab of your Adobe Identity Management (SAML) application.

    ![Screenshot shows to sync.](media/adobe-identity-management-provisioning-saml-tutorial/token.png)

## Step 3: Add Adobe Identity Management (SAML) from the Microsoft Entra application gallery

Add Adobe Identity Management (SAML) from the Microsoft Entra application gallery to start managing provisioning to Adobe Identity Management (SAML). If you have previously setup Adobe Identity Management (SAML) for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Adobe Identity Management (SAML)

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Adobe Identity Management (SAML) in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot shows the enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Adobe Identity Management (SAML)**.

    ![Screenshot shows the Adobe Identity Management (SAML) link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot shows the provisioning tab.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Adobe Identity Management (SAML) Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Adobe Identity Management (SAML). If the connection fails, ensure your Adobe Identity Management (SAML) account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Adobe Identity Management (SAML) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Adobe Identity Management (SAML) for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Adobe Identity Management (SAML) API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Adobe Identity Management (SAML) |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | emails[type eq "work"].value | String |  |  |
    | addresses[type eq "work"].country | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | urn:ietf:params:scim:schemas:extension:Adobe:2.0:User:emailAliases | String |  |  |
    | urn:ietf:params:scim:schemas:extension:Adobe:2.0:User:eduRole | String |  |  |

    Note

    The **eduRole** field accepts values like `Teacher or Student`, anything else is ignored.
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Adobe Identity Management (SAML) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Adobe Identity Management (SAML) for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Adobe Identity Management (SAML) |
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

## Change log

- 07/18/2023 - The app was added to Gov Cloud.
- 08/15/2023 - Added support for Schema Discovery.