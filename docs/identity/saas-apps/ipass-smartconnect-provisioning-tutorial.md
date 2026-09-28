---
layout: Conceptual
title: Configure iPass SmartConnect for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ipass-smartconnect-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to iPass SmartConnect.
ms.topic: how-to
ms.date: 2026-04-10T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c5656e90-1512-a994-4024-f692eb8e042f
document_version_independent_id: 919d8101-cfea-02ae-38a7-256e1532e724
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ipass-smartconnect-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ipass-smartconnect-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ipass-smartconnect-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cd81f7f2-1529-180a-ff76-338ad2153aeb
---

# Configure iPass SmartConnect for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in iPass SmartConnect and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to iPass SmartConnect.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

iPass SmartConnect is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- [An iPass SmartConnect tenant](https://www.ipass.com/).
- A user account in iPass SmartConnect with Admin permissions.

## Assigning users to iPass SmartConnect

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to iPass SmartConnect. Once decided, you can assign these users and/or groups to iPass SmartConnect by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to iPass SmartConnect

- It's recommended that a single Microsoft Entra user is assigned to iPass SmartConnect to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to iPass SmartConnect, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up iPass SmartConnect for provisioning

Before configuring iPass SmartConnect for automatic user provisioning with Microsoft Entra ID, you need to retrieve configuration information from the iPass SmartConnect admin console:

1. To retrieve the bearer token that's needed to authenticate against your iPass SmartConnect SCIM endpoint, refer to the very first time that you set up iPass SmartConnect as this value is only provided then.
2. If you don't have the bearer token, reach out to [iPass SmartConnect's support team](mailto:help@ipass.com) to retrieve a new one.

## Add iPass SmartConnect from the gallery

To configure iPass SmartConnect for automatic user provisioning with Microsoft Entra ID, you need to add iPass SmartConnect from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add iPass SmartConnect from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **iPass SmartConnect**, select **iPass SmartConnect** in the search box.
4. Select **iPass SmartConnect** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Screenshot of iPass SmartConnect in the results list.](common/search-new-app.png)

## Configuring automatic user provisioning to iPass SmartConnect

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in iPass SmartConnect based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for iPass SmartConnect, following the instructions provided in the [iPass SmartConnect Single sign-on article](ipasssmartconnect-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for iPass SmartConnect in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **iPass SmartConnect**.

    ![Screenshot of the iPass SmartConnect link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the Provisioning tab automatic configuration.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your iPass SmartConnect Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to iPass SmartConnect. If the connection fails, ensure your iPass SmartConnect account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to iPass SmartConnect in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in iPass SmartConnect for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of the Attribute Mappings page. A table lists Microsoft Entra ID and iPass SmartConnect attributes and the matching precedence.](media/ipass-smartconnect-provisioning-tutorial/userattribute.png)
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Connector limitations

- iPass SmartConnect only accepts usernames that have their domains registered in the iPass SmartConnect admin console.