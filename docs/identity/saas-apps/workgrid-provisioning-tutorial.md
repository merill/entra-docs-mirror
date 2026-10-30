---
layout: Conceptual
title: Configure Workgrid for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/workgrid-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Workgrid.
ms.topic: how-to
ms.date: 2026-04-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5840a47e-1cfb-dce6-e8f4-71cc3cbe73eb
document_version_independent_id: b1f99dc1-28c3-b69a-ae53-082ffbda8848
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/workgrid-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/workgrid-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/workgrid-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 87c73d0c-827d-5a85-af04-8d7ff5ce4d54
---

# Configure Workgrid for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Workgrid and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Workgrid.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Workgrid.
- Remove users in Workgrid when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Workgrid.
- Provision groups and group memberships in Workgrid.
- [Single sign-on](workgrid-tutorial) to Workgrid (recommended).
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [A Workgrid tenant](https://www.workgrid.com/)
- A user account in Workgrid with Admin permissions.

## Step 1: Assign users to Workgrid

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Workgrid. Once decided, you can assign these users and/or groups to Workgrid by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Workgrid

- It's recommended that a single Microsoft Entra user is assigned to Workgrid to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Workgrid, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 2: Set up Workgrid for provisioning

Before configuring Workgrid for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on Workgrid.

1. Log in into Workgrid. Navigate to **Users &gt; User Provisioning**.

    ![Screenshot of the Workgrid U I with the Users and User Provisioning options called out.](media/workgrid-provisioning-tutorial/user.png)
2. Under **Account Management API**, select **Create Credentials**.

    ![Screenshot of the Account Management A P I section with the Create Credentials option called out.](media/workgrid-provisioning-tutorial/scim.png)
3. Copy the **SCIM Endpoint** and **Access Token** values. These are entered in the **Tenant URL** and **Secret Token** field in the Provisioning tab of your Workgrid application.

    ![Screenshot of the Account Management A P I section with S C I M Endpoint and Access Token called out.](media/workgrid-provisioning-tutorial/token.png)

## Step 3: Add Workgrid from the gallery

To configure Workgrid for automatic user provisioning with Microsoft Entra ID, you need to add Workgrid from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Workgrid from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Workgrid**, select **Workgrid** in the search box.
4. Select **Workgrid** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Workgrid  in the results list](common/search-new-app.png)

## Step 4: Configure automatic user provisioning to Workgrid

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Workgrid based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Workgrid , following the instructions provided in the [Workgrid Single sign-on article](workgrid-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other

### Configure automatic user provisioning for Workgrid in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Workgrid**.

    ![Screenshot of Workgrid  link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of new configuration.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Workgrid Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Workgrid. If the connection fails, ensure your Workgrid account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Workgrid in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Workgrid for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Workgrid |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | displayName | String |  |  |
    | title | String |  |  |
    | emails[type eq "work"].value | String |  |  |
    | preferredLanguage | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | phoneNumbers[type eq "mobile"].value | String |  |  |
    | phoneNumbers[type eq "fax"].value | String |  |  |
    | externalId | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | String |  |  |
    | addresses[type eq "work"].locality | String |  |  |
    | addresses[type eq "work"].postalCode | String |  |  |
    | addresses[type eq "work"].formatted | String |  |  |
    | addresses[type eq "work"].region | String |  |  |
    | addresses[type eq "work"].streetAddress | String |  |  |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Workgrid in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Workgrid for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Workgrid |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | externalId | String |  | ✓ |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.