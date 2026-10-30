---
layout: Conceptual
title: Microsoft Entra provisioning setup (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: pmwongera
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory
ms.reviewer: marshmacy
description: Configure scoping filters, target containers, and attribute mappings to provision users and groups from Microsoft Entra ID to Active Directory.
ms.topic: how-to
ms.date: 2026-08-19T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: 1ba290a8-7b6e-a859-4f4d-70ea2d035424
document_version_independent_id: 1ba290a8-7b6e-a859-4f4d-70ea2d035424
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
platformId: 64b2e8b8-562e-f80d-0267-45154d31cab2
---

# Microsoft Entra provisioning setup (Preview) - Microsoft Entra ID | Microsoft Learn

This article guides you through configuring Microsoft Entra Cloud Sync to provision **users and groups** from Microsoft Entra ID to on-premises Active Directory Domain Services (AD DS). You create a configuration, choose which objects it provisions, set scoping filters and attribute value filtering, choose target containers, and customize attribute mappings.

Because the scoping choice determines whether attribute value filtering is available, scoping and attribute mapping are covered together here. When your configuration is complete, [test and enable it](how-to-test-and-enable-provisioning-entra-to-active-directory), which is the same for all deployment options. The final section covers tasks you perform after provisioning runs, such as verifying results and moving a provisioned user.

If you're looking for provisioning from AD to Microsoft Entra ID, see [Configure provisioning from Active Directory to Microsoft Entra ID](how-to-configure).

## Prerequisites

Complete the steps in [Prerequisites for provisioning from Microsoft Entra ID to Active Directory](how-to-prerequisites-provision-entra-to-active-directory) before you continue.

## Choose a deployment option

All deployment options use the same configuration type, **Microsoft Entra ID to AD sync**. What differs is which object types you bring into scope:

| Option | Provisions | Availability |
| --- | --- | --- |
| Groups only | Security groups and memberships | Generally available |
| Users only | Users | Preview |
| Users and groups | Both, in one configuration | Preview |

For guidance on choosing an option and scale considerations, see [Deployment options](concept-deployment-options-provision-to-active-directory).

## Create a configuration

To create a Microsoft Entra ID to AD provisioning configuration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.
3. Select **New configuration**.
4. Select **Microsoft Entra ID to AD sync**.
5. On the configuration screen, select your domain. Select **Create**.
6. The **Get started** screen opens. From here, you can continue configuring cloud sync.

The configuration is split into the following five sections:

| Section | Description |
| --- | --- |
| 1. Add scoping filters | Define which objects are in scope for provisioning. |
| 2. Map attributes | Map attributes between your Microsoft Entra ID users/groups and AD objects. |
| 3. Test | Test your configuration before you deploy it. |
| 4. View default properties | Review default settings and change them where appropriate. |
| 5. Enable your configuration | Enable the configuration and objects begin synchronizing. |

Sections 1 and 2 are covered in this article. For sections 3–5, see [Test and enable provisioning to Active Directory](how-to-test-and-enable-provisioning-entra-to-active-directory).

## Configure scoping filters

Scoping filters determine which objects are provisioned. The **Scoping filters** page provides a read-only view of the current configuration. Select **Edit** to open the wizard.

1. On the **Get started** screen, select **Add scoping filters**, or select **Scoping filters** on the left under **Manage**.

    [![Screenshot of the Scoping filters page showing the current scope settings, assignment, group membership, and target containers.](media/how-to-attribute-mapping-entra-to-active-directory/scoping-filters-overview.png)](media/how-to-attribute-mapping-entra-to-active-directory/scoping-filters-overview.png#lightbox)

### Scope by assignment

In **Edit** mode, use **Scope by assignment** to choose whether to sync all objects or selected objects. Attribute value filtering is available with either choice, but it's only appropriate with one of them:

- **All users and groups** — the next step is **Scope by attribute**. Add attribute value filters for every enabled object type (users, groups, or both), so that provisioning evaluates only the objects you need.

    [![Screenshot of the Scope by assignment step with All users and groups selected.](media/how-to-attribute-mapping-entra-to-active-directory/scope-all-users-groups.png)](media/how-to-attribute-mapping-entra-to-active-directory/scope-all-users-groups.png#lightbox)
- **Selected users and groups** — the next step is **Select users and groups**, where you pick specific objects. Attribute value filtering is available in this mode but isn't recommended, because your selection already determines the scope. For more information, see [Recommended configuration](concept-deployment-options-provision-to-active-directory#recommended-configuration).

    [![Screenshot of the Scope by assignment step with Selected users and groups selected.](media/how-to-attribute-mapping-entra-to-active-directory/scope-selected-users-groups.png)](media/how-to-attribute-mapping-entra-to-active-directory/scope-selected-users-groups.png#lightbox)

Note

If you select a security group that has a nested security group as its member, only the nested group is written back, not its members. To provision nested members, add all member groups to the scope as well.

### Attribute value filtering

Attribute-based scope filtering narrows which objects are provisioned by evaluating their attribute values. You configure it in the **Scope by attribute** step, on the **Users** tab, the **Groups** tab, or both.

Use it with **All users and groups**, where the filter is the only thing narrowing the scope: without one, every user and group in the tenant is evaluated on every cycle.

[![Screenshot of the Scope by attribute step with All users and groups selected, warning that no attribute value filter is configured.](media/how-to-attribute-mapping-entra-to-active-directory/scope-by-attribute-all-users-groups.png)](media/how-to-attribute-mapping-entra-to-active-directory/scope-by-attribute-all-users-groups.png#lightbox)

Don't use it with **Selected users and groups**, where your selection already narrows the scope, so a filter adds processing time without changing which objects are provisioned.

[![Screenshot of the Scope by attribute step with Selected users and groups selected, warning that attribute value filtering is unnecessary.](media/how-to-attribute-mapping-entra-to-active-directory/scope-by-attribute-selected-users-groups.png)](media/how-to-attribute-mapping-entra-to-active-directory/scope-by-attribute-selected-users-groups.png#lightbox)

The provisioning configuration displays a warning in both cases, but doesn't block you. For more information, see [Recommended configuration](concept-deployment-options-provision-to-active-directory#recommended-configuration).

#### Default security clauses

A default security clause is applied to groups on top of clauses that you create, by using `AND` logic:

`securityEnabled IS TRUE AND dirSyncEnabled IS FALSE AND mailEnabled IS FALSE`

The default security clause is evaluated before the clauses that you configure.

#### Filtering logic

A single clause defines one condition for one attribute value. Clauses within a single scoping filter are evaluated with `AND` — all must be `TRUE`.

[![Screenshot of an attribute scoping filter with two clauses that use AND logic.](media/how-to-attribute-mapping-entra-to-active-directory/attribute-scope-filter-and-logic.png)](media/how-to-attribute-mapping-entra-to-active-directory/attribute-scope-filter-and-logic.png#lightbox)

Multiple scoping filters are evaluated with `OR` — if any filter is `TRUE`, the object is provisioned.

[![Screenshot of two attribute scoping filters that use OR logic.](media/how-to-attribute-mapping-entra-to-active-directory/attribute-scope-filter-or-logic.png)](media/how-to-attribute-mapping-entra-to-active-directory/attribute-scope-filter-or-logic.png#lightbox)

#### Create an attribute-based filter

To create a filter that evaluates an attribute value:

1. Select **Add Attribute scoping filter**.
2. In **Name**, enter a name for the filter.
3. Under **Attribute**, select the attribute to evaluate.
4. Under **Operator**, select an operator (for example, `EQUALS`, `NOT EQUALS`, `INCLUDES`, `REGEX MATCH`).
5. Under **Value**, enter a value.
6. Select **Save**.

#### Supported operators

The following operators are supported:

| Operator | Description |
| --- | --- |
| `EQUALS` | Returns `TRUE` if the evaluated attribute exactly matches the input string. The comparison is case-sensitive. |
| `GREATER_THAN` | Returns `TRUE` if the evaluated attribute is greater than the specified value. The specified value and the evaluated attribute must be integers, for example, 0, 1, or 2. |
| `GREATER_THAN_OR_EQUALS` | Returns `TRUE` if the evaluated attribute is greater than or equal to the specified value. The specified value and the evaluated attribute must be integers. |
| `IS FALSE` | Returns `TRUE` if the evaluated attribute contains a Boolean value of `false`. |
| `IS NOT NULL` | Returns `TRUE` if the evaluated attribute isn't empty. |
| `IS NULL` | Returns `TRUE` if the evaluated attribute is empty. |
| `IS TRUE` | Returns `TRUE` if the evaluated attribute contains a Boolean value of `true`. |
| `NOT EQUALS` | Returns `TRUE` if the evaluated attribute doesn't match the input string. The comparison is case-sensitive. |
| `NOT REGEX MATCH` | Returns `TRUE` if the evaluated attribute doesn't match a regular expression pattern. It returns `FALSE` if the attribute is null or empty. |
| `REGEX MATCH` | Returns `TRUE` if the evaluated attribute matches a regular expression pattern. For example, `([1-9][0-9])` matches any number from 10 through 99. The comparison is case-sensitive. |

#### Use regular expressions to filter

For more advanced filtering, use `REGEX MATCH` to search an attribute string for a substring. For example, consider groups that have the following descriptions:

- `Contoso-Sales-US`
- `Contoso-Marketing-US`
- `Contoso-Operations-US`
- `Contoso-LT-US`

To provision only the Sales, Marketing, and Operations groups to Active Directory, use the following regular expression:

```text
REGEX MATCH description (?:^|\W)Sales|Marketing|Operations(?:$|\W)
```

The expression searches the group descriptions for the supplied words and provisions only matching groups.

For more information about writing expressions, see [Reference for writing expressions for attribute mappings in Microsoft Entra ID](../../app-provisioning/functions-for-customizing-application-data).

### Group membership to on-premises users

When group synchronization is enabled, you can optionally provision membership from cloud groups to on-premises users in the **Configure group membership** step. This setting is off by default.

[![Screenshot of the Configure group membership step with the option to provision membership to on-premises users.](media/how-to-attribute-mapping-entra-to-active-directory/provision-membership-on-premises-users.png)](media/how-to-attribute-mapping-entra-to-active-directory/provision-membership-on-premises-users.png#lightbox)

### Scope using directory extensions

For more advanced scoping and filtering, you can use directory extensions. For an overview, see [Directory extensions for provisioning Microsoft Entra ID to Active Directory](custom-attribute-mapping-entra-to-active-directory). For a step-by-step tutorial, see [Using directory extensions when provisioning to Active Directory](tutorial-directory-extension-group-provisioning).

## Configure the target container

Use the **Target container** to control the organizational unit (OU) where user and group objects are created in Active Directory. You can use a **constant**, **direct**, or **expression** mapping on the `parentDistinguishedName` attribute.

[![Screenshot of the Configure target container step showing the user and group target containers.](media/how-to-attribute-mapping-entra-to-active-directory/configure-target-container.png)](media/how-to-attribute-mapping-entra-to-active-directory/configure-target-container.png#lightbox)

- **Users** — the default user target container automatically preserves the original OU of a user whose Source of Authority (SOA) is converted to the cloud (the default `parentDistinguishedName` expression uses `onPremisesDistinguishedName`). A cloud-native user is created in `CN=Users,DC=<selected AD domain>`, which you can override.

    [![Screenshot of the expression used to map the user target container.](media/how-to-attribute-mapping-entra-to-active-directory/edit-user-target-container-mapping.png)](media/how-to-attribute-mapping-entra-to-active-directory/edit-user-target-container-mapping.png#lightbox)
- **Groups** — the default group target container is `CN=Users,DC=<selected AD domain>`. To place groups in different OUs by attribute, use an expression with the `Switch()` function. The following example routes groups by display name:

    ```text
    Switch([displayName],"OU=Default,OU=container,DC=contoso,DC=com","Marketing","OU=Marketing,OU=container,DC=contoso,DC=com","Sales","OU=Sales,OU=container,DC=contoso,DC=com")
    ```

    [![Screenshot of an expression that configures multiple group target containers.](media/how-to-attribute-mapping-entra-to-active-directory/multiple-target-containers.png)](media/how-to-attribute-mapping-entra-to-active-directory/multiple-target-containers.png#lightbox)

    Display name is a weak routing key because it can change and isn't guaranteed to follow a consistent pattern. To route groups by a stable value, or to keep a group in the organizational unit it already occupies, use a directory extension instead. For more information, see Preserve the OU path.

### Preserve the OU path

How the original OU is preserved depends on the object type:

- **Users** — preservation is built in. The default `parentDistinguishedName` mapping re-creates a SOA-converted user in their original OU, so no extra configuration is required.
- **Groups** — the original OU isn't detected automatically. Use the `GroupDN` directory extension to capture the group's distinguished name (DN) before you convert its SOA, then reference that extension in the OU and common name (CN) mapping expressions.

To set up the extension, see [Preserve a group's organizational unit and name](how-to-preserve-group-organizational-unit-entra-to-active-directory). Complete that setup before you convert the group to cloud-managed, then use the expressions that follow.

### Preserve a group's original organizational unit

To map a SOA-converted group to its original OU, adapt the sample expression by replacing `extension_<AppIdWithoutHyphens>_GroupDN` with the extension attribute name in your tenant, and `<Default ParentDistinguishedName>` with the target OU to use when the extension value is empty:

```text
IIF(
    IsPresent([extension_<AppIdWithoutHyphens>_GroupDN]),
    Replace(
        Mid(
            Mid(
                Replace([extension_<AppIdWithoutHyphens>_GroupDN], "\,", , , "\2C", , ),
                Instr(Replace([extension_<AppIdWithoutHyphens>_GroupDN], "\,", , , "\2C", , ), ",", , ),
                9999
            ),
            2,
            9999
        ),
        "\2C", , , ",", ,
    ),
    "<Default ParentDistinguishedName>"
)
```

Set **Default value (if null)** to the target OU to use when the `GroupDN` extension is empty.

Apply the expression to the target-container mapping:

1. Under **Group target container**, select **Edit attribute mapping**.
2. Change **Mapping type** to **Expression**.
3. Paste the expression into the expression box.
4. Select **Apply**, and then select **Save**.

### Preserve a group's original common name

Use the same `GroupDN` extension to preserve the common name (CN). The expression extracts the CN from the stored distinguished name and uses the group display name and object ID as a fallback:

```text
IIF(
    IsPresent([extension_<AppIdWithoutHyphens>_GroupDN]),
    Replace(
        Replace(
            Replace(
                Word(Replace([extension_<AppIdWithoutHyphens>_GroupDN], "\,", , , "\2C", , ), 1, ","),
                "CN=", , , "", ,
            ),
            "cn=", , , "", ,
        ),
        "\2C", , , ",", ,
    ),
    Append(Append(Left(Trim([displayName]), 51), "_"), Mid([objectId], 25, 12))
)
```

Apply the expression to the `cn` attribute mapping, then select **Save schema**.

When you finish configuring scoping filters and target containers, select **Save**. A message tells you what to configure next; select the link to continue.

## Configure attribute mapping

Microsoft Entra Cloud Sync maps attributes between your Microsoft Entra ID users/groups and the AD objects. Because the AD schema isn't discoverable, each Microsoft Entra ID to AD configuration uses a fixed set of default mappings, which you can customize for your business needs.

### Keep the same group name

By default, `sAMAccountName` isn't synchronized from Microsoft Entra ID to Active Directory, so a newly created group in AD receives a randomly generated `sAMAccountName`. To keep a consistent group name in AD, create a custom mapping to `sAMAccountName`. For example, use the following expression:

```text
Join("_", [displayName], "Contoso_Group")
```

The expression combines the `displayName` value with `Contoso_Group`. For example, a group with the display name `Marketing` receives the `sAMAccountName` value `Marketing_Contoso_Group`.

Important

Ensure that every custom `sAMAccountName` value is unique within Active Directory.

### Change other attribute mappings as needed

The following tables list the default user and group attribute mappings. You can change any of these mappings based on your requirements — modify an existing mapping, delete one, or add a new one. Some mappings are managed by the service and can't be edited.

To add a mapping:

1. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.
2. Under **Configuration**, select your Microsoft Entra ID to AD configuration.
3. On the left, select **Attribute mapping**.
4. At the top, select the object type you're mapping: **user**, **group**, or **contact**.
5. Select **Add attribute mapping**, and then select the mapping type:

    - **Direct** — the target attribute takes the value of the source attribute.
    - **Constant** — the target attribute takes a fixed string that you specify.
    - **Expression** — the target attribute takes the result of an expression.
    - **None** — the target attribute is left unmodified.
6. Fill in the remaining options for the mapping type you chose, select when to apply the mapping, and then select **Apply**.
7. Select **Save schema**. Saving the schema triggers a synchronization.

For more information about writing expressions, see [Reference for writing expressions for attribute mappings in Microsoft Entra ID](../../app-provisioning/functions-for-customizing-application-data).

#### User attribute mappings

| Target attribute (Active Directory) | Source attribute (Microsoft Entra ID) | Mapping type |
| --- | --- | --- |
| `accountDisabled` | `Not([accountEnabled])` | Expression |
| `cn` | `Append(Append(Left(Trim([displayName]), 51), "_"), Mid([objectId], 25, 12))` | Expression |
| `co` | `IgnoreFlowIfNullOrEmpty(Trim([country]))` | Expression |
| `company` | `IgnoreFlowIfNullOrEmpty(Trim([companyName]))` | Expression |
| `department` | `IgnoreFlowIfNullOrEmpty(Trim([department]))` | Expression |
| `displayName` | `displayName` | Direct |
| `employeeID` | `IgnoreFlowIfNullOrEmpty([employeeId])` | Expression |
| `givenName` | `IgnoreFlowIfNullOrEmpty(Trim([givenName]))` | Expression |
| `l` | `IgnoreFlowIfNullOrEmpty(Trim([city]))` | Expression |
| `manager` | `manager` | Direct |
| `mobile` | `IgnoreFlowIfNullOrEmpty(Trim([mobile]))` | Expression |
| `msDS-ObjectSoa` | `Cloud` | Constant |
| `parentDistinguishedName` | expression preserving the original OU | Expression |
| `postalCode` | `IgnoreFlowIfNullOrEmpty(Trim([postalCode]))` | Expression |
| `preferredLanguage` | `IgnoreFlowIfNullOrEmpty(Trim([preferredLanguage]))` | Expression |
| `sAMAccountName` | `Left(Item(Split([userPrincipalName], "@"), 1), 15)` | Expression |
| `sn` | `IgnoreFlowIfNullOrEmpty(Trim([surname]))` | Expression |
| `st` | `IgnoreFlowIfNullOrEmpty(Trim([state]))` | Expression |
| `streetAddress` | `IgnoreFlowIfNullOrEmpty(Trim([streetAddress]))` | Expression |
| `userPrincipalName` | `IIF(IsPresent([onPremisesUserPrincipalName]), [onPremisesUserPrincipalName], Append(Item(Split([userPrincipalName], "@"), 1), Append("@", %DomainFQDN%)))` | Expression |

Some user mappings (for example, `adminDescription` and `msDS-ExternalDirectoryObjectId`) are managed by the service, aren't visible in the UI, and must not be edited.

#### Group attribute mappings

| Target attribute (Active Directory) | Source attribute (Microsoft Entra ID) | Mapping type |
| --- | --- | --- |
| `cn` | `Append(Append(Left(Trim([displayName]),51),"_"),Mid([objectId],25,12))` | Expression |
| `description` | `Left(Trim([description]),448)` | Expression |
| `displayName` | `displayName` | Direct |
| `isSecurityGroup` | `True` | Constant |
| `member` | `members` | Direct |
| `parentDistinguishedName` | `CN=Users,DC=<selected AD domain>` | Constant |
| `UniversalScope` | `True` | Constant |

Service-managed group mappings (`adminDescription`, `msDS-ExternalDirectoryObjectId`, `ObjectGUID`) aren't visible in the UI and must not be edited.

### Directory extensions and custom attribute mapping

Microsoft Entra Cloud Sync lets you add directory extensions and map them to custom attributes. For more information, see [Directory extensions for provisioning Microsoft Entra ID to Active Directory](custom-attribute-mapping-entra-to-active-directory).

When your attribute mappings are complete, select **Save schema**. A message tells you what to configure next; select the link to continue.

## Verify and manage provisioned objects

The following tasks apply after provisioning runs. Before you work through them, [test and enable your configuration](how-to-test-and-enable-provisioning-entra-to-active-directory).

### Verify provisioning

After you convert SOA and the object is in scope, run provisioning and confirm the result. These steps apply to all three deployment options: users only, groups only, or users and groups.

**Groups:**

- Confirm that the SOA-converted group is available in the provisioning configuration's group scope.

    [![Screenshot of a SOA-converted group selected in the provisioning configuration's group scope.](media/tutorial-group-provision/group-scope.png)](media/tutorial-group-provision/group-scope.png#lightbox)
- When the job runs, the SOA-converted group is provisioned successfully. In **Provisioning logs**, search for the group and verify it was provisioned.

    [![Screenshot of a successful group update in the provisioning logs.](media/tutorial-group-provision/provisioning-logs.png)](media/tutorial-group-provision/provisioning-logs.png#lightbox)
- Open the provisioning log details and confirm that the group was **matched** with an existing target group.

    [![Screenshot of provisioning log details showing a group matched and updated in Active Directory.](media/tutorial-group-provision/matched.png)](media/tutorial-group-provision/matched.png#lightbox)
- On the **Modified Properties** tab, confirm that the target group's `adminDescription` and `cn` attributes are updated.

    [![Screenshot of provisioning log modified properties showing updated cn and adminDescription attributes.](media/tutorial-group-provision/confirm-updates.png)](media/tutorial-group-provision/confirm-updates.png#lightbox)

#### Verify in AD DS

In **Active Directory Users and Computers**, confirm that the original group is updated in its expected OU rather than a duplicate group being created.

[![Screenshot of a provisioned security group in its Active Directory organizational unit.](media/tutorial-group-provision/verify.png)](media/tutorial-group-provision/verify.png#lightbox)

Open the group properties and verify that the expected group name, scope, and attributes are present.

[![Screenshot of the updated SOA-converted group's general properties in Active Directory.](media/tutorial-group-provision/updated-group.png)](media/tutorial-group-provision/updated-group.png#lightbox)

[![Screenshot of the updated SOA-converted group's Attribute Editor showing its distinguished name, cn, and adminDescription values.](media/tutorial-group-provision/group-properties.png)](media/tutorial-group-provision/group-properties.png#lightbox)

### Cloud skips changes made in AD after SOA conversion

After you convert an object's SOA to the cloud, the cloud is the source of authority. If you edit an attribute of that object directly in AD DS (for example, rename a group), Cloud Sync **skips** the object during provisioning. In **Provisioning logs**, the object shows as **Skipped**, and the details explain that the object isn't synced because its SOA is converted to the cloud.

[![Screenshot of an SOA-converted group's name being changed directly in Active Directory.](media/tutorial-group-provision/update-group-name.png)](media/tutorial-group-provision/update-group-name.png#lightbox)

[![Screenshot of the provisioning logs showing the modified SOA-converted group with a Skipped status.](media/tutorial-group-provision/skipped.png)](media/tutorial-group-provision/skipped.png#lightbox)

[![Screenshot of provisioning log details explaining that export was skipped because the group's SOA was converted to the cloud.](media/tutorial-group-provision/sync-blocked.png)](media/tutorial-group-provision/sync-blocked.png#lightbox)

### Move a provisioned user to a different organizational unit

After a user is provisioned, changing the **Target container** doesn't move them, and moving the object manually in AD DS is reverted on the next sync cycle. This behavior is expected, because the default `parentDistinguishedName` expression checks whether the user already has an on-premises location:

```text
IIF(IsNullOrEmpty([onPremisesDistinguishedName]), "OU=Cloud_Users,DC=contoso,DC=com", Replace([onPremisesDistinguishedName], , "^.*?,(?=(?:CN|OU|DC)=)", , "", , ))
```

When `onPremisesDistinguishedName` is empty, the user is created in the constant target container you specified. When it's populated, the expression derives the OU from that attribute instead and ignores the constant. That precedence preserves the original OU of a user whose SOA is converted to the cloud. It's also why an already-provisioned user keeps returning to the OU recorded on their cloud object.

A cloud-native user has no `onPremisesDistinguishedName` until the first provisioning cycle, which writes the value back to the cloud object. For the full list of attributes written back, see [On-premises attributes written back to Microsoft Entra ID](how-provisioning-to-active-directory-works#on-premises-attributes-written-back-to-microsoft-entra-id).

[![Screenshot of a user's on-premises properties in Microsoft Entra ID showing the on-premises distinguished name.](media/how-to-attribute-mapping-entra-to-active-directory/on-premises-distinguished-name-original-organizational-unit.png)](media/how-to-attribute-mapping-entra-to-active-directory/on-premises-distinguished-name-original-organizational-unit.png#lightbox)

To move a user, use the option that matches the scope of the change:

- **All users that match a mapping rule** — change the target container mapping so it points to the new OU, then select **Save**. Provisioning restarts and moves every user that matches the mapping rules on the next cycle.
- **A single user** — update that user's `onPremisesDistinguishedName` attribute in Microsoft Entra ID.
- **A user that's moving to a different domain** — remove the user from the current configuration's scope, then add the user to the scope of the configuration that targets the other domain.

The `onPremisesDistinguishedName` attribute is read-only unless you're assigned at least the [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) role. The Microsoft Entra admin center doesn't expose on-premises attributes for editing, so use Microsoft Graph to update a single user:

```http
PATCH https://graph.microsoft.com/v1.0/users/{user-id}
Content-Type: application/json

{
    "onPremisesDistinguishedName": "CN=Cloud User,OU=Cloud_Users,DC=contoso,DC=com"
}
```

A `204 No Content` response confirms the update. The user moves to the new OU on the next sync cycle.

[![Screenshot of a Microsoft Graph PATCH request that updates the on-premises distinguished name and returns 204 No Content.](media/how-to-attribute-mapping-entra-to-active-directory/graph-update-on-premises-distinguished-name.png)](media/how-to-attribute-mapping-entra-to-active-directory/graph-update-on-premises-distinguished-name.png#lightbox)

To confirm the move, open the user's entry in **Provisioning logs** and select **Modified Properties**. The `parentDistinguishedName` row shows the old and new values.

[![Screenshot of provisioning log details showing the old and new parentDistinguishedName values.](media/how-to-attribute-mapping-entra-to-active-directory/provisioning-log-parent-distinguished-name-updated.png)](media/how-to-attribute-mapping-entra-to-active-directory/provisioning-log-parent-distinguished-name-updated.png#lightbox)

### Roll back a SOA-converted user or group

If you roll back a SOA-converted user or group so that AD DS owns it again, provisioning stops syncing changes for that object and removes it from the configuration scope. The on-premises object isn't deleted, and on-premises control resumes in the next sync cycle.

To confirm a rollback, check the **Audit logs** to verify that sync no longer happens for the object because it's managed on-premises, then confirm in AD DS that the object is still present.