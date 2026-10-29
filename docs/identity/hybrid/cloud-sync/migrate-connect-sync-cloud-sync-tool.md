---
layout: Conceptual
title: Migrate to Microsoft Entra Cloud Sync with the Migration Tool - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/migrate-connect-sync-cloud-sync-tool
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: srutto
ms.author: sharonrutto
ms.service: entra-id
manager: pmwongera
description: Learn how to migrate from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync and validate synchronization after activation.
ms.subservice: hybrid-cloud-sync
ms.topic: how-to
ms.custom: msecd-doc-authoring-1028
ms.date: 2026-10-21T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: c87834d1-af5c-2ce2-d1f6-6fb6179708a3
document_version_independent_id: c87834d1-af5c-2ce2-d1f6-6fb6179708a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/migrate-connect-sync-cloud-sync-tool.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/migrate-connect-sync-cloud-sync-tool
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/migrate-connect-sync-cloud-sync-tool.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: dacb2989-8912-adc8-6036-37627cdefa9a
---

# Migrate to Microsoft Entra Cloud Sync with the Migration Tool - Microsoft Entra ID | Microsoft Learn

Use the guided migration tool to move supported synchronization settings from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync. The tool assesses your environment, creates the required Cloud Sync configurations, and performs a preactivation Provision on Demand check. It then places Connect Sync in staging mode, activates Cloud Sync, and guides you through postactivation validation. Before you begin, review the prerequisites and supported migration scenarios.

Important

Start the migration from the active Connect Sync server. The migration tool can't be started from a Connect Sync server in staging mode.

## Prerequisites

- An account with the [**Hybrid Identity Administrator**](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) role to connect to Microsoft Entra and create and manage Cloud Sync configurations.
- Domain Admin credentials for every selected Active Directory forest. The wizard validates these credentials and uses them to configure the group managed service account (gMSA) for the provisioning agent.
- A supported version of Microsoft Entra Connect Sync. The migration option appears only for organizations and Connect Sync installations that are eligible for the current migration wave.
- An environment that meets the current migration-tool limits:
    - One Active Directory forest with no more than 2,000 in-scope objects.
    - Additive organizational unit (OU) inclusion scoping with no more than 30 included containers in each domain.
    - No migration-blocking features, such as custom synchronization rules, group filtering, a custom user principal name (UPN), directory extensions, device synchronization, or unsupported writeback scenarios.
- A review of the [supported scenarios and feature comparison](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync) for other differences between Connect Sync and Cloud Sync.
- Access to the active Microsoft Entra Connect Sync server. You can't run the migration tool from a server in staging mode.
- A two-week validation period after migration. Keep Microsoft Entra Connect Sync installed during this period.

Note

Cloud Sync can support capabilities that the current guided migration tool doesn't transfer. The limits on this page describe eligibility for the guided experience, not the complete set of Cloud Sync capabilities. Review the [migration decision guide](connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync) separately.

Cloud Sync supports device synchronization, but device synchronization is currently a migration blocker for the guided tool. Don't remove required device synchronization to bypass readiness. Review the decision guide and [Device Sync documentation](device-sync) before planning migration.

The migration tool supports transferring the following synchronization scenarios:

- User synchronization.
- Group synchronization.
- Password hash synchronization (PHS).
- Password writeback.
- Exchange hybrid writeback.
- Supported domain and organizational unit scoping.

## Launch the migration tool

Start the guided migration from the active Microsoft Entra Connect Sync server. The wizard shows an overview of the migration stages before it changes your environment.

1. Open the Microsoft Entra Connect Sync wizard on the active server.
2. Select **Configure**.
3. Select **Transition to Cloud Sync**.

    [![Screenshot of the Transition to Cloud Sync task in the Microsoft Entra Connect Sync wizard.](media/migrate-connect-sync-cloud-sync-tool/launch-migration-tool.png)](media/migrate-connect-sync-cloud-sync-tool/launch-migration-tool.png#lightbox)
4. Review the migration overview.

    [![Screenshot of the migration overview and its five migration stages.](media/migrate-connect-sync-cloud-sync-tool/migration-overview.png)](media/migrate-connect-sync-cloud-sync-tool/migration-overview.png#lightbox)

## Connect to Microsoft Entra and Active Directory

Connect the tool to Microsoft Entra and your on-premises Active Directory so that it can assess the current synchronization setup.

1. When prompted, sign in to Microsoft Entra with an account that has the **Hybrid Identity Administrator** role.
2. For each selected forest, enter Domain Admin credentials when prompted.

The tool verifies access to the current Microsoft Entra Connect Sync configuration and checks for conditions that might require attention before migration.

## Review environment readiness

The readiness review can include domains, scope, enabled features, authentication-related settings, writeback settings, object limits, existing Cloud Sync agents or configurations, and unsupported synchronization rules. The wizard also displays the Connect Sync accidental-deletion protection setting and deletion threshold. These settings must be readable and valid before migration can continue.

Use the readiness results to determine your next action:

| Readiness result | What it means | Customer action |
| --- | --- | --- |
| Supported | The scenario can proceed through the guided migration tool. | Review the assessment and continue. |
| Attention required | The environment contains a setting that you need to review. | Follow the linked guidance and rerun or resume the assessment as documented. |
| Migration blocked | The environment doesn't meet the current guided-tool requirements. | Don't bypass the result. Remediate the documented condition, wait for the required capability, or request more time when applicable. |

For feature, scope, and object-limit blockers, review the tool prerequisites. For device synchronization, review [Device Sync](device-sync). For accidental-deletion protection, see [Accidental deletions](how-to-accidental-deletes).

To review the assessment and proceed when eligible:

1. Review each result and any blocking conditions.
2. Review the accidental-deletion protection setting and deletion threshold.
3. Enter the email address that should receive quarantine notifications.
4. Download the readiness report.
5. Select the transition consent checkbox, and then select **Start Transition**.

    [![Screenshot of a successful environment readiness review with the report download and transition consent options.](media/migrate-connect-sync-cloud-sync-tool/environment-readiness-review.png)](media/migrate-connect-sync-cloud-sync-tool/environment-readiness-review.png#lightbox)

Important

If the review blocks migration, don't try to bypass the result. Remediate the identified condition, or wait for the required capability.

## Transfer the configuration

The migration tool transfers supported settings automatically. It installs and registers the Cloud Sync provisioning agent, creates a Cloud Sync configuration for each selected, in-scope Active Directory domain, and creates the synchronization jobs required for the supported features detected in your environment.

1. Wait while the migration tool transfers the configuration.
2. Monitor the transfer progress until it completes.
3. Confirm in the wizard that the transfer completed.
4. In the Microsoft Entra admin center, verify the created Cloud Sync configurations and synchronization jobs.

    [![Screenshot of the configuration transfer progress and completed migration tasks.](media/migrate-connect-sync-cloud-sync-tool/transfer-progress.png)](media/migrate-connect-sync-cloud-sync-tool/transfer-progress.png#lightbox)

Note

The newly created Cloud Sync configurations remain disabled during the transfer. Connect Sync remains the active exporter until activation.

[![Screenshot of a transferred Cloud Sync configuration in a disabled state.](media/migrate-connect-sync-cloud-sync-tool/disabled-cloud-sync-configuration.png)](media/migrate-connect-sync-cloud-sync-tool/disabled-cloud-sync-configuration.png#lightbox)

## Verify the configuration with Provision on Demand

Use Provision on Demand to test a representative object in each migrated domain configuration before you activate Cloud Sync. A successful result confirms that the agent can read the selected Active Directory object and that the Cloud Sync configuration can process it.

1. In the migration wizard, select **Open Entra Portal**, and then open the newly created Cloud Sync configuration in the Microsoft Entra admin center.

    [![Screenshot of the Cloud Sync verification page before Provision on Demand is confirmed.](media/migrate-connect-sync-cloud-sync-tool/verify-activate-cloud-sync.png)](media/migrate-connect-sync-cloud-sync-tool/verify-activate-cloud-sync.png#lightbox)
2. For each migrated domain configuration, complete these actions:

    1. Select **Provision on demand**.
    2. Enter the distinguished name of a representative test user or group that your organization has approved for migration testing.
    3. Select **Provision**.
    4. Review the detailed result. Don't rely only on the final success indicator.
3. If password writeback is enabled, verify that tenant-level self-service password reset (SSPR) writeback is enabled, and then select the password-writeback confirmation checkbox.
4. Return to the migration wizard.
5. Confirm that Provision on Demand completed successfully for each migrated domain configuration.
6. Select **Complete transfer to Cloud Sync**.

## Activate Cloud Sync

Activation changes the active synchronization path. The migration tool enables the transferred Cloud Sync configuration and jobs, places Connect Sync in staging mode, and starts the initial Cloud Sync synchronization. Connect Sync continues import and synchronization processing locally but no longer performs normal exports to Microsoft Entra ID.

1. After you select **Complete transfer to Cloud Sync**, wait while the migration tool activates Cloud Sync.
2. Confirm that activation completes and the initial Cloud Sync synchronization starts.

    [![Screenshot of the activation confirmation showing that Cloud Sync is active and Connect Sync is in staging mode.](media/migrate-connect-sync-cloud-sync-tool/cloud-sync-activated.png)](media/migrate-connect-sync-cloud-sync-tool/cloud-sync-activated.png#lightbox)

Caution

Don't uninstall Connect Sync during initial validation.

## Validate synchronization results

Use the validation page to compare the Connect Sync staging result with the active Cloud Sync result. The wizard automatically compares one aggregate **Total Objects** count, checks required Cloud Sync job health, and confirms that Connect Sync is in staging mode. It doesn't automatically validate individual users, groups, memberships, or writeback operations.

1. Compare the aggregate **Total Objects** counts and confirm that the expected counts reconcile.

    [![Screenshot of the Validate Migration page showing matching object counts and passed synchronization checks.](media/migrate-connect-sync-cloud-sync-tool/validate-object-counts.png)](media/migrate-connect-sync-cloud-sync-tool/validate-object-counts.png#lightbox)
2. Review Cloud Sync job health, last synchronization information, and provisioning errors.

    [![Screenshot of a healthy Cloud Sync configuration with enabled agents and synchronization status details.](media/migrate-connect-sync-cloud-sync-tool/transferred-cloud-sync-jobs.png)](media/migrate-connect-sync-cloud-sync-tool/transferred-cloud-sync-jobs.png#lightbox)
3. Manually validate representative users, groups, memberships, and enabled writeback scenarios.
4. Investigate any persistent object-level differences.
5. After all required checks pass, select the validation consent checkbox, and then select **Complete Migration**.
6. Keep Connect Sync installed for the approved two-week validation period before you uninstall it.

If you need to wait for the next Connect Sync staging cycle, close the wizard so that it releases the Connect Sync configuration mutex. The wizard preserves the transition state. To resume validation, reopen Microsoft Entra Connect Sync, select **Transition to Microsoft Entra Cloud Sync**, review the overview, and sign in to Microsoft Entra again if prompted. Continue to the validation page and refresh the results.

### What the migration tool does not validate automatically

The aggregate **Total Objects** comparison doesn't validate individual objects or business-specific outcomes. Manually validate:

- Individual users and groups.
- Group memberships and manager relationships.
- Password hash synchronization results.
- Password writeback and Exchange hybrid writeback.
- Other business-critical object and attribute behavior.

Use this checklist before completing validation:

- Confirm aggregate object counts.
- Review Cloud Sync job health and last synchronization information.
- Review provisioning errors.
- Validate representative users and groups.
- Validate group memberships and manager relationships used by your organization.
- Validate every enabled writeback scenario.
- Investigate persistent object-level differences.
- Keep Connect Sync installed during the two-week validation period.

## Request more time to migrate

Microsoft notifies eligible organizations through in-product experiences and email. The notification identifies your organization's migration window or deadline and directs you to the migration guidance.

Important

Use the migration date in your organization's tenant-specific notification. Connect Sync version retirement, authentication changes, and Cloud Sync migration can have different timelines.

If a confirmed technical or business blocker prevents you from completing the migration by the deadline in your notification, open a Microsoft Support request for a temporary Cloud Sync migration exception. Exceptions are reviewed individually, aren't guaranteed, and don't remove the requirement to migrate.

Include the following information in your support request:

- Your Microsoft Entra tenant ID and organization name.
- The requested exception end date and why you need more time.
- The readiness report, a description of the confirmed blocking condition, and relevant error evidence.
- The expected customer or business impact if enforcement proceeds.
- The mitigations that you tried and why they didn't resolve the blocker.
- A migration plan with milestones and a target completion date.

For diagnostic evidence and redaction requirements, see Collect evidence for Microsoft Support.

## Troubleshoot common issues

Use the troubleshooting table to investigate migration issues and collect evidence for Microsoft Support.

| Issue | What to check | Support evidence to collect |
| --- | --- | --- |
| Migration option is missing | Start on the active Connect Sync server, not a server in staging mode. Verify that the Connect Sync version is supported and that your organization and installation are eligible for the current migration wave. See Prerequisites. | Exact error text, if displayed, and a redacted screenshot. |
| Readiness review blocks migration | Review the blocking feature, scope, object limit, accidental-deletion protection setting, or configuration conflict. | Readiness report and a redacted screenshot of the blocking result. |
| Transfer fails | Review Connect Sync trace logs for credential validation, agent installation, registration, Microsoft Graph operations, or job creation failures. | Trace log excerpt, timestamp, wizard step, error text, and correlation identifier, if shown. |
| Activation fails | Follow the recovery instructions in the wizard. Don't delete, disable, or retag migration-owned Cloud Sync resources because manual changes can interfere with recovery. | Diagnostic ID, exported wizard logs, timestamp, wizard step, and error text. |
| Provision on Demand fails | Confirm agent health, directory connectivity, permissions, the object distinguished name, and the detailed provisioning result. | Provision on Demand result details and provisioning logs. |
| Validation counts differ | Close the wizard while you wait for the next Connect Sync staging cycle. Reopen the wizard, return to validation, refresh the aggregate count comparison, and investigate persistent object-level differences. | Validation screenshot, last-sync times, job health, and relevant provisioning errors. |
| Existing Cloud Sync configuration is detected | Determine whether the existing configuration is a compatible writeback configuration or a conflicting Active Directory-to-Microsoft Entra configuration. | Configuration names, directions, scopes, and status, with tenant identifiers redacted. |

## Collect evidence for Microsoft Support

Collect the evidence relevant to the issue before you open a support request:

- The readiness report.
- Exact error text, the wizard step, and the timestamp.
- A diagnostic or correlation ID, if displayed.
- Exported wizard logs and relevant Connect Sync trace log excerpts.
- Provisioning-agent health and Cloud Sync job status.
- Provision on Demand result details.
- Relevant provisioning errors and last synchronization information.
- Redacted screenshots of the issue.

Submit evidence only through the secure Microsoft Support channel. Before you upload reports, logs, or screenshots, remove credentials, secrets, tokens, certificate material, personal data, internal hostnames, distinguished names, and unrelated tenant identifiers that Microsoft Support doesn't need for the investigation. Keep requested tenant and correlation identifiers so Support can investigate the issue.