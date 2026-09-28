---
layout: Conceptual
title: Configure Miro for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/miro-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Miro.
ms.topic: how-to
ms.date: 2026-03-16T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3ba82fdc-29cc-0c65-04e1-17577f3305b7
document_version_independent_id: 316f75cb-4f53-c530-49eb-c4cb7cb15d00
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/miro-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/miro-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/miro-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bae8725a-f477-5ee9-8bfe-cc1f52538a6e
---

# Configure Miro for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Miro and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Miro.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Miro tenant](https://miro.com/pricing/)
- A user account in Miro with Admin permissions.

## Assigning users to Miro

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Miro. Once decided, you can assign these users and/or groups to Miro by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to Miro

- It's recommended that a single Microsoft Entra user is assigned to Miro to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Miro, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up Miro for provisioning

To retrieve the needed **Secret Token** contact [Miro Support Team](mailto:support@miro.com). This value is entered in the Secret Token field in the Provisioning tab of your Miro application.

## Add Miro from the gallery

Before configuring Miro for automatic user provisioning with Microsoft Entra ID, you need to add Miro from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Miro from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Miro** in the search box.
4. Select **Miro** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configuring automatic user provisioning to Miro

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Miro based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Miro, following the instructions provided in the [Miro Single sign-on article](miro-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

Note

To learn more about Miro's SCIM endpoint, refer [this](https://help.miro.com/hc/en-us/articles/360036777814).

### To configure automatic user provisioning for Miro in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Miro**.

    ![The Miro link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, input `https://miro.com/api/v1/scim` in **Tenant URL**. Input the **SCIM Authentication Token** value retrieved earlier in **Secret Token**. Select **Test Connection** to ensure Microsoft Entra ID can connect to Miro. If the connection fails, ensure your Miro account has Admin permissions and try again.

    ![Tenant URL + Token](common/provisioning-testconnection-tenanturltoken.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Miro in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Miro for update operations. Select the **Save** button to commit any changes.

    ![Miro User Attributes](media/miro-provisioning-tutorial/userattributes.png)
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Miro in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Miro for update operations. Select the **Save** button to commit any changes. Uncheck **Create** and **Delete** under **Target Object Actions** as Miro SCIM API doesn't support creating and deleting groups.

    ![Miro Group Attributes](media/miro-provisioning-tutorial/groupattributes.png)
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector limitations

- Miro's SCIM endpoint doesn't allow **Create** and **Delete** operations on groups. It only supports group **Update** operation.

## Troubleshooting Tips

- If experiencing errors with group creation, then it's required to disable it by unchecking **Create** and **Delete** under **Target Object Actions** as Miro SCIM API doesn't support creating and deleting groups.

    ![Miro Group Tips](media/miro-provisioning-tutorial/groupattributes.png)