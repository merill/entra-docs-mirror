---
layout: Conceptual
title: Configure Templafy SAML2 for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/templafy-saml-2-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Templafy SAML2.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: 136dfb48-9625-2ec0-7999-de0cdffff99b
document_version_independent_id: 35623c2b-dc09-640d-1211-b9242fb430cd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/templafy-saml-2-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/templafy-saml-2-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/templafy-saml-2-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 253408ba-daa0-13b0-eed1-06c5cac04b64
---

# Configure Templafy SAML2 for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Templafy SAML2 and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Templafy SAML2.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Templafy SAML2.
- Remove users in Templafy SAML2 when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Templafy SAML2.
- Provision groups and group memberships in Templafy SAML2.
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [A Templafy tenant](https://www.templafy.com/pricing/).
- A user account in Templafy with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Templafy SAML2](../app-provisioning/customize-application-attributes).

## Assigning users to Templafy SAML2

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Templafy SAML2. Once decided, you can assign these users and/or groups to Templafy SAML2 by following the instructions [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

## Important tips for assigning users to Templafy SAML2

- It's recommended that a single Microsoft Entra user is assigned to Templafy SAML2 to test the automatic user provisioning configuration. More users and/or groups may be assigned later.
- When assigning a user to Templafy SAML2, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 2: Configure Templafy SAML2 to support provisioning with Microsoft Entra ID

Before configuring Templafy SAML2 for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on Templafy SAML2.

1. Sign in to your Templafy Admin Console. Select **Administration**.

    ![Screenshot of Templafy Admin Console.](media/templafy-saml-2-provisioning-tutorial/templafy-admin.png)
2. Select **Authentication Method**.

    ![Screenshot of the Templafy administration section with the Authentication method option called out.](media/templafy-saml-2-provisioning-tutorial/templafy-auth.png)
3. Copy the **SCIM Api-key** value. This value is entered in the **Secret Token** field in the Provisioning tab of your Templafy SAML2 application.

    ![A screenshot of the S C I M A P I key.](media/templafy-saml-2-provisioning-tutorial/templafy-token.png)

## Step 3: Add Templafy SAML2 from the gallery

To configure Templafy SAML2 for automatic user provisioning with Microsoft Entra ID, you need to add Templafy SAML2 from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Templafy SAML2 from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Templafy SAML2**, select **Templafy SAML2** in the search box.
4. Select **Templafy SAML2** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

    ![Screenshot of Templafy SAML2 in the results list.](common/search-new-app.png)

## Step 4: Configure automatic user provisioning to Templafy SAML2

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Templafy SAML2 based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Templafy, following the instructions provided in the [Templafy Single sign-on article](templafy-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### Configure automatic user provisioning for Templafy SAML2 in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Templafy SAML2**.

    ![Screenshot of Templafy SAML2 link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, enter `https://scim.templafy.com/scim` in **Tenant URL**. Enter the **SCIM API-key** value retrieved earlier in **Secret Token**. Select **Test Connection** to ensure Microsoft Entra ID can connect to Templafy. If the connection fails, ensure your Templafy account has Admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Templafy SAML2 in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the user accounts in Templafy SAML2 for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | displayName | String |  |
    | title | String |  |
    | preferredLanguage | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | phoneNumbers[type eq "work"].value | String |  |
    | phoneNumbers[type eq "mobile"].value | String |  |
    | phoneNumbers[type eq "fax"].value | String |  |
    | externalId | String |  |
    | addresses[type eq "work"].locality | String |  |
    | addresses[type eq "work"].postalCode | String |  |
    | addresses[type eq "work"].region | String |  |
    | addresses[type eq "work"].streetAddress | String |  |
    | addresses[type eq "work"].country | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |

    Note

    Schema Discovery feature is enabled for this application.
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Templafy SAML2 in the **Attribute Mappings** section. The attributes selected as **Matching** properties are used to match the groups in Templafy SAML2 for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | displayName | String | ✓ |
    | members | Reference |  |
    | externalId | String |  |

    Note

    Schema Discovery feature is enabled for this application.
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Change log

- 05/04/2023 - Added support for **Schema Discovery**.