---
layout: Conceptual
title: Use map UserType with Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-map-usertype
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to map the UserType attribute with cloud sync.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange
locale: en-us
document_id: 30b86453-ae19-6534-543a-37f9e8e2beb0
document_version_independent_id: c03aa0ba-5784-ea3d-f940-b398a756089f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-map-usertype.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-map-usertype
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-map-usertype.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 4cb47924-3081-00c3-5096-47022d9b2ded
---

# Use map UserType with Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn

Cloud sync supports synchronization of the **UserType** attribute for User objects.

By default, the **UserType** attribute isn't enabled for synchronization because there's no corresponding **UserType** attribute in on-premises Active Directory. You must manually add this mapping for synchronization. Before you do this step, you must take note of the following behavior enforced by Microsoft Entra ID:

- Microsoft Entra-only accepts two values for the **UserType** attribute: Member and Guest.
- If the **UserType** attribute isn't mapped in cloud sync, Microsoft Entra users created through directory synchronization would have the **UserType** attribute set to Member.

Before you add a mapping for the **UserType** attribute, you must first decide how the attribute is derived from on-premises Active Directory. The following approaches are the most common:

- Designate an unused on-premises Active Directory attribute, such as extensionAttribute1, to be used as the source attribute. The designated on-premises Active Directory attribute should be of the type string, be single-valued, and contain the value Member or Guest.
- If you choose this approach, you must ensure that the designated attribute is populated with the correct value for all existing user objects in on-premises Active Directory that are synchronized to Microsoft Entra ID before you enable synchronization of the **UserType** attribute.

## Add the UserType mapping

To add the **UserType** mapping:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. Under **Manage attributes**, select **Click to edit mappings**.

    ![Screenshot that shows editing the attribute mappings.](media/how-to-map-usertype/usertype-1.png)
3. Select **Add attribute mapping**.

    ![Screenshot that shows adding a new attribute mapping.](media/how-to-map-usertype/usertype-2.png)
4. Select the mapping type. You can do the mapping in one of three ways:

- A direct mapping, for example, from an Active Directory attribute
- An expression, such as IIF(InStr([userPrincipalName], "@partners") &gt; 0,"Guest","Member")
- A constant, for example, make all user objects as Guest

    ![Screenshot that shows adding a UserType attribute.](media/how-to-map-usertype/usertype-3.png)

1. In the **Target attribute** dropdown box, select **UserType**.
2. Select **Apply** at the bottom of the page to create a mapping for the Microsoft Entra ID **UserType** attribute.