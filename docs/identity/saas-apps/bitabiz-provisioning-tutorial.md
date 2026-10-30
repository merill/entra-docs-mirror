---
layout: Conceptual
title: Configure BitaBIZ for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bitabiz-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to BitaBIZ.
ms.topic: how-to
ms.date: 2026-02-27T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4a240dfe-6848-7524-3043-6ab12413c736
document_version_independent_id: 25c14a7c-7276-bab9-012f-ae1b3cc0940b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bitabiz-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bitabiz-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bitabiz-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 969f78f1-2530-019e-9b0b-1fa695a0daea
---

# Configure BitaBIZ for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in BitaBIZ and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to BitaBIZ.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- [A BitaBIZ tenant](https://bitabiz.dk/en/price/).
- A user account in BitaBIZ with Admin permissions.

## Assigning users to BitaBIZ

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to BitaBIZ. Once decided, you can assign these users and/or groups to BitaBIZ by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to BitaBIZ

- It's recommended that a single Microsoft Entra user is assigned to BitaBIZ to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to BitaBIZ, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Setup BitaBIZ for provisioning

Before configuring BitaBIZ for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on BitaBIZ.

1. Sign in to your [BitaBIZ Admin Console](https://www.bitabiz.com/login?lang=en). Select **SETUP ADMIN**.

    ![Screenshot of the BitaBIZ Admin Console, with Setup admin highlighted.](media/bitabiz-provisioning-tutorial/setup-admin.png)
2. Navigate to **INTEGRATION**.

    ![Screenshot of the BitaBIZ Admin Console, with Integration highlighted.](media/bitabiz-provisioning-tutorial/integration.png)
3. Navigate to **Microsoft Entra provisioning**. Select **Enabled** in Automatic user provisioning. Copy the values for **SCIM Provisioning endpoint URL** and **Bearer Token**. These values are entered in the Tenant URL and Secret Token fields in the Provisioning tab of your BitaBIZ application.

    ![BitaBIZ Add SCIM](media/bitabiz-provisioning-tutorial/authentication.png)

## Add BitaBIZ from the gallery

To configure BitaBIZ for automatic user provisioning with Microsoft Entra ID, you need to add BitaBIZ from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add BitaBIZ from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **BitaBIZ**, select **BitaBIZ** in the search box.
4. Select **BitaBIZ** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![BitaBIZ in the results list](common/search-new-app.png)

## Configuring automatic user provisioning to BitaBIZ

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in BitaBIZ based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for BitaBIZ, following the instructions provided in the [BitaBIZ Single sign-on article](bitabiz-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other

### To configure automatic user provisioning for BitaBIZ in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **BitaBIZ**.

    ![The BitaBIZ link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
6. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
7. In the **Tenant URL** field, input your BitaBIZ Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to BitaBIZ. If the connection fails, ensure your BitaBIZ account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
8. Select **Create** to create your configuration.
9. Select **Properties** in the **Overview** page.
10. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to BitaBIZ in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in BitaBIZ for update operations. Select the **Save** button to commit any changes.

    ![BitaBIZ User Attributes](media/bitabiz-provisioning-tutorial/user-attribute.png)
13. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Connector limitations

- BitaBIZ requires **userName**, **email**, **firstName** and **lastName** as mandatory attributes.
- BitaBIZ doesn't support hard deletes currently.