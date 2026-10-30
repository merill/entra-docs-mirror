---
layout: Conceptual
title: Configure Genesys Cloud for Azure for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/purecloud-by-genesys-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Genesys Cloud for Azure.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
locale: en-us
document_id: 0882aa5f-e8db-3de4-5ecd-ecc5d8211647
document_version_independent_id: 8f4ee9aa-d74d-57cd-2555-3528cb434802
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/purecloud-by-genesys-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/purecloud-by-genesys-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/purecloud-by-genesys-provisioning-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 76364e7f-0a30-3b41-54ef-9338c9be38d0
---

# Configure Genesys Cloud for Azure for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Genesys Cloud for Azure and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Genesys Cloud for Azure](https://www.genesys.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Genesys Cloud for Azure
- Remove users in Genesys Cloud for Azure when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Genesys Cloud for Azure
- Provision groups and group memberships in Genesys Cloud for Azure
- [Single sign-on](purecloud-by-genesys-tutorial) to Genesys Cloud for Azure (recommended)
- Long lived bearer token authentication supported.

Genesys Cloud for Azure is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A PureCloud [organization](https://help.mypurecloud.com/?p=81984).
- A User with [permissions](https://help.mypurecloud.com/?p=24360) to create an Oauth Client.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Genesys Cloud for Azure](../app-provisioning/customize-application-attributes).

## Step 2: Configure Genesys Cloud for Azure to support provisioning with Microsoft Entra ID

1. Create an [Oauth Client](https://help.mypurecloud.com/?p=188023) configured in your PureCloud organization.
2. Generate a token [with your oauth client](https://developer.mypurecloud.com/api/rest/authorization/use-client-credentials.html).
3. If you're wanting to automatically provision Group membership within PureCloud, you must [create Groups](https://help.mypurecloud.com/?p=52397) in PureCloud with an identical name to the group in Microsoft Entra ID.

## Step 3: Add Genesys Cloud for Azure from the Microsoft Entra application gallery

Add Genesys Cloud for Azure from the Microsoft Entra application gallery to start managing provisioning to Genesys Cloud for Azure. If you have previously setup Genesys Cloud for Azure for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Genesys Cloud for Azure

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Genesys Cloud for Azure in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Diagram that shows Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Genesys Cloud for Azure**.

    ![Diagram that shows the Genesys Cloud for Azure link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, input your Genesys Cloud for Azure API URL and Oauth Token in the **Tenant URL** and **Secret Token** fields respectively. The API URL is structured as `{{API Url}}/api/v2/scim/v2`, using the API URL for your PureCloud region from the [PureCloud Developer Center](https://developer.mypurecloud.com/api/rest/index.html). Select **Test Connection** to ensure Microsoft Entra ID can connect to Genesys Cloud for Azure. If the connection fails, ensure your Genesys Cloud for Azure account has Admin permissions and try again.

    ![Screenshot shows the Admin Credentials dialog box, where you can enter your Tenant U R L and Secret Token.](media/purecloud-by-genesys-provisioning-tutorial/provisioning.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Genesys Cloud for Azure in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Genesys Cloud for Azure for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Genesys Cloud for Azure API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Genesys Cloud for Azure |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | displayName | String |  | ✓ |
    | emails[type eq "work"].value | String |  |  |
    | title | String |  |  |
    | phoneNumbers[type eq "mobile"].value | String |  |  |
    | phoneNumbers[type eq "work"].value | String |  |  |
    | phoneNumbers[type eq "work2"].value | String |  |  |
    | phoneNumbers[type eq "work3"].value | String |  |  |
    | phoneNumbers[type eq "work4"].value | String |  |  |
    | phoneNumbers[type eq "home"].value | String |  |  |
    | phoneNumbers[type eq "microsoftteams"].value | String |  |  |
    | roles | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |  |
    | urn:ietf:params:scim:schemas:extension:genesys:purecloud:2.0:User:externalIds[authority eq ‘microsoftteams’].value | String |  |  |
    | urn:ietf:params:scim:schemas:extension:genesys:purecloud:2.0:User:externalIds[authority eq ‘ringcentral’].value | String |  |  |
    | urn:ietf:params:scim:schemas:extension:genesys:purecloud:2.0:User:externalIds[authority eq ‘zoomphone].value | String |  |  |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Genesys Cloud for Azure in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Genesys Cloud for Azure for update operations. Select the **Save** button to commit any changes. Genesys Cloud for Azure doesn't support group creation or deletion and only supports updating of groups.

    | Attribute | Type | Supported for filtering | Required by Genesys Cloud for Azure |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | externalId | String |  |  |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change log

- 09/10/2020 - Added support for extension enterprise attribute **employeeNumber**.
- 05/18/2021 - Added support for core attributes **phoneNumbers[type eq "work2"]**, **phoneNumbers[type eq "work3"]**, **phoneNumbers[type eq "work4"]**, **phoneNumbers[type eq "home"]**, **phoneNumbers[type eq "microsoftteams"]** and roles. And also added support for custom extension attributes **urn:ietf:params:scim:schemas:extension:genesys:purecloud:2.0:User:externalIds[authority eq ‘microsoftteams’]**, **urn:ietf:params:scim:schemas:extension:genesys:purecloud:2.0:User:externalIds[authority eq ‘zoomphone]** and **urn:ietf:params:scim:schemas:extension:genesys:purecloud:2.0:User:externalIds[authority eq ‘ringcentral’]**.