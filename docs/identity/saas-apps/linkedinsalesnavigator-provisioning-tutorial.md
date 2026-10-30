---
layout: Conceptual
title: Configure LinkedIn Sales Navigator for automatic user provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/linkedinsalesnavigator-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to LinkedIn Sales Navigator.
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 81b15ebd-eca1-f311-00fc-1a9abe364ab8
document_version_independent_id: 25623b8b-214f-852a-ee78-7b6d7e182924
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/linkedinsalesnavigator-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/linkedinsalesnavigator-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/linkedinsalesnavigator-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aec7dc3e-0dad-4b82-accf-63218d8767d5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f260444a-7ec6-4768-8e41-ad2438092724
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5ef81bda-71d6-4820-e508-12489d2b78ac
---

# Configure LinkedIn Sales Navigator for automatic user provisioning - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show you the steps you need to perform in LinkedIn Sales Navigator and Microsoft Entra ID to automatically provision and deprovision user accounts from Microsoft Entra ID to LinkedIn Sales Navigator.

## Prerequisites

The scenario outlined in this article assumes that you already have the following items:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A LinkedIn Sales Navigator tenant
- An administrator account in LinkedIn Sales Navigator with access to the LinkedIn Account Center

Note

Microsoft Entra ID integrates with LinkedIn Sales Navigator using the SCIM protocol.

## Assigning users to LinkedIn Sales Navigator

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID is synchronized.

Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Microsoft Entra ID represent the users who need access to LinkedIn Sales Navigator. Once decided, you can assign these users to LinkedIn Sales Navigator by following the instructions here:

[Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to LinkedIn Sales Navigator

- It's recommended that a single Microsoft Entra user be assigned to LinkedIn Sales Navigator to test the provisioning configuration. Additional users and/or groups might be assigned later.
- When assigning a user to LinkedIn Sales Navigator, you must select the **User** role in the assignment dialog. The "Default Access" role doesn't work for provisioning.

## Configuring user provisioning to LinkedIn Sales Navigator

This section guides you through connecting your Microsoft Entra ID to LinkedIn Sales Navigator's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Microsoft Entra ID.

Tip

You might also choose to enable SAML-based single sign-on for LinkedIn Sales Navigator, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.

### To configure automatic user account provisioning to LinkedIn Sales Navigator in Microsoft Entra ID:

The first step is to retrieve your LinkedIn access token. If you're an Enterprise administrator, you can self-provision an access token. In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.

Note

If you're accessing the account center directly rather than through a link, you can reach it using the following steps.

1. Sign in to Account Center.
2. Select **Admin** &gt; **Admin Settings** .
3. Select **Advanced Integrations** on the left sidebar. You're directed to the account center.
4. Select **+ Add new SCIM configuration** and follow the procedure by filling in each field.

    Note

    When auto-assign licenses option isn't enabled, it means that only user data is synced.

    ![Screenshot shows the LinkedIn Account Center Global Settings.](media/linkedinsalesnavigator-provisioning-tutorial/linkedin_1.png)

    Note

    When auto-license assignment is enabled, you need to note the application instance and license type. Licenses are assigned on a first come, first serve basis until all the licenses are taken.

    ![Screenshot shows the S C I M Setup page.](media/linkedinsalesnavigator-provisioning-tutorial/linkedin_2.png)
5. Select **Generate token**. You should see your access token display under the **Access token** field.
6. Save your access token to your clipboard or computer before leaving the page.
7. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
8. Browse to **Entra ID** &gt; **Enterprise apps**
9. If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using the search field. Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in the application gallery. Select LinkedIn Sales Navigator from the search results, and add it to your list of applications.
10. Select your instance of LinkedIn Sales Navigator, select the **Provisioning** tab.

    ![Provisioning tab](common/provisioning.png)
11. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
12. Fill in the following fields under **Admin Credentials** :

    - In the **Tenant URL** field, enter https://developer.linkedin.com.
    - In the **Secret Token** field, enter the access token you generated in step 1 and select **Test Connection** .
    - You should see a success notification on the upper-right side of your portal.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
13. Select **Create** to create your configuration.
14. Select **Properties** on the **Overview** page.
15. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
16. Select **Attribute Mapping** in the left panel and select **users**.
17. Review the user and group attributes that's synchronized from Microsoft Entra ID to LinkedIn Sales Navigator. The attributes selected as **Matching** properties are used to match the user accounts and groups in LinkedIn Sales Navigator for update operations. Select the Save button to commit any changes.

    ![Screenshot shows Mappings, including Attribute Mappings.](media/linkedinsalesnavigator-provisioning-tutorial/linkedin_4.png)
18. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
19. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
20. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.