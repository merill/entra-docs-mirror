---
layout: Conceptual
title: Configure RFPIO for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/rfpio-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to RFPIO.
ms.topic: how-to
ms.date: 2026-04-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f2a2c4b5-6746-fa0b-ff20-c924bea1c91d
document_version_independent_id: e17db01e-db5e-7fec-500e-b57e1352e101
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/rfpio-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/rfpio-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/rfpio-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 63367e22-8726-f53f-2ed3-0ca797cbf4e0
---

# Configure RFPIO for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in RFPIO and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to RFPIO.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- [A RFPIO tenant](https://www.rfpio.com/product/).
- A user account in RFPIO with Admin permissions.

## Assigning users to RFPIO

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to RFPIO. Once decided, you can assign these users and/or groups to RFPIO by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to RFPIO

- It's recommended that a single Microsoft Entra user is assigned to RFPIO to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to RFPIO, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up RFPIO for provisioning

Before configuring RFPIO for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on RFPIO.

1. Sign in to your RFPIO Admin Console. On the bottom left of the admin console, select **Tenant**.

    ![Screenshot of RFPIO Admin Console](media/rfpio-provisioning-tutorial/aadtest0.png)
2. Select **Organization Settings**.

    ![Screenshot of RFPIO Admin](media/rfpio-provisioning-tutorial/aadtest.png)
3. Navigate to **USER MANAGEMENT** &gt; **SECURITY** &gt; **SCIM**.

    ![Screenshot of RFPIO Add SCIM](media/rfpio-provisioning-tutorial/scim.png)
4. Ensure that **Auto User Provisioning** is enabled. Select **GENERATE SCIM API TOKEN**.

    ![Screenshot of the S C I M section with the GENERATE S C I M A P I TOKEN option called out.](media/rfpio-provisioning-tutorial/generate.png)
5. Save the **SCIM API Token** as this token isn't displayed again for security purpose. This value is entered in the **Secret Token** field in the Provisioning tab of your RFPIO application.

    ![Screenshot of the S C I M section with the Warning dialog box that appears after you select SUBMIT.](media/rfpio-provisioning-tutorial/auth.png)

## Add RFPIO from the gallery

To configure RFPIO for automatic user provisioning with Microsoft Entra ID, you need to add RFPIO from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add RFPIO from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **RFPIO**, select **RFPIO** in the results panel, and then select the **Add** button to add the application.

    ![Screenshot of RFPIO in the results list](common/search-new-app.png)

## Configuring automatic user provisioning to RFPIO

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in RFPIO based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for RFPIO, following the instructions provided in the [RFPIO Single sign-on article](rfpio-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for RFPIO in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **RFPIO**.

    ![Screenshot of the RFPIO link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of the Provisioning Mode dropdown list with the Automatic option called out.](common/provisioning-automatic.png)
6. In the **Tenant URL** field, input your RFPIO Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to RFPIO. If the connection fails, ensure your RFPIO account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page showing notification and deletion settings.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select users.
11. Review the user attributes that are synchronized from Microsoft Entra ID to RFPIO in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in RFPIO for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of RFPIO User Attributes](media/rfpio-provisioning-tutorial/userattributes.png)
12. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Connector Limitations

- RFPIO doesn't support groups provisioning currently.