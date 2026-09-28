---
layout: Conceptual
title: Configure Lucid (All Products) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lucid-all-products-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Lucid (All Products).
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: d8008eee-7b64-0a4d-174b-d7e6ed55ec4f
document_version_independent_id: 39d2fd08-a2a0-c287-9477-d740410edf03
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lucid-all-products-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lucid-all-products-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lucid-all-products-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cdfb5503-5222-cf15-fb82-206886523e49
---

# Configure Lucid (All Products) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Lucid (All Products) and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Lucid (All Products)](https://lucid.co/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Lucid (All Products).
- Remove users in Lucid (All Products) when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Lucid (All Products).
- Provision groups and group memberships in Lucid (All Products).
- [Single sign-on](lucid-tutorial) to Lucid (All Products) (recommended)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in Lucid (All Products) with Admin rights.
- Confirm that you're on an Enterprise account with an up-to-date pricing plan. To upgrade, please contact our sales team.
- Contact your Lucidchart Customer Success Manager so that they can enable SCIM for your account.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Lucid (All Products)](../app-provisioning/customize-application-attributes).

## Step 2: Configure Lucid (All Products) to support provisioning with Microsoft Entra ID

1. Log in to [Lucid Admin Console](https://lucid.app/). Navigate to **Admin**.
2. Select **App integration** in the left-hand menu.
3. Select the **SCIM** tile.
4. Select **Generate Token**. Lucid will populate the **Bearer Token** text field with a unique code for you to share with Azure.Copy and save the **Bearer token**. This value is entered in the **Secret Token** \* field in the Provisioning tab of your Lucid(All Products) application.

    ![Screenshot of token generation.](media/lucid-all-products-provisioning-tutorial/generate-token.png)

## Step 3: Add Lucid (All Products) from the Microsoft Entra application gallery

Add Lucid (All Products) from the Microsoft Entra application gallery to start managing provisioning to Lucid (All Products). If you have previously setup Lucid (All Products) for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Lucid (All Products)

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Lucid (All Products) based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Lucid (All Products) in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Lucid (All Products)**.

    ![Screenshot of the Lucid (All Products) link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Lucid (All Products) Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Lucid (All Products). If the connection fails, ensure your Lucid (All Products) account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Lucid (All Products) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Lucid (All Products) for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Lucid (All Products) API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Lucid (All Products) |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | emails[type eq "work"].value | String |  | ✓ |
    | active | Boolean |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | urn:ietf:params:scim:schemas:extension:lucid:2.0:User:billingCode | String |  |  |
    | urn:ietf:params:scim:schemas:extension:lucid:2.0:User:productLicenses.Lucidchart | String |  |  |
    | urn:ietf:params:scim:schemas:extension:lucid:2.0:User:productLicenses.Lucidspark | String |  |  |
    | urn:ietf:params:scim:schemas:extension:lucid:2.0:User:productLicenses.LucidscaleExplorer | String |  |  |
    | urn:ietf:params:scim:schemas:extension:lucid:2.0:User:productLicenses.LucidscaleCreator | String |  |  |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Lucid (All Products) in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Lucid (All Products) for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Lucid (All Products) |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.