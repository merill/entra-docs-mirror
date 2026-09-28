---
layout: Conceptual
title: Configure Dropbox for Business for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/dropboxforbusiness-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Dropbox for Business.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 12a2bfc5-6fd3-18a9-d2b5-f9be57183c0e
document_version_independent_id: a380e6fb-6db3-c596-5d4e-d8a1060f706b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/dropboxforbusiness-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/dropboxforbusiness-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/dropboxforbusiness-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fbc1fda1-a1fb-e2bb-789e-a4cc14e2332c
---

# Configure Dropbox for Business for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Dropbox for Business and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Dropbox for Business.

Important

In the future, Microsoft and Dropbox are deprecating the old Dropbox integration. This was originally planned for 4/1/2021, but has been postponed indefinitely. However, to avoid disruption of service, we recommend migrating to the new SCIM 2.0 Dropbox integration which supports Groups. To migrate to the new Dropbox integration, add and configure a new instance of Dropbox for Provisioning in your Microsoft Entra tenant using the steps below. Once you have configured the new Dropbox integration, disable Provisioning on the old Dropbox integration to avoid Provisioning conflicts. For more detailed steps on migrating to the new Dropbox integration, see [Update to the newest Dropbox for Business application using Microsoft Entra ID](https://help.dropbox.com/installs-integrations/third-party/update-dropbox-azure-ad-connector) and [Connect Dropbox with Microsoft Entra ID](https://help.dropbox.com/integrations/microsoft-entra-id).

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Dropbox for Business tenant](https://www.dropbox.com/business/pricing)
- A user account in Dropbox for Business with Admin permissions.

## Add Dropbox for Business from the gallery

Before configuring Dropbox for Business for automatic user provisioning with Microsoft Entra ID, you need to add Dropbox for Business from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Dropbox for Business from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Dropbox for Business**, select **Dropbox for Business** in the search box.
4. Select **Dropbox for Business** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Screenshot of Dropbox for Business in the results list.](common/search-new-app.png)

## Assigning users to Dropbox for Business

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Dropbox for Business. Once decided, you can assign these users and/or groups to Dropbox for Business by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Dropbox for Business

- It's recommended that a single Microsoft Entra user is assigned to Dropbox for Business to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Dropbox for Business, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Configuring automatic user provisioning to Dropbox for Business

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Dropbox for Business based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Dropbox for Business, following the instructions provided in the [Dropbox for Business single sign-on article](dropboxforbusiness-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Dropbox for Business in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Dropbox for Business**.

    ![Screenshot of The Dropbox for Business link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Dropbox Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Dropbox. If the connection fails, ensure your Dropbox account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. On the **Sign-in to Dropbox for Business to link with Microsoft Entra ID** dialog, sign in to your Dropbox for Business tenant and verify your identity.

    ![Screenshot of Dropbox for Business sign-in.](media/dropboxforbusiness-provisioning-tutorial/dropbox01.png)
8. Select **Test Connection** to ensure Microsoft Entra ID can connect to Dropbox for Business. If the connection fails, ensure your Dropbox for Business account has Admin permissions and try again.

    ![Screenshot of Token.](common/provisioning-testconnection-oauth.png)
9. Select **Create** to create your configuration.
10. Select **Properties** on the **Overview** page.
11. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.
12. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
13. Select **Attribute Mapping** in the left panel and select **users**.
14. Review the user attributes that are synchronized from Microsoft Entra ID to Dropbox in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of Dropbox User Attributes.](media/dropboxforbusiness-provisioning-tutorial/dropbox-user-attributes.png)
15. Select **Attribute Mapping** in the left panel and select **Groups**.
16. Review the group attributes that are synchronized from Microsoft Entra ID to Dropbox in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Dropbox for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of Dropbox Group Attributes.](media/dropboxforbusiness-provisioning-tutorial/dropbox-group-attributes.png)
17. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
18. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
19. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Connector Limitations

- Dropbox doesn't support suspending invited users. If an invited user is suspended, that user is deleted.