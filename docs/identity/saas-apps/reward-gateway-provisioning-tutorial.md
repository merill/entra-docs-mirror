---
layout: Conceptual
title: Configure Reward Gateway for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/reward-gateway-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Reward Gateway.
ms.topic: how-to
ms.date: 2026-04-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5d3ee061-d42b-8f9d-a98a-c8ba055938a3
document_version_independent_id: 2379d6e5-f70a-883f-fc74-1ec1776aaa2f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/reward-gateway-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/reward-gateway-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/reward-gateway-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 36b565f9-f1db-fa39-cdc0-4ee4544bbd1f
---

# Configure Reward Gateway for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Reward Gateway and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Reward Gateway.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

This connector is currently in public preview. For more information about previews, see [Universal License Terms For Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- A [Reward Gateway tenant](https://www.rewardgateway.com/).
- A user account in Reward Gateway with Admin permissions.

## Assigning users to Reward Gateway

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Reward Gateway. Once decided, you can assign these users and/or groups to Reward Gateway by following the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

## Important tips for assigning users to Reward Gateway

- It's recommended that a single Microsoft Entra user is assigned to Reward Gateway to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Reward Gateway, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Setup Reward Gateway for provisioning

Before configuring Reward Gateway for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on Reward Gateway.

1. Sign in to your [Reward Gateway Admin Console](https://rewardgateway.photoshelter.com/login/). Select **Integrations**.

    ![Screenshot of the Reward Gateway Admin Console with the Integrations option called out.](media/reward-gateway-provisioning-tutorial/image00.png)
2. Select **My Integration**.

    ![Screenshot of the two Integrations options with the My Integrations option called out.](media/reward-gateway-provisioning-tutorial/image001.png)
3. Copy the values of **SCIM URL (v2)** and **OAuth Bearer Token**. These values are entered in the Tenant URL and Secret Token field in the Provisioning tab of your Reward Gateway application.

    ![Screenshot of the My Integrations panel with the OAuth Bearer Token text box called out.](media/reward-gateway-provisioning-tutorial/image03.png)

## Add Reward Gateway from the gallery

To configure Reward Gateway for automatic user provisioning with Microsoft Entra ID, you need to add Reward Gateway from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Reward Gateway from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Reward Gateway**, select **Reward Gateway** in the search box.
4. Select **Reward Gateway** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

    ![Screenshot of the Reward Gateway in the results list.](common/search-new-app.png)

## Configuring automatic user provisioning to Reward Gateway

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Reward Gateway based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Reward Gateway, following the instructions provided in the [Reward Gateway Single sign-on article](reward-gateway-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Reward Gateway in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of the Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Reward Gateway**.

    ![Screenshot of the Reward Gateway link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Reward Gateway Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Reward Gateway. If the connection fails, ensure your Reward Gateway account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page showing notification and deletion settings.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select users.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Reward Gateway in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Reward Gateway for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of the Attribute Mappings section with six mappings displayed.](media/reward-gateway-provisioning-tutorial/user-attributes.png)
12. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Connector limitations

Reward Gateway doesn't support group provisioning currently.