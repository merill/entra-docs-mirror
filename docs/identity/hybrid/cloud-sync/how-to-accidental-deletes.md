---
layout: Conceptual
title: Microsoft Entra Cloud Sync accidental deletes - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-accidental-deletes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This topic describes how to use the accidental delete feature to prevent deletions.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1cc4a0a1-a3b2-20b5-84b7-5432be86045e
document_version_independent_id: 71ff9b16-a139-5c35-d280-16515b82496d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-accidental-deletes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-accidental-deletes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-accidental-deletes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f371f894-2689-dcac-fc40-e4414ea75fba
---

# Microsoft Entra Cloud Sync accidental deletes - Microsoft Entra ID | Microsoft Learn

The following document describes the accidental deletion feature for Microsoft Entra Cloud Sync. The accidental delete feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and groups. This feature allows you to:

- Configure the ability to prevent accidental deletes automatically.
- Set the # of objects (threshold) beyond which the configuration takes effect.
- Set up a notification email address so they can get an email notification once the sync job in question is put in quarantine for this scenario.

Note

If you have specified accidental delete prevention four group provisioning to Microsoft Entra ID, be aware this only prevents the group from being deleted. This does not prevent members from being deleted. To prevent members from being deleted, you should configure accidental delete prevention on synchronized users.

To use this feature, you set the threshold for the number of objects that, if deleted, synchronization should stop. So if this number is reached, the synchronization stops and a notification is sent to the email that is specified. This notification allows you to investigate what is going on.

For more information and an example, see the following video.

## Configure accidental delete prevention

To use the new feature, follow the steps below.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. Select **Properties**.
3. Click the pencil next to **Basics**
4. On the right, fill in the following information.
    - **Notification email** - email used for notifications
    - **Prevent accidental deletions** - check this box to enable the feature
    - **Accidental deletion threshold** - enter the number of objects to stop synchronization and send a notification

## Recovering from an accidental delete instance

If you encounter an accidental delete you see this message on the status of your provisioning agent configuration. It says **Delete threshold exceeded**.

![Accidental delete status](media/how-to-accidental-deletes/delete-1.png)

By clicking on **Delete threshold exceeded**, you'll see the sync status info. This action will provide more details.

![Sync status](media/how-to-accidental-deletes/delete-2.png)

By right-clicking on the ellipses, you get the following options:

- View provisioning log
- View agent
- Allow deletes

![Right click](media/how-to-accidental-deletes/delete-3.png)

Using **View provisioning log**, you can see the **StagedDelete** entries and review the information provided on the users that have been deleted.

![Provisioning logs](media/how-to-accidental-deletes/delete-7.png)

### Allowing deletes

The **Allow deletes** action, deletes the objects that triggered the accidental delete threshold. Use the following procedure to accept these deletes.

1. Right-click on the ellipses and select **Allow deletes**.
2. Click **Yes** on the confirmation to allow the deletions.

![Yes on confirmation](media/how-to-accidental-deletes/delete-4.png)

1. You'll see confirmation that the deletions were accepted and the status will return to healthy with the next cycle.

![Accept deletes](media/how-to-accidental-deletes/delete-8.png)

### Rejecting deletions

If you don't want to allow the deletions, you need to do the following actions:

- Investigate the source of the deletions.
- Fix the issue (example, OU was moved out of scope accidentally and you've now readded it back to the scope).
- Run **Restart sync** on the agent configuration.