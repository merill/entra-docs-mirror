---
layout: Conceptual
title: Configure SmartFile for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/smartfile-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to SmartFile.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e2940d20-b937-dcdc-2fc9-2a7a18f2ed6b
document_version_independent_id: f98e272d-6b1d-2424-066a-61bd9c64b206
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/smartfile-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/smartfile-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/smartfile-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3259f49e-78ca-2cff-6d7a-0d69687f1845
---

# Configure SmartFile for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in SmartFile and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to SmartFile.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

SmartFile is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [A SmartFile tenant](https://www.SmartFile.com/pricing/).
- A user account in SmartFile with Admin permissions.

## Assigning users to SmartFile

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to SmartFile. Once decided, you can assign these users and/or groups to SmartFile by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to SmartFile

- It's recommended that a single Microsoft Entra user is assigned to SmartFile to test the automatic user provisioning configuration. More users and/or groups may be assigned later.
- When assigning a user to SmartFile, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up SmartFile for provisioning

Before configuring SmartFile for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on SmartFile and collect more details needed.

1. Sign into your SmartFile Admin Console. Navigate to the top-right hand corner of the SmartFile Admin Console. Select **Product Key**.

    ![SmartFile Admin Console](media/smartfile-provisioning-tutorial/login.png)
2. To generate a bearer token, copy the **Product Key** and **Product Password**. Paste them in a notepad with a colon in between them.

    ![Screenshot of the Product Key section with the Product Key and Product Password text boxes called out.](media/smartfile-provisioning-tutorial/auth.png)

    ![Screenshot of plaintext showing Product Key and Product Password separated by a colon.](media/smartfile-provisioning-tutorial/key.png)

## Add SmartFile from the gallery

To configure SmartFile for automatic user provisioning with Microsoft Entra ID, you need to add SmartFile from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add SmartFile from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SmartFile**, select **SmartFile** in the search box.
4. Select **SmartFile** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![SmartFile in the results list](common/search-new-app.png)

## Configuring automatic user provisioning to SmartFile

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in SmartFile based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for SmartFile, following the instructions provided in the [SmartFile Single sign-on article](smartfile-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other

### To configure automatic user provisioning for SmartFile in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **SmartFile**.

    ![Screenshot of the SmartFile link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your SmartFile Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to SmartFile. If the connection fails, ensure your SmartFile account has the required admin permissions and try again.

    Note

    Enter `https://<SmartFile sitename>.smartfile.com/ftp/scim` in the **Tenant URL**. Example : `https://demo1test.smartfile.com/ftp/scim`.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of the Provisioning properties page showing notification and deletion settings.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to SmartFile in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in SmartFile for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the SmartFile API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    ![Screenshot of SmartFile user attribute mappings configuration.](media/smartfile-provisioning-tutorial/userattribute.png)
12. Review the group attributes that are synchronized from Microsoft Entra ID to SmartFile in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in SmartFile for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of SmartFile group attribute mappings configuration.](media/smartfile-provisioning-tutorial/groupattribute.png)
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Connector limitations

- SmartFile only supports hard deletes.