---
layout: Conceptual
title: Configure Dynamic Signal for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/dynamic-signal-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Dynamic Signal.
ms.topic: how-to
ms.date: 2026-04-22T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 54155194-743b-03b7-3367-6bc6807df52b
document_version_independent_id: 5f97ce71-8908-8dfe-3cd1-5127dba8bb6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/dynamic-signal-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/dynamic-signal-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/dynamic-signal-provisioning-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: aa56c365-f7d1-3106-cbbf-f0860df2565d
---

# Configure Dynamic Signal for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Dynamic Signal and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Dynamic Signal.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Dynamic Signal tenant](https://dynamicsignal.com/)
- A user account in Dynamic Signal with Admin permissions.

## Step 1: Add Dynamic Signal from the gallery

Before configuring Dynamic Signal for automatic user provisioning with Microsoft Entra ID, you need to add Dynamic Signal from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Dynamic Signal from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Dynamic Signal**, select **Dynamic Signal** in the search box.
4. Select **Dynamic Signal** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

    ![Screenshot of Dynamic Signal in the results list.](common/search-new-app.png)

## Step 2: Assign users to Dynamic Signal

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Dynamic Signal. Once decided, you can assign these users and/or groups to Dynamic Signal by following the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to Dynamic Signal

- It's recommended that a single Microsoft Entra user is assigned to Dynamic Signal to test the automatic user provisioning configuration. More users and/or groups may be assigned later.
- When assigning a user to Dynamic Signal, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 3: Configure automatic user provisioning to Dynamic Signal

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Dynamic Signal based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Dynamic Signal, following the instructions provided in the [Dynamic Signal single sign-on article](dynamicsignal-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### Configure automatic user provisioning for Dynamic Signal in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Dynamic Signal**.

    ![Screenshot of Dynamic Signal link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the New configuration option on the Provisioning page.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, input the **Tenant URL** and **Secret Token** of your Dynamic Signal's account. To find these values, follow the next two steps.
7. In the Dynamic Signal admin console, navigate to **Admin &gt; Advanced &gt; API**.

    ![Screenshot of the Dynamic Signal admin console. Advanced is highlighted in the Admin menu. The Advanced menu is also visible, with A P I highlighted.](media/dynamic-signal-provisioning-tutorial/secret-token-1.png)

    Copy the **SCIM API URL** to **Tenant URL**. Select **Generate New Token** to generate a **Bearer Token** and copy the value to **Secret Token**.

    ![Screenshot of the Tokens page, with S C I M A P I U R L, Generate new token, and Bearer token highlighted, and a placeholder in the Bearer token box.](media/dynamic-signal-provisioning-tutorial/secret-token-2.png)
8. After you enter the tenant URL and secret token, select **Test Connection** to ensure Microsoft Entra ID can connect to Dynamic Signal. If the connection fails, ensure your Dynamic Signal account has Admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
9. Select **Create** to create your configuration.
10. Select **Properties** on the **Overview** page.
11. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
12. Select **Attribute Mapping** in the left panel and select **users**.
13. Review the user attributes that are synchronized from Microsoft Entra ID to Dynamic Signal in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Dynamic Signal for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of the Dynamic Signal User Attributes.](media/dynamic-signal-provisioning-tutorial/user-mapping-attributes.png)
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 4: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector Limitations

- Dynamic Signal doesn't support permanent user deletes from Microsoft Entra ID. To delete a user permanently in Dynamic Signal, the operation has to be made through the Dynamic Signal admin console UI.
- Dynamic Signal doesn't currently support groups.