---
layout: Conceptual
title: Conditional Access - Block access by location - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-block-by-location
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy to block access to resources by IP location.
ms.reviewer: lhuangnorth
ms.date: 2026-03-24T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: 5815957c-cc37-2982-7a50-16e96c0378b8
document_version_independent_id: 33f22bdb-1675-96b0-27ad-8d1ba7cc5a75
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-block-by-location.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-block-by-location
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-block-by-location.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: b40b4a1c-16c7-91e1-0ee1-87ba05826e7f
---

# Conditional Access - Block access by location - Microsoft Entra ID | Microsoft Learn

## Overview

With the location condition in Conditional Access, you can control access to your cloud apps based on the network location of a user. The location condition is commonly used to block access from countries/regions where your organization knows traffic shouldn't come from. For more information about IPv6 support, see the article [IPv6 support in Microsoft Entra ID](/en-us/troubleshoot/azure/active-directory/azure-ad-ipv6-support).

Note

Conditional Access policies are enforced after first-factor authentication is completed. Conditional Access isn't intended to be an organization's first line of defense for scenarios like denial-of-service (DoS) attacks, but it can use signals from these events to determine access.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Named locations**.
3. Choose the type of location to create.
    - **Countries location** or **IP ranges location**.
    - Give your location a name.
4. Provide the **IP ranges** or select the **Countries/Regions**for the location you're specifying.
    - If you select IP ranges, you can optionally **Mark as trusted location**.
    - If you choose Countries/Regions, you can optionally choose to include unknown areas.
5. Select **Create**

More information about the location condition in Conditional Access can be found in the article, [Conditional Access: Network assignment conditions](concept-assignment-network)

## Create a Conditional Access policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Network**.
    1. Set **Configure** to **Yes**
    2. Under **Include**, select **Selected networks and locations**
        1. Select the blocked location you created for your organization.
        2. Select **Select**.
8. Under **Access controls** &gt; **Grant**, select **Block access**, then select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).