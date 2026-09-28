---
layout: Conceptual
title: Create and manage a catalog of resources in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-catalog-create
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to create a new container of resources and access packages in entitlement management.
editor: HANKI
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
ms.reviewer: hanki
ms.custom: sfi-image-nochange
locale: en-us
document_id: 55d650b9-5110-e264-3126-9f9948a358fb
document_version_independent_id: e284037b-42b7-3b59-6efb-63b7b0155868
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-catalog-create.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-catalog-create
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-catalog-create.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: f5d6cb23-fef6-9505-f522-e8abb6cac60a
---

# Create and manage a catalog of resources in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

This article shows you how to create and manage a catalog of resources and access packages in entitlement management. Catalogs are also used in [access reviews (preview)](catalog-access-reviews).

## Create a catalog

A catalog is a container of resources and access packages. You create a catalog when you want to group related resources and access packages. An administrator can create a catalog. In addition, a user delegated to the [catalog creator](entitlement-management-delegate) role can create a catalog for resources that they own. A nonadministrator who creates the catalog becomes the first catalog owner. A catalog owner can add more users, groups of users, or application service principals as catalog owners.

To create a catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog creator. Identities who were assigned the User Administrator role will no longer be able to create catalogs or manage access packages in a catalog they don't own. If identities in your organization were assigned the User Administrator role to configure catalogs, access packages, or policies in entitlement management, you should instead assign these identities the Identity Governance Administrator role.
2. Browse to **ID Governance** &gt; **Catalogs**.

    ![Screenshot that shows entitlement management catalogs in the Microsoft Entra admin center.](media/entitlement-management-catalog-create/catalogs.png)
3. Select **New catalog**.
4. Enter a unique name for the catalog and provide a description.

    Users see this information in an access package's details.
5. If you want the access packages in this catalog to be available for users to request as soon as they're created, set **Enabled** to **Yes**.
6. If you want to allow users in external directories from connected organizations to be able to request access packages in this catalog, set **Enabled for external users** to **Yes**. The access packages must also have a policy allowing users from connected organizations to request. If the access packages in this catalog are intended only for users already in the directory, then set **Enabled for external users** to **No**.

    Note

    This setting controls whether external users can **request** access packages through self-service. This setting isn't required for administrators to [directly assign](entitlement-management-access-package-assignments) external users to an access package, which is controlled by the access package's policy.

    ![Screenshot that shows the New catalog pane.](media/entitlement-management-shared/new-catalog.png)
7. Select **Create** to create the catalog.

## Create a catalog programmatically

There are two ways to create a catalog programmatically.

### Create a catalog with Microsoft Graph

You can create a catalog by using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission, or an application with the `EntitlementManagement.ReadWrite.All` application permission, can call the API to [create a catalog](/en-us/graph/api/entitlementmanagement-post-catalogs?view=graph-rest-1.0&amp;preserve-view=true).

### Create a catalog with PowerShell

You can also create a catalog in PowerShell with the `New-MgEntitlementManagementCatalog` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.2.0 or later.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"
$catalog = New-MgEntitlementManagementCatalog -DisplayName "Marketing"
```

## Add resources to a catalog

To include resources in an access package, the resources must exist in a catalog. The types of resources you can add to a catalog for use in access packages include groups, applications, SharePoint Online sites, and (in preview) SAP IAG resources.

- Groups can be cloud-created Microsoft 365 Groups or cloud-created Microsoft Entra security groups.

    - Groups that originate in an on-premises Active Directory can't be assigned as resources because their owner or member attributes can't be changed in Microsoft Entra ID. To give a user access to an application that uses AD security group memberships, you can either change the source of authority of an existing group configure it for group writeback, or create a new security group in Microsoft Entra ID, configure [group writeback to AD](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory), and [enable that group to be written to AD](entitlement-management-group-writeback), so that the cloud-created group can be used by an AD-based application.
    - Groups that originate in Exchange Online as Distribution groups can't be modified in Microsoft Entra ID either, so they can't be added to catalogs.
- Applications can be Microsoft Entra enterprise applications, which include software as a service (SaaS) applications, on-premises applications, and your own applications integrated with Microsoft Entra ID.

    - If your application hasn't yet been integrated with Microsoft Entra ID, see [govern access for applications in your environment](identity-governance-applications-prepare) and [integrate an application with Microsoft Entra ID](identity-governance-applications-integrate) and add the application to your directory prior to adding it to the catalog.
    - For more information on how to select appropriate resources for applications with multiple roles, see [how to determine which resource roles to include in an access package](entitlement-management-access-package-resources#determine-which-resource-roles-to-include-in-an-access-package).
- Sites can be SharePoint Online sites or SharePoint Online site collections.

Note

Search SharePoint Site by site name or an exact URL as the search box is case sensitive.

- [Catalog access reviews (preview)](catalog-access-reviews) also allow [custom data provided resources](custom-data-resource-access-reviews) to be included in a catalog.

\*\*Prerequisite roles:\*\*See [Required roles to add resources to a catalog](entitlement-management-delegate#required-roles-to-add-resources-to-a-catalog).

To add resources to a catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to add resources to.
4. On the left menu, select **Resources**.
5. Select **Add resources**.
6. Select the resource type **Groups and Teams**, **Applications**, or **SharePoint sites**.

    If you don't see a resource that you want to add or you're unable to add a resource, make sure you have the required Microsoft Entra directory role and entitlement management role. You might need to have someone with the required roles add the resource to your catalog. For more information, see [Required roles to add resources to a catalog](entitlement-management-delegate#required-roles-to-add-resources-to-a-catalog).
7. Select one or more resources of the type that you want to add to the catalog.

    ![Screenshot that shows the Add resources to a catalog pane.](media/entitlement-management-catalog-create/catalog-add-resources.png)
8. When you finish, select **Add**.

    These resources can now be included in access packages within the catalog.

### Add resource attributes in the catalog

Attributes are required fields that requestors are asked to answer before they submit their access request. Their answers for these attributes are shown to approvers and also stamped on the user object in Microsoft Entra ID.

Note

All attributes set up on a resource require an answer before a request for an access package containing that resource can be submitted. If requestors don't provide an answer, their request won't be processed.

To require attributes for access requests:

1. Select **Resources** on the left menu, and a list of resources in the catalog appears.
2. Select the ellipsis next to the resource where you want to add attributes, and then select **Require attributes**.

    ![Screenshot that shows selecting Require attributes](media/entitlement-management-catalog-create/resources-require-attributes.png)
3. Select the attribute type:

    1. **Built-in** includes Microsoft Entra user profile attributes.
    2. **Directory schema extension** provides a way to store more data in Microsoft Entra users. You can extend the schema by [creating an extension attribute](../identity/app-provisioning/user-provisioning-sync-attributes-for-mapping#create-an-extension-attribute-in-a-tenant-with-cloud-only-users). These extension attributes on user objects can be used to send out claims to applications during provisioning or single-sign on.
4. If you chose **Built-in**, select an attribute from the dropdown list. If you chose **Directory schema extension**, enter the attribute name in the text box.

    Note

    The User.mobilePhone attribute is a sensitive property that can be updated only by some administrators. Learn more at [Who can update sensitive user attributes?](/en-us/graph/api/resources/users#who-can-update-sensitive-attributes).
5. Select the answer format you want requestors to use for their answer. Answer formats include **short text**, **multiple choice**, and **long text**.
6. If you select multiple choice, select **Edit and localize** to configure the answer options.

    1. In the **View/edit question** pane that appears, enter the response options you want to give the requestor when they answer the question in the **Answer values** boxes.
    2. Select the language for the response option. You can localize response options if you choose more languages.
    3. Enter as many responses as you need, and then select **Save**.
7. If you want the attribute value to be editable during direct assignments and self-service requests, select **Yes**.

    Note

    ![Screenshot that shows making attributes editable.](media/entitlement-management-catalog-create/attributes-are-editable.png)

    - If you select **No** in the **Attribute value is editable** box and the attribute value *is empty*, users can enter the value of that attribute. After saving, the value can't be edited.
    - If you select **No** in the **Attribute value is editable** box and the attribute value *isn't empty*, users can't edit the preexisting value during direct assignments and self-service requests.

    ![Screenshot that shows adding localizations.](media/entitlement-management-catalog-create/add-attributes-questions.png)
8. If you want to add localization, select **Add localization**.

    1. In the **Add localizations for question** pane, select the language code for the language in which you want to localize the question related to the selected attribute.
    2. In the language you configured, enter the question in the **Localized Text** box.
    3. After you add all the localizations you need, select **Save**.

        ![Screenshot that shows saving the localizations.](media/entitlement-management-catalog-create/attributes-add-localization.png)
9. After all attribute information is completed on the **Require attributes** page, select **Save**.

### Add a Multi-Geo SharePoint site

1. If you have [Multi-Geo](/en-us/microsoft-365/enterprise/multi-geo-capabilities-in-onedrive-and-sharepoint-online-in-microsoft-365) enabled for SharePoint, select the environment you want to select sites from.

    ![Screenshot that shows the Select SharePoint Online sites pane.](media/entitlement-management-catalog-create/sharepoint-multi-geo-select.png)
2. Then select the sites you want to be added to the catalog.

### Add a resource to a catalog programmatically

You can also add a resource to a catalog by using Microsoft Graph. A user in an appropriate role, or a catalog and resource owner, with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission can call the API to [create a resourceRequest](/en-us/graph/api/entitlementmanagement-post-resourcerequests?view=graph-rest-1.0&amp;preserve-view=true). An application with the application permission `EntitlementManagement.ReadWrite.All` and permissions to change resources, such as `Group.ReadWrite.All`, can also add resources to the catalog.

### Add a resource to a catalog with PowerShell

You can also add a resource to a catalog in PowerShell with the `New-MgEntitlementManagementResourceRequest` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.1.x or later module version. The following example shows how to add a group to a catalog as a resource using Microsoft Graph PowerShell cmdlets module version 2.4.0.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All,Group.ReadWrite.All"

$g = Get-MgGroup -Filter "displayName eq 'Marketing'"
if ($null -eq $g) {throw "no group" }

$catalog = Get-MgEntitlementManagementCatalog -Filter "displayName eq 'Marketing'"
if ($null -eq $catalog) { throw "no catalog" }
$params = @{
  requestType = "adminAdd"
  resource = @{
    originId = $g.Id
    originSystem = "AadGroup"
  }
  catalog = @{ id = $catalog.id }
}

New-MgEntitlementManagementResourceRequest -BodyParameter $params
sleep 5
$ar = Get-MgEntitlementManagementCatalog -AccessPackageCatalogId $catalog.Id -ExpandProperty resources
$ar.resources
```

## Remove resources from a catalog

You can remove resources from a catalog. A resource can be removed from a catalog only if it isn't being used in any of the catalog's access packages.

**Prerequisite roles:** See [Required roles to add resources to a catalog](entitlement-management-delegate#required-roles-to-add-resources-to-a-catalog).

To remove resources from a catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to remove resources from.
4. On the left menu, select **Resources**.
5. Select the resources you want to remove.
6. Select **Remove**. Optionally, select the ellipsis (**...**) and then select **Remove resource**.

## Add more catalog owners

The user who created a catalog becomes the first catalog owner. To delegate management of a catalog, add users to the catalog owner role. Adding more catalog owners helps to share the catalog management responsibilities.

To assign a user to the catalog owner role:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to add administrators to.
4. On the left menu, select **Roles and administrators**.

    ![Screenshot that shows catalog roles and administrators.](media/entitlement-management-shared/catalog-roles-administrators.png)
5. Select **Add owners** to select the members for these roles.
6. Select **Select** to add these members.

## Edit a catalog

You can edit the name and description for a catalog. Users see this information in an access package's details.

To edit a catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog creator.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to edit.
4. On the catalog's **Overview** page, select **Edit**.
5. Edit the catalog's name, description, or enabled settings.

    ![Screenshot that shows editing catalog settings.](media/entitlement-management-shared/catalog-edit.png)
6. Select **Save**.

## Delete a catalog

You can delete a catalog, but only if it doesn't have any access packages.

To delete a catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog creator.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to delete.
4. On the catalog's **Overview** page, select **Delete**.
5. On the message box that appears, select **Yes**.

### Delete a catalog programmatically

You can also delete a catalog by using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission can call the API to [delete an accessPackageCatalog](/en-us/graph/api/accesspackagecatalog-delete).