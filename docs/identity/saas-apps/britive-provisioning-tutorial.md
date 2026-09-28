---
layout: Conceptual
title: Configure Britive for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/britive-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Britive.
ms.topic: how-to
ms.date: 2026-02-27T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: dc0fa6b9-57fb-85dc-c195-54f68f3df867
document_version_independent_id: d49f0ce7-77db-b9e5-64ff-832f0c3cf6a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/britive-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/britive-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/britive-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3d7c95ea-168e-5c51-a853-1b44881a5bb8
---

# Configure Britive for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Britive and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Britive](https://www.britive.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in Britive
- Remove users in Britive when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Britive
- Provision groups and group memberships in Britive
- [Single sign-on](britive-tutorial) to Britive (recommended)
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A [Britive](https://www.britive.com/) tenant.
- A user account in Britive with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Britive](../app-provisioning/customize-application-attributes).

## Step 2: Configure Britive to support provisioning with Microsoft Entra ID

The application has to be manually configured using the steps provided in this section:

1. Log in to the Britive application with administrator privileges.
2. Select **Admin-&gt;Identity Management-&gt;Identity Providers**.
3. Select **Add Identity Provider**. Enter the name and description. Select the **Add** button.

    ![Identity Provider](media/britive-provisioning-tutorial/identity.png)
4. A configuration page similar to the one displayed below is shown.

    ![Configuration Page](media/britive-provisioning-tutorial/configuration.png)
5. Select **SCIM** tab. Change the SCIM provider from Generic to Azure and save the changes. Copy the SCIM URL and note it down. These values are entered in the **Tenant URL** boxes on the Provisioning tab of your Britive application in the Azure portal.

    ![SCIM Page](media/britive-provisioning-tutorial/scim.png)
6. Select **Create Token**. Select the validity of the token as required and select the **Create Token** button.

    ![Create Token](media/britive-provisioning-tutorial/create-token.png)
7. Copy the token generated and note it down. Select OK. Note that the user isn't able to see the token again. Select the **Recreate token** button to generate a new token if needed. These values are entered in the **Secret Token** and Tenant URL boxes on the Provisioning tab of your getAbstract application.

    ![Copy Token](media/britive-provisioning-tutorial/copy-token.png)

## Step 3: Add Britive from the Microsoft Entra application gallery

Add Britive from the Microsoft Entra application gallery to start managing provisioning to Britive. If you have previously set up Britive for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Britive

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Britive based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Britive in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Britive**.

    ![The Britive link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Britive Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Britive. If the connection fails, ensure your Britive account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Britive in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Britive for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Britive API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | displayName | String |  |
    | title | String |  |
    | externalId | String |  |
    | preferredLanguage | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | nickName | String |  |
    | userType | String |  |
    | locale | String |  |
    | timezone | String |  |
    | emails[type eq "home"].value | String |  |
    | emails[type eq "other"].value | String |  |
    | emails[type eq "work"].value | String |  |
    | phoneNumbers[type eq "home"].value | String |  |
    | phoneNumbers[type eq "other"].value | String |  |
    | phoneNumbers[type eq "pager"].value | String |  |
    | phoneNumbers[type eq "work"].value | String |  |
    | phoneNumbers[type eq "mobile"].value | String |  |
    | phoneNumbers[type eq "fax"].value | String |  |
    | addresses[type eq "work"].formatted | String |  |
    | addresses[type eq "work"].streetAddress | String |  |
    | addresses[type eq "work"].locality | String |  |
    | addresses[type eq "work"].region | String |  |
    | addresses[type eq "work"].postalCode | String |  |
    | addresses[type eq "work"].country | String |  |
    | addresses[type eq "home"].formatted | String |  |
    | addresses[type eq "home"].streetAddress | String |  |
    | addresses[type eq "home"].locality | String |  |
    | addresses[type eq "home"].region | String |  |
    | addresses[type eq "home"].postalCode | String |  |
    | addresses[type eq "home"].country | String |  |
    | addresses[type eq "other"].formatted | String |  |
    | addresses[type eq "other"].streetAddress | String |  |
    | addresses[type eq "other"].locality | String |  |
    | addresses[type eq "other"].region | String |  |
    | addresses[type eq "other"].postalCode | String |  |
    | addresses[type eq "other"].country | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Britive in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Britive for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | displayName | String | ✓ |
    | externalId | String |  |
    | members | Reference |  |
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a few users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.