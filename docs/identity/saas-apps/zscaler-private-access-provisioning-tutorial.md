---
layout: Conceptual
title: Configure Zscaler Private Access (ZPA) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-private-access-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Zscaler Private Access (ZPA).
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 48aa572a-2894-e17c-7b10-befb1760bc21
document_version_independent_id: 3c5e7d6a-3716-b104-7eec-0fc1d58fbc05
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-private-access-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-private-access-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-private-access-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b5e8351b-5b97-4498-38c2-a321f3037820
---

# Configure Zscaler Private Access (ZPA) for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Zscaler Private Access (ZPA) and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Zscaler Private Access (ZPA).

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Zscaler Private Access (ZPA) is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A Zscaler Private Access (ZPA) tenant](https://www.zscaler.com/pricing-and-plans#contact-us)
- A user account in Zscaler Private Access (ZPA) with Admin permissions.

## Step 1: Assign users to Zscaler Private Access (ZPA)

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Zscaler Private Access (ZPA). Once decided, you can assign these users and/or groups to Zscaler Private Access (ZPA) by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips to assign users to Zscaler Private Access (ZPA)

- It's recommended that a single Microsoft Entra user is assigned to Zscaler Private Access (ZPA) to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Zscaler Private Access (ZPA), you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Step 2: Set up Zscaler Private Access (ZPA) for provisioning

1. Sign in to your [Zscaler Private Access (ZPA) Admin Console](https://admin.private.zscaler.com/). Navigate to **Administration &gt; IdP Configuration**.

    ![Screenshot of Zscaler Private Access (ZPA) Admin Console.](media/zscaler-private-access-provisioning-tutorial/idpconfig.png)
2. Verify to make sure that an IdP for **Single sign-on** is configured. If no IdP is set up, then add one by selecting the plus icon at the top right corner of the screen.

    ![Screenshot of Zscaler Private Access (ZPA) Add SCIM.](media/zscaler-private-access-provisioning-tutorial/plusicon.png)
3. Follow through the **Add IdP Configuration** wizard to add an IdP. Leave the **Single sign-on** field set to **User**. Provide a **Name** and select the **Domains** from the drop-down list. Select **Next** to navigate to the next window.

    ![Screenshot of Zscaler Private Access (ZPA) Add IdP.](media/zscaler-private-access-provisioning-tutorial/addidp.png)
4. Download the **Service Provider Certificate**. Select **Next** to navigate to the next window.

    ![Screenshot of Zscaler Private Access (ZPA) SP certificate.](media/zscaler-private-access-provisioning-tutorial/spcertificate.png)
5. In the next window, upload the **Service Provider Certificate** downloaded previously.

    ![Screenshot of Zscaler Private Access (ZPA) upload certificate.](media/zscaler-private-access-provisioning-tutorial/uploadfile.png)
6. Scroll down to provide the **Single sign-On URL** and **IdP Entity ID**.

    ![Screenshot of Zscaler Private Access (ZPA) IdP ID.](media/zscaler-private-access-provisioning-tutorial/idpid.png)
7. Scroll down to **Enable SCIM Sync**. Select **Generate New Token** button. Copy the **Bearer Token**. This value is entered in the Secret Token field in the Provisioning tab of your Zscaler Private Access (ZPA) application.

    ![Screenshot of Zscaler Private Access (ZPA) Create Token.](media/zscaler-private-access-provisioning-tutorial/token.png)
8. To locate the **Tenant URL**, navigate to **Administration &gt; IdP Configuration**. Select the name of the newly added IdP configuration listed on the page.

    ![Screenshot of Zscaler Private Access (ZPA) Idp Name.](media/zscaler-private-access-provisioning-tutorial/idpname.png)
9. Scroll down to view the **SCIM Service Provider Endpoint** at the end of the page. Copy the **SCIM Service Provider Endpoint**. This value is entered in the Tenant URL field in the Provisioning tab of your Zscaler Private Access (ZPA) application.

    ![Screenshot of the Zscaler Private Access (ZPA) SCIM URL.](media/zscaler-private-access-provisioning-tutorial/tenanturl.png)

## Step 3: Add Zscaler Private Access (ZPA) from the gallery

Before configuring Zscaler Private Access (ZPA) for automatic user provisioning with Microsoft Entra ID, you need to add Zscaler Private Access (ZPA) from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Zscaler Private Access (ZPA) from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zscaler Private Access (ZPA)**, select **Zscaler Private Access (ZPA)** in the search box.
4. Select **Zscaler Private Access (ZPA)** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

    ![Screenshot of Zscaler Private Access (ZPA) in the results list.](common/search-new-app.png)

## Step 4: Configure automatic user provisioning to Zscaler Private Access (ZPA)

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Zscaler Private Access (ZPA) based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Zscaler Private Access (ZPA) by following the instructions provided in the [Zscaler Private Access (ZPA) Single sign-on article](zscalerprivateaccess-tutorial). Single sign-on can be configured independently of automatic user provisioning, although these two features complement each other.

Note

When users and groups are provisioned or de-provisioned we recommend to periodically restart provisioning to ensure that group memberships are properly updated. Doing a restart will force our service to re-evaluate all the groups and update the memberships.

Note

To learn more about Zscaler Private Access's SCIM endpoint, refer [this](https://www.zscaler.com/partners/microsoft).

### Configure automatic user provisioning for Zscaler Private Access (ZPA) in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler Private Access (ZPA)**.

    ![Screenshot of the Zscaler Private Access (ZPA) link in the Applications list.](common/all-applications.png)
3. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
4. Select **+ New configuration**.

    ![Screenshot of the New configuration option on the Provisioning page.](common/application-provisioning.png)
5. Under the **Admin Credentials** section, enter the **SCIM Service Provider Endpoint** value retrieved earlier in **Tenant URL**. Input the **Bearer Token** value retrieved earlier in **Secret Token**. Select **Test Connection** to ensure Microsoft Entra ID can connect to Zscaler Private Access (ZPA). If the connection fails, ensure your Zscaler Private Access (ZPA) account has Admin permissions and try again.

    ![Screenshot of the Provisioning test connection.](common/provisioning-testconnection-tenanturltoken.png)
6. Select **Create** to create your configuration.
7. Select **Properties** on the **Overview** page.
8. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
9. Select **Attribute Mapping** in the left panel and select **users**.
10. Review the user attributes that are synchronized from Microsoft Entra ID to Zscaler Private Access (ZPA) in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Zscaler Private Access (ZPA) for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Zscaler Private Access |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | externalId | String |  |  |
    | active | Boolean |  |  |
    | emails[type eq "work"].value | String |  |  |
    | name.givenName | String |  |  |
    | name.familyName | String |  |  |
    | displayName | String |  |  |
    | userType | String |  |  |
    | nickName | String |  |  |
    | title | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter | string |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |  |
11. Select **Groups**.
12. Review the group attributes that are synchronized from Microsoft Entra ID to Zscaler Private Access (ZPA) in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Zscaler Private Access (ZPA) for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Zscaler Private Access |
    | --- | --- | --- | --- |
    | displayName | String | ✓ | ✓ |
    | members | Reference |  |  |
    | externalId | String |  |  |
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 5: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.