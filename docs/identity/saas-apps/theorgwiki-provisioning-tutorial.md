---
layout: Conceptual
title: Configure TheOrgWiki for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/theorgwiki-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to TheOrgWiki.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 41043954-9f9d-25a5-e29e-a0683a216ad0
document_version_independent_id: 95dfc982-08ce-8d6c-0c92-e0055186ea2b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/theorgwiki-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/theorgwiki-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/theorgwiki-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 35a4380d-2442-8a15-ee5a-57ad2e770d6b
---

# Configure TheOrgWiki for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in TheOrgWiki and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to TheOrgWiki.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in TheOrgWiki.
- Remove users in TheOrgWiki when they don't require access anymore.
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [An OrgWiki tenant](https://www.theorgwiki.com/welcome/).
- A user account in TheOrgWiki with Admin permissions.

## Step 1: Assign users to TheOrgWiki

Microsoft Entra ID uses a concept called assignments to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to TheOrgWiki. Once decided, you can assign these users and/or groups to TheOrgWiki by following the instructions [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to TheOrgWiki

- It's recommended that a single Microsoft Entra user is assigned to TheOrgWiki to test the automatic user provisioning configuration. More users and/or groups may be assigned later.
- When assigning a user to TheOrgWiki, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 2: Set up TheOrgWiki for provisioning

Before configuring TheOrgWiki for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on TheOrgWiki.

1. Sign in to your [TheOrgWiki Admin Console](https://www.theorgwiki.com/login/). Select **Admin Console**.

    ![Screenshot of Org Wiki with the user avatar and the Admin Console called out.](media/theorgwiki-provisioning-tutorial/login.png)
2. In Admin Console, Select **Settings tab**.

    ![Screenshot of the The Org Wiki Admin Console with the Settings tab called out.](media/theorgwiki-provisioning-tutorial/settings.png)
3. Navigate to **Service Accounts**.

    ![Screenshot of the Service Accounts page in the Org Wiki Admin Console.](media/theorgwiki-provisioning-tutorial/serviceaccount.png)
4. Select **+Service Account**. Under **Service Account Type**, select **Token Based**. Select **Save**.

    ![Screenshot of the New Service Account dialog box with the Service Account Type, Token Based, and Save options called out.](media/theorgwiki-provisioning-tutorial/auth.png)
5. Copy the **Active Tokens**. This value is entered in the Secret Token field in the Provisioning tab of your TheOrgWiki application.

    ![Screenshot of the Manage Tokens for S C I M provisioning dialog box.](media/theorgwiki-provisioning-tutorial/token.png)

## Step 3: Add TheOrgWiki from the gallery

To configure TheOrgWiki for automatic user provisioning with Microsoft Entra ID, you need to add TheOrgWiki from the Microsoft Entra application gallery to your list of managed SaaS applications.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TheOrgWiki**, select **TheOrgWiki** in the results panel.

    ![Screenshot of TheOrgWiki in the results list.](common/search-new-app.png)
4. Select the **Sign-up for TheOrgWiki** button which will redirect you to TheOrgWiki's login page.

    ![Screenshot of The Org Wiki login page with the URL called out.](media/theorgwiki-provisioning-tutorial/image00.png)
5. In the top right-hand corner, select **Login**.

    ![Screenshot of the upper-right corner of the login page with the Log In option called out.](media/theorgwiki-provisioning-tutorial/image02.png)
6. As TheOrgWiki is an OpenIDConnect app, choose to log in to OrgWiki using your Microsoft work account.

    ![Screenshot of the The Org Wiki sign in page with the Sign in with Microsoft option called out.](media/theorgwiki-provisioning-tutorial/image03.png)
7. After a successful authentication, the application is automatically added to your tenant and you'll be redirected to your TheOrgWiki account.

    ![Screenshot of OrgWiki Add SCIM.](media/theorgwiki-provisioning-tutorial/image04.png)

## Step 4: Configure automatic user provisioning to TheOrgWiki

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TheOrgWiki based on user and/or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for TheOrgWiki in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **TheOrgWiki**.

    ![Screenshot of OrgWiki link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, enter `https://<TheOrgWiki Subdomain 		value>.theorgwiki.com/api/v2/scim/v2/` in **Tenant URL**.

    Example: `https://test1.theorgwiki.com/api/v2/scim/v2/`

    Note

    The **Subdomain Value** can only be set during the initial sign-up process for TheOrgWiki.
7. Enter the token value in **Secret Token** field, that you retrieved earlier from TheOrgWiki. Select **Test Connection** to ensure Microsoft Entra ID can connect to TheOrgWiki. If the connection fails, ensure your TheOrgWiki account has Admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
8. Select **Create** to create your configuration.
9. Select **Properties** on the **Overview** page.
10. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to TheOrgWiki in the **Attribute- Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in TheOrgWiki for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of TheOrgWiki User Attributes.](media/theorgwiki-provisioning-tutorial/userattribute.png).
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.