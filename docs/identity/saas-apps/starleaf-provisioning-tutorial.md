---
layout: Conceptual
title: Configure StarLeaf for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/starleaf-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to StarLeaf.
ms.topic: how-to
ms.date: 2026-04-13T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 507011ea-cc92-8c7f-db58-aca0c087e1f7
document_version_independent_id: bed1b86d-c699-9bed-496e-25cf5c4cb3ae
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/starleaf-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/starleaf-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/starleaf-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3017d6d9-991e-6706-6549-c1f70a11f7a2
---

# Configure StarLeaf for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in StarLeaf and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to StarLeaf.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

This connector is currently in Preview. For more information about previews, see [Universal License Terms For Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

## Capabilities supported

- Create users in StarLeaf.
- Remove users in StarLeaf when they don't require access anymore.
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [A StarLeaf tenant](https://starleaf.com/).
- A user account in StarLeaf with Admin permissions.

## Step 1: Assign users to StarLeaf

Microsoft Entra ID uses a concept called assignments to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, you should decide which users and groups in Microsoft Entra ID need access to StarLeaf. Then you can assign the users and groups to StarLeaf by following [these instructions](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to StarLeaf

- It's recommended that a single Microsoft Entra user is assigned to StarLeaf to test the automatic user provisioning configuration. More users and groups can be assigned later.
- When you assign a user to StarLeaf, you must select any valid application-specific role (if available) in the assignment dialog. Users with the Default Access role are excluded from provisioning.

## Step 2: Set up StarLeaf for provisioning

Before you configure StarLeaf for automatic user provisioning with Microsoft Entra ID, you need to configure SCIM provisioning in StarLeaf:

1. Sign in to your StarLeaf Admin Console. Navigate to **Integrations** &gt; **Add integration**.

    ![Screenshot of the StarLeaf Admin Console with the Integrations and Add integration options called out.](media/starleaf-provisioning-tutorial/image00.png)
2. Select the **Type** to be Microsoft Entra ID. Enter a suitable name in **Name**. Select **Apply**.

    ![Screenshot of the Add integration dialog box with the Type and Name text boxes called out.](media/starleaf-provisioning-tutorial/image01.png)
3. The **SCIM base URL** and **Access token** values are then displayed. These values are entered in the **Tenant URL** and **Secret Token** fields in the Provisioning tab of your StarLeaf application.

    ![Screenshot of the Edit integration dialog box with the Type, Name, and SCIM base URL text boxes called out.](media/starleaf-provisioning-tutorial/image02.png)

## Step 3: Add StarLeaf from the gallery

To configure StarLeaf for automatic user provisioning with Microsoft Entra ID, you need to add StarLeaf from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add StarLeaf from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **StarLeaf**, select **StarLeaf** in the results panel.

    ![Screenshot of the StarLeaf in the results list.](common/search-new-app.png)

## Step 4: Configure automatic user provisioning to StarLeaf

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in StarLeaf based on user and/or group assignments in Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of the Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **StarLeaf**.

    ![Screenshot of the StarLeaf link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the New configuration option on the Provisioning page.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your StarLeaf Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to StarLeaf. If the connection fails, ensure your StarLeaf account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to StarLeaf in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in StarLeaf for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of the Attribute Mappings section showing nine mappings displayed.](media/starleaf-provisioning-tutorial/userattribute.png)
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector limitations

- StarLeaf doesn't currently support group provisioning.
- StarLeaf requires **email** and **userName** values to have the same source value.