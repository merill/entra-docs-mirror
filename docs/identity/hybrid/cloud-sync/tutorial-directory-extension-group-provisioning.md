---
layout: Conceptual
title: Use directory extensions when provisioning to Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/tutorial-directory-extension-group-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: pmwongera
description: Learn how to use directory extension attributes when provisioning users and groups from Microsoft Entra ID to Active Directory.
ms.topic: tutorial
ms.date: 2026-08-21T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange, msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: bc45cfd9-188f-fdbf-207f-b9d8e11bc5ab
document_version_independent_id: bc45cfd9-188f-fdbf-207f-b9d8e11bc5ab
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/tutorial-directory-extension-group-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/tutorial-directory-extension-group-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/tutorial-directory-extension-group-provisioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: dc24232e-280e-3a45-23ee-d2f43ff30dbf
---

# Use directory extensions when provisioning to Active Directory - Microsoft Entra ID | Microsoft Learn

A directory extension adds an attribute to the Microsoft Entra schema that Microsoft Entra ID owns. When you provision from Microsoft Entra ID to Active Directory, you can put that attribute to two uses: decide *which* objects are provisioned, or carry a *value* into an Active Directory attribute. Both uses work for users and for groups.

This article walks through one example of each. Select the **Groups** or **Users** tab in each step to follow the example you want. Your selection carries through the rest of the article.

| Tab | Example | Use |
| --- | --- | --- |
| **Groups** | `WritebackEnabled` | Provision only the groups whose extension value is true. |
| **Users** | `EmployeeCode` | Write the extension value into an Active Directory user attribute. |

For background on directory extensions, see [Directory extensions for provisioning Microsoft Entra ID to Active Directory](custom-attribute-mapping-entra-to-active-directory). For the general mapping interface and expression syntax, see [Configure provisioning to Active Directory](how-to-configure-entra-to-active-directory#configure-attribute-mapping).

Note

Microsoft Entra ID provides a built-in `isWritebackEnabled` property on groups that you can set through Microsoft Graph. You can filter on that property directly by using [attribute value filtering](how-to-configure-entra-to-active-directory#attribute-value-filtering), so you don't need a custom extension attribute to control which groups are written back. Use the steps in this article when you need to scope on a value that the built-in property doesn't cover.

Groups support attribute mapping as well. For a group whose Source of Authority is converted to Microsoft Entra ID, the `GroupDN` extension preserves the original organizational unit and common name. To create that extension, see [Preserve a group's organizational unit and name](how-to-preserve-group-organizational-unit-entra-to-active-directory). For the expression that reads it, see [Preserve a group's original organizational unit](how-to-configure-entra-to-active-directory#preserve-a-groups-original-organizational-unit).

## Before you begin

Both examples need the same starting point:

- A working environment that synchronizes users to Microsoft Entra ID.
- A healthy provisioning agent connected to the target Active Directory domain.
- A Microsoft Entra ID to Active Directory configuration, or permission to create one.

Each example then needs its own objects.

# [Groups](#tab/groups)
This example uses the following environment:

- Four synchronized users: Britta Simon, Lola Jacobson, Anna Ringdahl, and John Smith.
- Three organizational units in Active Directory: Sales, Marketing, and Groups.
- The Britta Simon and Anna Ringdahl user accounts reside in the Sales OU.
- The Lola Jacobson and John Smith user accounts reside in the Marketing OU.
- The Groups OU is where groups from Microsoft Entra ID are provisioned.

[![Diagram of group writeback with cloud sync.](../media/common-scenarios/group-writeback-1.png)](../media/common-scenarios/group-writeback-1.png#lightbox)

# [Users](#tab/users)
This example uses the following environment:

- A cloud-managed test user in Microsoft Entra ID.
- A target organizational unit, for example `OU=test,DC=Contoso,DC=com`.
- A writable target Active Directory user attribute, such as `extensionAttribute1`.

---

You can use the environment you create in this article for testing or for getting more familiar with cloud sync.

Tip

For a better experience executing Microsoft Graph PowerShell SDK cmdlets, use Visual Studio Code with `ms-vscode.powershell` extension in [ISE Mode](/en-us/powershell/scripting/dev-cross-plat/vscode/how-to-replicate-the-ise-experience-in-vscode).

## Install and connect Microsoft Graph PowerShell SDK

1. If not yet installed, follow [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation) documentation to install the main modules of Microsoft Graph PowerShell SDK: `Microsoft.Graph`.
2. Open PowerShell with Administrative privileges.
3. To set the execution policy, run (press [A] Yes to all when prompted):

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```
4. Connect to your tenant (be sure to accept on-behalf of when signing in):

    ```powershell
    Connect-MgGraph -Scopes "Directory.ReadWrite.All", "Application.ReadWrite.All", "User.ReadWrite.All", "Group.ReadWrite.All"
    ```

    Important

    Authenticate interactively. Don't put account passwords in scripts.

## Create the CloudSyncCustomExtensionsApp application and service principal

Both examples store their extension on the same application, so you only need to do this once.

Important

Directory extension for Microsoft Entra Cloud Sync is only supported for applications with the identifier URI `api://<tenantId>/CloudSyncCustomExtensionsApp` and the [Tenant Schema Extension App](../connect/how-to-connect-sync-feature-directory-extensions#configuration-changes-in-azure-ad-made-by-the-wizard) created by Microsoft Entra Connect.

1. Get the Tenant ID:

    ```powershell
    $tenantId = (Get-MgOrganization).Id
    $tenantId
    ```

    Note

    This outputs your current Tenant ID. You can confirm this Tenant ID by navigating to [Microsoft Entra admin center](https://entra.microsoft.com/) &gt; **Entra ID** &gt; **Overview**.
2. Using the `$tenantId` variable from the previous step, check to see if the CloudSyncCustomExtensionsApp exists.

    ```powershell
    $cloudSyncCustomExtApp = Get-MgApplication -Filter "identifierUris/any(uri:uri eq 'api://$tenantId/CloudSyncCustomExtensionsApp')"
    $cloudSyncCustomExtApp
    ```
3. If a CloudSyncCustomExtensionsApp exists, skip to the next step. Otherwise, create the new CloudSyncCustomExtensionsApp app:

    ```powershell
    $cloudSyncCustomExtApp = New-MgApplication -DisplayName "CloudSyncCustomExtensionsApp" -IdentifierUris "api://$tenantId/CloudSyncCustomExtensionsApp"
    $cloudSyncCustomExtApp
    ```
4. Check if the CloudSyncCustomExtensionsApp application has a service principal associated. If you just created a new app, skip to the next step.

    ```powershell
    Get-MgServicePrincipal -Filter "AppId eq '$($cloudSyncCustomExtApp.AppId)'"
    ```
5. If you just created a new app, or a service principal isn't returned, create a service principal for CloudSyncCustomExtensionsApp:

    ```powershell
    New-MgServicePrincipal -AppId $cloudSyncCustomExtApp.AppId
    ```

Note

Creating a directory extension in Microsoft Entra ID doesn't require a provisioning agent restart. Restart the agent only when it needs to discover a newly added Active Directory schema attribute.

## Prepare the objects to provision

# [Groups](#tab/groups)
Create two groups in Microsoft Entra ID. One group is Sales and the other is Marketing.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. At the top, select **New group**.
4. Make sure the **Group type** is set to **security**.
5. For the **Group Name**, enter **Sales**.
6. For **Membership type**, keep it at assigned.
7. Select **Create**.
8. Repeat this process using **Marketing** as the **Group Name**.

Now add users to the groups you created.

1. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
2. At the top, in the search box, enter **Sales**.
3. Select the new **Sales** group.
4. On the left, select **Members**.
5. At the top, select **Add members**.
6. Put a check next to **Britta Simon** and **Anna Ringdahl**, and then select **Select**.
7. On the far left, select **All groups** and repeat this process using the **Marketing** group, adding **Lola Jacobson** and **John Smith**.

Note

When adding users to the Marketing group, make note of the group ID on the overview page. This ID is used later to add the newly created property to the group.

# [Users](#tab/users)
Identify the cloud-managed user you want to provision to Active Directory, and confirm you can retrieve it:

```powershell
$testUser = Get-MgUser -Filter "userPrincipalName eq '<test-user-UPN>'"
$testUser
```

You can optionally bring the user into scope through a group instead of selecting the user directly:

1. Create an assigned Microsoft Entra security group, such as **AD-Provisioning-Test**.
2. Add the cloud-managed test user to the group.
3. Select that group when you configure user scope in cloud sync.

Important

The extension value stays on each user. Group membership only brings the user into provisioning scope; it doesn't carry the value.

---

## Create the directory extension

# [Groups](#tab/groups)
Tip

This example creates a custom extension attribute called `WritebackEnabled` to use in a Microsoft Entra Cloud Sync scoping filter, so that only groups with `WritebackEnabled` set to true are written back to on-premises Active Directory. It works similarly to the built-in `isWritebackEnabled` property described earlier in this article.

Under the CloudSyncCustomExtensionsApp, create the extension attribute and assign it to Group objects:

```powershell
New-MgApplicationExtensionProperty -ApplicationId $cloudSyncCustomExtApp.Id -Name 'WritebackEnabled' -DataType 'Boolean' -TargetObjects 'Group'
```

This cmdlet creates an extension attribute that looks like `extension_<AppIdWithoutHyphens>_WritebackEnabled`.

# [Users](#tab/users)
Under the CloudSyncCustomExtensionsApp, create the extension attribute and assign it to User objects:

```powershell
New-MgApplicationExtensionProperty -ApplicationId $cloudSyncCustomExtApp.Id -Name 'EmployeeCode' -DataType 'String' -TargetObjects 'User'
```

This cmdlet creates an extension attribute that looks like `extension_<AppIdWithoutHyphens>_EmployeeCode`. Retrieve the generated name, because you need it when you add the attribute mapping:

```powershell
$userExtension = Get-MgApplicationExtensionProperty -ApplicationId $cloudSyncCustomExtApp.Id |
    Where-Object Name -Like '*_EmployeeCode' | Select-Object -First 1

$userExtensionName = $userExtension.Name
$userExtensionName
```

---

## Set the extension value

# [Groups](#tab/groups)
Set a value on the newly created property for the Marketing group.

1. Get the extension property:

    ```powershell
    $gwbEnabledExtAttrib = Get-MgApplicationExtensionProperty -ApplicationId $cloudSyncCustomExtApp.Id |
        Where-Object {$_.Name -Like '*WritebackEnabled'} | Select-Object -First 1
    $gwbEnabledExtName = $gwbEnabledExtAttrib.Name
    ```
2. Get the `Marketing` group:

    ```powershell
    $marketingGrp = Get-MgGroup -ConsistencyLevel eventual -Filter "DisplayName eq 'Marketing'"
    ```
3. Set the value `True` for the Marketing group:

    ```powershell
    Update-MgGroup -GroupId $marketingGrp.Id -AdditionalProperties @{$gwbEnabledExtName = $true}
    ```
4. To confirm, read the property value:

    ```powershell
    $marketingGrp = Get-MgGroup -ConsistencyLevel eventual -Filter "DisplayName eq 'Marketing'" -Property Id,$gwbEnabledExtName
    $marketingGrp.AdditionalProperties.$gwbEnabledExtName
    ```

# [Users](#tab/users)
1. Set the value on the test user:

    ```powershell
    Update-MgUser -UserId $testUser.Id -AdditionalProperties @{ $userExtensionName = "EMP-1001" }
    ```
2. To confirm, read the property value:

    ```powershell
    $testUser = Get-MgUser -UserId $testUser.Id -Property "id,displayName,$userExtensionName"
    $testUser.AdditionalProperties[$userExtensionName]
    ```

---

### Set the extension value by using Microsoft Graph Explorer

You can set the value through [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) instead of PowerShell. Make sure you consented to the required permission by selecting **Modify permissions**.

# [Groups](#tab/groups)
1. Navigate to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and consent to `Group.ReadWrite.All`.
2. Sign in using your tenant administrator account. A Hybrid Identity Administrator account was used to create this scenario and might be sufficient.
3. At the top, change **GET** to **PATCH**.
4. In the address box, enter `https://graph.microsoft.com/v1.0/groups/<Group Id>`.
5. In the request body, enter:

    ```json
    {
      "extension_<AppIdWithoutHyphens>_WritebackEnabled": true
    }
    ```
6. Select **Run query**.

    [![Screenshot of running the graph query.](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-1.png)](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-1.png#lightbox)
7. If done correctly, you see `[]`.
8. At the top, change **PATCH** to **GET** and look at the properties of the Marketing group. Select **Run query**. You should see the newly created attribute.

    [![Screenshot of group properties.](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-2.png)](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-2.png#lightbox)

# [Users](#tab/users)
1. Navigate to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and consent to `User.ReadWrite.All`.
2. Sign in using your tenant administrator account.
3. At the top, change **GET** to **PATCH**.
4. In the address box, enter `https://graph.microsoft.com/v1.0/users/<User Id>`.
5. In the request body, enter:

    ```json
    {
      "extension_<AppIdWithoutHyphens>_EmployeeCode": "EMP-1001"
    }
    ```
6. Select **Run query**.
7. At the top, change **PATCH** to **GET** and look at the properties of the user. Select **Run query**. You should see the newly created attribute.

---

## Use the extension in your cloud sync configuration

# [Groups](#tab/groups)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.
3. Select **New configuration**.
4. Select **Microsoft Entra ID to AD sync**.

    [![Screenshot of configuration selection.](media/how-to-configure-entra-to-active-directory/entra-to-ad-1.png)](media/how-to-configure-entra-to-active-directory/entra-to-ad-1.png#lightbox)
5. On the configuration screen, select your domain. Select **Create**.

    [![Screenshot of a new configuration.](media/how-to-configure/new-ux-configure-2.png)](media/how-to-configure/new-ux-configure-2.png#lightbox)
6. The **Get started** screen opens. From here, you can continue configuring cloud sync.
7. On the left, select **Scoping filters**, then select **Group scope** &gt; **All groups**.
8. Select **Edit attribute mapping** and change the **Target Container** to `OU=Groups,DC=Contoso,DC=com`. Select **Save**.
9. Select **Add Attribute scoping filter**.
10. Type a name for the scoping filter: `Filter groups with Writeback Enabled`.
11. Under **Target Attribute**, select the newly created attribute that looks like `extension_<AppIdWithoutHyphens>_WritebackEnabled`.

    Important

    Some of the target attributes displayed in the dropdown list might not be usable as a scoping filter because not all properties can be managed in Microsoft Entra ID, for example `extensionAttribute[1-15]`. That's why we recommend creating a custom extension property for this purpose.

    [![Screenshot of available attributes.](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-4.png)](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-4.png#lightbox)
12. Under **Operator**, select **IS TRUE**.
13. Select **Save**, and then select **Save**.
14. Leave the configuration disabled and come back to it.

# [Users](#tab/users)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.
3. Select **New configuration** and select **Microsoft Entra ID to AD sync**, or open an existing configuration.
4. Select the Active Directory domain and a healthy provisioning agent.
5. On the left, select **Scoping filters**, and configure **User scope**. Select the test user directly, or select the group that contains the user.
6. Select **Edit attribute mapping** for users and set the **Target Container** to the complete Active Directory distinguished name, for example `OU=test,DC=Contoso,DC=com`.
7. Add the attribute mapping:

    | Setting | Value |
    | --- | --- |
    | Mapping type | Direct |
    | Source attribute | `extension_<AppIdWithoutHyphens>_EmployeeCode` |
    | Target attribute | `extensionAttribute1`, or another writable Active Directory user attribute |
8. Select **Save**.
9. Leave the configuration disabled until you review the scope, target container, and mappings.

---

## Test and verify

# [Groups](#tab/groups)
Note

When using on-demand provisioning, members aren't automatically provisioned. You need to select which members you wish to test on, and there's a five member limit.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Enter **Marketing** in the **Selected group** box.
4. From the **Selected users** section, select **Lola Jacobson** and **John Smith**.
5. Select **Provision**. It should successfully provision.

    [![Screenshot of successful provision.](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-5.png)](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-5.png#lightbox)
6. Now try with the **Sales** group and add **Britta Simon** and **Anna Ringdahl**. This shouldn't provision, because the Sales group doesn't have the extension value set.

    [![Screenshot of provisioning being blocked.](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-6.png)](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-6.png#lightbox)
7. In Active Directory, you should see the newly created Marketing group.

    [![Screenshot of new group in active directory users and computers.](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-7.png)](media/tutorial-directory-extension-group-provision/directory-extension-group-provision-7.png#lightbox)
8. You can now browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync** &gt; **Overview** to review and enable your configuration and start synchronizing.

# [Users](#tab/users)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Select the test user. If you used group scope, select the group and then explicitly select the test user.
4. Select **Provision**.
5. Review the import, scope evaluation, matching, and export steps.

Confirm the value landed in Active Directory:

```powershell
Get-ADUser -Filter "UserPrincipalName -eq '<test-user-UPN>'" -SearchBase "OU=test,DC=Contoso,DC=com" -Properties extensionAttribute1 |
    Select-Object DistinguishedName,extensionAttribute1
```

The expected value is `extensionAttribute1 = EMP-1001`.

To review the result in the provisioning logs, browse to **Entra ID** &gt; **Monitoring & health** &gt; **Provisioning logs** and filter by the test user and your cloud sync configuration. Confirm that:

- Scope evaluation passed.
- The user was created or matched in Active Directory.
- Under **Modified properties**, the directory extension was mapped to `extensionAttribute1`.
- The export operation succeeded.

---

## Directory extensions on users converted from Active Directory

When you convert a user's Source of Authority to Microsoft Entra ID, the attributes that Active Directory previously owned must already be visible in Microsoft Entra ID, either as directory attributes or as directory schema extensions. For the full list of preconditions, see [Prepare your environment to convert user Source of Authority](../prepare-user-source-of-authority-environment).

That means a converted user usually already has the extension values it needs, so you don't create new extensions for those attributes. Instead, you map from the extensions that already hold the values.

Extensions created by Microsoft Entra Connect live on the [Tenant Schema Extension App](../connect/how-to-connect-sync-feature-directory-extensions#configuration-changes-in-azure-ad-made-by-the-wizard), which is supported as a mapping source alongside CloudSyncCustomExtensionsApp. Add the mapping the same way as in the **Users** tab, selecting the existing extension as the source attribute. Converting Source of Authority doesn't require you to re-register or recreate the extension.