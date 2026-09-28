---
layout: Conceptual
title: Configure Configure Atlassian Cloud for for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/atlassian-cloud-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Atlassian Cloud.
ms.topic: how-to
ms.date: 2026-02-26T00:00:00.0000000Z
locale: en-us
document_id: 04509836-867e-279f-c1d6-135a237d357e
document_version_independent_id: e05a10ce-c46b-334e-78e2-30b416ed904a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/atlassian-cloud-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/atlassian-cloud-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/atlassian-cloud-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d3966032-f11e-3e30-0132-d8d826dfac84
---

# Configure Configure Atlassian Cloud for for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Atlassian Cloud and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Atlassian Cloud](https://www.atlassian.com/cloud) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- [Discover existing](../app-provisioning/how-to-account-discovery) users in Atlassian Cloud
- Create users in Atlassian Cloud
- Remove users in Atlassian Cloud when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Atlassian Cloud
- Provision groups and group memberships in Atlassian Cloud
- [Single sign-on](atlassian-cloud-tutorial) to Atlassian Cloud (recommended)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Make sure you're an admin for an Atlassian organization. See [Organization administration.](https://support.atlassian.com/organization-administration/docs/explore-an-atlassian-organization).
- Verify one or more or your domains in your organization. See [Domain verification](https://support.atlassian.com/user-management/docs/verify-a-domain-to-manage-accounts).
- Subscribe to Atlassian Access from your organization. See [Atlassian Access security policies and features](https://support.atlassian.com/security-and-access-policies/docs/understand-atlassian-access).
- [An Atlassian Cloud tenant](https://www.atlassian.com/licensing/cloud) with an Atlassian Access subscription.
- Make sure you're an admin for at least one Jira or Confluence site that you want to grant synced users access to.

    Note

    This integration is also available to use from Microsoft Entra US Government Cloud environment. You can find this application in the Microsoft Entra US Government Cloud Application Gallery and configure it in the same way as you do from public cloud.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Atlassian Cloud](../app-provisioning/customize-application-attributes).

## Step 2: Configure Atlassian Cloud to support provisioning with Microsoft Entra ID

1. Navigate to [Atlassian Admin Console](http://admin.atlassian.com/). Select your organization if you have more than one.
2. Select **Security &gt; Identity providers**.
3. Select your Identity provider directory.
4. Select **Set up user provisioning**.
5. Copy the values for **SCIM base URL** and **API key**. You need them when you configure Azure.
6. Save your **SCIM configuration**.

    Note

    Make sure you store these values in a safe place, as we won't show them to you again.

    Users and groups are automatically be provisioned to your organization. See the [user provisioning](https://support.atlassian.com/provisioning-users/docs/understand-user-provisioning) page for more details on how your users and groups sync to your organization.

## Step 3: Add Atlassian Cloud from the Microsoft Entra application gallery

Add Atlassian Cloud from the Microsoft Entra application gallery to start managing provisioning to Atlassian Cloud. If you have previously setup Atlassian Cloud for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configuring automatic user provisioning to Atlassian Cloud

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Atlassian Cloud based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Atlassian Cloud in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Atlassian Cloud**.

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Atlassian Cloud**.

    ![The Atlassian Cloud link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Set the **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter the **Tenant URL** and **Secret Token** retrieved earlier from your Atlassian Cloud's account. Select **Test Connection** to ensure Microsoft Entra ID can connect to Atlassian Cloud. If the connection fails, ensure your Atlassian Cloud account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

![Screenshot of Provisioning properties.](common/provisioning-properties.png)

1. Select **Attribute Mapping** in the left panel and select **users**.
2. Review the user attributes that are synchronized from Microsoft Entra ID to Atlassian Cloud in the **Attribute Mapping** section. **The email attribute is used to match Atlassian Cloud accounts with your Microsoft Entra accounts.** Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | userName | String |
    | active | Boolean |
    | name.familyName | String |
    | name.givenName | String |
    | emails[type eq "work"].value | String |
3. Select **Groups**.
4. Review the group attributes that are synchronized from Microsoft Entra ID to Atlassian Cloud in the **Attribute Mapping** section. The display name attribute is used to match Atlassian Cloud groups with your Microsoft Entra groups. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | displayName | String |
    | externalId | String |
    | members | Reference |
5. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
6. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
7. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Connector Limitations

- Atlassian Cloud only supports provisioning updates for users with verified domains. Changes made to users from a non-verified domain aren't pushed to Atlassian Cloud. Learn more about Atlassian verified domains [here](https://support.atlassian.com/provisioning-users/docs/understand-user-provisioning/).
- Atlassian Cloud doesn't support group renames today. This means that any changes to the displayName of a group in Microsoft Entra ID aren't updated and reflected in Atlassian Cloud.
- The value of the **mail** user attribute in Microsoft Entra ID is only populated if the user has a Microsoft Exchange Mailbox. If the user doesn't have one, it's recommended to map a different desired attribute to the **emails** attribute in Atlassian Cloud.

## Change log

- 06/15/2020 - Added support for batch PATCH for groups.
- 04/21/2021 - Added support for **Schema Discovery**.
- 10/14/2022 - Updated Connector Limitations.