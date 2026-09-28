---
layout: Conceptual
title: Configure Freshservice Provisioning for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/freshservice-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Freshservice Provisioning.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: fbab44ca-dc3b-4b8d-b2fe-b13b8403d628
document_version_independent_id: 34e25c5d-0d65-2f40-8bce-2bd976751195
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/freshservice-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/freshservice-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/freshservice-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fd2c9bd8-9f4f-7cd0-e76f-d365989c1dd6
---

# Configure Freshservice Provisioning for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Freshservice Provisioning and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to [Freshservice Provisioning](https://effy.co.in/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Freshservice Provisioning
- Remove users in Freshservice Provisioning when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Freshservice Provisioning
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A [Freshservice account](https://www.freshservice.com) with the Organizational Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Freshservice Provisioning](../app-provisioning/customize-application-attributes).

## Step 2: Configure Freshservice Provisioning to support provisioning with Microsoft Entra ID

1. On your Freshservice account, install the **Azure Provisioning (SCIM)** app from the marketplace by navigating to **Freshservice Admin** &gt; **Apps** &gt; **Get Apps**.
2. In the configuration screen, provide your **Freshservice Domain** (for example, `acme.freshservice.com`) and the **Organization Admin API key**.
3. Select **Continue**.
4. Highlight and copy the **Bearer Token**. This value is entered in the **Secret Token** field in the Provisioning tab of your Freshservice Provisioning application.
5. Select **Install** to complete the installation.
6. The **Tenant URL** is `https://scim.freshservice.com/scim/v2`. This value is entered in the **Tenant URL** field in the Provisioning tab of your Freshservice Provisioning application.

## Step 3: Add Freshservice Provisioning from the Microsoft Entra application gallery

Add Freshservice Provisioning from the Microsoft Entra application gallery to start managing provisioning to Freshservice Provisioning. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Freshservice Provisioning

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in Freshservice Provisioning based on user assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Freshservice Provisioning in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Freshservice Provisioning**.

    ![The Freshservice Provisioning link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Freshservice Provisioning Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Freshservice Provisioning. If the connection fails, ensure your Freshservice Provisioning account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Freshservice Provisioning in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Freshservice Provisioning for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Freshservice Provisioning API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported For Filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | emails[type eq "work"].value | String |  |
    | displayName | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | phoneNumbers[type eq "work"].value | String |  |
    | phoneNumbers[type eq "mobile"].value | String |  |
    | addresses[type eq "work"].formatted | String |  |
    | locale | String |  |
    | title | String |  |
    | timezone | String |  |
    | externalId | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |
    | urn:ietf:params:scim:schemas:extension:freshservice:2.0:User:isAgent | String |  |

Note

Custom extension attributes can be added to your schema to meet your application's needs by following the below steps:

- Under Mappings, select **Provision Microsoft Entra users**.
- At the bottom of the page, select **Show advanced options**.
- Select **Edit attribute list for Freshservice**.
- At the bottom of the attribute list, enter information about the custom attribute in the fields provided. The custom attribute urn namespace must follow the pattern as shown in the below example. The **CustomAttribute** can be customized per your application's requirements, for example: urn:ietf:params:scim:schemas:extension:freshservice:2.0:User:**isAgent**.
- The appropriate data type has to be selected for the custom attribute and select **Save**.
- Navigate back to the default mappings screen and select **Add New Mapping**. The custom attributes will show up in the **Target Attribute** list dropdown.

1. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
2. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
3. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.