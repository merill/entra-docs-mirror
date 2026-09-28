---
layout: Conceptual
title: Configure Brivo Onair Identity Connector for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/brivo-onair-identity-connector-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Brivo Onair Identity Connector.
ms.topic: how-to
ms.date: 2026-02-27T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 46e5af7f-5a67-6a14-be20-96e02f030ff4
document_version_independent_id: c3c50976-d732-bf8b-5401-79f28c68b991
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/brivo-onair-identity-connector-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/brivo-onair-identity-connector-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/brivo-onair-identity-connector-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 75c65bc9-fae1-fb3a-ca00-ea891e621b6f
---

# Configure Brivo Onair Identity Connector for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Brivo Onair Identity Connector and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Brivo Onair Identity Connector.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Brivo Onair Identity Connector.
- Remove users in Brivo Onair Identity Connector when they don't require access anymore.
- Long lived bearer token authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Brivo Onair Identity Connector tenant](https://www.brivo.com/lp/quote)
- A user account in Brivo Onair Identity Connector with Senior Administrator permissions.

## Assigning users to Brivo Onair Identity Connector

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Brivo Onair Identity Connector. Once decided, you can assign these users and/or groups to Brivo Onair Identity Connector by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to Brivo Onair Identity Connector

- It's recommended that a single Microsoft Entra user is assigned to Brivo Onair Identity Connector to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Brivo Onair Identity Connector, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Setup Brivo Onair Identity Connector for provisioning

1. Sign in to your [Brivo Onair Identity Connector Admin Console](https://acs.brivo.com/login/). Navigate to **Account &gt; Account Settings**.

    ![Brivo Onair Identity Connector Admin Console](media/brivo-onair-identity-connector-provisioning-tutorial/admin.png)
2. Select **Microsoft Entra ID** tab. On the **Microsoft Entra ID** details page re-enter the password of your senior administrator account. Select **Submit**.

    ![Brivo Onair Identity Connector azure](media/brivo-onair-identity-connector-provisioning-tutorial/azuread.png)
3. Select **Copy Token** button and save the **Secret Token**. This value is entered in the Secret Token field in the Provisioning tab of your Brivo Onair Identity Connector application.

    ![Brivo Onair Identity Connector token](media/brivo-onair-identity-connector-provisioning-tutorial/token.png)

## Add Brivo Onair Identity Connector from the gallery

Before configuring Brivo Onair Identity Connector for automatic user provisioning with Microsoft Entra ID, you need to add Brivo Onair Identity Connector from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Brivo Onair Identity Connector from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Brivo Onair Identity Connector** in the search box.
4. Select **Brivo Onair Identity Connector** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configuring automatic user provisioning to Brivo Onair Identity Connector

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Brivo Onair Identity Connector based on user and/or group assignments in Microsoft Entra ID.

### To configure automatic user provisioning for Brivo Onair Identity Connector in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Brivo Onair Identity Connector**.

    ![The Brivo Onair Identity Connector link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Input `https://scim.brivo.com/ActiveDirectory/v2/` in **Tenant URL**. Input the **SCIM Authentication Token** value retrieved earlier in **Secret Token**. Select **Test Connection** to ensure Microsoft Entra ID can connect to Brivo Onair Identity Connector. If the connection fails, ensure your Brivo Onair Identity Connector account has Admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Brivo Onair Identity Connector in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Brivo Onair Identity Connector for update operations. Select the **Save** button to commit any changes.

    ![Brivo Onair Identity Connector User Attributes](media/brivo-onair-identity-connector-provisioning-tutorial/user-attributes.png)
12. Select **Groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Brivo Onair Identity Connector in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Brivo Onair Identity Connector for update operations. Select the **Save** button to commit any changes.

    ![Brivo Onair Identity Connector Group Attributes](media/brivo-onair-identity-connector-provisioning-tutorial/group-attributes.png)
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.