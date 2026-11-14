---
layout: Conceptual
title: Configuration management in Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/configuration-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about baseline templates, deployments, cross-tenant monitors, and drift detection in Microsoft Entra Tenant Governance.
ms.topic: concept-article
ms.date: 2026-11-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 11bf4ac6-07d1-7705-eca6-6cc39548becc
document_version_independent_id: 11bf4ac6-07d1-7705-eca6-6cc39548becc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/configuration-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/configuration-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/configuration-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 749e47a0-442e-7211-331f-f0ae9e4faab5
---

# Configuration management in Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn

Configuration management in Microsoft Entra Tenant Governance lets you capture current settings, define configuration baselines, standardize baselines as templates, deploy configuration, and monitor tenants for drift.

Configuration management supports operations in the **home tenant** and in **other tenants** that are connected through [governance relationships](governance-relationships). The home tenant is the tenant where you manage the operation. Other tenants are governed tenants that you select as targets.

Tenant Governance Basic includes both home-tenant and cross-tenant configuration management. Tenant Governance Premium isn't required solely to manage configuration across governed tenants; Premium licenses add monitoring and snapshot capacity. For details, see [Microsoft Entra Tenant Governance licensing](licensing).

The monitor view shows the configuration management navigation, monitor definitions, and entry points for results and drifts.

[![Screenshot of monitors with Tenant Governance navigation and results and drifts tabs.](../media/tenant-governance-configuration-management/monitors-overview.png)](../media/tenant-governance-configuration-management/monitors-overview.png#lightbox)

Note

Configuration management is built on the Microsoft Graph [Tenant Configuration Management APIs](/en-us/graph/unified-tenant-configuration-management-concept-overview), which are generally available. These APIs provide the configuration-as-code capabilities described in this article, including snapshots, baselines, monitors, and drift detection.

## Resources

A **resource** represents a macro configuration component that you can manage through configuration-as-code. The tenant configuration management solution supports hundreds of resource types that you can include in your configuration baselines. Each resource defines multiple properties that the solution can manage.

For example, a Conditional Access policy in Microsoft Entra ID is represented by the `microsoft.entra.conditionalaccesspolicy` resource. That resource exposes properties such as `ExcludedUsers`, `IncludedGroups`, and `State` that you can define in your configuration baseline. For a full list of resources, see [Overview of Tenant Configuration Management](/en-us/graph/unified-tenant-configuration-management-concept-overview).

## Baselines

A **baseline** is the JSON representation of the configuration you want to monitor or deploy for a given tenant. It consists of a list of resources and the defined values for their associated properties. A baseline can contain multiple instances of a given resource type.

For example, a configuration baseline can define multiple instances of Exchange Online transport rules as part of its definition. To learn more about configuration baselines, see [Configuration baseline](/en-us/graph/api/resources/configurationbaseline?view=graph-rest-1.0&amp;preserve-view=true).

## Configuration baseline templates (Preview)

A **configuration baseline template** is a reusable baseline definition. Use Configuration baseline templates to standardize baseline definitions across monitors and deployments. Templates help you reuse approved settings and simplify setup across environments and tenants.

A configuration baseline template defines resource settings. It's different from a [governance policy template](governance-policy-templates), which defines access through a governance relationship.

For lifecycle and versioning guidance, see [Configuration baseline templates](configuration-baseline-templates).

## Configuration deployments (Preview)

A **configuration deployment** applies baseline-defined settings to a target tenant. Use Configuration deployments to apply baseline-defined configuration to the home tenant or governed tenants.

Deployments change configuration; monitors evaluate it. After deployment, use a monitor to verify that the target tenant aligns with the baseline and to detect later changes. For status and failure handling, see [Configuration deployments](configuration-deployments).

## Monitors

**Monitors** are core to the tenant configuration management solution. They run the processes responsible for continuously monitoring your tenants for configuration drifts. Each monitor references a JSON configuration baseline that specifies the resources to validate. The monitor definition also includes a name, description, schedule frequency, and a configuration mode that specifies the actions to perform when drifts are detected.

### Cross-tenant monitors (Preview)

A monitor targets either the home tenant or another tenant connected through an active governance relationship. For other-tenant monitoring, configure the required delegated permissions and workload access before creating the monitor. A relationship alone doesn't grant every workload permission.

Choose **Monitors** under **Tenant management** for the home tenant, or **Monitors (Preview)** under **Other tenants** for a governed tenant. Select a governed target in the other-tenant creation wizard. Review results and drift records in the context of that target tenant.

[![Screenshot of governed-tenant monitors with target tenant and run status columns.](../media/tenant-governance-configuration-management/governed-tenant-monitors.png)](../media/tenant-governance-configuration-management/governed-tenant-monitors.png#lightbox)

Note

The Unified Tenant Configuration Management service principal must have read permissions for the resource types defined in the associated baselines. This requirement applies to both monitors and snapshot jobs. See [Authentication setup](/en-us/graph/utcm-authentication-setup) to learn how to grant the required permissions.

To learn more about monitors, see [configurationMonitor](/en-us/graph/api/resources/configurationmonitor?view=graph-rest-1.0&amp;preserve-view=true).

## Monitoring results

Every time a monitor executes based on its specified schedule, it produces a **monitoring result** that summarizes the execution. A monitoring result contains the execution duration, a status that indicates whether resource evaluation succeeded, and a count of detected drifts.

Monitoring results can describe runs in the home tenant or governed tenants. Use tenant filters to distinguish results for each target tenant.

If drifts are detected, the monitoring result reports their presence but doesn't include drift details. To get detailed information about each drift, query the associated configuration drift objects.

To learn more about monitoring results, see [configurationMonitoringResult](/en-us/graph/api/configurationmonitoringresult-get?view=graph-rest-1.0&amp;preserve-view=true).

## Configuration drifts

When a delta exists between what a configuration baseline defines and the actual settings on a tenant, Tenant Governance reports a **configuration drift**. Configuration drifts are associated with a monitor and contain detailed information about the detected delta. Each drift object identifies the affected resource and lists each property whose current value differs from the baseline definition.

Drift records belong to the monitor's target tenant, whether it's the home tenant or a governed tenant. After you remediate a detected drift, the next monitor execution automatically marks the configuration drift object as `fixed` if the resource matches the baseline. To learn more about configuration drifts, see [configurationDrift](/en-us/graph/api/resources/configurationdrift?view=graph-rest-1.0&amp;preserve-view=true).

## Snapshot jobs

When you initiate a request to generate a snapshot, an asynchronous job collects the current state of the specified resources. This **snapshot job** generates the actual JSON content of the requested snapshot. When the job completes, it returns a status of `succeeded` and a `resourceLocation` URL where you can download the JSON snapshot.

Important

Snapshot jobs and their associated snapshots have a retention period of 7 days, after which they're deleted. Download and store generated snapshots before the retention period expires.

The generated snapshot schema matches the schema of configuration baselines. Use a snapshot to create a baseline template, deployment, or monitor. Review the captured values before using them as your desired configuration.

To learn more about snapshot jobs, see [configurationSnapshotJob](/en-us/graph/api/resources/configurationsnapshotjob?view=graph-rest-1.0&amp;preserve-view=true).