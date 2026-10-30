---
layout: Conceptual
title: Configure Funnel Leasing for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/funnel-leasing-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Funnel Leasing.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: ff1761fc-a475-a70a-eca7-5ee5f2d2c9b6
document_version_independent_id: 5bd19eef-3efb-6f67-bb87-7c2268753c68
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/funnel-leasing-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/funnel-leasing-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/funnel-leasing-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 202ddbfc-885a-b539-2a0d-60a531edb487
---

# Configure Funnel Leasing for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Funnel Leasing and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to [Funnel Leasing](https://funnelleasing.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Funnel Leasing.
- Remove users in Funnel Leasing when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Funnel Leasing.
- [Single sign-on](../enterprise-apps/add-application-portal-setup-oidc-sso) to Funnel Leasing (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A live community in Funnel or at least a confirmation that all the required configuration is done on the Funnel side in preparation for a go-live date.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Funnel Leasing](../app-provisioning/customize-application-attributes).

## Step 2: Configure Funnel Leasing to support provisioning with Microsoft Entra ID

Contact your Funnel Account Manager and let them know you want to enable Microsoft Entra user provisioning, they will provide an authentication Bearer token.

## Step 3: Add Funnel Leasing from the Microsoft Entra application gallery

Add Funnel Leasing from the Microsoft Entra application gallery to start managing provisioning to Funnel Leasing. If you have previously setup Funnel Leasing for SSO you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Funnel Leasing

This section guides you through connecting your Microsoft Entra ID to Funnel's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Funnel based on user assignment in Microsoft Entra ID.

### To configure automatic user provisioning for Funnel Leasing in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Funnel**.

    ![Screenshot of the Funnel Leasing link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Funnel Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Funnel. If the connection fails, ensure your Funnel account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Funnel in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Funnel for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Funnel API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Funnel Leasing |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | title | String |  |  |
    | emails[type eq "work"].value | String |  | ✓ |
    | name.givenName | String |  | ✓ |
    | name.familyName | String |  | ✓ |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | phoneNumbers[type eq "mobile"].value | String |  |  |
    | externalId | String |  |  |
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Role and Group Mappings

To associate an Azure user to a Funnel role, or an Azure user to a Funnel employee group, Funnel uses a custom mapping functionality.

- Which Azure fields are used?

    For role mappings, Funnel looks at the SCIM `title` attribute by default. This SCIM attribute is mapped to the `jobTitle` Azure user attribute by default.

    For group mappings, Funnel looks at the SCIM `userType` attribute by default. This SCIM attribute is mapped to the `department` Azure user attribute by default.

    If you want to change which fields are used, you can edit the **Attribute Mappings** section and map your desired fields to `title` and `userType`.
- Which values are used?

    For initial setup, determine every value that you want to use for role and group mappings. Provide these values to your Funnel Account Manager to set up the configuration in Funnel.

    For example, if you want to set the `jobTitle` field with an `agent` value, you need to tell your Funnel Account Manager which Funnel role this value should be mapped.

    If you need to update or add new values in the future, you need to notify your Funnel Account Manager.
- How do I associate a user to several roles and groups?

    It isn't possible to associate a user to several Funnel roles, but it's possible to associate a user to several Funnel employee groups.

    To associate a user to several Funnel employee groups, you need to specify multiple values in the `department` user attribute (or whichever attribute you mapped to `userType`). Each value will need to be separated by a delimiter. By default the `-` character is used as the delimiter. To use another delimiter, you need to notify your Funnel account manager.