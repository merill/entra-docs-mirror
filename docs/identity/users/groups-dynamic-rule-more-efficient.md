---
layout: Conceptual
title: Create simpler and faster rules for dynamic membership groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-dynamic-rule-more-efficient
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to optimize your membership rules to automatically populate groups.
ms.topic: concept-article
ms.date: 2025-01-15T00:00:00.0000000Z
ms.reviewer: jordandahl
ms.custom: it-pro
locale: en-us
document_id: a0ca9750-2f42-b2bb-18af-0fe63da855d3
document_version_independent_id: 37a046aa-10d3-477b-448a-3b50d0ec72c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-dynamic-rule-more-efficient.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-dynamic-rule-more-efficient
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-dynamic-rule-more-efficient.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: f595c404-71ab-8049-6df7-97762c034f38
---

# Create simpler and faster rules for dynamic membership groups - Microsoft Entra ID | Microsoft Learn

## Overview

This article discusses the most common methods that you can use to simplify your rules for dynamic membership groups. Rules that are simpler and more efficient result in better processing times for dynamic groups.

When you're writing membership rules for dynamic membership groups, follow the tips in this article to ensure that you create these rules as efficiently as possible.

## Minimize use of the -match operator

Minimize your use of the `-match` operator in rules as much as possible. Instead, explore if it's possible to use the `-startsWith`, `-endsWith` or `-eq` operator. `-eq` is preferred when the full attribute value is known; `-startsWith` and `-endsWith` are next most efficient when only a prefix or suffix is known. Consider using other properties that allow you to write rules to select the users for a group without using the `-match` operator.

For example, if you want a rule for the group that contains all users whose city is Lagos, don't use a rule like these:

- `user.city -match "ago"`
- `user.city -match ".*?ago.*"`

It's better to use a rule like this example:

- `user.city -startsWith "Lag"`

Or, best of all:

- `user.city -eq "Lagos"`

Similarly, for email-domain rules, don't use:

- user.mail -match ".\*@Contoso.com$"
- user.mail -notMatch ".\*@Contoso.com$"

It's better to use:

- user.userPrincipalName -endsWith "@Contoso.com"
- user.mail -notEndsWith "@Contoso.com"

## Minimize use of the -contains operator

As with `-match`, minimize your use of the `-contains` operator in rules as much as possible. Instead, explore if it's possible to use the `-startsWith`, `-endsWith` or `-eq` operator. Using `-contains` can increase processing times, especially for tenants that have many dynamic membership groups.

## Use fewer -or operators

Identify when your rule uses various values for the same property, linked together with `-or` operators. Instead, use the `-in` operator to group them into a single criterion. A single criterion makes the rule easier to evaluate.

For example, don't use a rule like this one:

```
(user.department -eq "Accounts" -and user.city -eq "Lagos") -or 
(user.department -eq "Accounts" -and user.city -eq "Ibadan") -or 
(user.department -eq "Accounts" -and user.city -eq "Kaduna") -or 
(user.department -eq "Accounts" -and user.city -eq "Abuja") -or 
(user.department -eq "Accounts" -and user.city -eq "Port Harcourt")
```

It's better to use a rule like this example:

- `user.department -eq "Accounts" -and user.city -in ["Lagos", "Ibadan", "Kaduna", "Abuja", "Port Harcourt"]`

Conversely, identify similar subcriteria with the same property not equal to various values that are linked with `-and` operators. Then use the `-notin` operator to group them into a single criterion to make the rule easier to understand and evaluate.

For example, don't use a rule like this one:

- `(user.city -ne "Lagos") -and (user.city -ne "Ibadan") -and (user.city -ne "Kaduna") -and (user.city -ne "Abuja") -and (user.city -ne "Port Harcourt")`

It's better to use a rule like this example:

- `user.city -notin ["Lagos", "Ibadan", "Kaduna", "Abuja", "Port Harcourt"]`

## Avoid redundant criteria

Ensure that you aren't using redundant criteria in your rule. For example, don't use a rule like this one:

- `user.city -eq "Lagos" or user.city -startswith "Lag"`

It's better to use a rule like this example:

- `user.city -startswith "Lag"`