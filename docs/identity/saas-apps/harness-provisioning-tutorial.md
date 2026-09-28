---
layout: Conceptual
title: Configure Harness for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/harness-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Harness.
ms.topic: how-to
ms.date: 2026-06-18T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7a8d293e-ffb2-a0a2-4c8c-e6594ae83ddb
document_version_independent_id: 56ac0f58-3eba-9302-bede-a0c8b2d169bf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/harness-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/harness-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/harness-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f1b6ec9d-ecac-8b4b-681b-a76e480b0e3c
---

# Configure Harness for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article explains how to configure Microsoft Entra ID to automatically provision and deprovision users or groups to Harness. Automatic provisioning eliminates manual user management by synchronizing user lifecycle changes from your identity provider to Harness.

Note

This article describes a connector that is built on top of the Microsoft Entra user provisioning service. For information about this service, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Harness tenant](https://harness.io/pricing/)
- A user account in Harness with *Admin* permissions

## Assign users to Harness

Before you configure provisioning, you must assign users or groups to the Harness application in Microsoft Entra ID. Microsoft Entra ID uses **assignments** to determine which users should receive access to selected applications. In the context of automatic user provisioning, only the users or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, decide which users or groups in Microsoft Entra ID need access to Harness. You can then assign these users or groups to Harness by following the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Recommendations for user assignment

Start with a small test group before you roll out provisioning to your entire organization. Assign a single Microsoft Entra user to Harness to test the automatic user provisioning configuration. After you verify that provisioning works correctly, you can assign additional users or groups.

When you assign a user to Harness, you must select a valid application-specific role (if available) in the **Assignment** dialog box. Users with the *Default Access* role are excluded from provisioning.

If you currently have a Harness App Integration setup in Microsoft Entra ID and are now trying to set up one for Harness, ensure that the user information is also included in the App Integration before you attempt to log into Harness through SSO.

## Set up Harness for provisioning

You must generate a SCIM API token in Harness before you can configure provisioning in Microsoft Entra ID. This token allows Microsoft Entra ID to securely connect to the Harness SCIM endpoint and provision users.

1. Sign in to your [Harness Admin Console](https://app.harness.io/auth/#/signin), select your profile at the bottom left corner of the page, and go to **Profile Overview**.

    ![Screenshot of the Harness Admin Console with the profile menu used to open Profile Overview.](media/harness-provisioning-tutorial/admin.png)
2. Under **My API Keys**, select **+API Key**. The window to create an API key opens.

    ![Screenshot of the Harness Profile Overview page showing the +API Key button under My API Keys.](media/harness-provisioning-tutorial/apikeys.png)
3. Specify a **Name** and select **Save**. Harness creates an API key for your account.

    ![Screenshot of the Harness new API key dialog with the Name box and Save button.](media/harness-provisioning-tutorial/addkey.png)
4. To create a token for your API key, select **+Token** under your newly created API key.

    a. Provide a name and select **Generate token**.

    b. Copy the token value to a safe location. You'll need this token to configure the connection in Microsoft Entra ID.

    c. Select **Close**.

    ![Screenshot of the Harness token dialog showing the Generate token and Close buttons.](media/harness-provisioning-tutorial/api-token.png)

## Add Harness from the gallery

You must add the Harness application from the Microsoft Entra application gallery before you can configure automatic user provisioning. This registers Harness as a managed SaaS application in your Microsoft Entra tenant.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![The &quot;All applications&quot; link](common/enterprise-applications.png)
3. To add a new application, select the **New application** button at the top of the pane.

    ![The &quot;New application&quot; button](common/add-new-app.png)
4. In the search box, enter **Harness**, select **Harness** in the results list, and then select the **Add** button to add the application.

    ![Screenshot of the Microsoft Entra gallery search results with Harness selected and the Add button.](media/harness-provisioning-tutorial/search-new-app.png)

## Configure automatic user provisioning to Harness

After you add Harness from the gallery and generate a SCIM token, you can configure the provisioning connection. This section walks through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users or groups in Harness based on user or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Harness by following the instructions in the [Harness single sign-on article](harness-tutorial). You can configure single sign-on independent of automatic user provisioning, although these two features complement each other.

Note

To learn more about the Harness SCIM endpoint, see the Harness [API Keys](https://developer.harness.io/docs/platform/automation/api/add-and-manage-api-keys/) article.

To configure automatic user provisioning for Harness in Microsoft Entra ID, do the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Harness**.

    ![The Harness link in the applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under **Admin Credentials**, do the following:

    ![Tenant URL + Token](common/provisioning-testconnection-tenanturltoken.png)

    - In the **Tenant URL** box, enter **`https://app.harness.io/gateway/api/scim/account/<your_harness_account_ID>`**. You can obtain your Harness account ID from the URL in your browser when you are logged into Harness.
    - In the **Secret Token** box, enter the SCIM Authentication Token value that you saved in step 3 of the "Set up Harness for provisioning" section.
    - Select **Test Connection** to ensure that Microsoft Entra ID can connect to Harness. If the connection fails, ensure that your Harness account has *Admin* permissions, and then try again.

        ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Harness in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Harness for update operations. Select the **Save** button to commit any changes.

    ![Harness user &quot;Attribute Mappings&quot; pane](media/harness-provisioning-tutorial/userattributes.png)
12. Under **Mappings**, select **Synchronize Microsoft Entra groups to Harness**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Harness in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Harness for update operations. Select the **Save** button to commit any changes.

    ![Harness group &quot;Attribute Mappings&quot; pane](media/harness-provisioning-tutorial/groupattributes.png)
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you are ready to provision, select **Start Provisioning** from the **Overview** page.

## Monitor your deployment

After you start provisioning, monitor the provisioning logs to verify that users and groups sync correctly between Microsoft Entra ID and Harness.

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.