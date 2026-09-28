---
layout: Conceptual
title: Configure Foodee for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/foodee-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Foodee.
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2e979f02-42b1-1941-1eed-0ba34453ca30
document_version_independent_id: 398a3954-fa24-87f1-6331-3c5c94b347e9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/foodee-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/foodee-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/foodee-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9aee158b-e8a3-8628-f091-d781bf6a32c2
---

# Configure Foodee for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article shows you how to configure Microsoft Entra ID in Foodee and Microsoft Entra ID to automatically provision or deprovision users or groups to Foodee.

Note

The article describes a connector that's built on top of the Microsoft Entra user provisioning service. To learn what this service does and how it works, and to get answers to frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

This connector is currently in preview. For more information about previews, see [Universal License Terms For Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

## Prerequisites

This article assumes that you've met the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Foodee tenant](https://www.food.ee/about-us/)
- A user account in Foodee with Admin permissions

## Assign users to Foodee

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, you should decide which users or groups in Microsoft Entra ID need access to Foodee. After you've made this determination, you can assign these users or groups to Foodee by following the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

## Important tips for assigning users to Foodee

When you're assigning users, keep the following tips in mind:

- We recommend that you assign only a single Microsoft Entra user to Foodee to test the configuration of automatic user provisioning. You can assign additional users or groups later.
- When you're assigning a user to Foodee, select any valid application-specific role, if it's available, in the **Assignment** pane. Users who have the *Default Access* role are excluded from provisioning.

## Set up Foodee for provisioning

Before you configure Foodee for automatic user provisioning by using Microsoft Entra ID, you need to enable System for Cross-domain Identity Management (SCIM) provisioning in Foodee.

1. Sign in to [Foodee](https://www.food.ee/login/), and then select your tenant ID.

    ![Screenshot of the main menu of the Foodee enterprise portal. A Tenant ID placeholder is visible in the menu.](media/foodee-provisioning-tutorial/tenant.png)
2. Under **Enterprise portal**, select **Single Sign On**.

    ![Screenshot of the Foodee Enterprise Portal left-pane menu.](media/foodee-provisioning-tutorial/scim.png)
3. Copy the value in the **API Token** box for later use. You'll enter it in the **Secret Token** box in the **Provisioning** tab of your Foodee application.

    ![Screenshot of a page in the Foodee enterprise portal. An A P I token value is highlighted.](media/foodee-provisioning-tutorial/token.png)

## Add Foodee from the gallery

To configure Foodee for automatic user provisioning by using Microsoft Entra ID, you need to add Foodee from the Microsoft Entra application gallery to your list of managed SaaS applications.

To add Foodee from the Microsoft Entra application gallery, do the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Screenshot of The Enterprise applications pane.](common/enterprise-applications.png)
3. To add a new application, select **New application** at the top of the pane.

    ![Screenshot of the New application button.](common/add-new-app.png)
4. In the search box, enter **Foodee**, select **Foodee** in the results pane, and then select **Add** to add the application.

    ![Screenshot of Foodee in the results list.](common/search-new-app.png)

## Configure automatic user provisioning to Foodee

In this section, you configure the Microsoft Entra provisioning service to create, update, and disable users or groups in Foodee based on user or group assignments in Microsoft Entra ID.

Tip

You can also enable SAML-based single sign-on for Foodee by following the instructions in the [Foodee single sign-on article](foodee-tutorial). You can configure single sign-on independent of automatic user provisioning, though these two features complement each other.

Configure automatic user provisioning for Foodee in Microsoft Entra ID by doing the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Screenshot of Enterprise applications pane.](common/enterprise-applications.png)
3. In the **Applications** list, select **Foodee**.

    ![Screenshot of the Foodee link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the Provisioning Mode dropdown list with the Automatic option called out.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Foodee Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Foodee. If the connection fails, ensure your Foodee account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Under **Attribute Mappings**, review the user attributes that are synchronized from Microsoft Entra ID to Foodee. The attributes that are selected as **Matching** properties are used to match the *user accounts* in Foodee for update operations.

    ![Screenshot of the Attribute Mappings page. A table lists Microsoft Entra ID and Foodee attributes and the matching precedence.](media/foodee-provisioning-tutorial/userattribute.png)
13. To commit your changes, select **Save**.
14. Under **Mappings**, select **Synchronize Microsoft Entra groups to Foodee**.
15. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
16. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
17. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

You can use the **Current Status** section to monitor progress and follow links to your provisioning activity report. The report describes all actions that are performed by the Microsoft Entra provisioning service on Foodee. For more information, see [Check the status of user provisioning](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user). To read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).