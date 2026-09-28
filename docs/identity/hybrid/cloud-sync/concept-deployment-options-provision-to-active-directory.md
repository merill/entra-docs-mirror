---
layout: Conceptual
title: Microsoft Entra provisioning options (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/concept-deployment-options-provision-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: mwongerapk
ms.reviewer: marshmacy
ms.subservice: hybrid-cloud-sync
ms.topic: concept-article
ms.date: 2026-08-10T00:00:00.0000000Z
description: Compare group-only, user-only, and combined Microsoft Entra Cloud Sync options for provisioning from Microsoft Entra ID to Active Directory.
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: d8fe8003-b00a-1cb9-8705-7f0a627509be
document_version_independent_id: d8fe8003-b00a-1cb9-8705-7f0a627509be
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/concept-deployment-options-provision-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/concept-deployment-options-provision-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/concept-deployment-options-provision-to-active-directory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: ab17f4c3-d29a-85c6-c4b9-0104a22aec73
---

# Microsoft Entra provisioning options (Preview) - Microsoft Entra ID | Microsoft Learn

When you provision from Microsoft Entra ID to on-premises Active Directory Domain Services (AD DS) with Microsoft Entra Cloud Sync, you choose *what* a configuration provisions through its **scoping filters**. This article compares the three deployment options and helps you pick the right one and the right scale.

For a conceptual introduction, see [Overview of provisioning from Microsoft Entra ID to Active Directory](overview-provision-entra-id-to-active-directory). To configure any of these options, see [Configure provisioning to Active Directory](how-to-configure-entra-to-active-directory).

## The three deployment options

All three options use the same configuration type in Cloud Sync — **Microsoft Entra ID to AD sync**. What differs is the object types you bring into scope.

| Option | Provisions | Availability | Choose when |
| --- | --- | --- | --- |
| **Groups only** | Security groups, along with their memberships to on-premises owned users | Generally available | You want to govern access to on-premises applications for on-premises owned users only. Cloud-native users and users whose Source of Authority (SOA) is converted to the cloud don't need access to on-premises applications. |
| **Users only** | Users | Preview | You want to govern identity lifecycle in Microsoft Entra ID while keeping access governance in AD. |
| **Users and groups** | Users and security groups, along with their memberships to both on-premises owned and cloud-owned users | Preview | You want to govern identity lifecycle and access to on-premises applications from Microsoft Entra ID. |

Note

Provisioning **users** (users-only and users-and-groups) is currently in **preview**. Provisioning **groups** is generally available.

### How you select an option

You select the option in the scoping filters of a configuration:

- To provision **users**, bring users into scope.
- To provision **groups**, bring security groups into scope.
- To provision **both**, enable both object types in the same configuration.

For the step-by-step scoping procedure, see [Configure provisioning to Active Directory](how-to-configure-entra-to-active-directory#configure-scoping-filters).

## Configurations per domain and per tenant

There can be only one configuration per AD domain, so you don't run separate user and group configurations against the same domain. Instead, you choose which object types that domain's configuration brings into scope:

- Enable **both** users and groups to manage both object types for the domain in one place.
- Enable **one** object type if you only need to provision users or only groups. If you later decide to provision the other type, change the existing configuration to include it rather than creating a second one.

Configurations for different domains remain independent, so you can scope, schedule, and troubleshoot each domain separately. You can run up to 20 configurations per tenant, subject to the [license requirements](how-to-prerequisites-provision-entra-to-active-directory). This limit covers all configurations, whether they provision users, groups, or both.

## Performance and scale limits

Provisioning performance is affected by tenant size and by the number of objects in scope. Users, groups, and group membership links all count toward the same total. Because users have no membership model, each user counts as a single object, while a group counts as one object plus one for each of its membership links.

### Recommended configuration

Your scoping choices determine how much work the service does on every cycle. The provisioning configuration displays a warning when a choice is likely to slow provisioning down, but it doesn't block you from saving the configuration. The following table describes what to configure and why.

| Setting | Recommendation | Why |
| --- | --- | --- |
| **All users and groups** | Add at least one attribute value filter. | Without a filter, every user and group in the tenant is evaluated on every cycle, including objects you never intend to provision. Cycles take longer, and performance degrades further as the tenant grows. |
| **Selected users and groups** | Don't add attribute value filters. | Your selection already determines which objects are provisioned. A filter adds processing time to every cycle without changing which objects are provisioned. |
| **Provision membership to on-premises users** | Treat it as transitional. Convert the group's Source of Authority to the cloud and provision the group to Active Directory instead. | This setting writes membership links for members whose Source of Authority is still on-premises, which the service resolves per member on every cycle. Converting the group to cloud-managed removes the need for those links entirely. |

The two scoping modes have opposite filter requirements. **All users and groups** needs a filter to narrow an otherwise unbounded scope, while **Selected users and groups** is already narrow, so a filter is pure overhead. If you change an existing configuration from **All** to **Selected**, remove the attribute value filters you added.

### Prefer cloud-managed groups over on-premises membership

Provisioning membership to on-premises users keeps a cloud group aligned with members that Active Directory still owns. It works, but it isn't the best use of the feature: every cycle spends effort maintaining links to objects that another system controls.

The recommended end state is to [convert the group's Source of Authority to Microsoft Entra ID](../how-to-group-source-of-authority-configure) and provision that cloud-managed group to Active Directory. The group and its members are then managed in one place, and there are no membership links to synchronized users left to maintain.

### What isn't supported

Groups that are larger than 50K members aren't supported.

### Scale limits for groups and memberships

| Scoping mode | In-scope groups | Membership links (direct members) | Notes |
| --- | --- | --- | --- |
| **Selected security groups** | Up to 10K groups. The Cloud Sync pane in the Microsoft Entra admin center allows selecting and displaying up to 999 groups. To add more than 999 groups, see Expanded group selection via API. | Up to 250K total members across all in-scope groups. | Use this mode if your tenant exceeds any of these values: more than 200K users, more than 40K groups, or more than 1M group memberships. |
| **All security groups** with at least one attribute scoping filter | Up to 20K groups. | Up to 500K total members across all in-scope groups. | Use this mode only if your tenant satisfies all of these conditions: fewer than 200K users, fewer than 40K groups, and fewer than 1M group memberships. |

### Scale limits for users

| Configuration | Scale limit | Notes |
| --- | --- | --- |
| **Users only** | Up to 200K users | This limit aligns with the supported tenant scale conditions for group provisioning: fewer than 200K users, fewer than 40K groups, and fewer than 1M group memberships. No groups or membership links are processed in this configuration; all in-scope objects are users. |
| **Users and groups** | Measure the combined total against the limits in the preceding table | Users, groups, and membership links count toward the same total. |

### What to do if you exceed limits

Exceeding the recommended limits slows initial and delta sync and can cause sync errors. If this happens:

- **Too many groups or members in Selected security groups mode**: Reduce the number of in-scope groups. Because there's only one configuration per AD domain, you can't split a single domain's scope across multiple configurations.
- **Too many groups or members in All security groups mode**: Switch to **Selected security groups** mode.
- **Too many users in scope**: Narrow the user scoping filter so that fewer users are in scope.
- **A group exceeds 50K members**: Split membership across multiple groups, or adopt staged groups to keep each group under the cap.

### Expanded group selection via API

If you need to select more than 999 groups, use the [Grant an appRoleAssignment for a service principal](/en-us/graph/api/serviceprincipal-post-approleassignedto) API:

```https
POST https://graph.microsoft.com/v1.0/servicePrincipals/{servicePrincipalID}/appRoleAssignedTo
Content-Type: application/json

{
  "principalId": "",
  "resourceId": "",
  "appRoleId": ""
}
```

Where:

- **principalId**: Group object ID.
- **resourceId**: Job's service principal ID.
- **appRoleId**: Identifier of the app role exposed by the resource service principal.

App role IDs by cloud:

| Cloud | appRoleId |
| --- | --- |
| Public | `1a0abf4d-b9fa-4512-a3a2-51ee82c6fd9f` |
| AzureChinaCloud | `15af7fd5-1a3f-4034-8ea1-1afa3d5ecf63` |
| AzureUSGovernment | `d8fa317e-0713-4930-91d8-1dbeb150978f` |
| AzureUSNatCloud | `50a55e47-aae2-425c-8dcb-ed711147a39f` |
| AzureUSSecCloud | `52e862b9-0b95-43fe-9340-54f51248314f` |

## More considerations

- Group membership written to AD DS includes only members that have an AD DS account. Those members can be on-premises synchronized users, cloud-managed users that Cloud Sync provisions to AD DS because they're in scope of user provisioning, or other cloud-created security groups. A cloud-managed user that has no AD DS account is skipped.
- On-premises synchronized users must have the `onPremisesObjectIdentifier` attribute set, matching a corresponding `objectGUID` in the target AD DS environment.
- Only global Microsoft Entra ID tenants can provision from Microsoft Entra ID to AD DS. Tenants such as B2C aren't supported.
- The provisioning job runs on a recurring schedule.