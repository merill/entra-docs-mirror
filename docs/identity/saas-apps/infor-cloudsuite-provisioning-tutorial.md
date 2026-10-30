---
layout: Conceptual
title: Configure Infor CloudSuite for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/infor-cloudsuite-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Infor CloudSuite.
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 84b31467-8709-dc57-e48c-21528c528fa7
document_version_independent_id: de7c7950-0c34-24cd-7caf-821b01d47653
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/infor-cloudsuite-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/infor-cloudsuite-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/infor-cloudsuite-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 82239581-3814-9831-3d82-dd5a60a50b09
---

# Configure Infor CloudSuite for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Infor CloudSuite and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Infor CloudSuite.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
        - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
        - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
        - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- [An Infor CloudSuite tenant](https://www.infor.com/products)
- A user account in Infor CloudSuite with Admin permissions.

## Assigning users to Infor CloudSuite

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Infor CloudSuite. Once decided, you can assign these users and/or groups to Infor CloudSuite by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to Infor CloudSuite

- It's recommended that a single Microsoft Entra user is assigned to Infor CloudSuite to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Infor CloudSuite, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up Infor CloudSuite for provisioning

1. Sign in to your [Infor CloudSuite Admin Console](https://www.infor.com/customer-center). Select the user icon and then navigate to **user management**.

    ![Infor CloudSuite Admin Console](media/infor-cloudsuite-provisioning-tutorial/admin.png)
2. Select the menu icon on the left top corner of the screen. Select **Manage**.

    ![Infor CloudSuite Add SCIM](media/infor-cloudsuite-provisioning-tutorial/manage.png)
3. Navigate to **SCIM Accounts**.

    ![Infor CloudSuite SCIM Account](media/infor-cloudsuite-provisioning-tutorial/scim.png)
4. Add an admin user by selecting the plus icon. Provide a **SCIM Password** and type the same password under **Confirm Password**. Select the folder icon to save the password. You then see an **User Identifier** generated for the admin user.

    ![Infor CloudSuite Admin user](media/infor-cloudsuite-provisioning-tutorial/newuser.png)

    ![Infor CloudSuite password](media/infor-cloudsuite-provisioning-tutorial/password.png)
5. To generate the bearer token, copy the **User Identifier** and **SCIM Password**. Paste them in notepad++ separated by a colon. Encode the string value by navigating to **Plugins &gt; MIME Tools &gt; Basic64 Encode**.

    ![Screenshot of a Notepad++ document. In the Plugins menu, MIME tools is highlighted. In the MIME tools menu, Base64 encode is highlighted.](media/infor-cloudsuite-provisioning-tutorial/token.png)

    To generate the bearer token using PowerShell instead of Notepad++, use the following commands:

    ```powershell
    $Identifier = "<User Identifier>"
     $SCIMPassword = "<SCIM Password>"
     $bytes = [System.Text.Encoding]::UTF8.GetBytes($($Identifier):$($SCIMPassword))
     [Convert]::ToBase64String($bytes)
    ```
6. Copy the bearer token. This value is entered in the Secret Token field in the Provisioning tab of your Infor CloudSuite application.

## Add Infor CloudSuite from the gallery

Before configuring Infor CloudSuite for automatic user provisioning with Microsoft Entra ID, you need to add Infor CloudSuite from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Infor CloudSuite from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Infor CloudSuite**, select **Infor CloudSuite** in the search box.
4. Select **Infor CloudSuite** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Infor CloudSuite in the results list](common/search-new-app.png)

## Configuring automatic user provisioning to Infor CloudSuite

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Infor CloudSuite based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Infor CloudSuite, following the instructions provided in the [Infor CloudSuite Single sign-on article](infor-cloud-suite-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Infor CloudSuite in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Infor CloudSuite**.

    ![The Infor CloudSuite link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Infor CloudSuite Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Infor CloudSuite. If the connection fails, ensure your Infor CloudSuite account has the required admin permissions and try again.

    Note

    Enter `https://mingle-t20b-scim.mingle.awsdev.infor.com/INFORSTS_TST/v2/scim` in **Tenant URL**.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Infor CloudSuite in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Infor CloudSuite for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Infor CloudSuite API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Infor CloudSuite |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | displayName | String |  |  |
    | externalId | String |  |  |
    | name.familyName | String |  |  |
    | name.givenName | String |  |  |
    | displayName | String |  |  |
    | title | String |  |  |
    | emails[type eq "work"].value | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | urn:ietf:params:scim:schemas:extension:infor:2.0:User:actorId | String |  |  |
    | urn:ietf:params:scim:schemas:extension:infor:2.0:User:federationId | String |  |  |
    | urn:ietf:params:scim:schemas:extension:infor:2.0:User:ifsPersonId | String |  |  |
    | urn:ietf:params:scim:schemas:extension:infor:2.0:User:lnUser | String |  |  |
    | urn:ietf:params:scim:schemas:extension:infor:2.0:User:userAlias | String |  |  |
12. Review the group attributes that are synchronized from Microsoft Entra ID to Infor CloudSuite in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Infor CloudSuite for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Infor CloudSuite |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
    | externalId | String |  |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you've configured provisioning, use the following resources to monitor your deployment:

- Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users have been provisioned successfully or unsuccessfully
- Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
- If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states [here](../app-provisioning/application-provisioning-quarantine-status).

## Change log

02/15/2023 - Added support for custom extension user attributes **urn:ietf:params:scim:schemas:extension:infor:2.0:User:actorId**, **urn:ietf:params:scim:schemas:extension:infor:2.0:User:federationId**, **urn:ietf:params:scim:schemas:extension:infor:2.0:User:ifsPersonId**, **urn:ietf:params:scim:schemas:extension:infor:2.0:User:inUser**, and **urn:ietf:params:scim:schemas:extension:infor:2.0:User:userAlias**.