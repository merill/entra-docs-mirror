---
layout: Conceptual
title: Configure DocuSign for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/docusign-provisioning-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and DocuSign.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: 814d6866-8de9-1924-981f-c2589f291bd7
document_version_independent_id: 580a9310-a775-1147-fc52-d92964b14984
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/docusign-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/docusign-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/docusign-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 30cd839c-ec12-31f8-e582-22d384d68fee
---

# Configure DocuSign for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show you the steps you need to perform in DocuSign and Microsoft Entra ID to automatically provision and de-provision user accounts from Microsoft Entra ID to DocuSign.

## Prerequisites

The scenario outlined in this article assumes that you already have the following items:

- A Microsoft Entra tenant.
- A DocuSign single sign-on enabled subscription.
- A user account in DocuSign with Team Admin permissions.

## Assigning users to DocuSign

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Microsoft Entra ID represent the users who need access to your DocuSign app. Once decided, you can assign these users to your DocuSign app by following the instructions here:

[Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to DocuSign

- It's recommended that a single Microsoft Entra user is assigned to DocuSign to test the provisioning configuration. Additional users may be assigned later.
- When assigning a user to DocuSign, you must select a valid user role. The "Default Access" role doesn't work for provisioning.

Note

Microsoft Entra ID doesn't support group provisioning with the Docusign application, only users can be provisioned.

## Enable User Provisioning

This section guides you through connecting your Microsoft Entra ID to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Microsoft Entra ID.

Tip

You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in the [Azure portal](https://portal.azure.com). Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.

### To configure user account provisioning:

The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field. Otherwise, select **Add** and search for **DocuSign** in the application gallery. Select DocuSign from the search results, and add it to your list of applications.
4. Select your instance of DocuSign, then select the **Provisioning** tab.
5. Select **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/provisioning-automatic.png)
6. In the **Tenant URL** field, input your DocuSign Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to DocuSign. If the connection fails, ensure your DocuSign account has the required admin permissions and try again.
7. Select **Properties** on the **Overview** page.
8. Select **Create** to create your configuration.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.
10. In the **Notification Email** field, enter the email address of a person who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
11. Select **Attribute Mapping** in the left panel and select **users**.
12. In the **Attribute Mappings** section, review the user attributes that are synchronized from Microsoft Entra ID to DocuSign. The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations. Select the Save button to commit any changes.
13. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
14. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Troubleshooting Tips

- Provisioning a role or permission profile for a user in Docusign can be accomplished by using an expression in your attribute mappings using the [switch](../app-provisioning/functions-for-customizing-application-data#switch) and [singleAppRoleAssignment](../app-provisioning/functions-for-customizing-application-data#singleapproleassignment) functions. For example, the expression below will provision the ID "8032066" when a user has the "DS Admin" role assigned in Microsoft Entra ID. It doesn't provision any permission profile if the user isn't assigned a role on the Microsoft Entra ID side. The ID can be retrieved from the DocuSign [portal](https://support.docusign.com/).

Switch(SingleAppRoleAssignment([appRoleAssignments])," ", "DS Admin", "8032066")