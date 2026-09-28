---
layout: Conceptual
title: Configure Jive for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/jive-provisioning-tutorial
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
description: Learn the steps you need to perform in Jive and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to Jive.
ms.topic: how-to
ms.date: 2026-04-10T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 36984817-633d-671a-408c-ab56aa81f640
document_version_independent_id: 65f66ddc-7bfa-46bd-2fab-7d4828acab6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/jive-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/jive-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/jive-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 03c0c8c4-d79e-8666-ae4e-d1c1a69ef647
---

# Configure Jive for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show you the steps you need to perform in Jive and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to Jive.

## Prerequisites

The scenario outlined in this article assumes that you already have the following items:

- A Microsoft Entra tenant.
- A Jive single-sign on enabled subscription.
- A user account in Jive with Team Admin permissions.

## Assigning users to Jive

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID is synchronized.

Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Microsoft Entra ID represent the users who need access to your Jive app. Once decided, you can assign these users to your Jive app by following the instructions here:

[Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Jive

- It's recommended that a single Microsoft Entra user be assigned to Jive to test the provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Jive, you must select a valid user role. The "Default Access" role doesn't work for provisioning.

## Enable User Provisioning

This section guides you through connecting your Microsoft Entra ID to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Jive, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.

### To configure user account provisioning:

The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive. As part of this procedure, you're required to provide a user security token you need to request from Jive.com.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. If you have already configured Jive for single sign-on, search for your instance of Jive using the search field. Otherwise, select **Add** and search for **Jive** in the application gallery. Select Jive from the search results, and add it to your list of applications.
4. Select your instance of Jive, then select the **Provisioning** tab.
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/provisioning-automatic.png)
6. In the **Tenant URL** field, enter your Jive Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Jive. If the connection fails, ensure your Jive account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. In the **Attribute Mappings** section, review the user attributes that are synchronized from Microsoft Entra ID to Jive. The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations. Select the Save button to commit any changes.
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).