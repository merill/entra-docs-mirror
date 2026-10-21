---
layout: FAQ
title: Migrate from Microsoft Entra Connect Sync to Cloud Sync FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/cloud-sync-migration-faq
summary: >
  <p>This article answers frequently asked questions about migrating from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync. For platform capabilities, see the <a href="connect-to-cloud-sync-decision-guide">decision guide</a>. For guided-tool eligibility and procedures, see the <a href="migrate-connect-sync-cloud-sync-tool#prerequisites">guided migration tool</a>. To choose a guided or documented manual path, see <a href="migrate-azure-ad-connect-to-cloud-sync#choose-a-migration-path">Choose a migration path</a>.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: mwongerapk
description: Frequently asked questions about migrating from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync, including eligibility, timelines, feature parity, and post-migration behavior.
ms.topic: faq
ms.date: 2026-10-21T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1028
ms.subservice: hybrid-cloud-sync
ai-usage: ai-assisted
locale: en-us
document_id: 8c7ad143-ae27-8fdd-2958-60ea42403728
document_version_independent_id: 8c7ad143-ae27-8fdd-2958-60ea42403728
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/cloud-sync-migration-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/cloud-sync-migration-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/cloud-sync-migration-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: e562428b-3a74-fe18-5f24-1d905c747417
---

# Migrate from Microsoft Entra Connect Sync to Cloud Sync FAQ - Microsoft Entra ID | Microsoft Learn

This article answers frequently asked questions about migrating from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync. For platform capabilities, see the [decision guide](connect-to-cloud-sync-decision-guide). For guided-tool eligibility and procedures, see the [guided migration tool](migrate-connect-sync-cloud-sync-tool#prerequisites). To choose a guided or documented manual path, see [Choose a migration path](migrate-azure-ad-connect-to-cloud-sync#choose-a-migration-path).

## Migration eligibility and timeline

### How will I know when it's my turn to migrate to Cloud Sync?

Microsoft notifies your organization when it becomes eligible to begin migration. Eligibility is determined by factors including your current configuration and supported scenarios, and migration is rolled out in phases. When it's time, you receive clear instructions through official communication channels on how to proceed.

### What if my organization can't migrate within the recommended window?

If a confirmed technical or business blocker prevents migration by the date in your tenant-specific notification, [request more time through Microsoft Support](migrate-connect-sync-cloud-sync-tool#request-more-time-to-migrate). Exception requests are reviewed individually, aren't guaranteed, and don't remove the requirement to migrate.

### Why do I see different dates?

Cloud Sync migration deadlines and windows are organization-specific. Connect Sync version retirement, authentication changes, and other product changes can have different timelines. Follow the migration date in your organization's tenant-specific notification. For exception timing and required evidence, see [Request more time to migrate](migrate-connect-sync-cloud-sync-tool#request-more-time-to-migrate).

### How long does migration take?

Migration time varies with your environment and readiness results. Plan separately for:

- **Readiness remediation:** Review and resolve the conditions identified by the [readiness assessment](migrate-connect-sync-cloud-sync-tool#review-environment-readiness).
- **Configuration transfer:** The tool transfers only supported settings and creates the required Cloud Sync configurations and jobs.
- **Initial synchronization:** After activation, Cloud Sync starts initial synchronization. Review job health and synchronization results.
- **Validation:** Keep Connect Sync installed during the documented [two-week validation period](migrate-connect-sync-cloud-sync-tool#validate-synchronization-results), and manually validate objects, references, and enabled writeback scenarios.

## Migration process

### How do I migrate from Connect Sync to Cloud Sync?

To prepare for migration, explore the following resources:

- [What is Cloud Sync](what-is-cloud-sync)
- [Cloud Sync deep dive - how it works](concept-how-it-works)
- [Guided migration-tool prerequisites and limits](migrate-connect-sync-cloud-sync-tool#prerequisites)
- [Step-by-step migration guidance](migrate-azure-ad-connect-to-cloud-sync)

**Migration scenarios:**

- [Migrate to Microsoft Entra Cloud Sync for a synced Active Directory forest](tutorial-pilot-aadc-aadccp)
- [Migrate Microsoft Entra Connect Sync group writeback v2 to Microsoft Entra Cloud Sync](migrate-group-writeback)
- [Microsoft Entra Cloud Sync vs. Microsoft Entra Connect Sync feature comparison](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync)

### Can I run Connect Sync and Cloud Sync side by side?

Connect Sync and Cloud Sync must not simultaneously export normal changes for the same object and attribute set. During the documented manual phased-migration process, objects remain in Connect Sync scope while the `cloudNoFlow` and `JoinNoFlow` rules prevent normal Connect Sync exports and preserve required references. Follow the [manual migration procedure](tutorial-pilot-aadc-aadccp#create-a-custom-user-inbound-rule), and remove Connect Sync scope only after migration and [reference validation](tutorial-pilot-aadc-aadccp#plan-scope-removal-from-microsoft-entra-connect-sync) are complete.

### Why can't I see the Transition to Cloud Sync option?

Check the [guided migration-tool prerequisites](migrate-connect-sync-cloud-sync-tool#prerequisites):

- Start the task on the active Connect Sync server, not a server in staging mode.
- Use a supported Connect Sync version on the active installation.
- Your organization and installation must be eligible for the current migration wave.

### What does the migration tool validate?

The tool assesses readiness and transfers supported configurations. Before activation, complete [Provision on Demand](migrate-connect-sync-cloud-sync-tool#verify-the-configuration-with-provision-on-demand) for each migrated domain configuration. After activation, the wizard compares an aggregate **Total Objects** count, checks required Cloud Sync job health, and confirms that Connect Sync is in staging mode.

Individual users, groups, memberships, manager relationships, password hash synchronization results, writeback operations, and business-specific outcomes require manual validation. Follow the [validation checklist](migrate-connect-sync-cloud-sync-tool#what-the-migration-tool-does-not-validate-automatically).

### Can I test migration before fully rolling it out?

Yes. You can pilot the migration using a test Active Directory forest before committing to a full rollout. The tutorial [Migrate to Microsoft Entra Cloud Sync for a synced Active Directory forest](tutorial-pilot-aadc-aadccp) walks you through a sandbox migration. You can also use [on-demand provisioning](how-to-on-demand-provision) to validate configuration changes by applying them to a single user.

## Configuration and customization

### Will my existing configurations be preserved during migration?

During [guided-tool activation](migrate-connect-sync-cloud-sync-tool#activate-cloud-sync), the tool enables Cloud Sync and places Connect Sync in staging mode. Keep Connect Sync installed during the documented validation period. For manual migration, [back up your Connect Sync configuration](tutorial-pilot-aadc-aadccp#back-up-your-microsoft-entra-connect-configuration) before making changes by using the [import and export settings](../connect/how-to-connect-import-export-config) feature.

### Will customizations carry over automatically?

Only supported configurations are transferred. Review the [tool prerequisites](migrate-connect-sync-cloud-sync-tool#prerequisites) and [readiness result](migrate-connect-sync-cloud-sync-tool#review-environment-readiness), then validate the transferred configuration. Complete [on-demand provisioning](how-to-on-demand-provision) before activation as described in [Verify the configuration with Provision on Demand](migrate-connect-sync-cloud-sync-tool#verify-the-configuration-with-provision-on-demand). After activation, follow the [validation guidance](migrate-connect-sync-cloud-sync-tool#validate-synchronization-results). The [feature comparison](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync) describes platform capabilities, not automatic transfer support.

## Feature support and compatibility

### Why can Cloud Sync support a feature that the guided migration tool blocks?

The [decision guide](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync) describes Cloud Sync platform capabilities. The [migration-tool prerequisites and limits](migrate-connect-sync-cloud-sync-tool#prerequisites) describe what the current guided experience can assess and transfer. A supported Cloud Sync capability doesn't automatically mean that the guided tool can migrate it. Use a documented manual migration procedure only when one is available for your scenario. Otherwise, continue using Connect Sync.

### Cloud Sync supports device synchronization. Why does the migration tool block my environment?

Cloud Sync supports device synchronization, but the guided migration tool currently lists it as a blocking condition. Don't remove required Device Sync configuration to bypass readiness. Review the [decision guide](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync), [tool requirements](migrate-connect-sync-cloud-sync-tool#prerequisites), and [Device Sync documentation](device-sync) before planning migration. The Device Sync article describes configuration, not a device migration sequence.

### Which Connect Sync features are currently supported in Cloud Sync?

For a full feature comparison, see the [Connect Sync to Cloud Sync decision guide](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync). The decision guide includes a detailed comparison table covering 40+ capabilities and their availability in Cloud Sync.

### What happens if I rely on features that aren't yet available in Cloud Sync?

Review the [decision guide](connect-to-cloud-sync-decision-guide#decision-framework) to identify unsupported requirements. Continue using Connect Sync when a required capability or documented migration procedure isn't available. If you've received a migration notification and a confirmed blocker prevents you from meeting its deadline, [request more time through Microsoft Support](migrate-connect-sync-cloud-sync-tool#request-more-time-to-migrate). An exception isn't automatic or guaranteed.

### What happens to hybrid authentication features like Pass-Through Authentication (PTA)?

Once you migrate to Cloud Sync, your hybrid authentication features that enable on-premises credentials to be used for accessing cloud resources continue to be available. Features like [Pass-Through Authentication](../connect/how-to-connect-pta) and [seamless single sign-on](../connect/how-to-connect-sso) are configured separately from the sync tool and remain functional after migration through the Connect Sync configuration wizard.