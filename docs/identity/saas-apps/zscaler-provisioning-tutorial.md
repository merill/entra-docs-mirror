---
layout: Conceptual
title: Configure Zscaler ZNet for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Zscaler ZNet.
ms.topic: how-to
ms.date: 2026-03-30T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 82889a73-9f84-9d77-94d6-47cb4c504773
document_version_independent_id: 6f0cfdbc-9aba-d5af-61d1-79e7f72084a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b1b3616b-a84b-fe61-8c61-7872ab0c72b4
---

# Configure Zscaler ZNet for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Zscaler ZNet and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Zscaler ZNet.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Zscaler ZNet tenant
- A user account in Zscaler ZNet with Admin permissions

Note

The Microsoft Entra provisioning integration relies on the Zscaler ZNet SCIM API, which is available to Zscaler ZNet developers for accounts with the Enterprise package.

## Step 1: Add Zscaler ZNet from the gallery

Before configuring Zscaler ZNet for automatic user provisioning with Microsoft Entra ID, you need to add Zscaler ZNet from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Zscaler ZNet from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the search box, type **Zscaler ZNet**, select **Zscaler ZNet** from result panel then select **Add** button to add the application.

    ![Screenshot of Zscaler ZNet in the results list.](common/search-new-app.png)

## Step 2: Assign users to Zscaler ZNet

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Zscaler ZNet. Once decided, you can assign these users and/or groups to Zscaler ZNet by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Zscaler ZNet

- It's recommended that a single Microsoft Entra user is assigned to Zscaler ZNet to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Zscaler ZNet, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 3: Configure automatic user provisioning to Zscaler ZNet

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Zscaler ZNet based on user and/or group assignments in Microsoft Entra ID.

Note

Open a [support ticket](https://help.zscaler.com/) to create a domain on Zscaler ZNet.

Tip

You may also choose to enable SAML-based single sign-on for Zscaler ZNet, following the instructions provided in the [Zscaler ZNet single sign-on article](zscaler-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

Note

When users and groups are provisioned or de-provisioned we recommend to periodically restart provisioning to ensure that group memberships are properly updated. Doing a restart will force our service to re-evaluate all the groups and update the memberships. Please be aware that the restart can take time if you're syncing all users and groups in your tenant or have assigned large groups with 50K+ members.

### Configure automatic user provisioning for Zscaler ZNet in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler ZNet**.
3. Select the **Provisioning** tab.

    ![Screenshot of the Zscaler ZNet - Provisioning Enterprise Application sidebar with the Provisioning option highlighted.](media/zscaler-provisioning-tutorial/provisioning-tab.png)
4. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
5. Under the **Admin Credentials** section, enter the **Tenant URL** and **Secret Token** of your Zscaler ZNet Beta account as described later in this article.
6. To obtain the **Tenant URL** and **Secret Token**, navigate to **Administration &gt; Authentication Settings** in the Zscaler ZNet portal user interface and select **SAML** under **Authentication Type**.

    ![Screenshot of the Authentication Settings page.](media/zscaler-provisioning-tutorial/secret-token-1.png)
7. Select **Configure SAML** to open **Configuration SAML** options.

    ![Screenshot of the Configure SAML dialog box with the Base URL and Bearer Token text boxes called out.](media/zscaler-provisioning-tutorial/secret-token-2.png)
8. Select **Enable SCIM-Based Provisioning** to retrieve **Base URL** and **Bearer Token**, then save the settings. Copy the **Base URL** to **Tenant URL**, and **Bearer Token** to **Secret Token**.
9. Upon populating the fields shown in Step 5, select **Test Connection** to ensure Microsoft Entra ID can connect to Zscaler ZNet. If the connection fails, ensure your Zscaler ZNet account has Admin permissions and try again.

    ![Screenshot of Token.](common/provisioning-testconnection-tenanturltoken.png)
10. Select **Create** to create your configuration.
11. Select **Properties** on the **Overview** page.
12. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
13. Select **Attribute Mapping** in the left panel and select **users**.
14. Review the user attributes that are synchronized from Microsoft Entra ID to Zscaler ZNet in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Zscaler ZNet for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Zscaler ZNet |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | externalId | String |  | ✓ |
    | active | Boolean |  | ✓ |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | displayName | String |  | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  | ✓ |
15. Select **Groups**.
16. Review the group attributes that are synchronized from Microsoft Entra ID to Zscaler ZNet in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Zscaler ZNet for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Zscaler ZNet |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
    | externalId | String |  | ✓ |
17. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
18. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
19. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 4: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.