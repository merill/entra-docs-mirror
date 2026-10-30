---
layout: Conceptual
title: Configure Box for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/box-userprovisioning-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Box .
ms.topic: how-to
ms.date: 2026-03-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e60d73e2-2709-5f22-5d31-fc2bca7ede41
document_version_independent_id: e3b73f91-7660-0621-0df0-767ea6fe7cb7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/box-userprovisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/box-userprovisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/box-userprovisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9b820408-1b4e-d13d-3aa2-3472758d706b
---

# Configure Box for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show the steps you need to perform in Box and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to Box.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Box is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

To configure Microsoft Entra integration with Box, you need the following items:

- A Microsoft Entra tenant
- A Box Business plan or better

Note

When you test the steps in this article, we recommend that you do *not* use a production environment.

Note

Apps need to be enabled in the Box application first.

To test the steps in this article, follow these recommendations:

- don't use your production environment, unless it's necessary.
- If you don't have a Microsoft Entra trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## Step 1: Assign users to Box

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID is synchronized.

Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Microsoft Entra ID represent the users who need access to your Box app. Once decided, you can assign these users to your Box app by following the instructions here:

[Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

## Step 2: Assign users and groups

The **Box &gt; Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box. Assignment of a user or group causes the following things to occur:

- Microsoft Entra ID permits the assigned user (either by direct assignment or group membership) to authenticate to Box. If a user isn't assigned, then Microsoft Entra ID doesn't permit them to sign in to Box and returns an error on the Microsoft Entra sign-in page.
- An app tile for Box is added to the user's [application launcher](../enterprise-apps/end-user-experiences).
- If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.

    - If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.
    - If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups. The group and user memberships are preserved upon being written to Box.

You can use the **Attributes &gt; Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes &gt; Provisioning** tab to configure how user and group attributes flow from Microsoft Entra ID to Box during provisioning operations.

### Important tips for assigning users to Box

- It's recommended that a single Microsoft Entra user assigned to Box to test the provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to box, you must select a valid user role. The "Default Access" role doesn't work for provisioning.

## Step 3: Enable Automated User Provisioning

This section guides through connecting your Microsoft Entra ID to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Microsoft Entra ID.

If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.

- If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.
- If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups. The group and user memberships are preserved upon being written to Box.

Tip

You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.

### Configure automatic user account provisioning

The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. If you have already configured Box for single sign-on, search for your instance of Box using the search field. Otherwise, select **Add** and search for **Box** in the application gallery. Select Box from the search results, and add it to your list of applications.
4. Select your instance of Box, then select the **Provisioning** tab.
5. Select **+ New configuration**.

    ![Screenshot for the new configuration steps into the box.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, select **Authorize** to open a Box login dialog in a new browser window.
7. On the **Login to grant access to Box** page, provide the required credentials, and then select **Authorize**.

    ![Screenshot of the Log in to grant access to box screen, showing entry for Email and Password, and the Authorize button.](media/box-userprovisioning-tutorial/ic769546.png)
8. Select **Grant access to Box** to authorize this operation and to return to the Azure portal.

    ![Screenshot of the authorize access screen in Box, showing an explanatory message and the Grant access to Box button.](media/box-userprovisioning-tutorial/ic769549.png)
9. Select **Test Connection** to ensure Microsoft Entra ID can connect to your Box app. If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.
10. Select **Create** to create your configuration.
11. Select **Properties** in the **Overview** page.
12. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
13. Select **Attribute Mapping** in the left panel and select **users**.
14. In the **Attribute Mappings** section, review the user attributes that are synchronized from Microsoft Entra ID to Box. The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations. Select the Save button to commit any changes.
15. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
16. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
17. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.

![Integration status](media/box-userprovisioning-tutorial/ic769556.png)