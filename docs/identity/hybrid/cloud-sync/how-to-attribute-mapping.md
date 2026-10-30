---
layout: Conceptual
title: Attribute mapping in Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-attribute-mapping
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to use the cloud sync feature of Microsoft Entra Connect to map attributes.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 35b3514e-b8a9-e4c7-a0f7-236c3db9e98b
document_version_independent_id: 4b25143b-cfce-7002-e843-df7abb2b64b1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-attribute-mapping.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-attribute-mapping
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-attribute-mapping.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 387d5c23-9834-8d0d-bfad-f0469b55edc8
---

# Attribute mapping in Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn

You can use the cloud sync attribute mapping feature to map attributes between your on-premises user or group objects and the objects in Microsoft Entra ID.

[![Screenshot of new UX screen attribute mapping.](media/how-to-attribute-mapping/new-ux-mapping-1.png)](media/how-to-attribute-mapping/new-ux-mapping-1.png#lightbox)

The following document guides you through attribute scoping with Microsoft Entra Cloud Sync for provisioning from Active Directory to Microsoft Entra ID. If you're looking for information on attribute mapping from Microsoft Entra ID to AD, see [Configure Microsoft Entra ID to Active Directory provisioning](how-to-configure-entra-to-active-directory).

You can customize (change, delete, or create) the default attribute mappings according to your business needs. For a list of attributes that are synchronized, see [Attributes synchronized to Microsoft Entra ID](../connect/reference-connect-sync-attributes-synchronized).

Note

This article describes how to use the Microsoft Entra admin center to map attributes. For information on using Microsoft Graph, see [Transformations](how-to-transformation).

## Understand types of attribute mapping

With attribute mapping, you control how attributes are populated in Microsoft Entra ID. Microsoft Entra ID supports four mapping types:

| Mapping Type | Description |
| --- | --- |
| **Direct** | The target attribute is populated with the value of an attribute of the linked object in Active Directory. |
| **Constant** | The target attribute is populated with a specific string that you specify. |
| **Expression** | The target attribute is populated based on the result of a script-like expression. For more information, see [Expression Builder](how-to-expression-builder) and [Writing expressions for attribute mappings in Microsoft Entra ID](reference-expressions). |
| **None** | The target attribute is left unmodified. However, if the target attribute is ever empty, it's populated with the default value that you specify. |

Along with these basic types, custom attribute mappings support the concept of an optional *default* value assignment. The default value assignment ensures that a target attribute is populated with a value if Microsoft Entra ID or the target object doesn't have a value. The most common configuration is to leave this blank.

## Schema updates and mappings

Cloud sync occasionally updates the schema and the list of default attributes that are [synchronized](../connect/reference-connect-sync-attributes-synchronized). These default attribute mappings are available for new installations but won't automatically be added to existing installations. To add these mappings, you can follow the steps below.

1. Click on **add attribute mapping**
2. Select the Target attribute dropdown
3. You should see the new attributes that are available here.

The list of new mappings that were added.

| Attribute Added | Mapping Type | Added with Agent Version |
| --- | --- | --- |
| preferredDatalocation | Direct | 1.1.359.0 |
| EmployeeNumber | Direct | 1.1.359.0 |
| UserType | Direct | 1.1.359.0 |

For more information on how to map UserType, see [Map UserType with cloud sync](how-to-map-usertype).

## Understand properties of attribute mappings

Along with the type property, attribute mappings support certain attributes. These attributes depend on the type of mapping you have selected. The following sections describe the supported attribute mappings for each of the individual types. The following type of attribute mapping is available.

- Direct
- Constant
- Expression

### Direct mapping attributes

The following are the attributes supported by a direct mapping:

- **Source attribute**: The user attribute from the source system (example: Active Directory).
- **Target attribute**: The user attribute in the target system (example: Microsoft Entra ID).
- **Default value if null (optional)**: The value that is passed to the target system if the source attribute is null. This value is provisioned only when a user is created. It won't be provisioned when you're updating an existing user.
- **Apply this mapping**:
    - **Always**: Apply this mapping on both user-creation and update actions.
    - **Only during creation**: Apply this mapping only on user-creation actions.

[![Screenshot of editing attribute mapping.](media/how-to-attribute-mapping/new-ux-mapping-2.png)](media/how-to-attribute-mapping/new-ux-mapping-2.png#lightbox)

### Constant mapping attributes

The following are the attributes supported by a constant mapping:

- **Constant value**: The value that you want to apply to the target attribute.
- **Target attribute**: The user attribute in the target system (example: Microsoft Entra ID).
- **Apply this mapping**:
    - **Always**: Apply this mapping on both user-creation and update actions.
    - **Only during creation**: Apply this mapping only on user-creation actions.

### Expression mapping attributes

The following are the attributes supported by an expression mapping:

- **Expression**: This expression is the expression that is going to be applied to the target attribute. For more information, see [Expression Builder](how-to-expression-builder) and [Writing expressions for attribute mappings in Microsoft Entra ID](reference-expressions).
- **Default value if null (optional)**: The value that is passed to the target system if the source attribute is null. This value is provisioned only when a user is created. It won't be provisioned when you're updating an existing user.
- **Target attribute**: The user attribute in the target system (example: Microsoft Entra ID).
- **Apply this mapping**:

    - **Always**: Apply this mapping on both user-creation and update actions.
    - **Only during creation**: Apply this mapping only on user-creation actions.

## Add an attribute mapping - AD to Microsoft Entra ID

Use the following steps for configuring attribute mapping with a [AD to Microsoft Entra configuration](how-to-configure).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Attribute mapping**.
3. At the top, ensure that you have the correct object type selected. That is, user, group, or contact.
4. Click **Add attribute mapping**.

[![Screenshot of adding an attribute mapping.](media/how-to-attribute-mapping/new-ux-mapping-3.png)](media/how-to-attribute-mapping/new-ux-mapping-3.png#lightbox)

1. Select the mapping type. This can be one of the following:

    - **Direct**: The target attribute is populated with the value of an attribute of the linked object in Active Directory.
    - **Constant**: The target attribute is populated with a specific string that you specify.
    - **Expression**: The target attribute is populated based on the result of a script-like expression.
    - **None**: The target attribute is left unmodified.
2. Depending on what you have selected in the previous step, different options are available for filling in.
3. Select when to apply this mapping, and then select **Apply**. [![Screenshot of saving an attribute mapping.](media/how-to-attribute-mapping/new-ux-mapping-4.png)](media/how-to-attribute-mapping/new-ux-mapping-4.png#lightbox)
4. Back on the **Attribute mappings** screen, you should see your new attribute mapping.
5. Select **Save schema**. You'll be notified that once you save the schema, a synchronization occurs. Click **OK**. [![Screenshot of saving schema.](media/how-to-attribute-mapping/new-ux-mapping-5.png)](media/how-to-attribute-mapping/new-ux-mapping-5.png#lightbox)
6. Once the save is successful you'll see a notification on the right.

[![Screenshot of successful schema save.](media/how-to-attribute-mapping/new-ux-mapping-6.png)](media/how-to-attribute-mapping/new-ux-mapping-6.png#lightbox)

## Test your attribute mapping

To test your attribute mapping, you can use [on-demand provisioning](how-to-on-demand-provision):

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Enter the distinguished name of a user and select the **Provision** button.

[![Screenshot of user distinguished name.](media/how-to-on-demand-provision/new-ux-2.png)](media/how-to-on-demand-provision/new-ux-2.png#lightbox)

1. A success screen appears with four green check marks. Any errors appear to the left.

[![Screenshot of on-demand success.](media/how-to-on-demand-provision/new-ux-3.png)](media/how-to-on-demand-provision/new-ux-3.png#lightbox)