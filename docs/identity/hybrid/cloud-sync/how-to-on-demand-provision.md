---
layout: Conceptual
title: On-demand provisioning in Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-on-demand-provision
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to use the cloud sync feature of Microsoft Entra Connect to test configuration changes.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: bdab6310-6ecf-0795-edd3-4ad4ef159003
document_version_independent_id: 149e04b0-b61e-3e30-28a3-1d95ffa14046
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-on-demand-provision.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-on-demand-provision
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-on-demand-provision.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: cfc14bfd-c3dc-e9fa-08f6-7ccb1d56334b
---

# On-demand provisioning in Microsoft Entra Cloud Sync - Microsoft Entra ID | Microsoft Learn

You can use the cloud sync feature of Microsoft Entra Connect to test configuration changes by applying these changes to a single user. This on-demand provisioning helps you validate and verify that the changes made to the configuration were applied properly and are being correctly synchronized to Microsoft Entra ID.

This article covers on-demand provisioning for configurations that provision from Active Directory to Microsoft Entra ID. If you're looking for information about provisioning from Microsoft Entra ID to Active Directory, see [On-demand provisioning - Microsoft Entra ID to Active Directory](how-to-on-demand-provision-entra-to-active-directory).

Important

When you use on-demand provisioning, the scoping filters are not applied to the user that you selected. You can use on-demand provisioning on users who are outside the organization units that you specified.

For additional information and an example see the following video.

## Validate a user

To use on-demand provisioning, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Enter the distinguished name of a user and select the **Provision** button.

[![Screenshot of user distinguished name.](media/how-to-on-demand-provision/new-ux-2.png)](media/how-to-on-demand-provision/new-ux-2.png#lightbox)

1. After provisioning finishes, a success screen appears with four green check marks. Any errors appear to the left.

[![Screenshot of on-demand success.](media/how-to-on-demand-provision/new-ux-3.png)](media/how-to-on-demand-provision/new-ux-3.png#lightbox)

## Get details about provisioning

Now you can look at the user information and determine if the changes that you made in the configuration have been applied. The rest of this article describes the individual sections that appear in the details of a successfully synchronized user.

### Import user

The **Import user** section provides information on the user who was imported from Active Directory. This is what the user looks like before provisioning into Microsoft Entra ID. Select the **View details** link to display this information.

By using this information, you can see the various attributes (and their values) that were imported. If you created a custom attribute mapping, you can see the value here.

[![Screenshot of import user.](media/how-to-on-demand-provision/new-ux-4.png)](media/how-to-on-demand-provision/new-ux-4.png#lightbox)

### Determine if user is in scope

The **Determine if user is in scope** section provides information on whether the user who was imported to Microsoft Entra ID is in scope. Select the **View details** link to display this information.

By using this information, you can see if the user is in scope.

[![Screenshot of scope determination.](media/how-to-on-demand-provision/new-ux-5.png)](media/how-to-on-demand-provision/new-ux-5.png#lightbox)

### Match user between source and target system

The **Match user between source and target system** section provides information on whether the user already exists in Microsoft Entra ID and whether a join should occur instead of provisioning a new user. Select the **View details** link to display this information.

By using this information, you can see whether a match was found or if a new user is going to be created.

[![Screenshot of matching user.](media/how-to-on-demand-provision/new-ux-6.png)](media/how-to-on-demand-provision/new-ux-6.png#lightbox)

The matching details show a message with one of the three following operations:

- **Create**: A user is created in Microsoft Entra ID.
- **Update**: A user is updated based on a change made in the configuration.
- **Delete**: A user is removed from Microsoft Entra ID.

Depending on the type of operation that you've performed, the message varies.

### Perform action

The **Perform action** section provides information on the user who was provisioned or exported into Microsoft Entra ID after the configuration was applied. This is what the user looks like after provisioning into Microsoft Entra ID. Select the **View details** link to display this information.

By using this information, you can see the values of the attributes after the configuration was applied. Do they look similar to what was imported, or are they different? Was the configuration applied successfully?

This process enables you to trace the attribute transformation as it moves through the cloud and into your Microsoft Entra tenant.

[![Screenshot of perform action.](media/how-to-on-demand-provision/new-ux-7.png)](media/how-to-on-demand-provision/new-ux-7.png#lightbox)