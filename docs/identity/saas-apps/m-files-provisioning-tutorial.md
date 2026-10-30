---
layout: Conceptual
title: Configure M-Files for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/m-files-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to M-Files.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c28bb8be-bc65-6294-6fee-f401cd9b4e90
document_version_independent_id: 1ba95227-7ab7-4646-4852-04fff1ee8289
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/m-files-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/m-files-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/m-files-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2a6b01cb-b65f-d547-cdd7-98c69798bd55
---

# Configure M-Files for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both M-Files and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [M-Files](https://www.m-files.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in M-Files.
- Remove users in M-Files when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and M-Files.
- Provision groups and group memberships in M-Files.
- [Single sign-on](m-files-tutorial) to M-Files (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- M-Files Cloud Subscription (Classic Cloud isn't supported).
- A user account in M-Files with the Subscription admin or Access admin access to [M-Files Manage](https://manage.m-files.com/).

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and M-Files](../app-provisioning/customize-application-attributes).
4. The necessary mappings are predefined but you can map two additional data fields to M-Files.

## Step 2: Configure M-Files to support provisioning with Microsoft Entra ID

Before you set up user provisioning in M-Files, make sure that all vaults in your subscription have user synchronization disabled in M-Files Admin.

If you have previously configured user provisioning in M-Files Manage with your own Entra ID application, you can't change the configuration to use the M-Files application from the Microsoft Entra application gallery. If you want to use the M-Files application instead, delete the existing configuration from M-Files Manage and disable or delete the related Entra ID application. Then, follow these instructions to create the new configuration.

1. Log in to M-Files Manage at https://manage.m-files.com.
2. In the left-side page navigation, select **Provisioning**.
3. Go to the **Configuration** tab.
4. In **Create configuration for user provisioning**, select **Azure AD gallery app**.
5. Enter the necessary information.
    - In **Configuration name**, enter a unique name for the configuration.
    - Select **Default license type** for the provisioned users. All the provisioned users first get this license. You can change a user group's license type to a higher one after user groups have been provisioned. If there aren't enough available licenses of the default license type in the subscription, all the users don't get the license.
6. Select the copy icon (![Screenshot of the Copy icon.](media/m-files-provisioning-tutorial/icon.png) ) for each piece of data, that M-Files Manage created, and note down the values.

Note

The client secret isn't shown anywhere else when you close the dialog.

## Step 3: Add M-Files from the Microsoft Entra application gallery

Add M-Files from the Microsoft Entra application gallery to start managing provisioning to M-Files. If you have previously set up M-Files for SSO you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to M-Files

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for M-Files in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **M-Files**.

    ![Screenshot of the M-Files link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the New configuration option on the Provisioning page.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, enter your M-Files Tenant URL, Token Endpoint, Client Identifier and Client Secret. Select **Test Connection** to ensure Microsoft Entra ID can connect to M-Files. If the connection fails, make sure that the values you entered are correct and try again.

    ![Screenshot of Provisioning test connection.](media/m-files-provisioning-tutorial/test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
10. **Optional**: If you want to synchronize additional user information, you can define two additional fields to be synchronized to M-Files Manage. The information is shown in **Additional information 1** and **Additional information 2** on the **User information** page.

    1. Under the **Mappings** section, select **Synchronize Microsoft Entra users to M-Files**.
    2. In the **Attribute-Mapping** section, select **Add new mapping**.
    3. Use these values:
        - **Mapping type**: **Direct**
        - **Source attribute**: Enter the Entra ID attribute
        - **Target attribute**: Select **urn:ietf:params:scim:schemas:extension:info:2.0:User:info1** or **urn:ietf:params:scim:schemas:extension:info:2.0:User:info2**
        - **Match objects using this attribute**: **No**
        - **Apply this mapping**: **Always**
    4. Select **Ok**.
    5. **Optional**: To synchronize two additional data fields to M-Files Manage, add a second mapping with the other available target attribute.

    Note

    It isn't recommended to make changes to the default attribute mappings.
11. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
12. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
13. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.