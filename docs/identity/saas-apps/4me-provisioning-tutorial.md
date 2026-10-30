---
layout: Conceptual
title: Configure 4me for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/4me-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: mwongerapk
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to 4me.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ad809363-1cc8-7315-4c20-26d8966ab708
document_version_independent_id: e6e04c3c-5205-4d9a-24b5-001aae5286c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/4me-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/4me-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/4me-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 36f327f1-b2cc-cd33-3840-7bc3f1da456c
---

# Configure 4me for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in 4me and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to 4me.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

4me is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A 4me tenant](https://www.4me.com/)
- A user account in 4me with Admin permissions.

## Add 4me from the gallery

Before configuring 4me for automatic user provisioning with Microsoft Entra ID, you need to add 4me from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add 4me from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **4me**, select **4me** in the search box.
4. Select **4me** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![Screenshot of 4me in the results list.](common/search-new-app.png)

## Assigning users to 4me

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to 4me. Once decided, you can assign these users and/or groups to 4me by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to 4me

- It's recommended that a single Microsoft Entra user is assigned to 4me to test the automatic user provisioning configuration. Additional users and/or groups can be assigned later.
- When assigning a user to 4me, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Configuring automatic user provisioning to 4me

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in 4me based on user and/or group assignments in Microsoft Entra ID.

Tip

You can also choose to enable SAML-based single sign-on for 4me, following the instructions provided in the [4me single sign-on article.(4me-tutorial.md). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for 4me in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **4me**.

    ![Screenshot of The 4me link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. To retrieve the **Tenant URL** and **Secret Token** of your 4me account, follow the walkthrough as described in Step 6.
7. Sign in to your 4me Admin Console. Navigate to **Settings**.

    ![Screenshot of 4me Settings.](media/4me-provisioning-tutorial/4me01.png)

    Type in **apps** in the search bar.

    ![Screenshot of 4me apps.](media/4me-provisioning-tutorial/4me02.png)

    Open the **SCIM** dropdown to retrieve the Secret Token and the SCIM endpoint.

    ![Screenshot of 4me SCIM.](media/4me-provisioning-tutorial/4me03.png)
8. Upon populating the fields shown in Step 5, select **Test Connection** to ensure Microsoft Entra ID can connect to 4me. If the connection fails, ensure your 4me account has Admin permissions and try again.

    ![Screenshot of Token.](common/provisioning-testconnection-tenanturltoken.png)
9. Select **Create** to create your configuration.
10. Select **Properties** in the **Overview** page.
11. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
12. Select **Attribute Mapping** in the left panel and select users.
13. Review the user attributes that are synchronized from Microsoft Entra ID to 4me in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in 4me for update operations. Please ensure that [4me supports filtering](https://developer.xurrent.com/v1/scim/users/) on the matching attribute you have chosen. Select the **Save** button to commit any changes.

    ![Screenshot of 4me User attributes list.](media/4me-provisioning-tutorial/4me-user-attributes-first-part.png)![Screenshot of 4me User attributes list-2.](media/4me-provisioning-tutorial/4me-user-attributes-second-part.png)
14. Select **groups**.
15. Review the group attributes that are synchronized from Microsoft Entra ID to 4me in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in 4me for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of 4me Group attributes list.](media/4me-provisioning-tutorial/4me-group-attribute.png)
16. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
17. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
18. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Connector Limitations

- 4me has different SCIM endpoint URLs for test and production environments. The former ends with **.qa** while the latter ends with **.com**
- 4me generated Secret Tokens have an expiration date of a month from generation.
- 4me doesn’t support **HARD DELETE** of Users. SCIM users are never really deleted in 4me, instead the **active** attribute of the SCIM user is set to **false** and the related 4me person record is disabled.