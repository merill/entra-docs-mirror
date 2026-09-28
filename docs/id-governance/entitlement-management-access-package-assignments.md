---
layout: Conceptual
title: View, add, and remove assignments for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-assignments
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to view, add, and remove assignments for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2026-05-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 270ab048-109b-7c3f-95a3-1d683d9433b6
document_version_independent_id: 1ff429c1-6d62-f4e9-9244-074d0573abdc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-assignments.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-assignments
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-assignments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3f6ff44d-5563-fcc9-a5bf-a87fd398d0af
---

# View, add, and remove assignments for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

In entitlement management, you can see who is assigned to access packages, their policy, status, and identity lifecycle (preview). If an access package has an appropriate policy, you can also directly assign identities to an access package. This article describes how to view, add, and remove assignments for access packages.

Note

These Microsoft Entra admin center steps require the signed-in user to be able to access the Microsoft Entra admin center. Entitlement management roles, such as Access package assignment manager, authorize assignment-management actions within entitlement management, but they don't by themselves change tenant-wide access settings for the admin center. If the **Restrict access to Microsoft Entra administration portal** user setting is enabled, verify that the delegated user can access the admin center, or use an authorized programmatic method. For more information about this setting, see [Default user permissions](../fundamentals/users-default-permissions).

## View who has an assignment

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access Package manager, and the Access Package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open an access package.
4. Select **Assignments** to see a list of active assignments.

    ![List of assignments to an access package](media/entitlement-management-access-package-assignments/assignments-list.png)
5. Select a specific assignment to see more details.
6. To see a list of assignments that didn't have all resource roles properly provisioned, select the filter status and select **Delivering**.

    You can see more details on delivery errors by locating the user's corresponding request on the **Requests** page.
7. To see expired assignments, select the filter status and select **Expired**.
8. To download a CSV file of the filtered list, select **Download**.

## View assignments programmatically

### View assignments with Microsoft Graph

You can also retrieve assignments in an access package using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.Read.All` or `EntitlementManagement.ReadWrite.All` permission can call the API to [list accessPackageAssignments](/en-us/graph/api/entitlementmanagement-list-assignments?view=graph-rest-1.0&amp;preserve-view=true). An application that has the application permission `EntitlementManagement.Read.All` or `EntitlementManagement.ReadWrite.All` permission can also use this API to retrieve assignments across all catalogs, and an application that has a role assignment in a catalog can use this API to retrieve assignments in that catalog.

Microsoft Graph will return the results in pages, and will continue to return a reference to the next page of results in the `@odata.nextLink` property with each response, until all pages of the results are read. To read all results, you must continue to call Microsoft Graph with the `@odata.nextLink` property returned in each response until the `@odata.nextLink` property is no longer returned, as described in [paging Microsoft Graph data in your app](/en-us/graph/paging).

While an Identity Governance Administrator can retrieve access packages from multiple catalogs, if user or application service principal is assigned only to catalog-specific delegated administrative roles, the request must supply a filter to indicate a specific access package, such as: `$filter=accessPackage/id eq '00001111-aaaa-2222-bbbb-3333cccc4444'`.

### View assignments with PowerShell

You can also retrieve assignments to an access package in PowerShell with the `Get-MgEntitlementManagementAssignment` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.1.x or later module version. This script illustrates using the Microsoft Graph PowerShell cmdlets module version 2.4.0 to retrieve all assignments to a particular access package. This cmdlet takes as a parameter the access package ID, which is included in the response from the `Get-MgEntitlementManagementAccessPackage` cmdlet. Be sure when using the `Get-MgEntitlementManagementAccessPackage` cmdlet to include the `-All` flag to cause all pages of assignments to be returned.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.Read.All"
$accesspackage = Get-MgEntitlementManagementAccessPackage -Filter "displayName eq 'Marketing Campaign'"
if ($null -eq $accesspackage) { throw "no access package"}
$assignments = @(Get-MgEntitlementManagementAssignment -AccessPackageId $accesspackage.Id -ExpandProperty target -All -ErrorAction Stop)
$assignments | ft Id,state,{$_.Target.id},{$_.Target.displayName}
```

The preceding query returns expired and delivering assignments along with delivered assignments. If you wish to exclude expired or delivering assignments, you can use a filter that includes the access package ID and the state of the assignments. This script illustrates using a filter to retrieve only the assignments in state `Delivered` for a particular access package. The script will then generate a CSV file `assignments.csv`, with one row per assignment.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.Read.All"
$accesspackage = Get-MgEntitlementManagementAccessPackage -Filter "displayName eq 'Marketing Campaign'"
if ($null -eq $accesspackage) { throw "no access package"}
$accesspackageId = $accesspackage.Id
$filter = "accessPackage/id eq '" + $accesspackageId + "' and state eq 'Delivered'"
$assignments = @(Get-MgEntitlementManagementAssignment -Filter $filter -ExpandProperty target -All -ErrorAction Stop)
$sp = $assignments | select-object -Property Id,{$_.Target.id},{$_.Target.ObjectId},{$_.Target.DisplayName},{$_.Target.PrincipalName}
$sp | Export-Csv -Encoding UTF8 -NoTypeInformation -Path ".\assignments.csv"
```

## Directly assign an identity

In some cases, you might want to directly assign specific identities to an access package so that identities don't have to go through the process of requesting the access package. To directly assign identities, the access package must have a policy that allows administrator direct assignments.

Note

When assigning identities to an access package, administrators will need to verify that the identities are eligible for that access package based on the existing policy requirements. Otherwise, the identities won't successfully be assigned to the access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access Package manager, and the Access Package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open an access package.
4. In the left menu, select **Assignments**.
5. Select **New assignment** to open Add user to access package.

    ![Screenshot of adding identities to an access package.](media/entitlement-management-access-package-assignments/assignments-add-user.png)
6. In the **Select policy** list, select a policy that the users' future requests and lifecycle will be governed and tracked by. If you want the selected users to have different policy settings, you can select **Create new policy** to add a new policy.
7. Once you select a policy, you are able to add users to select the users you want to assign this access package to, under the chosen policy.

    Note

    If you select a policy with questions, you can only assign one user at a time. If the external user already exists in the directory, use the **Identities in my directory** option and select the existing user. Use the **External user** option when the user doesn't exist in the directory.
8. Set the date and time you want the selected users' assignment to start and end. If an end date isn't provided, the policy's lifecycle settings are used.
9. Optionally provide a justification for your direct assignment for record keeping.
10. If the selected policy includes additional requestor information, select **View questions** to answer them on behalf of the users, then select **Save**.

    ![Assignments - click view questions](media/entitlement-management-access-package-assignments/assignments-view-questions.png)

    ![Assignments - questions pane](media/entitlement-management-access-package-assignments/assignments-questions-pane.png)
11. Select **Add** to directly assign the selected identities to the access package.

    After a few moments, select **Refresh** to see the identities in the Assignments list.

## Directly assign any identity

Entitlement management also allows you to directly assign external identities to an access package to make collaborating with partners easier. To do this, the access package must have a policy that allows identities not yet in your directory to request access.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access Package manager, and the Access Package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open an access package.
4. In the left menu, select **Assignments**.
5. Select **New assignment** to open **Assign access package to identities**.
6. In the **Select policy** list, select a policy that allows that is set to **For users not in your directory**
7. Select **External user**. You're able to specify which users you want to assign to this access package. ![Assignments - Add any user to access package](media/entitlement-management-access-package-assignments/assignments-add-any-user.png)
8. Enter the identity **Name** (optional) and the identity **Email address** (required).

    Note

    - The identity you want to add must be within the scope of the policy. For example, if your policy is set to **Specific connected organizations**, the identity email address must be from the domain(s) of the selected organization(s). If the identity you are trying to add has an email address of jen@*foo.com* but the selected organization’s domain is *bar.com*, you won't be able to add that identity to the access package.
    - Similarly, if you set your policy to include **All configured connected organizations**, the identity email address must be from one of your configured connected organizations. Otherwise, the identity won't be added to the access package.
    - If you wish to add any identity to the access package, you'll need to ensure that you select **All users (All connected organizations + any external user)** when configuring your policy.
9. Set the date and time you want the selected identity's assignment to start and end. If an end date isn't provided, the policy's lifecycle settings are used.
10. Select **Add** to directly assign the selected identities to the access package.
11. After a few moments, select **Refresh** to see the identities in the Assignments list.

## Directly assigning identities programmatically

### Assign an identity to an access package with Microsoft Graph

You can also directly assign identities to an access package using Microsoft Graph. An identity in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission, an application with the `EntitlementManagement.ReadWrite.All` application permission, or an application in a catalog role, can call the API to [create an accessPackageAssignmentRequest](/en-us/graph/api/entitlementmanagement-post-assignmentrequests?view=graph-rest-1.0&amp;preserve-view=true). In this request, the value of the `requestType` property should be `adminAdd`, and the `assignment` property is a structure that contains the `targetId` of the user being assigned.

### Assign a user to an access package with PowerShell

You can assign a user to an access package in PowerShell with the `New-MgEntitlementManagementAssignmentRequest` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.1.x or later module version. This script illustrates using the Microsoft Graph PowerShell cmdlets module version 2.4.0.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"
$accesspackage = Get-MgEntitlementManagementAccessPackage -Filter "displayname eq 'Marketing Campaign'" -ExpandProperty "assignmentpolicies"
if ($null -eq $accesspackage) { throw "no access package"}
$policy = $accesspackage.AssignmentPolicies[0]
$userid = "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
$params = @{
   requestType = "adminAdd"
   assignment = @{
      targetId = $userid
      assignmentPolicyId = $policy.Id
      accessPackageId = $accesspackage.Id
   }
}
New-MgEntitlementManagementAssignmentRequest -BodyParameter $params
```

You can also populate assignments for existing collections of users in your directory, including those assigned to an application, or listed in a text file. For more information, see [Add assignments of existing users who already have access to the application](entitlement-management-access-package-create-app#add-assignments-of-existing-users-who-already-have-access-to-the-application) and [Add assignments for any additional users who should have access to the application](entitlement-management-access-package-create-app#add-assignments-for-any-additional-users-who-should-have-access-to-the-application).

You can also assign multiple users that are in your directory to an access package using PowerShell with the `New-MgBetaEntitlementManagementAccessPackageAssignment` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.4.0 or later. This cmdlet takes as parameters

- the access package ID, which is included in the response from the `Get-MgEntitlementManagementAccessPackage` cmdlet,
- the access package assignment policy ID, which is included in the policy in the `assignmentpolicies` field in the response from the `Get-MgEntitlementManagementAccessPackage` cmdlet,
- the object IDs of the target users, either as an array of strings, or as a list of user members returned from the `Get-MgGroupMember` cmdlet.

For example, if you want to ensure all the users who are currently members of a group also have assignments to an access package, you can use this cmdlet to create requests for those users who don't currently have assignments. This cmdlet will only create assignments; it doesn't remove assignments for users who are no longer members of a group. If you wish to have the assignments of an access package track the membership of a group and add and remove assignments over time, use an [automatic assignment policy](entitlement-management-access-package-auto-assignment-policy) instead.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All,Directory.Read.All"
$members = @(Get-MgGroupMember -GroupId "a34abd69-6bf8-4abd-ab6b-78218b77dc15" -All)

$accesspackage = Get-MgEntitlementManagementAccessPackage -Filter "displayname eq 'Marketing Campaign'" -ExpandProperty "assignmentPolicies"
if ($null -eq $accesspackage) { throw "no access package"}
$policy = $accesspackage.AssignmentPolicies[0]
$req = New-MgBetaEntitlementManagementAccessPackageAssignment -AccessPackageId $accesspackage.Id -AssignmentPolicyId $policy.Id -RequiredGroupMember $members
```

If you wish to add an assignment for a user who isn't yet in your directory, you can use the `New-MgBetaEntitlementManagementAccessPackageAssignmentRequest` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) beta module version 2.1.x or later beta module version. This script illustrates using the Microsoft Graph `beta` profile and Microsoft Graph PowerShell cmdlets module version 2.4.0. This cmdlet takes as parameters

- the access package ID, which is included in the response from the `Get-MgEntitlementManagementAccessPackage` cmdlet,
- the access package assignment policy ID, which is included in policy in the `assignmentpolicies` field in the response from the `Get-MgEntitlementManagementAccessPackage` cmdlet,
- the email address of the target user.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"
$accesspackage = Get-MgEntitlementManagementAccessPackage -Filter "displayname eq 'Marketing Campaign'" -ExpandProperty "assignmentPolicies"
if ($null -eq $accesspackage) { throw "no access package"}
$policy = $accesspackage.AssignmentPolicies[0]
$req = New-MgBetaEntitlementManagementAccessPackageAssignmentRequest -AccessPackageId $accesspackage.Id -AssignmentPolicyId $policy.Id -TargetEmail "sample@example.com"
```

## Configure access assignment as part of a lifecycle workflow

In the Microsoft Entra Lifecycle Workflows feature, you can add a [Request user access package assignment](lifecycle-workflow-tasks#request-user-access-package-assignment) task to an onboarding workflow. The task can specify an access package which users should have. When the workflow runs for a user, then an access package assignment request is created automatically.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with at least both the [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) and [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) roles.
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select an employee onboarding or move workflow.
4. Select **Tasks** and select **Add task**.
5. Select **Request user access package assignment** and select **Add**.
6. Select the newly added task.
7. Select **Select Access package**, and choose the access package that new or moving users should be assigned to.
8. Select **Select Policy**, and choose the access package assignment policy in that access package.
9. Select **Save**.

## Remove an assignment

You can remove an assignment that a user or an administrator had previously requested.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open an access package.
4. In the left menu, select **Assignments**.
5. Select the check box next to the user whose assignment you want to remove from the access package.
6. Select the **Remove** button near the top of the left pane.

    ![Assignments - Remove user from access package](media/entitlement-management-access-package-assignments/remove-assignment-select-remove-assignment.png)

    A notification appears informing you that the assignment has been removed.

## Remove an assignment programmatically

### Remove an assignment with Microsoft Graph

You can also remove an assignment of a user to an access package using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission, an application with the `EntitlementManagement.ReadWrite.All` application permission, or an application in a catalog role, can call the API to [create an accessPackageAssignmentRequest](/en-us/graph/api/entitlementmanagement-post-assignmentrequests?view=graph-rest-1.0&amp;preserve-view=true). In this request, the value of the `requestType` property should be `adminRemove`, and the `assignment` property is a structure that contains the `id` property identifying the `accessPackageAssignment` being removed.

### Remove an assignment with PowerShell

You can remove a user's assignment in PowerShell with the `New-MgEntitlementManagementAssignmentRequest` cmdlet from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.1.x or later module version. This script illustrates using the Microsoft Graph PowerShell cmdlets module version 2.4.0.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"
$accessPackageId = "9f573551-f8e2-48f4-bf48-06efbb37c7b8"
$userId = "11bb11bb-cc22-dd33-ee44-55ff55ff55ff"
$filter = "accessPackage/Id eq '" + $accessPackageId + "' and state eq 'Delivered' and target/objectId eq '" + $userId + "'"
$assignment = Get-MgEntitlementManagementAssignment -Filter $filter -ExpandProperty target -all -ErrorAction stop
if ($assignment -ne $null) {
   $params = @{
      requestType = "adminRemove"
      assignment = @{ id = $assignment.id }
   }
   New-MgEntitlementManagementAssignmentRequest -BodyParameter $params
}
```

## Configure assignment removal as part of a lifecycle workflow

In the Microsoft Entra Lifecycle Workflows feature, you can add a [Remove access package assignment for user](lifecycle-workflow-tasks#remove-access-package-assignment-for-user) task to an offboarding workflow. That task can specify an access package the user might be assigned to. When the workflow runs for a user, then their access package assignment is removed automatically.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with at least both the [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) and [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) roles.
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select an employee offboarding workflow.
4. Select **Tasks** and select **Add task**.
5. Select **Remove access package assignment for user** and select **Add**.
6. Select the newly added task.
7. Select **Select Access packages**, and choose one or more access packages that users being offboarded should be removed from.
8. Select **Save**.