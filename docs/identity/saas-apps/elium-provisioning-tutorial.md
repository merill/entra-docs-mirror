---
layout: Conceptual
title: Configure Elium for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/elium-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Elium.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4cf1259f-525a-f17e-f4f8-fab4f9e8b1e0
document_version_independent_id: 010c5176-2568-f6ad-1a8c-ee0232070ef7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/elium-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/elium-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/elium-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ed833d56-43e9-fe90-da36-3d4b7a8551cc
---

# Configure Elium for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article shows how to configure Elium and Microsoft Entra ID to automatically provision and de-provision users or groups to Elium.

Note

This article describes a connector that's built on top of the Microsoft Entra user provisioning service. For important details about what this service does and how it works, and for frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

This connector is currently in preview. For more information about previews, see [Universal License Terms For Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

Elium is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Capabilities supported

- Create users in Elium.
- Remove users in Elium when they don't require access anymore.
- [Single sign-on](elium-tutorial) to Elium (recommended).
- Long lived bearer token authentication supported.

## Prerequisites

This article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [An Elium tenant](https://www.elium.com/pricing/)
- A user account in Elium, with admin permissions

## Assigning users to Elium

Microsoft Entra ID uses a concept called *assignments* to determine which users receive access to selected apps. In the context of automatic user provisioning, only the users and groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, decide which users and groups in Microsoft Entra ID need access to Elium. Then, assign those users and groups to Elium by following the steps in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

## Important tips for assigning users to Elium

We recommend that you assign a single Microsoft Entra user to Elium to test the automatic user-provisioning configuration. More users and groups can be assigned later.

When assigning a user to Elium, you must select a valid, application-specific role (if any are available) in the assignment dialog box. Users who have the **Default Access** role are excluded from provisioning.

## Set up Elium for provisioning

Before configuring Elium for automatic user provisioning with Microsoft Entra ID, you must enable System for Cross-domain Identity Management (SCIM) provisioning on Elium. Follow these steps:

1. Sign in to Elium and go to **My Profile** &gt; **Settings**.

    ![Settings menu item in Elium](media/elium-provisioning-tutorial/setting.png)
2. In the lower-left corner, under **ADVANCED**, select **Security**.

    ![Security link in Elium](media/elium-provisioning-tutorial/security.png)
3. Copy the **Tenant URL** and **Secret token** values. You'll use these values later, in corresponding fields in the **Provisioning** tab of your Elium application.

    ![Tenant URL and Secret token fields in Elium](media/elium-provisioning-tutorial/token.png)

## Add Elium from the gallery

To configure Elium for automatic user provisioning with Microsoft Entra ID, you must also add Elium from the Microsoft Entra application gallery to your list of managed software-as-a-service (SaaS) applications. Follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Microsoft Entra Enterprise applications blade](common/enterprise-applications.png)
3. To add a new application, select **New application** at the top of the pane.

    ![New application link](common/add-new-app.png)
4. In the search box, type **Elium**, select **Elium** in the results list, and then select **Add** to add the application.

    ![Gallery search box](common/search-new-app.png)

## Configure automatic user provisioning to Elium

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and groups in Elium, based on user and group assignments in Microsoft Entra ID.

Tip

You might also choose to enable single sign-on for Elium based on Security Assertion Markup Language (SAML) by following the instructions in the [Elium single sign-on article](elium-tutorial). You can configure single sign-on independently of automatic user provisioning, although the two features complement each other.

To configure automatic user provisioning for Elium in Microsoft Entra ID, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Microsoft Entra Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Elium**.

    ![Applications list in the Enterprise applications blade](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab in the Enterprise applications blade](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Elium Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Elium. If the connection fails, ensure your Elium account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Elium in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Elium for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Elium API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    ![Attribute mappings between Microsoft Entra ID and Elium](media/elium-provisioning-tutorial/userattribute.png)
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.