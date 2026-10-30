---
layout: Conceptual
title: 'Conditional Access Policy Insights: Monitoring and Evaluation - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-report-only
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Discover how to analyze Conditional Access policy results with tools like Azure Monitor and insights workbooks for better policy management.
ms.topic: concept-article
ms.date: 2026-06-01T00:00:00.0000000Z
ms.reviewer: kvenkit
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 1f70889b-b30f-8295-c6d1-60a6c1d7fc7f
document_version_independent_id: b322053d-123b-db51-8098-7c54328e2404
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-conditional-access-report-only.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-conditional-access-report-only
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-conditional-access-report-only.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ef61f7b4-ec79-34f8-50d9-6a2b3d50b60c
---

# Conditional Access Policy Insights: Monitoring and Evaluation - Microsoft Entra ID | Microsoft Learn

## Overview

Conditional Access helps organizations stay secure by applying the appropriate security access controls in the right circumstances. Understanding the impact of these policies is challenging, especially when deploying new policies. This article explains how to analyze the impact of Conditional Access policies using report-only mode and other tools.

Administrators have several options based on report-only mode. Report-only mode is a policy state that lets administrators test most Conditional Access policies before enabling them.

- Administrators can evaluate Conditional Access policies in report-only mode, except for items included in the "User Actions" scope.
- During sign-in, the system evaluates policies in report-only mode but doesn't enforce them.
- Results are logged in the **Conditional Access** and **Report-only** tabs of the Sign-in log details.
- Customers with an Azure Monitor subscription can monitor the impact of their Conditional Access policies using the Conditional Access insights workbook.

Warning

Policies in report-only mode that require a compliant device can prompt users on macOS, iOS, and Android devices to select a device certificate during policy evaluation, even though device compliance isn't enforced. These prompts can repeat until the device is compliant. To prevent end users from receiving prompts during sign-in, exclude the Mac, iOS, and Android device platforms from report-only policies that perform device compliance checks.

## Policy evaluation results

When a policy is evaluated for a given sign-in, there are several possible results:

| Result | Description |
| --- | --- |
| Report-only: Success | All configured policy conditions, required non-interactive grant controls, and session controls were satisfied. For example, a multifactor authentication requirement is satisfied by an MFA claim already present in the token, or a compliant device policy is satisfied by performing a device check on a compliant device. |
| Report-only: Failure | All configured policy conditions were satisfied but not all the required non-interactive grant controls or session controls were satisfied. For example, a policy applies to a user where a block control is configured, or a device fails a compliant device policy. |
| Report-only: User action required | All configured policy conditions were satisfied but user action would be required to satisfy the required grant controls or session controls. With report-only mode, the user isn't prompted to satisfy the required controls. For example, users aren't prompted for multifactor authentication challenges or terms of use. |
| Report-only: Not applied | Not all configured policy conditions were satisfied. For example, the user is excluded from the policy or the policy only applies to certain trusted named locations. |
| Success | Sign-in events where the policy applied, the requirements were met, and the policy would allow the sign-in to proceed. The sign-in might still be blocked by a different policy. |
| Failure | Sign-in events where the policy applied, the requirements weren't met, and the policy would block the sign-in. This might be by design, like when sign-ins from a specific location are blocked, or accidental when the policy is misconfigured. |
| Not applied | Sign-in events where the policy wasn't applied, for example, the user was excluded. |

## Reviewing results

Administrators can use several options to review the potential results of policies in their environment:

- Workbooks
- Sign-in logs
- Policy impact (preview)

### Policy impact

The policy impact view of Conditional Access lets admins with at least the Security Reader role see a snapshot of the potential or existing impacts of policies on interactive sign-ins in your organization. You can explore the impact over the past 24 hours, 7 days, or 1 month. You can also see and link to a sampling of sign-in events for more details.

[![Screenshot of Conditional Access policy impact example.](media/concept-conditional-access-report-only/policy-impact-example-report-only.png)](media/concept-conditional-access-report-only/policy-impact-example-report-only.png#lightbox)

### Workbooks

Administrators can create multiple policies in report-only mode, so it's important to understand both the individual impact of each policy and the combined impact of multiple policies evaluated together. The [Conditional Access Insights and Reporting workbook](howto-conditional-access-insights-reporting) lets administrators visualize Conditional Access policies, query and monitor the impact of a policy for a specific time range, set of applications, and users. Administrators can customize workbooks to meet their needs.

### Sign-in logs

For deeper evaluation of Conditional Access policies and their application at a specific sign-in, administrators might investigate individual sign-in events. Each event includes details about which Conditional Access policies were enabled, in report-only mode, applied, or not applied.

![Screenshot showing the report-only tab in a sign-in log.](media/concept-conditional-access-report-only/report-only-detail-in-sign-in-log.png)

## Using these options

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## Compare and validate policies before enforcement

Report-only mode is a valuable tool for validating policy changes progressively before you enforce them. Use the following practices to reduce the risk of unintended access disruptions:

- **Test new policies alongside enforced policies.** Create a new policy in report-only mode while your existing enforced policies remain active. This approach lets you observe what the new policy *would* do without affecting user access. Monitor the report-only results in sign-in logs to confirm the policy behaves as expected before you switch it to an enforced state.
- **Compare outcomes in the Insights workbook.** Use the [Conditional Access Insights and Reporting workbook](howto-conditional-access-insights-reporting) to view report-only and enforced policy results side by side for a specific time range, set of applications, and users. This comparison helps you identify where a new policy would change access decisions before those changes take effect. The workbook requires Microsoft Entra ID P1 and a Log Analytics workspace that's receiving sign-in logs; for details, see the workbook [prerequisites](howto-conditional-access-insights-reporting#prerequisites).
- **Validate changes to existing policies.** Before you modify an enforced policy, create a copy in report-only mode with your proposed changes. Compare the report-only copy's results against the original enforced policy to verify the intended effect. When you're satisfied, update the enforced policy and remove the copy.
- **Use AI-assisted phased rollout.** Where available, the [Conditional Access Optimization Agent](../../security-copilot/conditional-access-agent-optimization) creates suggested policies in report-only mode. You can review the agent's analysis and projected impact before deciding to enforce. For more information, see [Phased rollout with the Conditional Access Optimization Agent](../../security-copilot/conditional-access-agent-optimization-phased-rollout). The agent requires Microsoft Security Copilot with provisioned security compute units (SCUs) and Microsoft Entra ID P1, so it isn't enabled in every tenant; for details, see the agent [prerequisites](../../security-copilot/conditional-access-agent-optimization#prerequisites).
- **A note on A/B testing.** Conditional Access doesn't support classical A/B testing, which splits live traffic between two enforced variants of a policy. Where the Optimization Agent is enabled in your tenant, the closest native equivalent is the [Optimization Agent's phased rollout](../../security-copilot/conditional-access-agent-optimization-phased-rollout), which gradually applies a new policy to ordered groups while keeping the original report-only policy intact, so you can compare outcomes between cohorts before full enforcement.

Note

Report-only mode evaluates policies but doesn't enforce grant controls or session controls. Users aren't prompted for multifactor authentication or blocked by report-only policies. Some limitations apply, such as policies that use the **User Actions** scope. For more information, see the policy evaluation results in this article.