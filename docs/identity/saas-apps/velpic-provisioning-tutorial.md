---
layout: Conceptual
title: Configure Configuring Velpic for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/velpic-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Velpic.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 67f82338-6e63-df02-0e84-6f2429833021
document_version_independent_id: a3de909e-2415-9d15-199f-9cfa0b4cdbc0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/velpic-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/velpic-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/velpic-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 57065270-1c1e-1f4b-6065-cba91f3e34d1
---

# Configure Configuring Velpic for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show you the steps you need to perform in Velpic and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to Velpic.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following items:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
        - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
        - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
        - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Velpic tenant with the Enterprise plan or better enabled
- A user account in Velpic with Admin permissions

## Step 1: Assign users to Velpic

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID is synchronized.

Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Microsoft Entra ID represent the users who need access to your Velpic app. Once decided, you can assign these users to your Velpic app by following the instructions here:

[Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Velpic

- It's recommended that a single Microsoft Entra user be assigned to Velpic to test the provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Velpic, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog. The **Default Access** role doesn't work for provisioning, and these users are skipped.

## Step 2: Configure user provisioning to Velpic

This section guides you through connecting your Microsoft Entra ID to Velpic's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Velpic based on user and group assignment in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Velpic, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.

### Configure automatic user account provisioning to Velpic in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. If you have already configured Velpic for single sign-on, search for your instance of Velpic using the search field. Otherwise, select **Add** and search for **Velpic** in the application gallery. Select Velpic from the search results, and add it to your list of applications.
4. In the applications list, select **Velpic**.

    ![Screenshot of the Velpic link in the Applications list.](common/all-applications.png)
5. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
6. Select **+ New configuration**.

    ![Screenshot of New configuration.](common/application-provisioning.png)
7. Under the **Admin Credentials** section, enter the Tenant URL and Secret Token of Velpic.(You can find these values under your Velpic account: **Manage** &gt; **Integration** &gt; **Plugin** &gt; **SCIM**)

    ![Screenshot of Authorization Values.](media/velpic-provisioning-tutorial/velpic2.png)
8. Select **Test Connection** to ensure Microsoft Entra ID can connect to your Velpic app. If the connection fails, ensure your Velpic account has Admin permissions and try step 5 again.
9. Select **Create** to create your configuration.
10. Select **Properties** on the **Overview** page.
11. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
12. Select **Attribute Mapping** in the left panel and select **users**.
13. Review the user attributes that are synchronized from Microsoft Entra ID to Velpic. The attributes selected as **Matching** properties are used to match the user accounts in Velpic for update operations. Select the Save button to commit any changes.
14. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
15. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
16. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 3: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.