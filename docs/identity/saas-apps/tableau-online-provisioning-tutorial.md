---
layout: Conceptual
title: Configure Tableau Cloud for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tableau-online-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Tableau Cloud.
ms.topic: how-to
ms.date: 2026-04-14T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2d1d665b-e5f8-045a-e3c1-221769dc2fc3
document_version_independent_id: 6bbd0fef-c612-6fcf-d964-19246ec16196
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tableau-online-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tableau-online-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tableau-online-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e03a512b-dd62-48e6-cbc9-f6cf4a415fa1
---

# Configure Tableau Cloud for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to do in both Tableau Cloud and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Tableau Cloud](https://www.tableau.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Tableau Cloud.
- Remove users in Tableau Cloud when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Tableau Cloud.
- Provision groups and group memberships in Tableau Cloud.
- [Single sign-on](tableauonline-tutorial) to Tableau Cloud (recommended).
- Long lived bearer token authentication supported.
- Basic authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A [Tableau Cloud tenant](https://www.tableau.com/).
- A user account in Tableau Cloud with Admin permission

Note

The Microsoft Entra provisioning integration relies on the [Tableau Cloud REST API](https://onlinehelp.tableau.com/current/api/rest_api/en-us/help.htm). This API is available to Tableau Cloud developers.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Tableau Cloud](../app-provisioning/customize-application-attributes).

## Step 2: Configure Tableau Cloud to support provisioning with Microsoft Entra ID

Use the following steps to enable SCIM support with Microsoft Entra ID:

1. The SCIM functionality requires that you configure your site to support SAML single sign-on. If you haven't done this yet, complete the following sections in [Configure SAML with Microsoft Entra ID](https://help.tableau.com/current/online/en-us/saml_config_azure_ad.htm):

    - Step 1: [Open the Tableau Cloud SAML Settings](https://help.tableau.com/current/online/en-us/saml_config_azure_ad.htm#open-the-tableau-online-saml-settings).
    - Step 2: [Add Tableau Cloud to your Microsoft Entra applications](https://help.tableau.com/current/online/en-us/saml_config_azure_ad.htm#add-tableau-online-to-your-azure-ad-applications).

    Note

    If you don’t set up SAML single sign-on, your user is unable to sign into Tableau Cloud after they have been provisioned unless you manually change the user’s authentication method from SAML to Tableau or Tableau MFA in Tableau Cloud.
2. In Tableau Cloud, navigate to **Settings &gt; Authentication** page, then under **Automatic Provisioning and Group Synchronization (SCIM)**, select the **Enable SCIM** check box. This populates the **Base URL** and **Secret** boxes with values you use in the SCIM configuration of your IdP.

    Note

    The secret token is displayed only immediately after it's generated. If you lose it before you can apply it to Microsoft Entra ID, you can select **Generate New Secret**. In addition, the secret token is tied to the Tableau Cloud user account of the site administrator who enables SCIM support. If that user’s site role changes or the user is removed from the site, the secret token becomes invalid, and another site administrator must generate a new secret token and apply it to Microsoft Entra ID.

## Step 3: Add Tableau Cloud from the Microsoft Entra application gallery

Add Tableau Cloud from the Microsoft Entra application gallery to start managing provisioning to Tableau Cloud. If you have previously setup Tableau Cloud for SSO, you can use the same application. However it's recommended you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Tableau Cloud

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and groups in Tableau Cloud based on user and group assignments in Microsoft Entra ID.

Tip

You must enable SAML-based single sign-on for Tableau Cloud. Follow the instructions in the [Tableau Cloud single sign-on article](tableauonline-tutorial). If SAML isn't enabled, then the user that's provisioned isn't able to sign in.

### Configure automatic user provisioning for Tableau Cloud in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Tableau Cloud**.

    ![Screenshot of Tableau Cloud link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the New configuration option on the Provisioning page.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your Tableau Cloud Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Tableau Cloud. If the connection fails, ensure your Tableau Cloud account has the required admin permissions and try again.

    ![Screenshot of the Tableau Cloud test connection dialog.](media/tableau-online-provisioning-tutorial/tableau-test-connections.png)

    Note

    You'll have 2 options for your Authentication Method: **Bearer Authentication** and **Basic Authentication**. Make sure that you select Bearer Authentication. Basic authentication doesn't work for the SCIM 2.0 endpoint.
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Tableau Cloud in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Tableau Cloud for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Tableau Cloud API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Tableau Cloud |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | roles | String |  |  |
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Tableau Cloud in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Tableau Cloud for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Tableau Cloud |
    | --- | --- | --- | --- |
    | displayName | String | ✓ |  |
    | members | Reference |  |  |
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

### Update a Tableau Cloud application to use the Tableau Cloud SCIM 2.0 endpoint

In June 2022, Tableau released a SCIM 2.0 connector. Completing the steps below will update applications configured to use the Tableau API endpoint to the use the SCIM 2.0 endpoint. These steps remove any customizations previously made to the Tableau Cloud application, including:

- Authentication details (credentials used for provisioning, NOT the credentials used for SSO)
- Scoping filters
- Custom attribute mappings

Note

Be sure to note any changes that have been made to the settings listed above before completing the steps below. Failure to do so results in the loss of customized settings.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Tableau Cloud**.
3. In the Properties section of your new custom app, copy the **Object ID**.

    ![Screenshot of Tableau Cloud app.](media/tableau-online-provisioning-tutorial/tableau-cloud-properties.png)
4. In a new web browser window, navigate to `https://developer.microsoft.com/graph/graph-explorer` and sign in as the administrator for the Microsoft Entra tenant where your app is added.

    ![Screenshot of Microsoft Graph explorer sign in page.](media/tableau-online-provisioning-tutorial/tableau-graph-explorer-signin.png)
5. Check to make sure the account being used to the correct permissions. The permission **Directory.ReadWrite.All** is required to make this change.

    ![Screenshot of Microsoft Graph settings option.](media/tableau-online-provisioning-tutorial/tableau-graph-settings.png)

    ![Screenshot of Microsoft Graph permissions.](media/tableau-online-provisioning-tutorial/tableau-graph-permissions.png)
6. Using the ObjectID selected from the app previously, run the following command:

    `GET https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/`
7. Taking the "id" value from the response body of the GET request from above, run the command below, replacing "[job-id]" with the id value from the GET request. The value should have the format of "Tableau.xxxxxxxxxxxxxxx.xxxxxxxxxxxxxxx":

    `DELETE https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[job-id]`
8. In the Graph Explorer, run the command below. Replace "[object-id]" with the service principal ID (object ID) copied from the third step.

    `POST https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs { "templateId": "TableauOnlineSCIM" }`

    ![Screenshot of Microsoft Graph request.](media/tableau-online-provisioning-tutorial/tableau-cloud-graph.png)
9. Return to the first web browser window and select the Provisioning tab for your application. Your configuration will have been reset. You can confirm the upgrade has taken place by confirming the Job ID starts with **TableauOnlineSCIM**.
10. Under the Admin Credentials section, select "Bearer Authentication" as the authentication method and enter the Tenant URL and Secret Token of the Tableau instance you wish to provision to. ![Screenshot of Admin Credentials in Tableau Cloud.](media/tableau-online-provisioning-tutorial/tableau-test-connections.png)
11. Restore any previous changes you made to the application (Authentication details, Scoping filters, Custom attribute mappings) and re-enable provisioning.

Note

Failure to restore the previous settings may results in attributes (name.formatted for example) updating in Workplace unexpectedly. Be sure to check the configuration before enabling provisioning

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change log

- 09/30/2020 - Added support for attribute "authSetting" for Users.
- 06/24/2022 - Updated the app to be SCIM 2.0 compliant.