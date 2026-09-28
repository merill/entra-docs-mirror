---
layout: Conceptual
title: Configure Peakon for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/peakon-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Peakon .
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 77d4e6e5-a03e-55de-a7db-167418826f9c
document_version_independent_id: 9c69dd2f-1067-ed13-6af5-374dc3bcec70
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/peakon-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/peakon-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/peakon-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: dc6ad334-3f8f-9adb-dd18-93ddc075fb51
---

# Configure Peakon for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Peakon and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Peakon.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

This connector is currently in Preview. For more information about previews, see [Universal License Terms For Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

Peakon is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites.

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [A Peakon tenant](https://www.workday.com/en-us/products/employee-voice/overview.html).
- A user account in Peakon with Admin permissions.

## Step 1: Assigning users to Peakon

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Peakon. Once decided, you can assign these users and/or groups to Peakon by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Step 2: Important tips for assigning users to Peakon

- It's recommended that a single Microsoft Entra user is assigned to Peakon to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Peakon, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 3: Set up Peakon for provisioning

1. Sign in to your [Peakon Admin Console](https://app.Peakon.com/login). Select **Configuration**.

    ![Peakon Admin Console](media/peakon-provisioning-tutorial/peakon-admin-configuration.png)
2. Select **Integrations**.

    ![Screenshot of the Configuration options with the Integrations option called out.](media/peakon-provisioning-tutorial/peakon-select-integration.png)
3. Enable **Employee Provisioning**.

    ![Screenshot of the Employee Provisioning section with the Enable option called out.](media/peakon-provisioning-tutorial/peakon05.png)
4. Copy the values for **SCIM 2.0 URL** and **OAuth Bearer Token**. These values are entered in the **Tenant URL** and **Secret Token** field in the Provisioning tab of your Peakon application.

    ![Peakon Create Token](media/peakon-provisioning-tutorial/peakon04.png)

## Step 4: Add Peakon from the gallery

To configure Peakon for automatic user provisioning with Microsoft Entra ID, you need to add Peakon from the Microsoft Entra application gallery to your list of managed SaaS applications.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Peakon**, select **Peakon** in the search box.
4. Select **Peakon** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Peakon  in the results list](common/search-new-app.png)

## Step 5: Configure automatic user provisioning to Peakon

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Peakon based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Peakon, following the instructions provided in the [Peakon Single sign-on article](peakon-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Peakon in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Peakon**.

    ![The Peakon  link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Peakon Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Peakon. If the connection fails, ensure your Peakon account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Peakon in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Peakon for update operations. Select the **Save** button to commit any changes.

    ![Peakon User Attributes](media/peakon-provisioning-tutorial/peakon-user-attributes.png)
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector limitations

- All custom user attributes in Peakon have to be extended from Peakon's custom SCIM user extension of `urn:ietf:params:scim:schemas:extension:peakon:2.0:User`.