---
layout: Conceptual
title: Configure Cofense Recipient Sync for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cofense-provision-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Cofense Recipient Sync.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 4e84608a-0ee8-bfcd-48f2-b3ee931c64a5
document_version_independent_id: 367327a4-e4f3-27d7-4ad9-9fb92b928bb8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cofense-provision-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cofense-provision-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cofense-provision-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 14665350-7581-5f1f-1e51-0ca55af7091b
---

# Configure Cofense Recipient Sync for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Cofense Recipient Sync and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to [Cofense Recipient Sync](https://cofense.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in Cofense Recipient Sync
- Remove users in Cofense Recipient Sync when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Cofense Recipient Sync
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A standard operator account in Cofense PhishMe.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Cofense Recipient Sync](../app-provisioning/customize-application-attributes).

## Step 2: Configure Cofense Recipient Sync to support provisioning with Microsoft Entra ID

1. Login to Cofense PhishMe. Navigate to **Recipients &gt; Recipient Sync**.
2. Accept the terms and conditions and then select **Get Started**.

    ![Recipient Sync tnc](media/cofense-provisioning-tutorial/recipient-sync-toc.png)
3. Copy the values from the **URL** and **Token** fields.

    ![Recipient Sync](media/cofense-provisioning-tutorial/recipient-sync-getting-started.png)

## Step 3: Add Cofense Recipient Sync from the Microsoft Entra application gallery

Add Cofense Recipient Sync from the Microsoft Entra application gallery to start managing provisioning to Cofense Recipient Sync. If you have previously setup Cofense Recipient Sync for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Cofense Recipient Sync

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in Cofense Recipient Sync based on user in Microsoft Entra ID.

### To configure automatic user provisioning for Cofense Recipient Sync in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Cofense Recipient Sync**.

    ![The Cofense link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Set the **Provisioning Mode** to **Automatic**.

    ![Provisioning tab automatic](common/provisioning-automatic.png)
6. Under the **Admin Credentials** section, input the **SCIM 2.0 base url and SCIM Authentication Token** value retrieved earlier from Step 2. Select **Test Connection** to ensure Microsoft Entra ID can connect to Cofense Recipient Sync. If the connection fails, ensure your Cofense Recipient Sync account has Admin permissions and try again.

    ![Tenant URL Token](common/provisioning-testconnection-tenanturltoken.png)
7. In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Notification Email](common/provisioning-notification-email.png)
8. Select **Save**.
9. Under the **Mappings** section, select **Synchronize Microsoft Entra users to Cofense Recipient Sync**.
10. Review the user attributes that are synchronized from Microsoft Entra ID to Cofense Recipient Sync in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Cofense Recipient Sync for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | externalId | String | ✓ |
    | userName | String |  |
    | active | Boolean |  |
    | displayName | String |  |
    | name.formatted | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | name.honorificSuffix | String |  |
    | phoneNumbers[type eq "work"].value | String |  |
    | phoneNumbers[type eq "home"].value | String |  |
    | phoneNumbers[type eq "other"].value | String |  |
    | phoneNumbers[type eq "pager"].value | String |  |
    | phoneNumbers[type eq "mobile"].value | String |  |
    | phoneNumbers[type eq "fax"].value | String |  |
    | addresses[type eq "other"].formatted | String |  |
    | addresses[type eq "work"].formatted | String |  |
    | addresses[type eq "work"].streetAddress | String |  |
    | addresses[type eq "work"].locality | String |  |
    | addresses[type eq "work"].region | String |  |
    | addresses[type eq "work"].postalCode | String |  |
    | addresses[type eq "work"].country | String |  |
    | title | String |  |
    | emails[type eq "work"].value | String |  |
    | emails[type eq "home"].value | String |  |
    | emails[type eq "other"].value | String |  |
    | preferredLanguage | String |  |
    | nickName | String |  |
    | userType | String |  |
    | locale | String |  |
    | timezone | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |
11. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
12. To enable the Microsoft Entra provisioning service for Cofense Recipient Sync, change the **Provisioning Status** to **On** in the **Settings** section.

    ![Provisioning Status Toggled On](common/provisioning-toggle-on.png)
13. Define the users and/or groups that you would like to provision to Cofense Recipient Sync by choosing the desired values in **Scope** in the **Settings** section.

    ![Provisioning Scope](common/provisioning-scope.png)
14. When you're ready to provision, select **Save**.

    ![Saving Provisioning Configuration](common/provisioning-configuration-save.png)

This operation starts the initial synchronization cycle of all users and groups defined in **Scope** in the **Settings** section. The initial cycle takes longer to perform than subsequent cycles, which occur approximately every 40 minutes as long as the Microsoft Entra provisioning service is running.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change log

- 01/15/2020 - Change from "Only during Object Creation" to "Always" has been implemented for objectId -&gt; externalId mapping.