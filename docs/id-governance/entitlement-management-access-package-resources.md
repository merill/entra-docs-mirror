---
layout: Conceptual
title: Change resource roles for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to change the resource roles for an existing access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-25T00:00:00.0000000Z
locale: en-us
document_id: f925338f-e219-4fae-3ef7-460bcfc40d4e
document_version_independent_id: 4b2d9db3-90a2-e4d1-282f-44ebce285412
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-resources.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 9140a52b-ae4f-15f8-a27b-1af63d2d2b10
---

# Change resource roles for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

As an access package manager, you can change the resources in an access package at any time without worrying about provisioning the user's access to the new resources, or removing their access from the previous resources. This article describes how to change the resource roles for an existing access package.

This video provides an overview of how to change an access package.

## Check catalog for resources

If you need to add resources such as groups or apps to an access package, you should check whether the resources you need are available in the access package's catalog. If you're an access package manager, you can't add resources to a catalog, even if you own them. You're restricted to using the resources available in the catalog.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open the access package you want to check to ensure that its catalog has the necessary resources.
4. In the left menu, select **Catalog** and then open the catalog.
5. In the left menu, select **Resources** to see the list of resources in this catalog.

    ![List of resources in a catalog](media/entitlement-management-access-package-resources/catalog-resources.png)
6. If the resources aren't already in the catalog, and you're an administrator or a catalog owner, you can [add resources to a catalog](entitlement-management-catalog-create#add-resources-to-a-catalog). The types of resources you can add are groups, applications you've integrated with your directory, and SharePoint Online sites. For example:

    - Groups can be cloud-created Microsoft 365 Groups or cloud-created Microsoft Entra security groups. Groups that originate in an on-premises Active Directory can't be assigned as resources because their owner, or member, attributes can't be changed in Microsoft Entra ID. To give identities access to an application that uses AD security group memberships, create a new group in Microsoft Entra ID, configure [group writeback to AD](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory), and [enable that group to be written to AD](entitlement-management-group-writeback). Groups that originate in Exchange Online as Distribution groups can't be modified in Microsoft Entra ID either.
    - Applications can be Microsoft Entra enterprise applications, which include software as a service (SaaS) applications, on-premises applications that use a different directory or database, and your own applications integrated with Microsoft Entra ID. If your application hasn't yet been integrated with your Microsoft Entra directory, see [govern access for applications in your environment](identity-governance-applications-prepare) and [integrate an application with Microsoft Entra ID](identity-governance-applications-integrate).
    - Sites can be SharePoint Online sites or SharePoint Online site collections.
7. If you're an access package manager and you need to add resources to the catalog, you can ask the catalog owner to add them.

## Determine which resource roles to include in an access package

A resource role is a collection of permissions associated with and defined by a resource. Resources can be made available for identities to be assigned if you add resource roles from each of the catalog's resources to your access package. You can add resource roles that are provided by groups, teams, applications, and SharePoint sites. When a user receives an assignment to an access package, they're added to all the resource roles in the access package.

When they lose an access package assignment, then they're removed from all the resource roles in the access package.

Note

If identities were added to the resources outside of entitlement management, and they need to retain access even if they later receive access package assignments and their access package assignments expire, then don't add the resource roles to an access package.

If you want some identities to receive different resource roles than others, then you need to create multiple access packages in the catalog, with separate access packages for each of the resource roles. For example, if you wish to assign API permissions to an agent ID, then you'll need this to be in a separate access package from member or guest users, since member or guest users can't have API permissions assigned to them. You can also mark the access packages as [incompatible](entitlement-management-access-package-incompatible) with each other so identities can't request access to access packages that would give them excessive access.

In particular, applications can have multiple app roles. When you add an application's app role as a resource role to an access package, if that application has more than one app role, you need to specify the appropriate role for those identities in the access package.

Note

If an application has multiple app roles, and more than one role of that application are in an access package, then the user will receive all those application's included roles. If instead you want identities to only have some of the application's roles, then you'll need to create multiple access packages in the catalog, with separate access packages for each of the app roles.

In addition, applications can also rely upon security groups for expressing permissions. For example, an application might have a single app role `User` and also check the membership of two groups - a `Ordinary Users` group and a `Administrative Access` groups. A user of the application must be a member of exactly one of those two groups. If you wished to configure that identities could request either permission, then you would put into a catalog three resources: the application, the group `Ordinary Users` and the group `Administrative Access`. Then, you would create in that catalog two access packages, and indicate each access package is [incompatible](entitlement-management-access-package-incompatible#scenarios-for-separation-of-duties-checks) with the other:

- a first access package that has two resource roles, the application's app role `User` and membership of the group `Ordinary Users`
- a second access package that has two resource roles, the application's app role `User` and membership of the group `Administrative Access`

## Check if identities are already assigned to the resource role

When a resource role is added to an access package by an admin, identities who are already in that resource role, but don't have assignments to the access package, will remain in the resource role, but won't be assigned to the access package. For example, if an identity is a member of a group and then an access package is created and that group's member role is added to an access package, the identity won't automatically receive an assignment to the access package.

If you want the identity who had a resource role membership to also be assigned to the access package, you can [directly assign an identity](entitlement-management-access-package-assignments#directly-assign-an-identity) to an access package using the Microsoft Entra admin center, or in bulk via Graph or PowerShell. The identities you assign to the access package will then also receive access to the other resource roles in the access package. However, as those identities who were in the resource role already have access prior to being added to the access package, when their access package assignment is removed, they're removed from that resource role.

## Add resource roles

Note

You need to be a Global Administrator or a Privileged Role Administrator with Catalog Owner permissions to add Microsoft Entra Roles to a catalog. Once a Microsoft Entra Role is added to a catalog, Identity Governance Administrators and Access Package Managers can create access packages containing that Microsoft Entra Role, and other identities with permissions to manage access packages can assign identities to that Microsoft Entra Role. Similarly, Applications with EntitlementManagement.RW.All permissions cannot add Microsoft Entra Roles to catalogs unless they also have the Global Administrator or Privileged Role Administrator role with necessary Entitlement Management permissions.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privileged roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open the access package you want to add resource roles to.
4. In the left menu, select **Resource roles**.
5. Select **Add resource roles** to open the Add resource roles to access package page.

    ![Access package - Add resource roles](media/entitlement-management-access-package-resources/resource-roles-add.png)
6. Depending on whether you want to add a membership of a group or team, access to an application, SharePoint site, Microsoft Entra role (Preview), API permission, or SAP IAG access right (Preview), perform the steps in one of the following resource role sections.

## Add a group or team resource role

You can have entitlement management automatically add identities to a group or a team in Microsoft Teams when they're assigned an access package.

- When a membership of a group or team is a resource role that's part of an access package and a user is assigned to that access package, the user is added as a member to that group or team, if not already present.
- When a user's access package assignment expires, they're removed from the group or team, unless they currently have an assignment to another access package that includes that same group or team.

You can select any [Microsoft Entra security group or Microsoft 365 Group](/en-us/entra/fundamentals/how-to-manage-groups). Identities in an administrator role that can manage groups can add any group to a catalog; catalog owners can add any group to the catalog if they're owner of the group. Keep the following Microsoft Entra constraints in mind when selecting a group:

- When a user, including a guest, is added as a member to a group or team, they can see all the other members of that group or team.
- Microsoft Entra ID can't change the membership of a group that was synchronized from Windows Server Active Directory using Microsoft Entra Connect, or that was created in Exchange Online as a distribution group. If you plan to manage access to applications that use AD security groups, see [how to set up group writeback with entitlement management](entitlement-management-group-writeback).
- Dynamic membership groups can't be updated by adding or removing a member, so they aren't suitable for use with entitlement management.
- Microsoft 365 groups have additional constraints, described in the [overview of Microsoft 365 Groups for administrators](/en-us/microsoft-365/admin/create-groups/office-365-groups), including a limit of 100 owners per group, limits on how many members can access Group conversations concurrently, and 7,000 groups per member.

For more information, see [Compare groups](/en-us/office365/admin/create-groups/compare-groups) and [Microsoft 365 Groups and Microsoft Teams](/en-us/microsoftteams/office-365-groups).

1. On the **Add resource roles to access package** page, select **Groups and Teams** to open the Select groups pane.
2. Select the groups and teams you want to include in the access package.

    ![Access package - Add resource roles - Select groups](media/entitlement-management-access-package-resources/group-select.png)
3. Select **Select**.

    Once you select the group or team, the **Sub type** column lists one of the following subtypes:

    | Sub type | Description |
    | --- | --- |
    | Security | Used for granting access to resources. |
    | Distribution | Used for sending notifications to a group of people. |
    | Microsoft 365 | Microsoft 365 Group that isn't Teams-enabled. Used for collaboration between identities, both inside and outside your company. |
    | Team | Microsoft 365 Group that is Teams-enabled. Used for collaboration between identities, both inside and outside your company. |
4. In the **Role** list, select the role you want to assign. If the [group is managed by Privileged Identity Management](privileged-identity-management/groups-discover-groups), eligible memberships such as **Eligible Owner** and **Eligible Member** are also options that can be selected.

    You typically select the Member role. If you select the Owner role, then identities become an owner of the group, which allows those identities to add or remove other members or owners.

    ![Screenshot of available roles to be assigned to PIM for groups resource in an access package.](media/entitlement-management-access-package-create/pim-for-groups-roles.png)
5. Select **Add**.

    Any identity with existing assignments to the access package will automatically become members (or owners) of this group or team after it's added. For more information, see when changes are applied.

Note

If an Access Package expiration period exceeds the "*Expire eligible assignments after*" policy setting in the PIM managed group, it can cause discrepancies between Entitlement Management and Privileged Identity Management, leading to identities losing access while EM shows they're still assigned. For more information, see: [Using groups managed by Privileged Identity Management with access packages reference](entitlement-management-access-package-pim-reference).

## Add an application resource role

You can have Microsoft Entra ID automatically assign user identities access to a Microsoft Entra enterprise application, including SaaS applications, on-premises applications, and your organization's applications integrated with Microsoft Entra ID, when a user is assigned an access package. For applications that integrate with Microsoft Entra ID through federated single sign-on, Microsoft Entra ID issues federation tokens for identities assigned to the application.

If your application hasn't yet been integrated with your Microsoft Entra directory, see [govern access for applications in your environment](identity-governance-applications-prepare) and [integrate an application with Microsoft Entra ID](identity-governance-applications-integrate).

Applications can have multiple app roles defined in their manifest and managed through the [app roles UI](../identity-platform/howto-add-app-roles-in-apps#app-roles-ui). When you add an application's app role as a resource role to an access package, if that application has more than one app role, you need to specify the appropriate role for those identities in that access package. If you're developing applications, you can read more about how those roles are added to your applications in [How to: Configure the role claim issued in the SAML token for enterprise applications](../identity-platform/enterprise-app-role-management). If you're using the Microsoft Authentication Libraries, there's also a [code sample](../identity-platform/sample-v2-code) for how to use app roles for access control.

Note

If an application has multiple app roles, and more than one role of that application are in an access package, then the user will receive all those application's included roles. If instead you want identities to only have some of the application's roles, then you'll need to create multiple access packages in the catalog, with separate access packages for each of the app roles.

Once an app role is a resource of an access package:

- When a user is assigned that access package, the user is added to that app role, if not already present. If the application requires attributes, the values of the attributes collected from the request will be written onto the user.
- When a user's access package assignment expires, their access is removed from the application, unless they have an assignment to another access package that includes that app role. If the application required attributes, those attributes are removed from the user.

Here are some considerations when selecting an application:

- Applications can also have groups assigned to their app roles as well. You can choose to add a group in place of an application and its role in an access package, however then the application won't be visible to the user as part of the access package in the My Access portal.
- Microsoft Entra admin center can also show service principals for services that can't be selected as applications. In particular, **Exchange Online** and **SharePoint Online** are services, not applications that have resource roles in the directory, so they can't be included in an access package. Instead, use group-based licensing to establish an appropriate license for a user who needs access to those services.
- Applications that only support Personal Microsoft Account users for authentication, and don't support organizational accounts in your directory, don't have application roles and can't be added to access package catalogs.
- If your access package is for agent identities or service principals, then ensure that your application supports interactions from those identities. If the application provides APIs with OAuth permissions, add an API permission to the access package, instead of adding an app role. For more information, see [manage assignment of agent identities to an application](../identity/enterprise-apps/assign-agent-identities-to-applications).

1. On the **Add resource roles to access package** page, select **Applications** to open the Select applications pane.
2. Select the applications you want to include in the access package.

    ![Access package - Add resource roles - Select applications](media/entitlement-management-access-package-resources/application-select.png)
3. Select **Select**.
4. In the **Role** list, select an app role.

    ![Access package - Add resource role for an application](media/entitlement-management-access-package-resources/application-role.png)
5. Select **Add**.

    Any identities with existing assignments to the access package will automatically be given access to this application when it's added. For more information, see when changes are applied.

## Add a SharePoint site resource role

Microsoft Entra ID can automatically assign identities access to a SharePoint Online site or SharePoint Online site collection when they're assigned an access package.

1. On the **Add resource roles to access package** page, select **SharePoint sites** to open the Select SharePoint Online sites pane.

    ![Access package - Add resource roles - Select SharePoint sites - Portal view](media/entitlement-management-access-package-resources/resource-sharepoint-add.png)
2. Select the SharePoint Online sites you want to include in the access package.

    ![Access package - Add resource roles - Select SharePoint Online sites](media/entitlement-management-access-package-resources/sharepoint-site-select.png)
3. Select **Select**.
4. In the **Role** list, select a SharePoint Online site role.

    ![Access package - Add resource role for a SharePoint Online site](media/entitlement-management-access-package-resources/sharepoint-site-role.png)

    For SharePoint Online sites with a large number of roles, use the search box to find the role you want to add to the access package. Search returns matching SharePoint roles even when all available roles aren't initially displayed in the list.
5. Select **Add**.

    Any identities with existing assignments to the access package will automatically be given access to this SharePoint Online site when it's added. For more information, see when changes are applied.

## Add a Microsoft Entra role assignment

When identities need additional permissions to access your organization's resources, you can manage those permissions by assigning them Microsoft Entra roles through access packages. By assigning Microsoft Entra roles to employees, and guests, using Entitlement Management, you can look at a user's entitlements to quickly determine which roles are assigned to that user. When you include a Microsoft Entra role as a resource in an access package, you can also specify whether that role assignment is **eligible** or **active**.

Assigning Microsoft Entra roles through access packages helps to efficiently manage role assignments at scale and improves the role assignment lifecycle.

Note

We recommend that you use Privileged Identity Management to provide just-in-time access to a user to perform a task that requires elevated permissions. These permissions are provided through the Microsoft Entra Roles that are tagged as “privileged” in our documentation here: Microsoft Entra built-in roles. Entitlement Management is better suited for assigning users a bundle of resources, which can include a Microsoft Entra role, necessary to do one’s job. Users assigned to access packages tend to have more longstanding access to resources. While we recommend that you manage high-privileged roles through Privileged Identity Management, you can set up eligibility for those roles through access packages in Entitlement Management.

Follow these steps to include a Microsoft Entra role as a resource in an access package:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) or [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator) with Catalog Owner permissions.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
3. On the Access packages page, open the access package you want to add resource roles to and select **Resource roles**.
4. On the **Add resource roles to access package page**, select **Microsoft Entra roles (Preview)** to open the Select Microsoft Entra roles pane.
5. Select the Microsoft Entra roles you want to include in the access package. ![Screenshot of selecting role for access package.](media/entitlement-management-roles/select-role-access-package.png)
6. In the **Role** list, select **Eligible Member** or **Active Member**. ![Screenshot of choosing role for resource role in access package.](media/entitlement-management-roles/access-package-role.png)
7. Select **Add**.

Note

If you select **Eligible**, identities will become eligible for that role and can activate their assignment using Privileged Identity Management in the Microsoft Entra admin center. If you select **Active**, identities will have an active role assignment until they no longer have access to the access package. For Entra roles that are tagged as *“privileged”*, you'll only be able to select **Eligible**. You can find a list of privileged roles here: [Microsoft Entra built-in roles](../identity/role-based-access-control/permissions-reference).

To add a Microsoft Entra role programmatically, see: [Add a Microsoft Entra role as a resource in an access package programmatically](entitlement-management-roles#add-a-microsoft-entra-role-as-a-resource-in-an-access-package-programmatically).

## Add an API permission

This resource role is used for assigning API permissions to an AI agent's service principal or agent ID, as part of Microsoft Entra Agent ID.

For API permissions, resource ownership validation occurs both during onboarding the permissions to an access package and again when adding permissions to an access package. This additional validation helps ensure that only authorized resource owners can introduce or expand access to API Permissions through access packages.

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

1. Prior to including API permissions in an access package, ensure that the access package's policies are scoped to either all service principals or all agent IDs, as users cannot receive API permissions.
2. In the Resource roles tab, select **API Permissions**.
3. Choose the source application that provides the API: Microsoft Graph, another Microsoft feature, or an API your organization uses from one of your organization's own applications.
4. Select whether the agent's identity requires a delegated or an application permission.
5. Select the checkboxes for the necessary permissions.
6. Select **Update permissions**.

![Screenshot of adding API permissions as resource roles to an access package.](media/entitlement-management-access-package-create/api-permissions-roles.png)

Note

Because of the autonomous nature of agents and the potential risks they pose, certain high-risk Microsoft Graph API permissions are explicitly blocked for agents to prevent misuse or unintended access to sensitive data. The permissions listed in [Microsoft Graph permissions blocked for agents](/en-us/graph/api/resources/agentid-platform-overview?view=graph-rest-beta&amp;preserve-view=true#microsoft-graph-permissions-blocked-for-agents) can't be assigned to agent identities.

## Add a SAP IAG access right (Preview)

Once you have [integrated with SAP IAG](entitlement-management-sap-integration) and added SAP IAG as a resource to a catalog, then you can select the SAP IAG access rights to include in an access package.

1. In the Resource roles tab, select SAP IAG.
2. In the resources table, you can select the specific business roles you want to include in the access package and select **Next**. [![Screenshot of setting role for an SAP IAG resource.](media/entitlement-management-sap-integration/sap-resource-roles.png)](media/entitlement-management-sap-integration/sap-resource-roles.png#lightbox)

## Add resource roles programmatically

There are two ways to add a resource role to an access package programmatically, through Microsoft Graph, and through the PowerShell cmdlets for Microsoft Graph.

### Add resource roles to an access package with Microsoft Graph

You can add a resource role to an access package using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission can call the API to:

1. [List the resources in the catalog](/en-us/graph/api/accesspackagecatalog-list-resources?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) and [create an accessPackageResourceRequest](/en-us/graph/api/entitlementmanagement-post-resourcerequests?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) for any resources that aren't yet in the catalog.
2. [Retrieve the roles and scopes of each resource in the catalog](/en-us/graph/api/accesspackagecatalog-list-resources?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true#example-2-retrieve-the-roles-and-scopes-of-a-single-resource-in-a-catalog). This list of roles will then be used to select a role, when subsequently creating a resourceRoleScope.
3. [Create a resourceRoleScope](/en-us/graph/api/accesspackage-post-resourcerolescopes?view=graph-rest-1.0&amp;preserve-view=true) for each resource role needed in the access package.

### Add resource roles to an access package with Microsoft PowerShell

You can also add resource roles to an access package in PowerShell with the cmdlets from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.1.x or later module version.

First, retrieve the ID of the catalog, and of the resource in that catalog and its scopes and roles, that you want to include in the access package. Use a script similar to the following example. This assumes there's a single application resource in the catalog.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"

$catalog = Get-MgEntitlementManagementCatalog -Filter "displayName eq 'Marketing'" -All
if ($catalog -eq $null) { throw "catalog not found" }
$rsc = Get-MgEntitlementManagementCatalogResource -AccessPackageCatalogId $catalog.id -Filter "originSystem eq 'AadApplication'" -ExpandProperty scopes
if ($rsc -eq $null) { throw "resource not found" }
$filt = "(id eq '" + $rsc.Id + "')"
$rrs = Get-MgEntitlementManagementCatalogResource -AccessPackageCatalogId $catalog.id -Filter $filt -ExpandProperty roles,scopes
```

Then, assign the resource role from that resource to the access package. For example, if you wished to include the first resource role of the resource returned earlier as a resource role of an access package, you would use a script similar to the following.

```powershell
$apid = "00001111-aaaa-2222-bbbb-3333cccc4444"

$rparams = @{
    role = @{
        id =  $rrs.Roles[0].Id
        displayName =  $rrs.Roles[0].DisplayName
        description =  $rrs.Roles[0].Description
        originSystem =  $rrs.Roles[0].OriginSystem
        originId =  $rrs.Roles[0].OriginId
        resource = @{
            id = $rrs.Id
            originId = $rrs.OriginId
            originSystem = $rrs.OriginSystem
        }
    }
    scope = @{
        id = $rsc.Scopes[0].Id
        originId = $rsc.Scopes[0].OriginId
        originSystem = $rsc.Scopes[0].OriginSystem
    }
}

New-MgEntitlementManagementAccessPackageResourceRoleScope -AccessPackageId $apid -BodyParameter $rparams
```

If the role doesn't have an ID, then don't include the `id` parameter of the `role` structure in the request payload.

For more information, see [Create an access package in entitlement management for an application with a single role using PowerShell](entitlement-management-access-package-create-app).

## Remove resource roles

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open the access package you want to remove resource roles for.
4. In the left menu, select **Resource roles**.
5. In the list of resource roles, find the resource role you want to remove.
6. Select the ellipsis (**...**) and then select **Remove resource role**.

    Any identities with existing assignments to the access package will automatically have their access revoked to this resource role when it's removed.

## When changes are applied

In entitlement management, Microsoft Entra ID processes bulk changes for assignment and resources in your access packages several times a day. So, if you make an assignment, or change the resource roles of your access package, it can take up to 24 hours for that change to be made in Microsoft Entra ID, plus the amount of time it takes to propagate those changes to other Microsoft Online Services or connected SaaS applications. If your change affects just a few objects, the change will likely only take a few minutes to apply in Microsoft Entra ID, after which other Microsoft Entra components will then detect that change and update the SaaS applications. If your change affects thousands of objects, the change takes longer. For example, if you have an access package with 2 applications and 100 user assignments, and you decide to add a SharePoint site role to the access package, there can be a delay until all the identities are part of that SharePoint site role. You can monitor the progress through the Microsoft Entra audit log, the Microsoft Entra provisioning log, and the SharePoint site audit logs.

When you remove a member of a team, they're removed from the Microsoft 365 Group as well. Removal from the team's chat functionality might be delayed. For more information, see [Group membership](/en-us/microsoftteams/office-365-groups#group-membership).