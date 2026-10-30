---
layout: Conceptual
title: Configure Workplace from Meta for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/workplace-from-meta-provisioning-tutorial
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
description: Learn the steps you need to do in both Workplace from Meta and Microsoft Entra ID to configure automatic user provisioning.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7cf9096a-97ae-24da-a5d2-efe8ba2a4c69
document_version_independent_id: 7cf9096a-97ae-24da-a5d2-efe8ba2a4c69
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/workplace-from-meta-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/workplace-from-meta-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/workplace-from-meta-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b1dbb5b8-f2dd-4deb-a5a4-c4a33ed969ed
---

# Configure Workplace from Meta for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to do in both Workplace from Meta and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users to [Workplace from Meta](https://work.workplace.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Workplace from Meta
- Remove users in Workplace from Meta when they don't require access anymore
- Keep user attributes synchronized between Microsoft Entra ID and Workplace from Meta
- [Single sign-on](workplacebyfacebook-tutorial) to Workplace from Meta (recommended)

Workplace from Meta is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Workplace from Meta single-sign on enabled subscription

Note

To test the steps in this article, we don't recommend using a production environment.

To test the steps in this article, you should follow these recommendations:

- Don't use your production environment, unless it's necessary.
- If you don't have a Microsoft Entra trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).

## Step 1: Plan your provisioning deployment

Perform the following planning tasks before you configure provisioning:

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Workplace from Meta](../app-provisioning/customize-application-attributes).

## Step 2: Configure Workplace from Meta to support provisioning with Microsoft Entra ID

Before configuring and enabling the provisioning service, you need to decide what users in Microsoft Entra ID represent the users who need access to your Workplace from Meta app. Once decided, you can assign these users to your Workplace from Meta app by following these instructions:

- We recommend that a single Microsoft Entra user is assigned to Workplace from Meta to test the provisioning configuration. More users might be assigned later.
- When assigning a user to Workplace from Meta, you must select a valid user role. The "Default Access" role doesn't work for provisioning.

## Step 3: Add Workplace from Meta from the Microsoft Entra application gallery

Add Workplace from Meta from the Microsoft Entra application gallery to start managing provisioning to Workplace from Meta. If you have previously setup Workplace from Meta for single sign-on (SSO, you can use the same application. However, we recommended that you create a separate app when testing out the integration initially. Learn more about [adding an application from the gallery](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

Use the following steps to define which users and groups are in scope for provisioning:

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Workplace from Meta

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in Workplace from Meta App based on user assignments in Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Workplace from Meta**.

    ![Screenshot of the Workplace from Meta link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Ensure the "Tenant URL" section is populated with the correct endpoint: `https://scim.workplace.com/`. Under the **Admin Credentials** section, select **Authorize**. You're redirected to Workplace from Meta's authorization page. Enter your Workplace from Meta username and select the **Continue** button. Select **Test Connection** to ensure Microsoft Entra ID can connect to Workplace from Meta. If the connection fails, ensure your Workplace from Meta account has Admin permissions and try again.

    ![Screenshot shows Admin Credentials dialog box with an Authorize option.](media/workplace-by-facebook-provisioning-tutorial/provisionings.png)

    ![Screenshot of Authorize.](media/workplace-by-facebook-provisioning-tutorial/workplace-login.png)

    Note

    Failure to change the URL to `https://scim.workplace.com/` results in a failure when trying to save the configuration
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Workplace from Meta in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Workplace from Meta for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Workplace from Meta API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | userName | String |
    | displayName | String |
    | active | Boolean |
    | title | Boolean |
    | emails[type eq "work"].value | String |
    | name.givenName | String |
    | name.familyName | String |
    | name.formatted | String |
    | addresses[type eq "work"].formatted | String |
    | addresses[type eq "work"].streetAddress | String |
    | addresses[type eq "work"].locality | String |
    | addresses[type eq "work"].region | String |
    | addresses[type eq "work"].country | String |
    | addresses[type eq "work"].postalCode | String |
    | addresses[type eq "other"].formatted | String |
    | phoneNumbers[type eq "work"].value | String |
    | phoneNumbers[type eq "mobile"].value | String |
    | phoneNumbers[type eq "fax"].value | String |
    | externalId | String |
    | preferredLanguage | String |
    | urn:scim:schemas:extension:enterprise:1.0.manager | String |
    | urn:scim:schemas:extension:enterprise:1.0.department | String |
    | urn:scim:schemas:extension:enterprise:1.0.division | String |
    | urn:scim:schemas:extension:enterprise:1.0.organization | String |
    | urn:scim:schemas:extension:enterprise:1.0.costCenter | String |
    | urn:scim:schemas:extension:enterprise:1.0.employeeNumber | String |
    | urn:scim:schemas:extension:facebook:auth\_method:1.0:auth\_method | String |
    | urn:scim:schemas:extension:facebook:frontline:1.0.is\_frontline | Boolean |
    | urn:scim:schemas:extension:facebook:starttermdates:1.0.startDate | Integer |
12. To configure scoping filters, follow the steps in [Define conditional rules for provisioning user accounts](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a few users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Use the following guidance to monitor provisioning activity and verify that your deployment is working as expected:

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Troubleshooting tips

Use the following tips to diagnose and resolve common provisioning issues:

- If you see a user unsuccessfully created and there's an audit log event with the code "1789003", it means that the user is from an unverified domain.
- There are cases where users get an error 'ERROR: Missing Email field: You must provide an email Error returned from Facebook: Processing of the HTTP request resulted in an exception. See the HTTP response returned by the 'Response' property of this exception for details. This operation was retried zero times. The operation is retried again after this date.' This error is due to customers mapping mail, rather than userPrincipalName, to Facebook email, yet some users don't have a mail attribute. To avoid the errors and successfully provision the failed users to Workplace from Facebook, modify the attribute mapping to the Workplace from Facebook email attribute to Coalesce([mail],[userPrincipalName]) or unassign the user from Workplace from Facebook, or provision an email address for the user.
- There's an option in Workplace, which allows the existence of [users without email addresses.](https://www.workplace.com/resources/tech/account-management/email-less#enable) If this setting is toggled on the Workplace side, provisioning on the Azure side must be restarted in order for users without emails to successfully be created in Workplace.

## Update a Workplace from Meta application to use the Workplace from Meta SCIM 2.0 endpoint

In December 2021, Facebook released a SCIM 2.0 connector. Completing the steps in this section updates applications configured to use the SCIM 1.0 endpoint to use the SCIM 2.0 endpoint. These steps remove any customizations previously made to the Workplace from Meta application, including:

- Authentication details
- Scoping filters
- Custom attribute mappings

Note

Be sure to note any changes made to the settings listed in the previous section before completing the following steps. Failure to do so results in the loss of customized settings.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Workplace from Meta**.
3. In the Properties section of your new custom app, copy the Object ID.

    ![Screenshot of Workplace from Meta app in the Azure portal](media/workplace-by-facebook-provisioning-tutorial/app-properties.png)
4. In a new web browser window, go to https://developer.microsoft.com/graph/graph-explorer and sign in as the administrator for the Microsoft Entra tenant where your app is added.

    ![Screenshot of Microsoft Graph explorer sign in page](media/workplace-by-facebook-provisioning-tutorial/permissions.png)
5. Check to make sure the account being used has the correct permissions. The permission “Directory.ReadWrite.All” is required to make this change.

    ![Screenshot of Microsoft Graph settings option](media/workplace-by-facebook-provisioning-tutorial/permissions-2.png)

    ![Screenshot of Microsoft Graph permissions](media/workplace-by-facebook-provisioning-tutorial/permissions-3.png)
6. Using the Object ID copied in step 3 from the app's Properties section, run the following command to list the synchronization jobs configured for the service principal:

    ```http
    GET https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/
    ```
7. Taking the "id" value from the response body of the `GET` request in the previous step, run the following command, replacing "[job-id]" with the id value from the `GET` request. The value should have the format of "FacebookAtWorkOutDelta.xxxxxxxxxxxxxxx.xxxxxxxxxxxxxxx":

    ```http
    DELETE https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[job-id]
    ```
8. In the Microsoft Graph Explorer, run the following command to create a new synchronization job using the FacebookWorkplace template. Replace "[object-id]" with the service principal Object ID you copied from the app's Properties section.

    ```http
    POST https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs { "templateId": "FacebookWorkplace" }
    ```

    ![Screenshot of Microsoft Graph request](media/workplace-by-facebook-provisioning-tutorial/graph-request.png)
9. Return to the first web browser window and select the Provisioning tab for your application. Your configuration is reset. You can confirm the upgrade is successful by confirming the Job ID starts with "FacebookWorkplace."
10. Update the tenant URL in the Admin Credentials section to the following URL: `https://scim.workplace.com/`

    ![Screenshot of Admin Credentials in the Workplace from Meta app in the Azure portal](media/workplace-by-facebook-provisioning-tutorial/provisionings.png)
11. Restore any previous changes you made to the application (Authentication details, Scoping filters, Custom attribute mappings) and re-enable provisioning.

    Note

    Failure to restore Authentication details, Scoping filters, and Custom attribute mappings might result in attributes (name.formatted for example) updating in Workplace unexpectedly. Be sure to check the configuration before enabling provisioning

## Change log

The following changes have been made to this integration guidance:

- 09/10/2020 - Added support for enterprise attributes "division", "organization", "costCenter" and "employeeNumber." Added support for custom attributes "startDate", "auth\_method" and "frontline."
- 07/22/2021 - Updated the troubleshooting tips for customers with a mapping of mail to Facebook mail yet some users don't have a mail attribute.