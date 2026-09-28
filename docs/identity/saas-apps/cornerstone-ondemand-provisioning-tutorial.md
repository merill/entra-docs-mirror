---
layout: Conceptual
title: Configure Cornerstone OnDemand for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cornerstone-ondemand-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to Cornerstone OnDemand.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 478935d3-ee72-f272-2c7f-c2d687a12cc9
document_version_independent_id: 1401622a-3bfd-a4fc-5dd4-63bcec18f52f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cornerstone-ondemand-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cornerstone-ondemand-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cornerstone-ondemand-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d234dc86-f591-4f06-b174-6714d2a30d8b
---

# Configure Cornerstone OnDemand for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article demonstrates the steps to perform in Cornerstone OnDemand and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and deprovision users or groups to Cornerstone OnDemand.

Warning

This provisioning integration is no longer supported. As a result of this, the provisioning functionality of the Cornerstone OnDemand application in the Microsoft Entra Enterprise App Gallery is removed soon. The application's SSO functionality will remain intact. Microsoft is working with Cornerstone to build a new modernized provisioning integration, but there are no timelines on when it's completed.

Note

This article describes a connector that's built on top of the Microsoft Entra user provisioning service. For information on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to software-as-a-service (SaaS) applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you have:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..

- A Cornerstone OnDemand tenant.
- A user account in Cornerstone OnDemand with admin permissions.

Note

The Microsoft Entra provisioning integration relies on the [Cornerstone OnDemand web service](https://www.cornerstoneondemand.com/). This service is available to Cornerstone OnDemand teams.

## Add Cornerstone OnDemand from the Azure Marketplace

Before you configure Cornerstone OnDemand for automatic user provisioning with Microsoft Entra ID, add Cornerstone OnDemand from the Marketplace to your list of managed SaaS applications.

To add Cornerstone OnDemand from the Marketplace, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type \*\***Cornerstone OnDemand** and select **Cornerstone OnDemand** from the result panel. To add the application, select **Add**.

    ![Cornerstone OnDemand in the results list](common/search-new-app.png)

## Assign users to Cornerstone OnDemand

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users or groups that were assigned to an application in Microsoft Entra ID are synchronized.

Before you configure and enable automatic user provisioning, decide which users or groups in Microsoft Entra ID need access to Cornerstone OnDemand. To assign these users or groups to Cornerstone OnDemand, follow the instructions in [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal).

### Important tips for assigning users to Cornerstone OnDemand

- We recommend that you assign a single Microsoft Entra user to Cornerstone OnDemand to test the automatic user provisioning configuration. You can assign more users or groups later.
- When you assign a user to Cornerstone OnDemand, select any valid application-specific role, if available, in the assignment dialog box. Users with the **Default Access** role are excluded from provisioning.

## Configure automatic user provisioning to Cornerstone OnDemand

This section guides you through the steps to configure the Microsoft Entra provisioning service. Use it to create, update, and disable users or groups in Cornerstone OnDemand based on user or group assignments in Microsoft Entra ID.

To configure automatic user provisioning for Cornerstone OnDemand in Microsoft Entra ID, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cornerstone OnDemand**.

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Cornerstone OnDemand**.

    ![The Cornerstone OnDemand link in the applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Cornerstone OnDemand Provisioning](media/cornerstone-ondemand-provisioning-tutorial/provisioningtab.png)
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, enter the admin username, admin password, and domain of your Cornerstone OnDemand's account:

    - In the **Admin Username** box, fill in the domain or username of the admin account on your Cornerstone OnDemand tenant. An example is contoso\admin.
    - In the **Admin Password** box, fill in the password that corresponds to the admin username.
    - In the **Domain** box, fill in the web service URL of the Cornerstone OnDemand tenant. For example, the service is located at `https://ws-[corpname].csod.com/feed30/clientdataservice.asmx`, and for Contoso the domain is `https://ws-contoso.csod.com/feed30/clientdataservice.asmx`.
7. In the **Tenant URL** field, enter your Cornerstone OnDemand Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to Cornerstone OnDemand. If the connection fails, ensure your Cornerstone OnDemand account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
8. Select **Create** to create your configuration.
9. Select **Properties** on the **Overview** page.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. Review the user attributes that are synchronized from Microsoft Entra ID to Cornerstone OnDemand in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Cornerstone OnDemand for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Cornerstone OnDemand API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    ![Cornerstone OnDemand Attribute Mappings](media/cornerstone-ondemand-provisioning-tutorial/usermappingattributes.png)
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Connector limitations

The Cornerstone OnDemand **Position** attribute expects a value that corresponds to the roles on the Cornerstone OnDemand portal. To get a list of valid **Position** values, go to **Edit User Record &gt; Organization Structure &gt; Position** in the Cornerstone OnDemand portal.

![Cornerstone OnDemand Provisioning Edit User Record](media/cornerstone-ondemand-provisioning-tutorial/useredit.png)

![Cornerstone OnDemand Provisioning Position](media/cornerstone-ondemand-provisioning-tutorial/userposition.png)

![Cornerstone OnDemand Provisioning position list](media/cornerstone-ondemand-provisioning-tutorial/postionid.png)