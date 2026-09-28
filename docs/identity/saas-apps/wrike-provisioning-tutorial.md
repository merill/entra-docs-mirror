---
layout: Conceptual
title: Configure Wrike for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/wrike-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Wrike.
ms.topic: how-to
ms.date: 2026-04-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2402b5b1-0dbc-1f31-ec91-52c5fed7c7ec
document_version_independent_id: 0465486b-bab4-e329-3afd-b76f806729bd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/wrike-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/wrike-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/wrike-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 69fc6ce0-2d89-a10d-b96d-9d009a971544
---

# Configure Wrike for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps you perform in Wrike and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and deprovision users or groups to Wrike.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to software-as-a-service (SaaS) applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
        - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
        - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
        - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- [A Wrike tenant](https://www.wrike.com/price/)
- A user account in Wrike with admin permissions

## Step 1: Assign users to Wrike

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users or groups that were assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, decide which users or groups in Microsoft Entra ID need access to Wrike. Then assign these users or groups to Wrike by following the instructions here: [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to Wrike

- We recommend that you assign a single Microsoft Entra user to Wrike to test the automatic user provisioning configuration. More users or groups can be assigned later.
- When you assign a user to Wrike, you must select any valid application-specific role (if available) in the assignment dialog box. Users with the Default Access role are excluded from provisioning.

## Step 2: Set up Wrike for provisioning

Before you configure Wrike for automatic user provisioning with Microsoft Entra ID, you need to enable System for Cross-domain Identity Management (SCIM) provisioning on Wrike.

1. Sign in to your [Wrike admin console](https://www.Wrike.com/login/). Go to your Tenant ID. Select **Apps & Integrations**.

    ![Screenshot of Apps &amp; Integrations.](media/wrike-provisioning-tutorial/admin.png)
2. Go to **Microsoft Entra ID** and select it.
3. Select SCIM. Copy the **Base URL**.

    ![Screenshot of Base URL.](media/wrike-provisioning-tutorial/wrike-tenanturl.png)
4. Select **API** &gt; **Azure SCIM**.

    ![Screenshot of Azure SCIM.](media/wrike-provisioning-tutorial/wrike-add-scim.png)
5. A pop-up opens. Enter the same password that you created earlier to create an account.

    ![Screenshot of Wrike Create token.](media/wrike-provisioning-tutorial/password.png)
6. Copy the **Secret Token**, and paste it in Microsoft Entra ID. Select **Save** to finish the provisioning setup on Wrike.

    ![Screenshot of Permanent access token.](media/wrike-provisioning-tutorial/wrike-create-token.png)

## Step 3: Add Wrike from the gallery

Before you configure Wrike for automatic user provisioning with Microsoft Entra ID, add Wrike from the Microsoft Entra application gallery to your list of managed SaaS applications.

To add Wrike from the Microsoft Entra application gallery, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.Wrike\*\*, select **Wrike** in the results panel, and then select **Add** to add the application.

    ![Screenshot of Wrike in the results list.](common/search-new-app.png)

## Step 4: Configure automatic user provisioning to Wrike

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users or groups in Wrike based on user or group assignments in Microsoft Entra ID.

Tip

To enable SAML-based single sign-on for Wrike, follow the instructions in the [Wrike single sign-on article](wrike-tutorial). Single sign-on can be configured independently of automatic user provisioning, although these two features complement each other.

### Configure automatic user provisioning for Wrike in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Wrike**.

    ![Screenshot of the Wrike link in the Applications list.](common/all-applications.png)
3. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
4. Select **+ New configuration**.

    ![Screenshot of new configuration.](common/application-provisioning.png)
5. Under the Admin Credentials section, enter the **Base URL** and **Permanent access token** values retrieved earlier in **Tenant URL** and **Secret Token**, respectively. Select **Test Connection** to ensure that Microsoft Entra ID can connect to Wrike. If the connection fails, make sure that your Wrike account has admin permissions and try again.

    ![Screenshot of Tenant URL + token.](common/provisioning-testconnection-tenanturltoken.png)
6. Select **Create** to create your configuration.
7. Select **Properties** on the **Overview** page.
8. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
9. Select **Attribute Mapping** in the left panel and select **users**.
10. Review the user attributes that are synchronized from Microsoft Entra ID to Wrike in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the user accounts in Wrike for update operations. Select **Save** to commit any changes.

    ![Screenshot of Wrike user attributes.](media/wrike-provisioning-tutorial/wrike-user-attributes.png)
11. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
12. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
13. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.