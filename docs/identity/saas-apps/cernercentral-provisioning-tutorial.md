---
layout: Conceptual
title: Configure Cerner Central for automatic user provisioning in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cernercentral-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision users to a roster in Cerner Central.
ms.topic: how-to
ms.date: 2026-03-03T00:00:00.0000000Z
locale: en-us
document_id: 9d81852c-8939-2a3b-bff3-7041700b994e
document_version_independent_id: 643bc0e1-f80c-b437-139e-4277f8f8c05d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cernercentral-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cernercentral-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cernercentral-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 78b62210-02bc-2d8e-a841-af9431aaf63b
---

# Configure Cerner Central for automatic user provisioning in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show you the steps you need to perform in Cerner Central and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to a user roster in Cerner Central.

## Prerequisites

The scenario outlined in this article assumes that you already have the following items:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Cerner Central tenant

Note

Microsoft Entra ID integrates with Cerner Central using the SCIM protocol.

## Assigning users to Cerner Central

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling the provisioning service, you should decide what users and/or groups in Microsoft Entra ID represent the users who need access to Cerner Central. Once decided, you can assign these users to Cerner Central by following the instructions here:

[Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Cerner Central

- It's recommended that a single Microsoft Entra user be assigned to Cerner Central to test the provisioning configuration. Additional users and/or groups may be assigned later.
- Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster. Other Cerner solutions leverage this list of users in the user roster.
- When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog. Users with the "Default Access" role are excluded from provisioning.

## Configuring user provisioning to Cerner Central

This section guides you through connecting your Microsoft Entra ID to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Cerner Central, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other. For more information, see the [Cerner Central single sign-on article](cernercentral-tutorial).

### To configure automatic user account provisioning to Cerner Central in Microsoft Entra ID:

In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Microsoft Entra ID can use to connect to Cerner's SCIM endpoint. It's also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.

1. The first step is to ensure the people managing the Cerner and Microsoft Entra integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions. If necessary, use the URLs below to create CernerCare accounts in each applicable environment.

    - Sandbox: https://sandboxcernercare.com/accounts/create
    - Production: https://cernercare.com/accounts/create
2. Next, a system account must be created for Microsoft Entra ID. Use the instructions below to request a System Account for your sandbox and production environments.

    - Instructions: https://wiki.cerner.com/display/public/CernerCentral/Requesting+a+System+Account+in+System+Account+Management
    - Sandbox: https://sandboxcernercentral.com/system-accounts/
    - Production: https://cernercentral.com/system-accounts/
3. Next, generate an OAuth bearer token for each of your system accounts. To do this, follow the instructions below.

    - Instructions: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token
    - Sandbox: https://sandboxcernercentral.com/system-accounts/
    - Production: https://cernercentral.com/system-accounts/
4. Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration. For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.
5. Now you can configure Microsoft Entra ID to provision user accounts to Cerner. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
6. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
7. If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field. Otherwise, select **Add** and search for **Cerner Central** in the application gallery. Select Cerner Central from the search results, and add it to your list of applications.
8. Select your instance of Cerner Central, then select the **Provisioning** tab.
9. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)

    ![Screenshot of the Provisioning Mode dropdown list with the Automatic option called out.](common/provisioning-automatic.png)
10. Fill in the following fields under **Admin Credentials**:

    - In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.

> 
> Sandbox: `https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/`
> 
> Production: `https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/`

    - In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and select **Test Connection**.
    - You should see a success notification on the upper-right side of your portal.
11. Select **Create** to create your configuration.
12. Select **Properties** in the **Overview** page.
13. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
14. Select **Attribute Mapping** in the left panel and select **users**.
15. Review the user and group attributes to be synchronized from Microsoft Entra ID to Cerner Central. The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations. Select the Save button to commit any changes.
16. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
17. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
18. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.