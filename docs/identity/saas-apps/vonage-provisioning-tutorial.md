---
layout: Conceptual
title: Configure Vonage for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/vonage-provisioning-tutorial
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
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Vonage.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4a6006f2-72f8-e9be-3138-5aee21ed2b36
document_version_independent_id: 1550a9cb-c20f-8dd2-9f28-034a24d9aac1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/vonage-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/vonage-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/vonage-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 09d10b10-9052-bd7d-884e-c8a56e88de14
---

# Configure Vonage for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Vonage and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users and groups to [Vonage](https://www.vonage.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities Supported

- Create users in Vonage.
- Remove users in Vonage when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Vonage.
- [Single sign-on](vonage-tutorial) to Vonage (recommended).
- Code Auth Grant flow authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A [Vonage](https://www.vonage.com/) tenant.
- A user account in Vonage with Admin permission(Account Super User).

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Vonage](../app-provisioning/customize-application-attributes).

## Step 2: Configure Vonage to support provisioning with Microsoft Entra ID

1. Log in to [Vonage admin portal](http://admin.vonage.com) with an admin user.

    ![Screenshot of Log in to vonage admin portal.](media/vonage-provisioning-tutorial/log-in.png)
2. Navigate to **Account &gt; Single Sign-On Settings** on the left side menu.

    ![Screenshot of Single sign on settings.](media/vonage-provisioning-tutorial/single-sign-on-settings.png)
3. Select **User Settings** tab, toggle **Enable SCIM user provisioning** ON and select **Save**.

![Screenshot of Enable scim.](media/vonage-provisioning-tutorial/enable-scim.png)

## Step 3: Add Vonage from the Microsoft Entra application gallery

Add Vonage from the Microsoft Entra application gallery to start managing provisioning to Vonage. If you have previously setup Vonage for SSO you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Vonage

Note

Any user that's added to Vonage must have first name, last name and email. Otherwise the integration will fail.

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Vonage based on user and/or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for Vonage in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Vonage**.

    ![Screenshot of Vonage link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
6. Before the next step make sure you're authorized as Account Super User. For checking if the user is an Account Super User perform login at [Vonage admin portal](http://admin.vonage.com). You should see on the top left side similar to the picture below.

    ![Screenshot of Provisioning tab user.](media/vonage-provisioning-tutorial/account-super-user.png)
7. In the **Admin Credentials** section, select Authorize, make sure that you enter your Account Super User credentials, if it doesn't ask you to enter credentials make sure that you logged in with the Account Super User (you can check it http://admin.vonage.com/ on the upper left side, bellow your name you need to see "Account Super User"). Select **Test Connection** to ensure Microsoft Entra ID can connect to Vonage. If the connection fails, ensure your Vonage account has Admin permissions and try again.

    ![Screenshot of Token.](media/vonage-provisioning-tutorial/authorize.png)
8. Select **Create** to create your configuration.
9. Select **Properties** on the **Overview** page.
10. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to Vonage in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Vonage for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Vonage API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | emails[type eq "work"].value | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.