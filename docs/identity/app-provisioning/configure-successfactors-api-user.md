---
layout: Conceptual
title: Configure SAP SuccessFactors API user - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/configure-successfactors-api-user
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: Learn how to configure an API user in SAP SuccessFactors that can be used for provisioning integrations.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.reviewer: cmmdesai
ms.custom: sap-successfactors, provisioning
locale: en-us
document_id: 3b9fe473-1a34-f26d-9a1c-23e45083482f
document_version_independent_id: 3b9fe473-1a34-f26d-9a1c-23e45083482f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/configure-successfactors-api-user.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/configure-successfactors-api-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/configure-successfactors-api-user.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 1d8552d4-d9a1-3fe2-3e0b-89a094f113c9
---

# Configure SAP SuccessFactors API user - Microsoft Entra ID | Microsoft Learn

A common requirement of all the SuccessFactors provisioning connectors is that they require credentials of a SuccessFactors account with the right permissions to invoke the SuccessFactors OData APIs. This section describes steps to create the service account in SuccessFactors and grant appropriate permissions.

## Create/identify API user account in SuccessFactors

Work with your SuccessFactors admin team or implementation partner to create or identify a user account in SuccessFactors to invoke the OData APIs. The username and password credentials of this account are required when configuring the provisioning apps in Microsoft Entra ID.

## Create an API permissions role

1. Sign in to SAP SuccessFactors with a user account that has access to the Admin Center.
2. Search for **Manage Permission Roles**, then select **Manage Permission Roles** from the search results.

    ![Screenshot of the Manage Permission Roles search result in the SAP SuccessFactors Admin Center.](media/configure-successfactors-api-user/manage-permission-roles.png)
3. From the Permission Role List, select **Create New**.

![Screenshot of the Create New button on the Permission Role List page.](media/configure-successfactors-api-user/create-new-permission-role-1.png)
4. Add a **Role Name** and **Description** for the new permission role. The name and description should indicate that the role is for API usage permissions.
5. Under Permission settings, select **Permission...**, then scroll down the permission list and select **Manage Integration Tools**. Check the box for **Allow Admin to Access to OData API through Basic Authentication**.

![Screenshot of the Manage Integration Tools permission with the Allow Admin to Access to OData API through Basic Authentication option selected.](media/configure-successfactors-api-user/manage-integration-tools.png)
6. Scroll down in the same box and select **Employee Central API**. Add permissions to read using ODATA API and edit using ODATA API. Select the edit option if you plan to use the same account for the Writeback to SuccessFactors scenario.

![Screenshot of the Employee Central API permissions showing read and edit using ODATA API options.](media/configure-successfactors-api-user/odata-read-write-perm.png)
7. In the same permissions box, go to **User Permissions** &gt; **Employee Data** and review the attributes that the service account can read from the SuccessFactors tenant. For example, to retrieve the **Username** attribute from SuccessFactors, ensure that "View" permission is granted for this attribute. Similarly review each attribute for view permission.

![Screenshot of the Employee Data user permissions list for reviewing view access to attributes.](media/configure-successfactors-api-user/review-employee-data-permissions.png)

    Note

    For the complete list of attributes retrieved by this provisioning app, see [SuccessFactors Attribute Reference](sap-successfactors-attribute-reference).
8. Select **Done**. Select **Save Changes**.

## Create a permission group for the API user

1. In the SuccessFactors Admin Center, search for **Manage Permission Groups**, then select **Manage Permission Groups** from the search results. 
![Screenshot of the Manage Permission Groups search result in the SAP SuccessFactors Admin Center.](media/configure-successfactors-api-user/manage-permission-groups.png)
2. From the Manage Permission Groups window, select **Create New**. 
![Screenshot of the Create New button on the Manage Permission Groups window.](media/configure-successfactors-api-user/create-new-group.png)
3. Add a Group Name for the new group. The group name should indicate that the group is for API users. 
![Screenshot of the Group Name field when creating a new permission group.](media/configure-successfactors-api-user/permission-group-name.png)
4. Add members to the group. For example, you could select **Username** from the People Pool dropdown menu and then enter the username of the API account that's used for the integration. 
![Screenshot of adding members to a permission group by selecting Username from the People Pool dropdown.](media/configure-successfactors-api-user/add-group-members.png)
5. Select **Done** to finish creating the Permission Group.

## Grant the permission role to the permission group

1. In SuccessFactors Admin Center, search for **Manage Permission Roles**, then select **Manage Permission Roles** from the search results.
2. From the **Permission Role List**, select the role that you created for API usage permissions.
3. Under **Grant this role to...**, select the **Add...** button.
4. Select **Permission Group...** from the dropdown menu, then select **Select...** to open the Groups window to search and select the group that you created.
5. Review the Permission Role grant to the Permission Group.
6. Select **Save Changes**.