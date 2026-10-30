---
layout: Conceptual
title: Configure Zscaler One for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-one-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Zscaler One.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fd261e5e-58b0-a523-42bd-f3501c6ed4c7
document_version_independent_id: 33ee218c-5de4-707f-16ae-c3ce3c3e1969
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-one-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-one-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-one-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d51dc577-316f-33b5-d8bc-8ae436baedb1
---

# Configure Zscaler One for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article demonstrates the steps to perform in Zscaler One and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and deprovision users and groups to Zscaler One.

Note

This article describes a connector that's built on top of the Microsoft Entra user provisioning service. For information on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to software-as-a-service (SaaS) applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Zscaler One is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you have:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- A Zscaler One tenant.
- A user account in Zscaler One with admin permissions.

Note

The Microsoft Entra provisioning integration relies on the Zscaler One SCIM API. This API is available to Zscaler One developers for accounts with the Enterprise package.

## Step 1: Add Zscaler One from the Azure Marketplace

Before you configure Zscaler One for automatic user provisioning with Microsoft Entra ID, add Zscaler One from the Azure Marketplace to your list of managed SaaS applications.

To add Zscaler One from the Marketplace, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zscaler One** and select **Zscaler One** from the result panel. To add the application, select **Add**.

    ![Screenshot of Zscaler One in the results list.](common/search-new-app.png)

## Step 2: Assign users to Zscaler One

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users or groups that were assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, decide which users or groups in Microsoft Entra ID need access to Zscaler One. To assign these users or groups to Zscaler One, follow the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to Zscaler One

- We recommend that you assign a single Microsoft Entra user to Zscaler One to test the automatic user provisioning configuration. You can assign additional users or groups later.
- When you assign a user to Zscaler One, select any valid application-specific role, if available, in the assignment dialog box. Users with the **Default Access** role are excluded from provisioning.

## Step 3: Configure automatic user provisioning to Zscaler One

This section guides you through the steps to configure the Microsoft Entra provisioning service. Use it to create, update, and disable users or groups in Zscaler One based on user or group assignments in Microsoft Entra ID.

Tip

You also can enable SAML-based single sign-on for Zscaler One. Follow the instructions in the [Zscaler One single sign-on article](zscaler-one-tutorial). Single sign-on can be configured independently of automatic user provisioning, although these two features complement each other.

Note

When users and groups are provisioned or de-provisioned we recommend to periodically restart provisioning to ensure that group memberships are properly updated. Doing a restart will force our service to re-evaluate all the groups and update the memberships.

### Configure automatic user provisioning for Zscaler One in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler One**.

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Zscaler One**.

    ![Screenshot of The Zscaler One link in the applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot ofZscaler One Provisioning.](media/zscaler-one-provisioning-tutorial/provisioning-tab.png)
5. Select **+ New configuration**.

    ![Screenshot of new configuration.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, enter the **Tenant URL** and **Secret Token** of your Zscaler Beta account as described later in this article.
7. To obtain the tenant URL and secret token, go to **Administration** &gt; **Authentication Settings** in the Zscaler One portal UI. Under **Authentication Type**, select **SAML**.

    ![Screenshot of Zscaler One Authentication Settings.](media/zscaler-one-provisioning-tutorial/secret-token-1.png)
8. Select **Configure SAML** to open the **Configure SAML** options.

    ![Screenshot of Zscaler One Configure SAML.](media/zscaler-one-provisioning-tutorial/secret-token-2.png)
9. Select **Enable SCIM-Based Provisioning** to get the settings in **Base URL** and **Bearer Token**. Then save the settings. Copy the **Base URL** setting to **Tenant URL**. Copy the **Bearer Token** setting to **Secret Token**.
10. After you fill in the boxes shown in Step 5, select **Test Connection** to make sure that Microsoft Entra ID can connect to Zscaler One. If the connection fails, make sure your Zscaler One account has admin permissions and try again.

    ![Screenshot of Zscaler One Test Connection.](common/provisioning-testconnection-tenanturltoken.png)
11. Select **Create** to create your configuration.
12. Select **Properties** on the **Overview** page.
13. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
14. Select **Attribute Mapping** in the left panel and select **users**.
15. Review the user attributes that are synchronized from Microsoft Entra ID to Zscaler One in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the user accounts in Zscaler One for update operations. To save any changes, select **Save**.

    | Attribute | Type | Supported for filtering | Required by Zscaler One |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | displayName | String |  | ✓ |
    | externalId | String |  | ✓ |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  | ✓ |
16. Select **Groups**.
17. Review the group attributes that are synchronized from Microsoft Entra ID to Zscaler One in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the groups in Zscaler One for update operations. To save any changes, select **Save**.

    | Attribute | Type | Supported for filtering | Required by Zscaler One |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | externalId | String |  | ✓ |
    | members | Reference |  |  |
18. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
19. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
20. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 4: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change Logs

- 05/16/2022 - **Schema Discovery** feature enabled on this app.