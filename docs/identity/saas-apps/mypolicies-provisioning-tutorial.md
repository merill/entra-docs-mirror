---
layout: Conceptual
title: Configure myPolicies for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mypolicies-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to myPolicies.
ms.topic: how-to
ms.date: 2026-04-13T00:00:00.0000000Z
locale: en-us
document_id: e9fe2225-9701-9ce3-8903-954fcb735dd9
document_version_independent_id: 81b48111-7d46-0d0d-0a6c-3678baa2e9b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mypolicies-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mypolicies-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mypolicies-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e38284a7-b29a-02d6-e39e-f1907058377e
---

# Configure myPolicies for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in myPolicies and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to myPolicies.

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- - A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications)..
- [A myPolicies tenant](https://mypolicies.com/).
- A user account in myPolicies with Admin permissions.

## Assigning users to myPolicies

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been assigned to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to myPolicies. Once decided, you can assign these users and/or groups to myPolicies by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Important tips for assigning users to myPolicies

- It's recommended that a single Microsoft Entra user is assigned to myPolicies to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to myPolicies, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Set up myPolicies for provisioning

Before configuring myPolicies for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on myPolicies.

1. Reach out to your myPolicies representative at **support@mypolicies.com** to obtain the secret token needed to configure SCIM provisioning.
2. Save the token value provided by the myPolicies representative. This value is entered in the **Secret Token** field in the Provisioning tab of your myPolicies application.

## Add myPolicies from the gallery

To configure myPolicies for automatic user provisioning with Microsoft Entra ID, you need to add myPolicies from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add myPolicies from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **myPolicies**, select **myPolicies** in the search box.
4. Select **myPolicies** from results panel and then add the app. Wait a few seconds while the app is added to your tenant. ![myPolicies in the results list](common/search-new-app.png)

## Configuring automatic user provisioning to myPolicies

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in myPolicies based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for myPolicies, following the instructions provided in the [myPolicies Single sign-on article](mypolicies-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for myPolicies in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **myPolicies**.

    ![The myPolicies link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Provisioning tab in the myPolicies application.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the new application provisioning configuration page.](common/application-provisioning.png)
6. In the **Tenant URL** field, enter your myPolicies Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to myPolicies. If the connection fails, ensure your myPolicies account has the required admin permissions and try again.

    Note

    Enter `https://<myPoliciesCustomDomain>.mypolicies.com/scim` in the **Tenant URL** where `<myPoliciesCustomDomain>` is your myPolicies custom domain. You can retrieve your myPolicies customer domain from your URL. Example: `<demo0-qa>`.mypolicies.com.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of the Provisioning properties page.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to myPolicies in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in myPolicies for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the myPolicies API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | userName | String |
    | active | Boolean |
    | emails[type eq "work"].value | String |
    | name.givenName | String |
    | name.familyName | String |
    | name.formatted | String |
    | externalId | String |
    | addresses[type eq "work"].country | String |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | Reference |
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Connector limitations

- myPolicies always requires **userName**, **email** and **externalId**.
- myPolicies doesn't support hard deletes for user attributes.

## Change log

- 09/15/2020 - Added support for "country" attribute for Users.