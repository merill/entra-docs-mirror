---
layout: Conceptual
title: Map directory extensions in cross-tenant synchronization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-directory-extensions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.reviewer: hafowler
ms.service: entra-id
ms.subservice: multitenant-organizations
manager: dougeby
description: Map custom directory extension attributes in cross-tenant synchronization. Covers creating extensions, adding them to attribute mappings, and manual schema editing.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 21a28549-040d-3b14-5109-1058ed19d7f5
document_version_independent_id: 21a28549-040d-3b14-5109-1058ed19d7f5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/cross-tenant-synchronization-directory-extensions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/cross-tenant-synchronization-directory-extensions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/cross-tenant-synchronization-directory-extensions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: c96a701e-0e5d-0f5c-c677-19f241b9f5ac
---

# Map directory extensions in cross-tenant synchronization - Microsoft Entra ID | Microsoft Learn

## Overview

Directory extensions enable you to extend the schema in Microsoft Entra ID with your own attributes. You can map these directory extensions when provisioning users in cross-tenant synchronization. [Custom security attributes](../../fundamentals/custom-security-attributes-overview) are different and aren't supported in cross-tenant synchronization.

This article describes how to map directory extensions in cross-tenant synchronization.

## Prerequisites

- [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator) role to configure cross-tenant synchronization.
- [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) or [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) role to assign users to a configuration and to delete a configuration.

## Create directory extensions

If you don't already have directory extensions, you must create one or more directory extensions in the source or target tenant. You can create extensions using Microsoft Entra Connect or Microsoft Graph API. For information on how to create directory extensions, see [Syncing extension attributes for Microsoft Entra Application Provisioning](../app-provisioning/user-provisioning-sync-attributes-for-mapping).

## Map directory extensions

![Icon for the source tenant.](../../media/common/icons/entra-id-purple.png)**Source tenant**

Once you have one or more directory extensions, you can use them when mapping attributes in cross-tenant synchronization.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) of the source tenant.
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant synchronization**.
3. Select **Configurations** and then select your configuration.
4. Select **Provisioning** and expand the **Mappings** section.

    [![Screenshot that shows the Provisioning page with the Mappings section expanded.](media/common/provisioning-mappings.png)](media/common/provisioning-mappings.png#lightbox)
5. Select **Provision Microsoft Entra ID Users** to open the **Attribute Mapping** page.
6. Scroll to the bottom of the page and select **Add new mapping**.

    [![Screenshot that shows the Attribute Mappings page with the Add new mapping link.](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-new-mapping.png)](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-new-mapping.png#lightbox)
7. In the **Source attribute** drop-down list, select a source attribute.

    If you created a directory extension in the source tenant, select the directory extension.

    [![Screenshot that shows the Edit attribute page with the directory extension listed in Source Attribute.](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-source-attribute.png)](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-source-attribute.png#lightbox)

    If the directory extension isn't listed, make sure that the directory extension was created successfully. You can also try to manually add the directory extension to the attribute list as described in the next section.
8. In the **Target attribute** drop-down list, select a target attribute.

    If you created a directory extension in the target tenant, select the directory extension.
9. Select **Ok** to save the mapping.

## Manually add directory extensions to the attribute list

![Icon for the source tenant.](../../media/common/icons/entra-id-purple.png)**Source tenant**

If your directory extension wasn't automatically discovered, you can try the following steps to manually add the directory extension to the attribute list.

1. Sign in to the Microsoft Entra admin center of the source tenant using the following link:

    https://entra.microsoft.com/?Microsoft_AAD_Connect_Provisioning_forceSchemaEditorEnabled=true
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant synchronization**.
3. Select **Configurations** and then select your configuration.
4. Select **Provisioning** and expand the **Mappings** section.
5. Select **Provision Microsoft Entra ID Users** to open the **Attribute Mapping** page.
6. Scroll to the bottom and select the **Show advanced settings** checkbox.

    [![Screenshot of the Attribute Mapping page with advanced options displayed.](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-advanced-settings.png)](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-advanced-settings.png#lightbox)

    Tip

    If you don't see the **Edit attribute list** links, be sure that you are signed in to the Microsoft Entra admin center using the link in Step 1.
7. If you created a directory extension in the source tenant, select the **Edit attribute list for Microsoft Entra ID** link.
8. If you created an extension in the target tenant, select the **Edit attribute list for Azure Active Directory (target tenant)** link.
9. Add the directory extension and select the appropriate options.

    [![Screenshot of Edit Attributes List page with a directory extension added.](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-advanced-settings-directory-extension.png)](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-advanced-settings-directory-extension.png#lightbox)
10. Select **Save**.
11. Refresh the browser.
12. Browse to the **Attribute mappings** page and try to map the directory extension as described earlier in this article.

## Manually add directory extensions by editing the schema

![Icon for the source tenant.](../../media/common/icons/entra-id-purple.png)**Source tenant**

Follow these steps to manually add directory extensions to the schema by using the schema editor.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) of the source tenant.
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant synchronization**.
3. Select **Configurations** and then select your configuration.
4. Select **Provisioning** and expand the **Mappings** section.
5. Select **Provision Microsoft Entra ID Users** to open the **Attribute Mapping** page.
6. Scroll to the bottom and select the **Show advanced settings** checkbox.

    [![Screenshot of the Attribute Mapping page with link to schema editor.](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-advanced-settings.png)](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-advanced-settings.png#lightbox)
7. Select the **Review your schema here** link to open the **Schema editor** page.

    [![Screenshot of the Schema editor page the options to edit the schema in JSON.](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-schema-editor.png)](media/cross-tenant-synchronization-directory-extensions/provisioning-mappings-schema-editor.png#lightbox)
8. Download an original copy of the schema as a backup.
9. Modify the schema following your required configuration.
10. Select **Save**.
11. Refresh the browser.
12. Browse to the **Attribute mappings** page and try to map the directory extension as described earlier in this article.