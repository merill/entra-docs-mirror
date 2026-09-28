---
layout: Conceptual
title: Configure Zscaler Three for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-three-provisioning-tutorial
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
description: In this article,  you learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Zscaler Three.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8e954fc3-b0b0-d889-233d-2382ebb4863b
document_version_independent_id: 155039dc-6b45-230e-0a80-24450ae9e963
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-three-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-three-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-three-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 254aa774-36e1-ab2c-b282-ea0c70d7c152
---

# Configure Zscaler Three for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure Microsoft Entra ID to automatically provision and deprovision users and/or groups to Zscaler Three.

Note

This article describes a connector that's built on the Microsoft Entra user provisioning service. For important details on what this service does and how it works, and answers to frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Zscaler Three is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

To complete the steps outlined in this article, you need the following:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- A Zscaler Three tenant.
- A user account in Zscaler Three with admin permissions.

Note

The Microsoft Entra provisioning integration relies on the Zscaler ZSCloud SCIM API, which is available for Enterprise accounts.

## Step 1: Add Zscaler Three from the gallery

Before you configure Zscaler Three for automatic user provisioning with Microsoft Entra ID, you need to add Zscaler Three from the Microsoft Entra application gallery to your list of managed SaaS applications.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler Three**.
3. Select **Zscaler Three** in the results and then select **Add**.

![Results list](common/search-new-app.png)

## Step 2: Assign users to Zscaler Three

Microsoft Entra users need to be assigned access to selected apps before they can use them. In the context of automatic user provisioning, only the users or groups that are assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Zscaler Three. After you decide that, you can assign these users and groups to Zscaler Three by following the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to Zscaler Three

- We recommended that you first assign a single Microsoft Entra user to Zscaler Three to test the automatic user provisioning configuration. You can assign more users and groups later.
- When you assign a user to Zscaler Three, you need to select any valid application-specific role (if available) in the assignment dialog box. Users with the **Default Access** role are excluded from provisioning.

## Step 3: Set up automatic user provisioning

This section guides you through the steps for configuring the Microsoft Entra provisioning service to create, update, and disable users and groups in Zscaler Three based on user and group assignments in Microsoft Entra ID.

Tip

You might also want to enable SAML-based single sign-on for Zscaler Three. If you do, follow the instructions in the [Zscaler Three single sign-on article](zscaler-three-tutorial). Single sign-on can be configured independently of automatic user provisioning, but the two features complement each other.

Note

When users and groups are provisioned or de-provisioned we recommend to periodically restart provisioning to ensure that group memberships are properly updated. Doing a restart will force our service to re-evaluate all the groups and update the memberships.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler Three**.

    ![Screenshot of Enterprise applications.](common/enterprise-applications.png)
3. In the applications list, select **Zscaler Three**:

    ![Screenshot of Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab:

    ![Screenshot of Zscaler Three Provisioning.](media/zscaler-three-provisioning-tutorial/provisioning-tab.png)
5. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
6. In the **Admin Credentials** section, enter the **Tenant URL** and **Secret Token** of your Zscaler Three account, as described in the next step.
7. To get the **Tenant URL** and **Secret Token**, go to **Administration** &gt; **Authentication Settings** in the Zscaler Three portal and select **SAML** under **Authentication Type**:

    ![Screenshot of Zscaler Three Authentication Settings.](media/zscaler-three-provisioning-tutorial/secret-token-1.png)
8. Select **Configure SAML** to open the **Configure SAML** window:

    ![Screenshot of Configure SAML window.](media/zscaler-three-provisioning-tutorial/secret-token-2.png)
9. Select **Enable SCIM-Based Provisioning** and copy the **Base URL** and **Bearer Token**, and then save the settings. In the Azure portal, paste the **Base URL** into the **Tenant URL** box and the **Bearer Token** into the **Secret Token** box.
10. After you enter the values in the **Tenant URL** and **Secret Token** boxes, select **Test Connection** to make sure Microsoft Entra ID can connect to Zscaler Three. If the connection fails, make sure your Zscaler Three account has admin permissions and try again.

    ![Screenshot of Token.](common/provisioning-testconnection-tenanturltoken.png)
11. Select **Create** to create your configuration.
12. Select **Properties** on the **Overview** page.
13. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
14. Select **Attribute Mapping** in the left panel and select **users**.
15. Review the user attributes that are synchronized from Microsoft Entra ID to Zscaler Three in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the user accounts in Zscaler Three for update operations. Select **Save** to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Zscaler Three |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | externalId | String |  | ✓ |
    | active | Boolean |  | ✓ |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | displayName | String |  | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  | ✓ |
16. Select **Groups**.
17. Review the group attributes that are synchronized from Microsoft Entra ID to Zscaler Three in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the groups in Zscaler Three for update operations. Select **Save** to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Zscaler Three |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
    | externalId | String |  | ✓ |
18. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
19. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
20. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 4: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.