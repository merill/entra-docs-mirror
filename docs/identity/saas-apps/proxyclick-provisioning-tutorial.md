---
layout: Conceptual
title: Configure Proxyclick for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/proxyclick-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Proxyclick.
ms.topic: how-to
ms.date: 2026-03-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8d302a17-4890-7d2c-d898-27915f5a0265
document_version_independent_id: e0d5cd30-0c1a-9bbe-8472-a3982357ed5f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/proxyclick-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/proxyclick-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/proxyclick-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2d4fd84b-23ff-dfde-7b80-458684993b8e
---

# Configure Proxyclick for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Proxyclick and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Proxyclick.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Proxyclick tenant](https://www.proxyclick.com/pricing)
- A user account in Proxyclick with Admin permissions.

## Add Proxyclick from the gallery

Before configuring Proxyclick for automatic user provisioning with Microsoft Entra ID, you need to add Proxyclick from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Proxyclick from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Proxyclick**, select **Proxyclick** in the search box.
4. Select **Proxyclick** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

    ![Diagram that shows Proxyclick in the results list.](common/search-new-app.png)

## Assigning users to Proxyclick

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Proxyclick. Once decided, you can assign these users and/or groups to Proxyclick by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Proxyclick

- It's recommended that a single Microsoft Entra user is assigned to Proxyclick to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Proxyclick, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Configure automatic user provisioning to Proxyclick

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Proxyclick based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Proxyclick, following the instructions provided in the [Proxyclick single sign-on article](proxyclick-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Proxyclick in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Diagram that shows Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Proxyclick**.

    ![Diagram that shows the Proxyclick link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. To retrieve the **Tenant URL** and **Secret Token** of your Proxyclick account, follow the steps mentioned later in the document.
7. Sign in to your [Proxyclick Admin Console](https://app.proxyclick.com/login//?destination=%2Fdefault). Navigate to **Settings** &gt; **Integrations** &gt; **Browse Marketplace**.

    ![Diagram that shows Proxyclick Settings.](media/proxyclick-provisioning-tutorial/proxyclick09.png)

    ![Diagram that shows Proxyclick Integrations.](media/proxyclick-provisioning-tutorial/proxyclick01.png)

    ![Diagram that shows Proxyclick Marketplace.](media/proxyclick-provisioning-tutorial/proxyclick02.png)

    Select **Microsoft Entra ID**. Select **Install now**.

    ![Diagram that shows Proxyclick Microsoft Entra ID.](media/proxyclick-provisioning-tutorial/proxyclick03.png)

    ![Diagram that shows Proxyclick Install.](media/proxyclick-provisioning-tutorial/proxyclick04.png)

    Select **User Provisioning** and select **Start integration**.

    ![Diagram that shows Proxyclick User Provisioning.](media/proxyclick-provisioning-tutorial/proxyclick05.png)

    The appropriate settings configuration UI should now show up under **Settings** &gt; **Integrations**. Select **Settings** under **Microsoft Entra ID (User Provisioning)**.

    ![Diagram that shows Proxyclick Create.](media/proxyclick-provisioning-tutorial/proxyclick06.png)

    You can find the **Tenant URL** and **Secret Token** here.

    ![Diagram that shows Proxyclick Create Token.](media/proxyclick-provisioning-tutorial/proxyclick07.png)
8. Upon populating the fields shown in Step 5, select **Test Connection** to ensure Microsoft Entra ID can connect to Proxyclick. If the connection fails, ensure your Proxyclick account has Admin permissions and try again.

    ![Diagram that shows Token.](common/provisioning-testconnection-tenanturltoken.png)
9. Select **Create** to create your configuration.
10. Select **Properties** on the **Overview** page.
11. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
12. Select **Attribute Mapping** in the left panel and select **users**.
13. Review the user attributes that are synchronized from Microsoft Entra ID to Proxyclick in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Proxyclick for update operations. Select the **Save** button to commit any changes.

    ![Diagram that shows Proxyclick User Attributes.](media/proxyclick-provisioning-tutorial/proxyclick-user-attribute.png)
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector limitations

- Proxyclick requires **emails** and **userName** to have the same source value. Any updates to either attributes will modify the other value.
- Proxyclick doesn't support provisioning for groups.