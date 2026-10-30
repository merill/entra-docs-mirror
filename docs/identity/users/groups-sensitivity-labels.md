---
layout: Conceptual
title: Assign sensitivity labels to Microsoft Entra security groups (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-sensitivity-labels
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to apply sensitivity labels to cloud security groups in Microsoft Entra ID for consistent classification and governance.
ms.topic: how-to
ms.date: 2026-05-01T00:00:00.0000000Z
ms.reviewer: mbhargav
ms.custom:
- msecd-doc-authoring-1012
- sfi-ga-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 9ff88fb7-6be9-fbfc-d452-5ecd15d8ba95
document_version_independent_id: 9ff88fb7-6be9-fbfc-d452-5ecd15d8ba95
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-sensitivity-labels.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-sensitivity-labels
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-sensitivity-labels.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3ac647da-bf86-48d5-6dcf-9e679470aa45
---

# Assign sensitivity labels to Microsoft Entra security groups (preview) - Microsoft Entra ID | Microsoft Learn

Apply sensitivity labels to Microsoft Entra cloud security groups to extend the classification and governance you already use for Microsoft 365 groups. The same labels you publish in the Microsoft Purview portal and configure for groups and sites apply automatically to cloud security groups, with no separate label configuration required.

Note

This feature doesn't apply to security groups synced from on-premises Active Directory or Exchange-managed security groups. Labels also aren't supported on security groups with dynamic membership. See Known limitations for details.

Important

This feature is in preview. Certain behaviors, including the ability to change labels once they're set and enforcement for high-privilege roles, might change before general availability. To configure this feature, there must be at least one active Microsoft Entra ID P1 license in your Microsoft Entra organization.

## Key differences from Microsoft 365 group labeling

Sensitivity labels for cloud security groups share the same underlying label infrastructure as Microsoft 365 groups, but there are important behavioral differences:

| Behavior | Microsoft 365 groups | Cloud security groups |
| --- | --- | --- |
| **Label mutability** | Group owners and admins can change or remove labels at any time. | **Labels are immutable** once applied. You can't change or remove labels. |
| **Label assignment** | Assign labels when creating a group or on existing groups. | Assign labels when creating a group or on existing groups. To label a group with child groups, remove all child groups first, apply the label, and then add the child groups back. |
| **Membership validation** | Validate membership additions against label policies. | Validate membership additions against label policies. Validate existing membership against label guest policy on first assignment of label. |
| **Nesting support** | Microsoft 365 groups don't support nesting. | Supported, but child groups must have labels that are equally or more restrictive than the parent group's label. For details, see Nesting behavior with labeled groups. |
| **Admin / high-privilege bypass** | Admins respect label policies. | During preview, certain built-in admin roles and apps with specific permissions **can bypass label enforcement**. For the full list, see Known limitations. This behavior might change before general availability. |

Note

Sensitivity labels for mail-enabled security groups and distribution lists aren't supported.

## Why labels are immutable in preview

Microsoft 365 groups are collaboration constructs that apply membership to shared content and workloads such as SharePoint, Teams, and Exchange. In contrast, Microsoft Entra ID security groups are authorization primitives, which are security principals that Microsoft Entra ID and downstream access control systems evaluate for membership.

When a sensitivity label applied to a cloud security group forbids guest access, **Microsoft Entra ID must validate effective membership at evaluation time**. Effective membership includes both direct group members and members inherited transitively through nested groups. Validation ensures that no guests are present at any level of the group hierarchy.

Security groups are used directly in authorization decisions such as Conditional Access scoping, application access, and resource permissions. Their labeled membership represents a bundle of entitlements. Enforcement depends on Microsoft Entra ID's membership resolution and validation logic, not on administrative governance practices alone. **Current validation processes apply only on group creation or when a label is first assigned.** Extending these validation processes for other scenarios is in progress.

Warning

Sensitivity label policy changes in Microsoft Purview apply immediately to new policy checks, **but they don't alter existing group membership**. For example, if you change a label from allowing to blocking guest access, the new policy blocks guests in newly labeled groups and blocks new guest additions to existing labeled groups, but guests already in those groups remain until an owner or admin removes them.

**Avoid changing or deleting a label's policy after the label is in use on security groups.** Owners choose a label based on the protections it provides at assignment time. Weakening, tightening, or removing those protections can create a mismatch between the label's current policy and the group's existing state. For broader Purview guidance, see [Sensitivity labels in Microsoft Purview](/en-us/purview/sensitivity-labels) and [Enable sensitivity labels for containers and synchronize labels](/en-us/purview/sensitivity-labels-teams-groups-sites).

## Known limitations (preview)

During preview, the following limitations apply:

- **Label immutability:** You can't change or remove a label after you apply it. Choose labels carefully before you apply them.
- **High-privilege bypass:** The following admin roles and application permissions can bypass label policy enforcement when adding members. This behavior might change before general availability.

    - **Admin roles:** Global Administrator, User Administrator, Groups Administrator, Directory Writers, Exchange Administrator, SharePoint Administrator, SharePoint Advanced Management Administrator, Teams Administrator, Yammer Administrator, Helpdesk Administrator, Service Support Administrator
    - **Application permissions:**`Group.ReadWrite.All`, `Directory.ReadWrite.All`, `Directory.ReadWriteAdvanced.All`, `GroupMember.ReadWrite.All`
- **No nested group labeling:** You can't apply a label to a security group that contains nested groups. Remove all nested groups first, apply the label, label the child groups individually, and then add them back. Child group labels must be compatible with the parent.
- **Dynamic membership groups:** You can't apply sensitivity labels to security groups with dynamic membership in this release. While there are certain edge cases where you can apply a label to a dynamic group, the associated label policy isn't enforced.
- **On-premises and Exchange-managed groups:** Security groups synced from on-premises Active Directory and Exchange-managed security groups aren't supported.
- **Mail-enabled security groups and distribution lists:** Not supported.
- **Microsoft 365 admin center and My Groups:** Assigning sensitivity labels to security groups isn't supported in the Microsoft 365 admin center or in the [My Groups portal](https://myaccount.microsoft.com/groups). Use the Microsoft Entra admin center, the Azure portal, PowerShell, or Microsoft Graph instead.

## Prerequisites

Before you can assign sensitivity labels to cloud security groups, ensure the following conditions are met:

1. Your organization has at least one active **Microsoft Entra ID P1** or P2 license (or Microsoft 365 E3/E5).
2. The `EnableMIPLabels` setting is set to `True` for cloud security groups in your tenant directory settings.
3. Sensitivity labels are published in the Microsoft Purview portal with the **Groups & Sites** scope enabled.
4. Labels are synchronized to Microsoft Entra ID by using the `Execute-AzureADLabelSync` cmdlet. Labels can take up to 24 hours after synchronization to become available.
5. The [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation) is installed for the directory-settings and group-management cmdlets in this article.
6. [Security & Compliance PowerShell](/en-us/powershell/exchange/connect-to-scc-powershell) is installed and connected. The `Execute-AzureADLabelSync` cmdlet is available only in Security & Compliance PowerShell, not in the Microsoft Graph PowerShell SDK.

## Enable sensitivity label support in PowerShell

To apply sensitivity labels to cloud security groups, you must enable the feature by creating or updating tenant-level directory settings. Cloud security groups use the `Group.Security` settings template, which is separate from the `Group.Unified` template used for Microsoft 365 groups.

Note

If you already enabled sensitivity labels for Microsoft 365 groups, you still need to complete these steps to enable them for cloud security groups. The two group types use separate directory setting templates.

1. Open a PowerShell prompt and install the Graph modules required to run the cmdlets.

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    Install-Module Microsoft.Graph.Beta -Scope CurrentUser
    ```
2. Connect to your tenant.

    ```powershell
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    ```
3. Create the tenant-level directory settings for cloud security groups. Use the `Group.Security` template ID.

    ```powershell
    $params = @{
        templateId = "d209f6fa-3839-4d70-b83f-60b1c64d0e8f"
        values = @(
            @{
                name = "AllowToAddGuests"
                value = "True"
            }
            @{
                name = "EnableMIPLabels"
                value = "True"
            }
        )
    }
    New-MgBetaDirectorySetting -BodyParameter $params
    ```
4. Verify the settings were created.

    ```powershell
    (Get-MgBetaDirectorySetting | Where-Object {
        $_.DisplayName -eq "Group.Security"
    }).Values
    ```

    The output should show `EnableMIPLabels` set to `True`.

**If the settings already exist and you need to update them:**

```powershell
$Setting = Get-MgBetaDirectorySetting -Search DisplayName:"Group.Security"
$params = @{
    Values = @(
        @{
            Name = "EnableMIPLabels"
            Value = "True"
        }
    )
}
Update-MgBetaDirectorySetting -DirectorySettingId $Setting.Id `
    -BodyParameter $params
```

If you receive a `Request_BadRequest` error, the settings already exist. Use `Get-MgBetaDirectorySetting | Format-List` to find the correct setting ID, then issue the `Update-MgBetaDirectorySetting` cmdlet with that ID.

You also need to synchronize your sensitivity labels to Microsoft Entra ID. For instructions, see [Enable sensitivity labels for containers and synchronize labels](/en-us/purview/sensitivity-labels-teams-groups-sites#how-to-enable-sensitivity-labels-for-containers-and-synchronize-labels) in the Purview documentation.

## Assign a label to a new security group in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Groups Administrator.
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups** &gt; **New group**.
4. On the New Group page, select **Security** as the group type.
5. Fill out the required information and select a sensitivity label from the **Sensitivity label** dropdown.

    Warning

    Once you apply a sensitivity label and create the group, you can't change or remove the label. Verify the label aligns with your intended access and usage policy before you proceed. This behavior might change before general availability.
6. Add owners and members as needed. If the selected label includes a policy that blocks guest access, you can't add guest members.
7. Select **Create** to save your changes.

The group is created and the membership restrictions associated with the selected label are enforced.

## Assign a label to an existing security group in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Groups Administrator.
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups**, and then select the group you want to label.
4. On the group's page, select **Properties**.
5. Select a sensitivity label from the **Sensitivity label** dropdown.

    Warning

    Once you apply the label, you can't change or remove it. If the group's current membership conflicts with the selected label's policy (for example, the group contains guests and the label blocks guest access), the save operation fails. Resolve the conflict before you apply the label.
6. Select **Save** to apply your changes.

## Assign a label using PowerShell or Microsoft Graph

To manage labels and labeled-group membership programmatically, use the following PowerShell snippets that call the Microsoft Graph beta endpoint.

### Apply a label to a new security group

```powershell
$param = @{
    description = "Your Group Description"
    displayName = "Your Group Name"
    mailEnabled = $false
    securityEnabled = $true
    mailNickname = "YourGroupNickName"
    assignedLabels = @(
        @{ "LabelId" = "<labelID>" }
    )
}
New-MgBetaGroup @param
```

To retrieve available label IDs, use the [List sensitivityLabels](/en-us/graph/api/security-informationprotection-list-sensitivitylabels) Microsoft Graph API.

### Apply a label to an existing security group

```powershell
$assignedLabels = @(
    @{ "LabelId" = "<labelID>" }
)
Update-MgBetaGroup -GroupId <groupId> -AssignedLabels $assignedLabels
```

### Add a member to a labeled security group

```powershell
$userUPN = "user1@domain.com"
$user = Get-MgBetaUser -UserId $userUPN
$odataID = "https://graph.microsoft.com/v1.0/directoryObjects/" + $user.Id
New-MgBetaGroupMemberByRef -GroupId <groupId> -OdataId $odataID
```

When you add members to a labeled group, Microsoft Entra ID checks that the new member meets the label's restrictions. If the member doesn't meet the restrictions (for example, if you try to add a guest to a group with a no-guests policy), the operation is blocked and an error is returned.

## Nesting behavior with labeled groups

When you work with nested groups and sensitivity labels, the following rules apply:

- **You can't label a group that currently contains nested groups.** To label a parent group, remove all nested (child) groups first, apply the label to the parent, and then add the child groups back.
- **Child groups must have a compatible label.** When you add a child group back to a labeled parent, the child group's label must be at least as restrictive as the parent's label. You can't add a child group with a less restrictive label (lower priority) as a member of a more restrictive parent group.
- **You can't nest unlabeled groups under a labeled parent.** If the parent group has a label, you must label all child groups with a compatible label before you can add them.

### Steps to label a parent group with nested groups

1. Remove all nested groups from the parent group.
2. Apply the desired label to the parent group.
3. Apply labels to each child group (labels must be equal to or more restrictive than the parent's label).
4. Add the labeled child groups back to the parent group.

## Troubleshooting

### You can't assign sensitivity labels to a security group

The sensitivity label option appears for cloud security groups only when all the following conditions are met:

1. The organization has an active Microsoft Entra ID P1 license.
2. `EnableMIPLabels` is set to `True` in the `Group.Security` directory settings.
3. Sensitivity labels are published in the Microsoft Purview portal for this Microsoft Entra organization.
4. Labels are synchronized to Microsoft Entra ID by using the `Execute-AzureADLabelSync` cmdlet (run from Security & Compliance PowerShell). Labels can take up to 24 hours after synchronization to become available.
5. The sensitivity label scope is configured for **Groups & Sites**.
6. The group is a Cloud Security group with **assigned** membership type (not dynamic).
7. The current signed-in user has sufficient privileges to assign sensitivity labels (group owner or at least a Groups Administrator) and is within the scope of the sensitivity label publishing policy.

### Label assignment fails due to membership conflict

If you attempt to apply a label whose policy conflicts with the group's current membership, the operation fails with an error. Common scenarios include:

- **Applying a label that blocks guest access to a group that contains guest members.** Resolution: Remove the guest members, then apply the label.
- **Applying any label to a group that contains nested groups.** Resolution: Remove all nested groups, apply the label, label the child groups, and then add them back.

### Member addition fails due to label conflict

If you attempt to add a member (guest or nested group) to a cloud security group whose label policy conflicts with the group's current membership, the operation fails with an error. Common scenarios include:

- **Adding a guest member to a group with a label that blocks guest access.** Resolution: You can't add guests to a group whose label doesn't allow guest access.
- **Adding an unlabeled nested group to a labeled parent group.** Resolution: Apply a label to the nested group that's equally or more restrictive than the parent group's label, then add the nested group.
- **Adding a nested group with a less restrictive label to a parent group.** Resolution: The nested group must have a label that's equally or more restrictive than the parent group's label. If the nested group has a less restrictive label, you can't add it.

### You can't change or remove the label

During preview, you can't change sensitivity labels on cloud security groups. After you apply a label, you can't modify or remove it. To change a label, create a new security group with the correct label, and then re-add the members to the new group.

### Known issue: assignedLabels not returned in PowerShell

There's a known issue where the `assignedLabels` property might not be populated when you query a group through PowerShell. As a workaround, use Microsoft Graph Explorer or the Graph API directly:

```http
GET https://graph.microsoft.com/v1.0/groups/{groupId}?$select=assignedLabels
```

Or

```http
GET https://graph.microsoft.com/v1.0/groups/{groupId}/assignedlabels
```