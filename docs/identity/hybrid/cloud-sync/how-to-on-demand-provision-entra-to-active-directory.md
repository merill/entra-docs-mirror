---
layout: Conceptual
title: On-demand provisioning - Microsoft Entra ID to Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-on-demand-provision-entra-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to use on-demand provisioning when provisioning from Microsoft Entra ID to Active Directory.
ms.topic: how-to
ms.date: 2026-08-24T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange, msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: 7b1f8f34-8f50-586b-550e-30501a052201
document_version_independent_id: 7b1f8f34-8f50-586b-550e-30501a052201
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-on-demand-provision-entra-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-on-demand-provision-entra-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-on-demand-provision-entra-to-active-directory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dfe09513-b06b-c5ab-2251-4b2c2315fa54
---

# On-demand provisioning - Microsoft Entra ID to Active Directory - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Cloud Sync lets you test configuration changes by applying them to a single user or group before you enable the configuration for all in-scope objects.

Use this test to validate and verify that the changes you made to the configuration were applied properly and that objects are correctly synchronized to Active Directory.

This article covers on-demand provisioning for configurations that provision from Microsoft Entra ID to Active Directory. If you're looking for information about provisioning from Active Directory to Microsoft Entra ID, see [On-demand provisioning - Active Directory to Microsoft Entra ID](how-to-on-demand-provision).

The following is true for on-demand group provisioning:

- On-demand provisioning of groups supports updating up to five members at a time.
- On-demand provisioning doesn't support deleting groups that are deleted from Microsoft Entra ID. Those groups don't appear when you search for a group.
- On-demand provisioning doesn't support nested groups that aren't directly assigned to the application.
- The on-demand provisioning request API can only accept a single group with up to five members at a time.

## Verify a user or group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. On the left, select **Provision on demand**.
3. Select the **Users** or **Groups** tab, depending on which object type you want to test.

    [![Screenshot of the Provision on demand page with the Users and Groups tabs.](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-users-tab.png)](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-users-tab.png#lightbox)

Then follow the steps for the object type you selected.

# [Users](#tab/users)
1. In **Select a user**, search for the user by name, and then select the user.

    [![Screenshot of a user selected on the Users tab of the Provision on demand page.](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-select-user.png)](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-select-user.png#lightbox)
2. Select **Provision**.

# [Groups](#tab/groups)
1. In **Selected group**, search for the group by name, and then select the group.
2. Under **Selected users**, select **View members only** to choose from the group's current members, or **View all users** to search the whole directory. Then select the members you want to test.

    Note

    Members aren't provisioned automatically. Select the members you want to test, up to five at a time.

    [![Screenshot of a group selected on the Groups tab, with the options for choosing which members to test.](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-select-group.png)](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-select-group.png#lightbox)
3. Select **Provision**.

---

## Review the result

The result lists four steps: importing the object, evaluating it against your scoping filters, matching it against the target system, and performing the action in Active Directory. Select **View details** on any step to see what was evaluated.

A step reports **Success** when it completes, or **Skipped** when there was nothing to do, such as when the object in Active Directory already matches. To run the same test again, select **Retry**. To test a different object, select **Provision another object**.

# [Users](#tab/users)
[![Screenshot of the on-demand provisioning result for a user, showing the four steps and their status.](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-user-result.png)](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-user-result.png#lightbox)

# [Groups](#tab/groups)
[![Screenshot of the on-demand provisioning result for a group, showing the four steps and their status.](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-group-result.png)](media/how-to-on-demand-provision-entra-to-active-directory/provision-on-demand-group-result.png#lightbox)

---