---
layout: Conceptual
title: Configure Salesforce Sandbox for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/salesforce-sandbox-provisioning-tutorial
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
description: Learn the steps you need to perform in Salesforce Sandbox and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to Salesforce Sandbox.
ms.topic: how-to
ms.date: 2026-03-23T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1838df01-9725-c256-4ce8-239bb605d247
document_version_independent_id: 52bf593b-ef1e-cc7c-9c62-e438fe2d4e4f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/salesforce-sandbox-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/salesforce-sandbox-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/salesforce-sandbox-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ee1f1e33-0966-d584-f870-a347ed178efb
---

# Configure Salesforce Sandbox for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show you the steps you need to perform in Salesforce Sandbox and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to Salesforce Sandbox.

## Prerequisites

The scenario outlined in this article assumes that you already have the following items:

- A Microsoft Entra tenant.
- A valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education. You may use a free trial account for either service.
- A user account in Salesforce Sandbox with Team Admin permissions.

## Assigning users to Salesforce Sandbox

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling the provisioning service, you need to decide which users or groups in Microsoft Entra ID need access to your Salesforce Sandbox app. After you've made this decision, you can assign these users to your Salesforce Sandbox app by following the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Salesforce Sandbox

- It's recommended that a single Microsoft Entra user is assigned to Salesforce Sandbox to test the provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Salesforce Sandbox, you must select a valid user role. The "Default Access" role doesn't work for provisioning.

Note

The Salesforce Sandbox app will, by default, append a string to the username and email of the users provisioned. Usernames and Emails have to be unique across all of Salesforce so this is to prevent creating real user data in the sandbox which would prevent these users being provisioned to the production Salesforce environment

Note

This app imports custom roles from Salesforce Sandbox as part of the provisioning process, which the customer may want to select when assigning users.

## Enable automated user provisioning

This section guides you through connecting your Microsoft Entra ID to Salesforce Sandbox's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Microsoft Entra ID.

Tip

You may also choose to enabled SAML-based Single Sign-On for Salesforce Sandbox, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.

### Configure automatic user account provisioning

The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using the search field. Otherwise, select **Add** and search for **Salesforce Sandbox** in the application gallery. Select Salesforce Sandbox from the search results, and add it to your list of applications.
4. Select your instance of Salesforce Sandbox, then select the **Provisioning** tab.
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, provide the following configuration settings:

    1. In the **Admin Username** textbox, type a Salesforce Sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.
    2. In the **Admin Password** textbox, type the password for this account.
7. To get your Salesforce Sandbox security token, open a new tab and sign into the same Salesforce Sandbox admin account. On the top right corner of the page, select your name, and then select **Settings**.

    ![Screenshot shows the Settings link selected.](media/salesforce-sandbox-provisioning-tutorial/sf-my-settings.png)
8. On the left navigation pane, select **My Personal Information** to expand the related section, and then select **Reset My Security Token**.

    ![Screenshot shows Reset My Security Token selected from My Personal Information.](media/salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png)
9. On the **Reset Security Token** page, select the **Reset Security Token** button.

    ![Screenshot shows the Rest Security Token page, with explanatory text and the option to Reset Security Token](media/salesforce-sandbox-provisioning-tutorial/sf-reset-token.png)
10. Check the email inbox associated with this admin account. Look for an email from Salesforce Sandbox.com that contains the new security token.
11. Copy the token, go to your Microsoft Entra window, and paste it into the **Secret Token** field.
12. Select **Test Connection** to ensure Microsoft Entra ID can connect to your Salesforce Sandbox app.
13. Select **Create** to create your configuration.
14. Select **Properties** on the **Overview** page.
15. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
16. Select **Attribute Mapping** in the left panel and select **users**.
17. Review the user attributes that are synchronized from Microsoft Entra ID to Salesforce Sandbox. The attributes selected as **Matching** properties are used to match the user accounts in Salesforce Sandbox for update operations. Select the Save button to commit any changes.
18. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
19. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
20. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.