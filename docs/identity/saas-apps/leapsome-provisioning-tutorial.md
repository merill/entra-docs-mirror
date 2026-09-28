---
layout: Conceptual
title: Configure Leapsome for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/leapsome-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Leapsome.
ms.topic: how-to
ms.date: 2026-04-08T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d0de50c6-4f53-edd1-aff1-7cfe14e295ef
document_version_independent_id: 25470ce1-e94a-2797-9c20-c2a682d06349
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/leapsome-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/leapsome-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/leapsome-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 039f0c4d-1a88-e953-9862-294db5f2d6b1
---

# Configure Leapsome for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Leapsome and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Leapsome.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

This connector is currently in Preview. For more information about previews, see [Universal License Terms For Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- A [Leapsome](https://www.Leapsome.com/pricing) tenant.
- A user account in Leapsome with Admin permissions.

## Assigning users to Leapsome

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Leapsome. Once decided, you can assign these users and/or groups to Leapsome by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to Leapsome

- It's recommended that a single Microsoft Entra user is assigned to Leapsome to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Leapsome, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up Leapsome for provisioning

1. Sign in to your [Leapsome Admin Console](https://www.Leapsome.com/app/#/login). Navigate to **Settings &gt; Admin Settings**.

    ![Screenshot of Leapsome Admin Console.](media/leapsome-provisioning-tutorial/leapsome-admin-console.png)
2. Navigate to **Integrations &gt; SCIM User provisioning**.

    ![Screenshot of Leapsome Add SCIM.](media/leapsome-provisioning-tutorial/leapsome-add-scim.png)
3. Copy the **SCIM Authentication Token**. This value is entered in the Secret Token field in the Provisioning tab of your Leapsome application.

    ![Screenshot of Leapsome Create Token.](media/leapsome-provisioning-tutorial/leapsome-create-token.png)

## Add Leapsome from the gallery

Before configuring Leapsome for automatic user provisioning with Microsoft Entra ID, you need to add Leapsome from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Leapsome from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Leapsome**, select **Leapsome** in the search box.
4. Select **Leapsome** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Screenshot of Leapsome in the results list.](common/search-new-app.png)

## Configuring automatic user provisioning to Leapsome

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Leapsome based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Leapsome, following the instructions provided in the [Leapsome Single sign-on article](leapsome-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other

### To configure automatic user provisioning for Leapsome in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Leapsome**.

    ![Screenshot of the Leapsome link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Leapsome Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Leapsome. If the connection fails, ensure your Leapsome account has the required admin permissions and try again.

    Note

    Enter `https://www.leapsome.com/api/scim` in **Tenant URL**.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Leapsome in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Leapsome for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Leapsome API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    ![Screenshot of Leapsome User Attributes.](media/leapsome-provisioning-tutorial/leapsome-user-attributes.png)
12. Review the group attributes that are synchronized from Microsoft Entra ID to Leapsome in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Leapsome for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of Leapsome Group Attributes.](media/leapsome-provisioning-tutorial/leapsome-group-attributes.png)
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Connector Limitations

- Leapsome requires **userName** to be unique.
- Leapsome only allows work email addresses to be saved.