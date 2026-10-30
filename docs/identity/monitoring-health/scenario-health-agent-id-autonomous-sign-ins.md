---
layout: Conceptual
title: Investigate Agent ID autonomous sign-ins - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/scenario-health-agent-id-autonomous-sign-ins
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to investigate Microsoft Entra Health Monitoring signals and alerts for Agent ID autonomous sign-ins and mitigate application-only authentication failures.
ms.topic: how-to
ms.date: 2026-10-08T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 20144734-07ea-788b-917a-bf4b51176ac9
document_version_independent_id: 20144734-07ea-788b-917a-bf4b51176ac9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/scenario-health-agent-id-autonomous-sign-ins.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/scenario-health-agent-id-autonomous-sign-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/scenario-health-agent-id-autonomous-sign-ins.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: e5a173a1-4074-8382-cab5-c55f71543943
---

# Investigate Agent ID autonomous sign-ins - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health Monitoring provides tenant-level health signals and alerts when it detects a significant change in your tenant's activity. The **Agent ID autonomous sign-ins** scenario helps you investigate failures when agents authenticate and act as themselves.

This article explains how to interpret the scenario, correlate an alert with service-principal sign-in and audit logs, and mitigate common issues. For the shared investigation workflow, see [Investigate Microsoft Entra Health monitoring alerts](howto-investigate-health-scenario-alerts).

Important

Microsoft Entra Health scenario monitoring and alerts are currently in preview. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Understand what autonomous means

In application-only access, an agent requests a token for its own identity, not on behalf of a signed-in human user. It uses application permissions rather than delegated user permissions. An agent can use this access pattern even if it also supports interactive conversations with people. For the authentication flow, see [Authenticate and acquire tokens for autonomous agents](../../agent-id/autonomous-agent-authentication-authorization-flow).

For Microsoft Entra agent identities, token acquisition has two stages: the blueprint authenticates and obtains an exchange token for a child agent identity, and the child agent identity uses that token to request a resource access token. Credentials are configured on the blueprint, not on the child agent identity. See [Agent autonomous app OAuth flow](../../agent-id/agent-autonomous-app-oauth-flow).

Some agents use classic application identities or designated service principals instead of Microsoft Entra agent identities. These identities follow the application and service-principal authentication model. Don't assume that every service-principal sign-in is an agent sign-in or that every agent uses a blueprint.

### Identify the caller and token subject

The [agent sign-in properties](/en-us/graph/api/resources/agentic-agentsignin?view=graph-rest-beta&amp;preserve-view=true) distinguish the calling identity from the token subject:

| Property | Question it answers | How to use it |
| --- | --- | --- |
| `agent.agentType` | Who signed in? | The autonomous health impact assessment selects callers classified as `agenticAppInstance`. |
| `agent.agentSubjectType` | On whose behalf was the token requested? | The autonomous health impact assessment excludes `agentIDuser` subjects. |
| `agent.parentAppId` | Which parent application is associated with the caller? | Correlate an agent identity with its blueprint when this value is available. |

For this scenario's impact assessment, a failed event has a nonzero `status.errorCode`, an `agentType` of `agenticAppInstance`, and an `agentSubjectType` other than `agentIDuser`. Don't infer the scenario from `isInteractive = false` alone or require one specific subject value for all application-only events.

Note

An agent can run autonomously while using its own [agent's user account](../../agent-id/agent-users). That describes how the agent operates, not this health scenario's selection criteria. Events with an `agentIDuser` subject are investigated under [Agent ID interactive sign-ins](scenario-health-agent-id-interactive-sign-ins), not the autonomous health scenario.

### Health scenarios aren't sign-in log categories

The [four sign-in log types](concept-sign-ins#what-are-the-types-of-sign-in-logs) describe authentication activity, not whether an agent operates independently. For this scenario, start with **Service principal sign-ins**, not **User sign-ins (interactive)** or **User sign-ins (non-interactive)**.

An agent's token chain might also involve a managed identity or a blueprint. Those related events can help diagnose an earlier authentication failure, but they aren't automatically part of the autonomous health impact assessment. For log categories and agent details, see [Service principal sign-ins](concept-service-principal-sign-ins) and [Microsoft Entra Agent ID logs](../../agent-id/sign-in-audit-logs-agents).

## Prerequisites

Use the least privileged role for each task. Permission to investigate an alert doesn't grant permission to change credentials, application permissions, or Conditional Access policies.

- A tenant with a [Microsoft Entra P1 or P2 license](../../fundamentals/get-started-premium) is required to view health scenario signals.
- A tenant with a non-trial Microsoft Entra P1 or P2 license and at least 100 monthly active users is required to view alerts and receive alert notifications.
- [Reports Reader](../role-based-access-control/permissions-reference#reports-reader) is the least privileged role to view health signals, alerts, alert configurations, and sign-in logs.
- [Helpdesk Administrator](../role-based-access-control/permissions-reference#helpdesk-administrator) is the least privileged role to update alerts and alert notification configurations.
- For Microsoft Graph, use `HealthMonitoringAlert.Read.All` to read alerts, or `HealthMonitoringAlert.ReadWrite.All` to read and update them. Use `AuditLog.Read.All` to read sign-in logs; health alert permissions don't grant log access.
- Reading applied Conditional Access policies requires additional permissions and a supported role. See [List signIns permissions](/en-us/graph/api/signin-list?view=graph-rest-beta&amp;preserve-view=true#permissions).

For health role requirements, see [Microsoft Entra Health least privileged roles](../role-based-access-control/delegate-by-task#microsoft-entra-health-least-privileged-roles). If mitigation requires policy changes, also review the separate licensing and role requirements for [Conditional Access for agents](../conditional-access/agent-id) or [Conditional Access for workload identities](../conditional-access/workload-identity), as appropriate.

## Investigate the signals and alert

Start with the anomaly timeframe and affected applications. Then determine which identity and token acquisition stage failed.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Reports Reader.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**, and select **Health Monitoring**.
3. Select **Agent ID autonomous sign-ins**. If the scenario isn't listed among active alerts, select **All scenarios** to view its signals.

    [![Screenshot of Health Monitoring with the Agent ID autonomous sign-ins scenario and its active alert highlighted.](media/scenario-health-agent-id-autonomous-sign-ins/agent-id-autonomous-alert-summary.png)](media/scenario-health-agent-id-autonomous-sign-ins/agent-id-autonomous-alert-summary.png#lightbox)
4. Review the **Agent ID autonomous sign-ins completion volume** and **Agent ID autonomous sign-ins failure volume** graphs. Compare the change with scheduled workloads, deployments, and expected agent activity.
5. Select an active **Large increase in Agent ID autonomous sign-in failures** alert. Record the anomaly timeframe and review its signals and affected applications.
6. Under **Affected entities**, select **View** for applications. Use the affected application identifiers to narrow your investigation. The autonomous impact assessment groups applications by `appId`; it doesn't produce affected user or device lists. An application count isn't a count of failed token requests.
7. Browse to **Entra ID** &gt; **Agents**, and select **Sign-in logs** in the Agents blade. Select **Service principal sign-ins**, set the date range to the anomaly timeframe, and filter **Status** to **Failure**.

    [![Screenshot of sign-in logs opened from Agents, with Entra ID and Agents highlighted, the service principal sign-ins tab selected, and Status set to Failure.](media/scenario-health-agent-id-autonomous-sign-ins/agent-id-autonomous-sign-in-failures.png)](media/scenario-health-agent-id-autonomous-sign-ins/agent-id-autonomous-sign-in-failures.png#lightbox)
8. Correlate the affected application with individual events. Review the `appId`, `servicePrincipalId`, agent properties, target resource, error code, failure reason, credential type, and Conditional Access result. Expand grouped log rows to inspect individual requests.
9. Review the [audit logs](concept-audit-logs) for recent credential, federated trust, application permission, identity status, or policy changes. For agent identities, check whether affected agents share a blueprint.

If several agents from one blueprint fail at the same time, investigate shared credentials and blueprint-scoped policies before changing each agent separately. A failure affecting one resource might instead involve that resource's configuration or permissions. Confirm either explanation in the logs; failure volume alone doesn't establish an outage or an attack.

### Correlate the alert with Microsoft Graph

Retrieve the selected alert and expand its affected resource sample. Replace `{alertId}` with the alert's ID. See [Get a health monitoring alert](/en-us/graph/api/healthmonitoring-alert-get?view=graph-rest-beta&amp;preserve-view=true).

```http
GET https://graph.microsoft.com/beta/reports/healthMonitoring/alerts/{alertId}?$expand=enrichment/impacts/microsoft.graph.healthmonitoring.directoryobjectimpactsummary/resourceSampling
Prefer: include-unknown-enum-members
```

Use [getSummarizedServicePrincipalSignIns](/en-us/graph/api/auditlogroot-getsummarizedserviceprincipalsignins?view=graph-rest-beta&amp;preserve-view=true) for aggregated service-principal activity. The following request uses the documented application filter. Replace `{application-client-id}` with the affected application's `appId`, not its service principal object ID.

```http
GET https://graph.microsoft.com/beta/auditLogs/getSummarizedServicePrincipalSignIns(aggregationWindow='h1')?$filter=appId eq '{application-client-id}'
Prefer: include-unknown-enum-members
```

Follow any `@odata.nextLink` returned in the response. In the returned data, select failed rows matching the caller and subject criteria described earlier. Use `servicePrincipalId` to identify the specific service principal and `parentAppId`, when available, to correlate the agent with its blueprint.

The [summarizedSignIn resource](/en-us/graph/api/resources/summarizedsignin?view=graph-rest-beta&amp;preserve-view=true) groups events across multiple dimensions. Use `signInCount` for request volume; don't count rows as individual sign-ins or unique applications. Aggregation and log availability can differ from the health graphs, so don't expect the totals to match exactly.

For individual events, explicitly request the service-principal event type and replace the example UTC timestamps with your investigation interval. Without an event-type filter, the [List signIns API](/en-us/graph/api/signin-list?view=graph-rest-beta&amp;preserve-view=true) returns only interactive user sign-ins by default.

```http
GET https://graph.microsoft.com/beta/auditLogs/signIns?$filter=createdDateTime ge 2026-10-05T10:00:00Z and createdDateTime lt 2026-10-05T11:00:00Z and signInEventTypes/any(t: t eq 'servicePrincipal')
Prefer: include-unknown-enum-members
```

Correlate the returned events with the affected application, agent properties, and nonzero error code. The `Prefer` header lets you receive additional evolvable enumeration values rather than interpreting `unknownFutureValue` as a specific identity type.

Note

These Microsoft Graph examples use `/beta`. Beta APIs are subject to change and aren't supported for production applications.

## Mitigate common issues

Choose a mitigation from the matching event's error code and failure reason, not only the alert title. The following issues are investigation starting points, not a ranked list of the most frequent failures. For error meanings, see the [Microsoft identity platform error reference](../../identity-platform/reference-error-codes).

### Credentials are invalid or expired

`AADSTS7000215` indicates an invalid client secret. `AADSTS7000222` indicates expired client secret keys. For certificate-based authentication, inspect the event's failure reason and certificate configuration rather than assuming a secret error applies.

1. Ask the agent developer to identify the failing token request, its client ID, and the configured credential. For an agent identity, check the blueprint credential. For a classic application identity, check that application's credential.
2. Correct an invalid credential or rotate an expired credential through the approved deployment process. Don't add credentials directly to an agent identity or agent's user account.
3. Validate token acquisition with the replacement credential before removing the old credential from the deployment. If several child agents share the blueprint, verify recovery across the affected agents.

Use managed identity federation where supported instead of production client secrets. See [Configure autonomous agent credentials](../../agent-id/autonomous-agent-authentication-authorization-flow#configure-your-client-credentials).

### Federated identity trust doesn't match the presented assertion

`AADSTS70021` can indicate that no matching federated identity record was found for a presented assertion. A recently configured credential might also need time to propagate. See [Workload identity federation considerations](../../workload-id/workload-identity-federation-considerations).

1. Identify the failing exchange stage. Compare the presented assertion's issuer, subject, and audience with the intended federated identity credential. Don't share tokens or credentials when collecting diagnostic information.
2. For an agent identity, verify the blueprint client ID, the child agent client ID in `fmi_path`, and the parent-child relationship. The blueprint can impersonate only its child agent identities.
3. Correct the specific trust mismatch. After a recent trust change, allow time for propagation and use controlled retries. Repeatedly retrying a permanently mismatched assertion doesn't fix the configuration.

For the agent-specific token chain, see [Agent autonomous app OAuth flow](../../agent-id/agent-autonomous-app-oauth-flow). For managed identity trust configuration, see [Configure an application to trust a managed identity](../../workload-id/workload-identity-federation-config-app-trust-managed-identity).

### The application is missing, disabled, or requested in the wrong tenant

`AADSTS700016` indicates that the application wasn't found in the requested tenant. `AADSTS7000112` indicates a disabled application. `AADSTS500011` indicates that the resource service principal wasn't found in the tenant.

1. Compare the request's tenant, client ID, and resource with the intended deployment. Distinguish the blueprint client ID, child agent client ID, application object ID, and service principal object ID.
2. Review the affected identity and, for agent identities, its blueprint. Check audit events for disabling or deletion. Disabling a blueprint prevents its child agent identities from authenticating.
3. Ask the identity owner to correct a wrong identifier or tenant. If an identity was intentionally disabled for incident response or governance, don't reenable it without approval.

See [Disable agent identities](../../agent-id/disable-agent-identities) and [Agent identity blueprints](../../agent-id/agent-blueprint).

### Conditional Access blocks the agent

`AADSTS53003` indicates that Conditional Access blocked token issuance. A newly enforced block policy, agent risk, or an unintended policy assignment can explain increased failures.

1. Review the failed event's **Conditional Access** details, policy result, and target resource. Check policy assignments to the agent identity or its blueprint, including approval attributes and exclusions.
2. Review recent policy changes and risk information. If the agent uses a classic service principal, use workload identity policy guidance instead of assuming agent-specific targeting applies.
3. Maintain intentional security blocks. Ask the policy owner to correct only unintended scope or configuration, and review proposed changes in report-only mode before enforcement where appropriate.

Don't ask an application-only agent to complete a human MFA prompt or make it use delegated permissions to bypass the block. See [Secure autonomous agents with Conditional Access](../conditional-access/policy-autonomous-agents), [Conditional Access for workload identities](../conditional-access/workload-identity), and [Identity Protection for agents](../../id-protection/concept-risky-agents).

### Resource access or application permissions are misconfigured

`AADSTS650056` describes a misconfigured application and can involve permissions, consent, identifiers, or certificates. Use the full error details to identify the cause. For application-only access, delegated user consent isn't a substitute for the required application permissions.

1. Verify the requested resource and scope. Agent application-only token requests use the resource's `/.default` scope.
2. Ask an authorized administrator to review the required application permissions, app role assignments, and any permissions inherited from the blueprint. Declaring required permissions doesn't itself grant access.
3. Correct only the missing or unintended grant and retry the operation.

A downstream API `403` after successful token issuance can indicate insufficient authorization; it isn't automatically a failed sign-in counted by this health signal. If sign-in succeeds but the operation fails, investigate resource authorization and the API response separately. See [Grant application permissions to autonomous agents](../../agent-id/autonomous-agent-authentication-authorization-flow#grant-application-permissions) and [Inheritable permissions](../../agent-id/concept-inheritable-permissions).

## Confirm recovery

After you correct the cause, confirm that new sign-in events for the affected application and resource succeed and that failure volume returns toward its expected pattern. Verify the agent's intended operation as well as token acquisition. Account for processing delay when comparing new logs with health graphs.

Mark the alert as **Dismissed** only after you investigate it. Dismissing an alert doesn't restore credentials, permissions, or token issuance. For alert status and notification guidance, see [Investigate Microsoft Entra Health monitoring alerts](howto-investigate-health-scenario-alerts) and [Configure health alert notifications](howto-configure-health-alert-notifications).