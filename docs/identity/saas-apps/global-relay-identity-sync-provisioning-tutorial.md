---
layout: Conceptual
title: Configure Global Relay Identity Sync for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/global-relay-identity-sync-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Global Relay Identity Sync.
ms.topic: how-to
ms.date: 2026-04-08T00:00:00.0000000Z
locale: en-us
document_id: f344ee21-73b8-e663-c0db-7b886b78dd15
document_version_independent_id: 4c548916-f199-e53f-2383-ada2883e42f3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/global-relay-identity-sync-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/global-relay-identity-sync-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/global-relay-identity-sync-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: be3e74e0-db80-45a7-c9db-e8b68d5d493f
---

# Configure Global Relay Identity Sync for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Global Relay Identity Sync and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to Global Relay Identity Sync using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Global Relay Identity Sync
- Remove users in Global Relay Identity Sync when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Global Relay Identity Sync
- Provision groups and group memberships in Global Relay Identity Sync
- Client Credentials Authentication supported.

Note

Global Relay Identity Sync provisioning connector utilizes a SCIM authorization method that's no longer supported due to security concerns. Efforts are underway with Global Relay to switch to a more secure authorization method.

Note

Global Relay Identity Sync now supports Client credential authorization.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Global Relay Identity Sync](../app-provisioning/customize-application-attributes).

## Step 2: Configure Global Relay Identity Sync to support provisioning with Microsoft Entra ID

Contact your Global Relay Identity Sync representative to receive the Tenant URL. This value is entered in the **Tenant URL** field in the Provisioning tab of your Global Relay Identity Sync application.

## Step 3: Add Global Relay Identity Sync from the Microsoft Entra application gallery

Add Global Relay Identity Sync from the Microsoft Entra application gallery to start managing provisioning to Global Relay Identity Sync. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Global Relay Identity Sync

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Global Relay Identity Sync app based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Global Relay Identity Sync in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Global Relay Identity Sync**.

    ![The Global Relay Identity Sync link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Global Relay Identity Sync **Tenant URL, Client identifier, Client secret** and **OAuth token endpoint**. Select **Test connection** to ensure Microsoft Entra ID can connect to Global Relay Identity Sync. If the connection fails, ensure your Global Relay Identity Sync account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-button.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Global Relay Identity Sync in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Global Relay Identity Sync for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Global Relay Identity Sync API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | userName | String |
    | active | Boolean |
    | displayName | String |
    | title | String |
    | preferredLanguage | String |
    | name.givenName | String |
    | name.familyName | String |
    | name.formatted | String |
    | addresses[type eq "work"].formatted | String |
    | addresses[type eq "work"].streetAddress | String |
    | emails[type eq "work"].value | String |
    | addresses[type eq "work"].locality | String |
    | addresses[type eq "work"].region | String |
    | addresses[type eq "work"].postalCode | String |
    | addresses[type eq "work"].country | String |
    | addresses[type eq "other"].formatted | String |
    | phoneNumbers[type eq "work"].value | String |
    | phoneNumbers[type eq "mobile"].value | String |
    | phoneNumbers[type eq "fax"].value | String |
    | externalId | String |
    | name.honorificPrefix | String |
    | name.honorificSuffix | String |
    | nickName | String |
    | userType | String |
    | locale | String |
    | timezone | String |
    | emails[type eq "home"].value | String |
    | emails[type eq "other"].value | String |
    | phoneNumbers[type eq "home"].value | String |
    | phoneNumbers[type eq "other"].value | String |
    | phoneNumbers[type eq "pager"].value | String |
    | addresses[type eq "home"].streetAddress | String |
    | addresses[type eq "home"].locality | String |
    | addresses[type eq "home"].region | String |
    | addresses[type eq "home"].postalCode | String |
    | addresses[type eq "home"].country | String |
    | addresses[type eq "home"].formatted | String |
    | addresses[type eq "other"].streetAddress | String |
    | addresses[type eq "other"].locality | String |
    | addresses[type eq "other"].region | String |
    | addresses[type eq "other"].postalCode | String |
    | addresses[type eq "other"].country | String |
    | roles[primary eq "True"].display | String |
    | roles[primary eq "True"].type | String |
    | roles[primary eq "True"].value | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:proxyAddresses | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute1 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute2 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute3 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute4 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute5 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute6 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute7 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute8 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute9 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute10 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute11 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute12 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute13 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute14 | String |
    | urn:ietf:params:scim:schemas:extension:GlobalRelay:2.0:User:extensionAttribute15 | String |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Global Relay Identity Sync in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Global Relay Identity Sync for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | displayName | String |
    | members | Reference |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a few users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.