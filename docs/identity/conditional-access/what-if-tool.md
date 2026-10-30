---
layout: Conceptual
title: The Conditional Access What If tool - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/what-if-tool
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Simulate Conditional Access policy results with the What If tool to troubleshoot and optimize your environment.
ms.topic: troubleshooting-general
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: kvenkit
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5b96bf8a-e95d-292c-366d-c5d2a0f887b1
document_version_independent_id: f640200f-9a70-0109-e2b3-2187f0dfad02
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/what-if-tool.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/what-if-tool
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/what-if-tool.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 202a5003-8956-2373-5dec-d8a3b429633a
---

# The Conditional Access What If tool - Microsoft Entra ID | Microsoft Learn

## Overview

The **Conditional Access What If policy tool** helps you understand the result of [Conditional Access](overview) policies in your environment. It can be useful when simulating uncommon scenarios, enabling you to design more comprehensive security policies. Instead of manually testing your policies with multiple sign-ins, this tool helps you simulate a sign-in for a user, agent identity, or single tenant service principal. The simulation estimates how your policies affect this sign-in and generates a report.

The **What If** tool and [APIs](/en-us/graph/api/conditionalaccessroot-evaluate) let you quickly determine the policies that apply to a specific user, agent identity, or single tenant service principal. Use this information to troubleshoot issues, understand which policies apply to specific sign-in conditions, and test complex sign-in scenarios.

## How it works

The Conditional Access What If tool is powered by the [What If Evaluation API](/en-us/graph/api/conditionalaccessroot-evaluate). To use the tool, start by configuring the conditions of the sign-in scenario you want to simulate. The configuration should include:

- The user, agent identity (Preview), or single tenant service principal you want to test.
- The cloud apps, user action they would attempt to perform, or sensitive data protected by authentication context they would attempt to access.
- The sign-in conditions under which access would be attempted.

Important

The What If tool doesn't test for [Conditional Access service dependencies](service-dependencies). For example, if you're using **What If** to test a Conditional Access policy for Microsoft Teams, the result doesn't consider any policy that applies to Office 365 Exchange Online, a Conditional Access service dependency for Microsoft Teams.

Next, initiate a simulation run that evaluates your settings. Only policies that are enabled or in report-only mode are included in an evaluation run.

When the evaluation finishes, the tool generates a report of the affected policies. To gather more information about a Conditional Access policy, use [Conditional Access per-policy reporting](concept-conditional-access-report-only#policy-impact-preview) or the [Conditional Access insights and reporting workbook](howto-conditional-access-insights-reporting) for details about policies in report-only mode or currently enabled.

## Run the What If tool

You can find the **What If** tool in the **Microsoft Entra admin center** &gt; **Entra ID** &gt; **Conditional Access** &gt; **Policies** &gt; **What If**.

[![Screenshot of the Conditional Access Policies page with the What If tool highlighted in the toolbar.](media/what-if-tool/portal-showing-location-of-what-if-tool.png)](media/what-if-tool/portal-showing-location-of-what-if-tool.png#lightbox)

To run the What If evaluation, provide the conditions you want to evaluate.

## Conditions

The following conditions are required: identity, target resource, device platform, and client app. All other conditions are optional and are assumed to be set to **none** by default if no value is provided. For definitions of these conditions, see the article [Building a Conditional Access policy](concept-conditional-access-policies).

[![Screenshot of the What If page showing fields for entering conditions.](media/what-if-tool/supply-conditions-to-evaluate-in-the-what-if-tool.png)](media/what-if-tool/supply-conditions-to-evaluate-in-the-what-if-tool.png#lightbox)

## Evaluation

Start an evaluation by selecting **What If**. The evaluation result provides you with a report that consists of:

- An indicator showing whether classic policies exist in your environment.
- Policies that apply to your user, agent, or workload identity.
- Policies that don't apply to your user or workload identity.

[![Screenshot of an example of the policy evaluation in the What If tool showing policies that would apply.](media/what-if-tool/conditional-access-what-if-evaluation-result-example.png)](media/what-if-tool/conditional-access-what-if-evaluation-result-example.png#lightbox)

The list of policies that apply also includes [grant controls](concept-conditional-access-grant) and [session controls](concept-conditional-access-session) that must be satisfied.

The list of policies that don't apply includes the reasons why these policies don't apply. For each listed policy, the reason represents the first condition that wasn't satisfied.

**Has filter** indicates whether the policy has app filters that use custom security attributes.

## Key differences between the What If evaluation API and the legacy experience

The [What If Evaluation API](/en-us/graph/api/conditionalaccessroot-evaluate) is a Microsoft Graph API that is called by the Conditional Access experience. The API is different from the legacy What If evaluation in a few ways:

1. The What If API is a public and fully supported API. You can use it through the Conditional Access experience and the Microsoft Graph API.
2. The logic aligns with the authentication logic used during sign-in to provide more accurate policy evaluation.
3. The What If API expects all sign-in parameters to be defined for the evaluation to provide the most accurate results. If your tenant has policies with specific conditions and the sign-in details for those conditions aren't provided, the What If API can't evaluate those conditions.

Note

For application specification, provide the App ID. Groups of apps, such as **Office 365** or **Microsoft Admin Portals**, don't result in a match.

### Examples

This example highlights key differences:

Suppose you have a Conditional Access policy with the following configuration:

- User: All users
- Resource: Office 365
- Location: United States
- Sign-in risk: High

| Example | Parameters | Result based on legacy What If evaluation | Result based on the new What If evaluation API |
| --- | --- | --- | --- |
| 1 | UserId = “00aa00aa-bb11-cc22-dd33-44ee44ee44ee" | Applies | Does not apply |
| 2 | UserId = “00aa00aa-bb11-cc22-dd33-44ee44ee44ee"  ApplicationId = “00000003-0000-0ff1-ce00-000000000000" | Applies | Does not apply |
| 3 | UserId = “00aa00aa-bb11-cc22-dd33-44ee44ee44ee"  ApplicationId = “00000003-0000-0ff1-ce00-000000000000"  Location = “US” | Applies | Does not apply |
| 4 | UserId = “00aa00aa-bb11-cc22-dd33-44ee44ee44ee"  ApplicationId = “00000003-0000-0ff1-ce00-000000000000"  Location = “US”  Sign-in Risk = “High” | Applies | Applies |