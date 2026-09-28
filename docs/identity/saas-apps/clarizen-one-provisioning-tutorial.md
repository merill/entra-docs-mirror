---
layout: Conceptual
title: Configure Clarizen One for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/clarizen-one-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Clarizen One.
ms.topic: how-to
ms.date: 2026-03-04T00:00:00.0000000Z
locale: en-us
document_id: 82111b41-0f5b-eb39-2b5f-b66348067ab8
document_version_independent_id: 8b30e973-c49f-6aff-795d-4ac4aea4cf0b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/clarizen-one-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/clarizen-one-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/clarizen-one-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4afd1f12-2a15-860e-18e0-2edec6faccfe
---

# Configure Clarizen One for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Clarizen One and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Clarizen One](https://www.clarizen.com/) by using the Microsoft Entra provisioning service. For information on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to software as a service (SaaS) applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Clarizen One.
- Remove users in Clarizen One when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Clarizen One.
- Provision groups and group memberships in Clarizen One.
- [Single sign-on (SSO)](clarizen-tutorial) to Clarizen One is recommended.
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in Clarizen One with **Integration User** and **Lite Admin**[permissions](https://success.clarizen.com/hc/articles/360011833079-API-Keys-Support).

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Clarizen One](../app-provisioning/customize-application-attributes).

## Step 2: Configure Clarizen One to support provisioning with Microsoft Entra ID

1. Select one of the four following Tenant URLs according to your Clarizen One environment and data center:

    - US Production data center: `https://servicesapp2.clarizen.com/scim/v2`
    - EU Production data center: `https://serviceseu1.clarizen.com/scim/v2`
    - US Sandbox data center: `https://servicesapp.clarizentb.com/scim/v2`
    - EU Sandbox data center: `https://serviceseu.clarizentb.com/scim/v2`
2. Generate an [API key](https://success.clarizen.com/hc/articles/360011833079-API-Keys-Support). This value is entered in the **Secret Token** box on the **Provisioning** tab of your Clarizen One application.

## Step 3: Add Clarizen One from the Microsoft Entra application gallery

Add Clarizen One from the Microsoft Entra application gallery to start managing provisioning to Clarizen One. If you've previously set up Clarizen One for SSO, you can use the same application. When you test out the integration initially, create a separate app. To learn more about how to add an application from the gallery, see [Add an application to your Microsoft Entra tenant](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Clarizen One

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users or groups in TestApp based on user or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for Clarizen One in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Screenshot that shows the Enterprise applications pane.](common/enterprise-applications.png)
3. In the applications list, select **Clarizen One**.

    ![Screenshot that shows the Clarizen One link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot that shows the Provisioning tab.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Clarizen One Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Clarizen One. If the connection fails, ensure your Clarizen One account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Clarizen One in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Clarizen One for update operations. If you change the [matching target attribute](../app-provisioning/customize-application-attributes), you must ensure that the Clarizen One API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | userName | String |
    | displayName | String |
    | active | Boolean |
    | title | String |
    | emails[type eq "work"].value | String |
    | emails[type eq "home"].value | String |
    | emails[type eq "other"].value | String |
    | preferredLanguage | String |
    | name.givenName | String |
    | name.familyName | String |
    | name.formatted | String |
    | name.honorificPrefix | String |
    | name.honorificSuffix | String |
    | addresses[type eq "other"].formatted | String |
    | addresses[type eq "work"].formatted | String |
    | addresses[type eq "work"].country | String |
    | addresses[type eq "work"].region | String |
    | addresses[type eq "work"].locality | String |
    | addresses[type eq "work"].postalCode | String |
    | addresses[type eq "work"].streetAddress | String |
    | phoneNumbers[type eq "work"].value | String |
    | phoneNumbers[type eq "mobile"].value | String |
    | phoneNumbers[type eq "fax"].value | String |
    | phoneNumbers[type eq "home"].value | String |
    | phoneNumbers[type eq "other"].value | String |
    | phoneNumbers[type eq "pager"].value | String |
    | externalId | String |
    | nickName | String |
    | locale | String |
    | roles[primary eq "True".type] | String |
    | roles[primary eq "True".value] | String |
    | timezone | String |
    | userType | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Clarizen One in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Clarizen One for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | displayName | String |
    | externalId | String |
    | members | Reference |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Troubleshooting tips

When you assign a user to the Clarizen One gallery app, select only the **User** role. The following roles are invalid:

- Administrator (admin)
- Email Reporting user
- External user
- Financial user
- Social user
- Superuser
- Time & Expense user