---
layout: Conceptual
title: Search and filter groups members and owners (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-members-owners-search
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Search and filter groups members and owners in Microsoft Entra.
ms.topic: how-to
ms.date: 2025-09-04T00:00:00.0000000Z
ms.reviewer: Mohit
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 6864fd99-6f1f-a4db-931e-b5dfc915fec8
document_version_independent_id: 76c2f17c-011d-c0a5-b163-7399cce97701
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-members-owners-search.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-members-owners-search
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-members-owners-search.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 0cceae6d-41a6-7749-16af-944e82255656
---

# Search and filter groups members and owners (preview) - Microsoft Entra ID | Microsoft Learn

## Overview

This article tells you how to search for members and owners of a group and how to use search filters in Microsoft Entra ID, part of Microsoft Entra. Search functions for groups include:

- Groups search capabilities, such as substring search in group names
- Filtering and sorting options on member and owner lists
- Search capabilities for member and owner lists

## Group search and sort

On the **All groups** page, when you enter a search string, you can toggle between **contains** and **starts with** searches on the **All groups** page only.

Important

The contains search uses tokenized matching, not literal substring matching. This means the system breaks both your query and the stored values into smaller chunks (tokens), usually words or alphanumeric segments, and checks if any query token appears in the stored tokens.

The substring search is done using whole words only, and any special characters are searched for also as an ANDed search. For example, searching for -Name starts a search for the substring "Name" and a search for "-". Substring search is case-sensitive. Object ID or mailNickname properties are also searched.

![Screenshot of new substring searches on the All Groups page.](media/groups-members-owners-search/members-list.png)

For example, a search for “policy” returns both "MDM policy – West" and "Policy group." A group named "New\_policy" wouldn't be returned. You can sort the **All groups** list by name in ascending or descending order.

## Group member search and filter

### Search group member and owner lists

When you search the members or owners of a group, a tokenized contains search is automatically used. For example, a search for “Scott” returns both Scott Wilkinson and Maya Scott.

![Screenshot of new substring searches on the group members and owners lists.](media/groups-members-owners-search/groups-search-preview.png)

### Filter member and owner lists

You can also filter the group members and owners lists by user type. This information is found in the **User Type** column in the members or owners list. You can filter the list to see only members or guests.

The **Members** page includes all the unique members of group including anyone who inherits their group membership from another group.

You can also search and filter the lists individually. Filtering the all members list doesn't affect filters that are applied to the direct members list.

## Group memberships

You can also view group memberships on the **Group memberships** page. The **Group memberships** page supports search, sort, and filter operations that are similar to the other Groups pages.

## Group member counts

The group **Overview** page provides member counts for groups. You can see the total number of direct members for a group and the total membership count (all the unique members of group including inherited memberships) on the **Overview** page.

![Screenshot of higher accuracy in group membership counts.](media/groups-members-owners-search/member-numbers.png)