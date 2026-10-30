---
layout: Conceptual
title: Continuous access evaluation strict location enforcement in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation-strict-enforcement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Responding to changes in user state faster with continuous access evaluation strict location enforcement in Microsoft Entra ID
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: sreyanthmora
ms.custom: sfi-image-nochange
locale: en-us
document_id: 59216ba9-0ea9-5af1-16db-4764f5d952b1
document_version_independent_id: 011521ae-8bd8-02cf-2ae9-530b86b9f40c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-continuous-access-evaluation-strict-enforcement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-continuous-access-evaluation-strict-enforcement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-continuous-access-evaluation-strict-enforcement.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0e8c29f5-08f0-e3b9-6945-fc1ae530f7bf
---

# Continuous access evaluation strict location enforcement in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Strictly enforce location policies is a new enforcement mode for continuous access evaluation (CAE) used in Conditional Access policies. This new mode provides protection for resources, immediately stopping access if the IP address detected by the resource provider isn't allowed by Conditional Access policy. This option is the highest security modality of CAE location enforcement, and requires that administrators understand the routing of authentication and access requests in their network environment. See [Introduction to continuous access evaluation](concept-continuous-access-evaluation) for a review of how CAE-capable clients and resource providers, like the Outlook email client and Exchange Online, evaluate location changes.

| Location enforcement mode | Recommended network topology | If the IP address detected by the Resource isn't in the allowed list | Benefits | Configuration |
| --- | --- | --- | --- | --- |
| Standard (Default) | Suitable for all topologies | A short-lived token is issued only if Microsoft Entra ID detects an allowed IP address. Otherwise, access is blocked | Falls back to the pre-CAE location detection mode in split tunnel network deployments where CAE enforcement would affect productivity. CAE still enforces other events and policies. | None (Default Setting) |
| Strictly enforced location policies | Egress IP addresses are dedicated and enumerable for both Microsoft Entra ID and all resource provider traffic | Access blocked | Most secure, but requires well understood network paths | 1. Test IP address assumptions with a small population. 2. Enable "Strictly enforce" under Session controls. |

## Configure strictly enforced location policies

### Step 1 - Configure a Conditional Access location based policy for your target users

Before administrators create a Conditional Access policy requiring strict location enforcement, they must be comfortable using policies like the one described in [Conditional Access location based policies](policy-block-by-location). Test policies like this one with a subset of users before proceeding to the next step. Testing before enabling strict enforcement helps administrators avoid discrepancies between the allowed and actual IP addresses seen by Microsoft Entra ID during authentication.

### Step 2 - Test policy on a small subset of users

![Screenshot showing a Conditional Access policy with &quot;Strictly enforce location policies&quot; enabled.](media/concept-continuous-access-evaluation-strict-enforcement/conditional-access-policy-strictly-enforce-location-policies.png)

After enabling policies requiring strict location enforcement on a subset of test users, validate the testing experience using the filter **IP address (seen by resource)** in the Microsoft Entra sign-in logs. This validation allows administrators to find scenarios where strict location enforcement might block users with an unallowed IP seen by the CAE-enabled resource provider.

Before administrators turn on Conditional Access policies requiring strict location enforcement, they should:

- Ensure all authentication traffic towards Microsoft Entra ID and access traffic to resource providers are from dedicated egress IPs that are known.
    - Like Exchange Online, Teams, SharePoint Online, and Microsoft Graph
- Ensure that all IP addresses from which their users can access Microsoft Entra ID and resource providers are included in their [IP-based named locations](concept-assignment-network#ipv4-and-ipv6-address-ranges).
- Ensure that they aren't sending traffic to non-Microsoft 365 applications through Global Secure Access.
    - [Source IP restoration](../../global-secure-access/how-to-source-ip-restoration) isn't supported for these non-Microsoft 365 applications. Enabling strict location enforcement with Global Secure Access blocks access even if the user is in a trusted IP location.
- Review their Conditional Access policies to ensure that they don't have any policies that don't support CAE. For more information, see [CAE-supported Conditional Access policies](/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation#supported-location-policies).

If administrators don't perform this validation, their users might be negatively impacted. If traffic to Microsoft Entra ID or a CAE supported resource is through a shared or undefinable egress IP, don't enable strict location enforcement in your Conditional Access policies.

### Step 3 - Use the CAE Workbook to Identify IP addresses that should be added to your named locations

If you haven't already, create a new Azure Workbook using the public template "Continuous Access Evaluation Insights" to identify IP mismatch between IP address seen by Microsoft Entra ID and **IP address (seen by resource)**. In this case, you might have a split-tunnel network configuration. To ensure your users aren't accidentally locked out when strict location enforcement is enabled, administrators should:

- Investigate and identify any IP addresses identified in the CAE Workbook.
- Add public IP addresses associated with known organizational egress points to their defined [named locations](concept-assignment-network#ipv4-and-ipv6-address-ranges).

    [![Screenshot of cae-workbook with an example of IP address seen by resource filter.](media/concept-continuous-access-evaluation-strict-enforcement/continuous-access-evaluation-workbook.png)](media/concept-continuous-access-evaluation-strict-enforcement/continuous-access-evaluation-workbook.png#lightbox)

    The following screenshot shows an example of a client’s access to a resource being blocked. This block is due to policies requiring CAE strict location enforcement being triggered revoking the client’s session.

    ![Screenshot of the message a user sees if they are blocked by strict location enforcement.](media/concept-continuous-access-evaluation-strict-enforcement/blocked-due-to-strict-enforcement.png)

    This behavior can be verified in the sign-in logs. Look for **IP address (seen by resource)** and investigate adding this IP to [named locations](concept-assignment-network#ipv4-and-ipv6-address-ranges) if experiencing unexpected blocks from Conditional Access on users.

    ![Screenshot of a sign-in log entry with both IP address and IP address seen by resource.](media/concept-continuous-access-evaluation-strict-enforcement/activity-details-ip-differs.png)

    Looking at the **Conditional Access Policy details** tab provides more details of blocked sign-in events.

    ![Screenshot of Conditional Access Policy detail with the locations that were seen.](media/concept-continuous-access-evaluation-strict-enforcement/conditional-access-policy-details-authentication-block.png)

### Step 4 - Continue deployment

Repeat steps 2 and 3 with expanding groups of users until strictly enforce location policies are applied across the target user base. Roll out carefully to avoid impacting user experience.

## Troubleshooting with sign-in logs

Administrators can investigate the Sign-in logs to find cases with **IP address (seen by resource)**.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Add filters and columns to find events and remove unnecessary information.
    1. Add the **IP address (seen by resource)** column and filter out any blank items to narrow the scope. The **IP address (seen by resource)** is blank when the IP seen by Microsoft Entra ID matches the IP seen by the resource.

        [![Screenshot showing an example of how to find more information in the sign-in logs.](media/concept-continuous-access-evaluation-strict-enforcement/sign-in-logs-ip-address-seen-by-resource.png)](media/concept-continuous-access-evaluation-strict-enforcement/sign-in-logs-ip-address-seen-by-resource.png#lightbox)

        **IP address (seen by resource)** contains filter isn't empty in the following examples:

### Initial authentication

1. Authentication is successful using a CAE token.

    ![Screenshot showing a successful sign in with a CAE token.](media/concept-continuous-access-evaluation-strict-enforcement/activity-details-sign-ins-initial-authentication-success.png)
2. The **IP address (seen by resource)** is different from the IP address seen by Microsoft Entra ID. Although the IP address seen by the resource is known, there's no enforcement until the resource redirects the user for reevaluation of the IP address seen by the resource.

    ![Screenshot showing IP address and IP address seen by resource in the sign-in log.](media/concept-continuous-access-evaluation-strict-enforcement/activity-details-ip-differs.png)
3. Microsoft Entra authentication succeeds because strict location enforcement isn't applied at the resource level.

    ![Screenshot showing that a Conditional Access policy wasn't applied because the location is excluded.](media/concept-continuous-access-evaluation-strict-enforcement/conditional-access-policy-details-authentication-success.png)

### Resource redirect for reevaluation

1. Authentication fails, and a CAE token isn't issued.

    ![Screenshot showing a failed authentication.](media/concept-continuous-access-evaluation-strict-enforcement/activity-details-sign-ins-authentication-fails.png)
2. **IP address (seen by resource)** is different from the IP seen by Microsoft Entra ID.

    ![Screenshot showing a mismatch in IP addresses.](media/concept-continuous-access-evaluation-strict-enforcement/activity-details-ip-differs.png)
3. Authentication fails because **IP address (seen by resource)** isn't a known [named location](concept-assignment-network#ipv4-and-ipv6-address-ranges) in Conditional Access.

    ![Screenshot showing a Conditional Access policy applied, because the IP address was included in a block rule.](media/concept-continuous-access-evaluation-strict-enforcement/conditional-access-policy-details-authentication-block.png)