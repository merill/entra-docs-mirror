---
layout: Conceptual
title: Configure Keeper Password Manager & Digital Vault for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/keeper-password-manager-digitalvault-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Keeper Password Manager & Digital Vault.
ms.topic: how-to
ms.date: 2026-04-08T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b2d7bf6f-dcb9-1587-f0be-ca4b52157662
document_version_independent_id: 51a7ba4f-6102-825b-0909-a3adfbfba053
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/keeper-password-manager-digitalvault-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/keeper-password-manager-digitalvault-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/keeper-password-manager-digitalvault-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 27ff816e-884a-a076-1cbc-f8384027ece0
---

# Configure Keeper Password Manager & Digital Vault for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Keeper Password Manager & Digital Vault and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Keeper Password Manager & Digital Vault.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
        - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
        - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
        - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- [A Keeper Password Manager & Digital Vault tenant](https://keepersecurity.com/pricing.html?t=e)
- A user account in Keeper Password Manager & Digital Vault with Admin permissions.

## Add Keeper Password Manager & Digital Vault from the gallery

Before configuring Keeper Password Manager & Digital Vault for automatic user provisioning with Microsoft Entra ID, you need to add Keeper Password Manager & Digital Vault from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Keeper Password Manager & Digital Vault from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Keeper Password Manager & Digital Vault**, select **Keeper Password Manager & Digital Vault** in the search box.
4. Select **Keeper Password Manager & Digital Vault** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Keeper Password Manager &amp; Digital Vault in the results list](common/search-new-app.png)

## Assigning users to Keeper Password Manager & Digital Vault

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Keeper Password Manager & Digital Vault. Once decided, you can assign these users and/or groups to Keeper Password Manager & Digital Vault by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Keeper Password Manager & Digital Vault

- It's recommended that a single Microsoft Entra user is assigned to Keeper Password Manager & Digital Vault to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Keeper Password Manager & Digital Vault, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Configuring automatic user provisioning to Keeper Password Manager & Digital Vault

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Keeper Password Manager & Digital Vault based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Keeper Password Manager & Digital Vault, following the instructions provided in the [Keeper Password Manager & Digital Vault single sign-on article](keeperpasswordmanager-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Keeper Password Manager & Digital Vault in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Keeper Password Manager & Digital Vault**.

    ![The Keeper Password Manager &amp; Digital Vault link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Keeper Password Manager & Digital Vault Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Keeper Password Manager & Digital Vault. If the connection fails, ensure your Keeper Password Manager & Digital Vault account has the required admin permissions and try again.
7. Sign in to your [Keeper Admin Console](https://keepersecurity.com/console/#login). Select **Admin** and select an existing node or create a new one. Navigate to the **Provisioning** tab and select **Add Method**.

    ![Keeper Admin Console](media/keeper-password-manager-digitalvault-provisioning-tutorial/keeper-admin-console.png)

    Select **SCIM (System for Cross-Domain Identity Management**.

    ![Keeper Add SCIM](media/keeper-password-manager-digitalvault-provisioning-tutorial/keeper-add-scim.png)

    Select **Create Provisioning Token**.

    ![Keeper Create Endpoint](media/keeper-password-manager-digitalvault-provisioning-tutorial/keeper-create-endpoint.png)

    Copy the values for **URL** and **Token** and paste them into **Tenant URL** and **Secret Token** in Microsoft Entra ID. Select **Save** to complete the provisioning setup on Keeper.

    ![Keeper Create Token](media/keeper-password-manager-digitalvault-provisioning-tutorial/keeper-create-token.png)
8. Select **Create** to create your configuration.
9. Select **Properties** on the **Overview** page.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to Keeper Password Manager & Digital Vault in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Keeper Password Manager & Digital Vault for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Keeper Password Manager & Digital Vault API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    ![Keeper User Attributes](media/keeper-password-manager-digitalvault-provisioning-tutorial/keeper-user-attributes.png)
13. Review the group attributes that are synchronized from Microsoft Entra ID to Keeper Password Manager & Digital Vault in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Keeper Password Manager & Digital Vault for update operations. Select the **Save** button to commit any changes.

    ![Keeper Group Attributes](media/keeper-password-manager-digitalvault-provisioning-tutorial/keeper-group-attributes.png)
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Connector Limitations

- Keeper Password Manager & Digital Vault requires **emails** and **userName** to have the same source value, as any updates to either attributes will modify the other value.
- Keeper Password Manager & Digital Vault doesn't support user deletes, only disable. Disabled users appear as locked in the Keeper Admin Console UI.