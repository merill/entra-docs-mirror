---
layout: Conceptual
title: Configure Lexmark Cloud Services (SAML) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lexmark-cloud-services-provisioning-saml-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Lexmark Cloud Services (SAML).
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 620603ca-85c4-befc-30d0-e72b477f3f71
document_version_independent_id: 620603ca-85c4-befc-30d0-e72b477f3f71
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lexmark-cloud-services-provisioning-saml-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lexmark-cloud-services-provisioning-saml-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lexmark-cloud-services-provisioning-saml-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e5f6eabe-8bf0-933d-6f99-305af8ff246d
---

# Configure Lexmark Cloud Services (SAML) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Lexmark Cloud Services (SAML) and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to Lexmark Cloud Services (SAML) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Lexmark Cloud Services (SAML)
- Disable users in Lexmark Cloud Services (SAML) when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Lexmark Cloud Services (SAML) [Single sign-on](../enterprise-apps/add-application-portal-setup-oidc-sso) to Lexmark Cloud Services (SAML) (recommended).

Note

Lexmark Cloud Services (SAML) application currently only supports user provisioning. Group provisioning isn't supported and is planned for a future release.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A SAML federated organization in Lexmark Cloud Services with Organization Administrator role.
- Review the [lexmark documentation](https://support.lexmark.com/en_us/manuals-guides/online/Lexmark-Cloud-Platform/overview-v54808648.html?toc=2.5.0) on user provisioning.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Adobe Identity Management (SAML)](../app-provisioning/customize-application-attributes).

## Step 2: Configure Lexmark Cloud Services (SAML) to support provisioning with Microsoft Entra ID

1. Log in to Lexmark Cloud Services.
2. From the Dashboard card or the navigation waffle menu, select **Account Management**.

    ![Screenshot shows Account Management.](media/lexmark-cloud-services-provisioning-saml-tutorial/account-management.png)
3. If necessary, select your organization, and then select **Next**.

    ![Screenshot shows Organization Menu.](media/lexmark-cloud-services-provisioning-saml-tutorial/organization.png)
4. Ensure your organization is configured for SSO with [Lexmark Cloud Services (SAML) application](lexmark-cloud-services-tutorial).
5. In the **Select Organization** pane, select **User provisioning**.

    ![Screenshot shows User Provisioning Menu.](media/lexmark-cloud-services-provisioning-saml-tutorial/user-provisioning.png)
6. Select **Enable User Provisioning**.

    ![Screenshot shows Enable User Provisioning.](media/lexmark-cloud-services-provisioning-saml-tutorial/enable-user-provisioning-saml.png)
7. Provisioning details will be automatically populated when enabled.

    ![Screenshot shows User Provisioning Details.](media/lexmark-cloud-services-provisioning-saml-tutorial/provisioning-details.png)

## Step 3: Add Lexmark Cloud Services (SAML) from the Microsoft Entra application gallery

Add Lexmark Cloud Services (SAML) from the Microsoft Entra application gallery to start managing provisioning to Lexmark Cloud Services (SAML). If you have previously setup Lexmark Cloud Services (SAML) for SSO, you can use the same application. However, it is recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Configure automatic user provisioning to Lexmark Cloud Services (SAML)

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Lexmark Cloud Services (SAML) based on user and/or group assignments in Microsoft Entra ID

### To configure automatic user provisioning for Lexmark Cloud Services (SAML) in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an app owner or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot shows the enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Lexmark Cloud Services (SAML)**.

    ![Screenshot shows the Lexmark Cloud Services (SAML) link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot shows the provisioning tab.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the Tenant URL field, input your Lexmark Cloud Services (SAML) Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Lexmark Cloud Services (SAML). If the connection fails, ensure your Lexmark Cloud Services (SAML) account has Admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties:

    1. Enable notification emails and provide an email to receive quarantine emails.
    2. Enable accidental deletions prevention.
    3. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select users.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Lexmark Cloud Services (SAML) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Lexmark Cloud Services (SAML) for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Lexmark Cloud Services (SAML) API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Lexmark Cloud Services (SAML) |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | displayName | String |  |  |
    | preferredLanguage | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
12. Select **groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Lexmark Cloud Services (SAML) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Lexmark Cloud Services (SAML) for update operations. Select the **Save** button to commit any changes.
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.