---
layout: Conceptual
title: Configure Figma for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/figma-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Figma.
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 068a5d02-a7f2-5ebb-c32b-81061246b231
document_version_independent_id: f169a659-1df4-be9d-ce48-980f682f6ca4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/figma-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/figma-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/figma-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cc76a15d-3d07-17f6-6a5b-a0c9642e7e93
---

# Configure Figma for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Figma and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Figma.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Figma.
- Remove users in Figma when they don't require access anymore.
- [Single sign-on](figma-tutorial) to Figma (recommended).
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- [A Figma tenant](https://www.figma.com/pricing/).
- A user account in Figma with Admin permissions.

## Assign users to Figma.

Microsoft Entra ID uses a concept called assignments to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Figma. Once decided, you can assign these users and/or groups to Figma by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to Figma

- It's recommended that a single Microsoft Entra user is assigned to Figma to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Figma, you must select any valid application-specific role (if available) in the assignment dialog. Users with the Default Access role are excluded from provisioning.

## Set up Figma for provisioning

Before configuring Figma for automatic user provisioning with Microsoft Entra ID, you need to retrieve some provisioning information from Figma.

1. Sign in to your [Figma Admin Console](https://www.Figma.com/). Select the gear icon next to your tenant.

    ![Screenshot of the Figma admin console. A tenant named A A D Scim Test is visible. Next to the tenant, a gear icon is highlighted.](media/figma-provisioning-tutorial/image0.png)
2. Navigate to **General &gt; Update Log in Settings**.

    ![Screenshot of the General tab of the Figma admin console. Under Log in and provisioning, Update log in settings is highlighted.](media/figma-provisioning-tutorial/figma03.png)
3. Copy the **Tenant ID**. This value is used to construct the SCIM endpoint URL to be entered into the **Tenant URL** field in the Provisioning tab of your Figma application.

    ![Screenshot of the S A M L S S O section in the Figma admin console. A Tenant ID label and an adjacent link that says Copy are highlighted.](media/figma-provisioning-tutorial/figma-tenantid.png)
4. Scroll down and select **Generate API Token**.

    ![Screenshot of the S C I M provisioning section in the Figma admin console. A link labeled Generate A P I token is highlighted.](media/figma-provisioning-tutorial/token.png)
5. Copy the **API Token** value. This value is entered in the **Secret Token** field in the Provisioning tab of your Figma application.

    ![Screenshot of a page in the Figma admin console. Under Your provisioning A P I token, a placeholder for the token is highlighted.](media/figma-provisioning-tutorial/figma04.png)

## Add Figma from the gallery

To configure Figma for automatic user provisioning with Microsoft Entra ID, you need to add Figma from the Microsoft Entra application gallery to your list of managed SaaS applications.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Figma**, select **Figma** in the search box.
4. Select **Figma** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Screenshot of Figma  in the results list.](common/search-new-app.png)

## Configuring automatic user provisioning to Figma

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Figma based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Figma, following the instructions provided in the [Figma Single sign-on article](figma-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Figma in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Figma**.

    ![Screenshot of the Figma  link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the Provisioning Mode dropdown list with the Automatic option called out.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Figma Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Figma. If the connection fails, ensure your Figma account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to Figma in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Figma for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of Figma User Attributes.](media/figma-provisioning-tutorial/figma06.png)
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).