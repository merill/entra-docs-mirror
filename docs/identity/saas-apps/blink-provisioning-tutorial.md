---
layout: Conceptual
title: Configure Blink for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/blink-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Blink.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
locale: en-us
document_id: 24212d88-f106-1c80-c356-f94873739e03
document_version_independent_id: ae257daf-f007-971c-a02d-47e54db0ff43
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/blink-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/blink-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/blink-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d002ee75-5a23-f79a-46bc-d8c0da5307ce
---

# Configure Blink for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Blink and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users to Blink.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Blink is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Capabilities supported

- Create users in Blink.
- Remove users in Blink when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Blink.
- [Single sign-on](blink-tutorial) to Blink (recommended).
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Blink tenant](https://joinblink.com/pricing)
- A user account in Blink with Admin permissions.

## Assigning users to Blink

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or group members that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or group members in Microsoft Entra ID need access to Blink. Once decided, you can assign these users and/or groups to Blink by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to Blink

- It's recommended that a single Microsoft Entra user is assigned to Blink to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Blink, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Setup Blink for provisioning

1. Log a [Support Case](https://support.joinblink.com) or email **Blink support** at support@joinblink.com to request a SCIM token.
2. Copy the **SCIM Authentication Token**. This value is entered in the Secret Token field in the Provisioning tab of your Blink application.

## Add Blink from the gallery

Before configuring Blink for automatic user provisioning with Microsoft Entra ID, you need to add Blink from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Blink from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Blink**, select **Blink** in the search box.
4. Select **Blink** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Blink in the results list](common/search-new-app.png)

## Configuring automatic user provisioning to Blink

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in Blink based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Blink, following the instructions provided in the [Blink Single sign-on article](blink-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other

### To configure automatic user provisioning for Blink in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Blink**.

    ![The Blink link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Blink Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Blink. If the connection fails, ensure your Blink account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Blink in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Blink for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering |
    | --- | --- | --- |
    | userName | String | ✓ |
    | active | Boolean |  |
    | title | String |  |
    | emails[type eq "work"].value | String |  |
    | name.givenName | String |  |
    | name.familyName | String |  |
    | phoneNumbers[type eq "work"].value | String |  |
    | phoneNumbers[type eq "mobile"].value | String |  |
    | externalId | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |  |
    | urn:ietf:params:scim:schemas:extension:blink:2.0:User:company | String |  |
    | urn:ietf:params:scim:schemas:extension:blink:2.0:User:description | String |  |
    | urn:ietf:params:scim:schemas:extension:blink:2.0:User:location | String |  |
12. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you've configured provisioning, use the following resources to monitor your deployment:

- Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users have been provisioned successfully or unsuccessfully
- Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
- If the provisioning configuration seems to be in an unhealthy state, the application will go into quarantine. Learn more about quarantine states [here](../app-provisioning/application-provisioning-quarantine-status).

## Change log

- 01/14/2021 - Custom extension attributes **company**, **description**, and **location** have been added.