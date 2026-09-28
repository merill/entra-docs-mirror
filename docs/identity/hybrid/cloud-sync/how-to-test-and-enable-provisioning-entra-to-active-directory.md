---
layout: Conceptual
title: Test Microsoft Entra provisioning (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-test-and-enable-provisioning-entra-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: pmwongera
ms.reviewer: marshmacy
description: Test Microsoft Entra ID to Active Directory provisioning on demand, review default properties, and enable or manage the configuration.
ms.topic: how-to
ms.date: 2026-08-26T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange, msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: 349d85ca-ddbb-0cfd-b54a-3b9d1e04650b
document_version_independent_id: 349d85ca-ddbb-0cfd-b54a-3b9d1e04650b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-test-and-enable-provisioning-entra-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-test-and-enable-provisioning-entra-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-test-and-enable-provisioning-entra-to-active-directory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: dd11b10d-dbd8-7f08-1fa7-184dd1848386
---

# Test Microsoft Entra provisioning (Preview) - Microsoft Entra ID | Microsoft Learn

After you configure scoping filters and attribute mappings, test the configuration, review default properties, and enable it. These steps are the same for all deployment options: users only, groups only, or users and groups.

## Prerequisites

Complete the steps in [Configure Microsoft Entra ID to Active Directory provisioning](how-to-configure-entra-to-active-directory) before you continue.

## Test with on-demand provisioning

Before you enable the configuration for all in-scope objects, apply it to a single user or group and check the outcome. On-demand provisioning reports each step separately — import, scope evaluation, match, and the action taken on the target object — so you can see exactly where an object would fail.

Groups have one extra consideration: members aren't provisioned automatically, so you select up to five members to test alongside the group.

When the test finishes, the portal shows a message with the next configuration step. Select the link in that message to continue.

For the full procedure for both users and groups, see [On-demand provisioning - Microsoft Entra ID to Active Directory](how-to-on-demand-provision-entra-to-active-directory).

## Default properties: accidental deletes and email notifications

The default properties section provides settings for accidental deletions and email notifications.

[![Screenshot of the default properties option.](media/how-to-configure/new-ux-configure-10.png)](media/how-to-configure/new-ux-configure-10.png#lightbox)

The accidental delete feature protects you from configuration changes and on-premises directory changes that would affect many users and groups. It lets you:

- Prevent accidental deletes automatically.
- Set the number of objects (threshold) beyond which the protection takes effect.
- Set a notification email address for when a sync job is placed in quarantine for this scenario.

For more information, see [Accidental deletes](how-to-accidental-deletes).

Select the **pencil** next to **Basics** to change the defaults in a configuration.

[![Screenshot of the configuration basics properties.](media/how-to-configure/new-ux-configure-11.png)](media/how-to-configure/new-ux-configure-11.png#lightbox)

## Enable your configuration

After you finalize and test your configuration, enable it.

On the left, select **Overview** &gt; **Review and enable**, and then select **Enable configuration**.

[![Screenshot of reviewing and enabling a provisioning configuration.](media/how-to-test-enable-provisioning-active-directory/enable-provisioning-configuration.png)](media/how-to-test-enable-provisioning-active-directory/enable-provisioning-configuration.png#lightbox)

The service runs an initial cycle for all in-scope objects, followed by delta cycles on the recurring schedule.

## Quarantines

Cloud Sync monitors the health of your configuration and places unhealthy objects in a quarantine state. If most or all calls made against the target system consistently fail because of an error, such as invalid admin credentials, the sync job is marked as in quarantine. For more information, see [Provisioning quarantined problems](how-to-troubleshoot#provisioning-quarantined-problems).

## Restart provisioning

If you don't want to wait for the next scheduled run, trigger the provisioning run by using **Restart sync**.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.
3. Under **Configuration**, select your configuration.
4. At the top, select **Restart sync**.

## Remove a configuration

To delete a configuration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.
3. Under **Configuration**, select your configuration.
4. At the top of the configuration screen, select **Delete configuration**.

Important

There's no confirmation before a configuration is deleted. Make sure this is the action you want to take before you select **Delete**.