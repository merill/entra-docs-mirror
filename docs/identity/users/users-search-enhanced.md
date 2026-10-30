---
layout: Conceptual
title: User management enhancements - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-search-enhanced
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Describes how Microsoft Entra ID enables user search, filtering, and more information about your users.
ms.topic: how-to
ms.date: 2025-01-06T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: d2f60c2f-6bbe-69a3-04f9-7d20cf9dd159
document_version_independent_id: a230c850-a417-ce93-37f9-f7f5899a3709
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-search-enhanced.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-search-enhanced
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-search-enhanced.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c9c57034-5fe7-e12e-4cd3-338d9f6443df
---

# User management enhancements - Microsoft Entra ID | Microsoft Learn

## Overview

This article describes how to use the user management enhancements in the Microsoft Entra admin center. In this article, you review the **All users** and **user profile** pages.

Enhancements include:

- Preloaded scrolling so that you no longer have to select **Load more** to view more users.
- More user properties can be added as columns including city, country/region, employee ID, employee type, and external user state.
- More user properties can be filtered on including custom security attributes, on-premises extension attributes, and manager.
- More ways to customize your view, like using drag-and-drop to reorder columns.
- Copy and share your customized All Users view with others.
- An enhanced User Profile experience that gives you quick insights about a user and lets you view and edit more properties.

Note

These enhancements aren't currently available for Azure AD B2C tenants.

## All users page

The columns and filters available on the **All users** page have been updated. In addition to the existing columns for managing your list of users, the option to add more user properties as columns and filters including employee ID, employee hire date, on-premises attributes, and more has been added.

![Screenshot of new user properties displayed on All users page and user profile pages.](media/users-search-enhanced/user-properties.png)

### Reorder columns

You can customize your list view by reordering the columns on the page in one of two ways. One way is to directly drag and drop the columns on the page. Another way is to select **Columns** to open the column picker and then drag and drop the three-dot "handle" next to any given column.

### Share views

If you want to share your customized list view with another person, you can select **Copy link to current view** in the upper right corner to share a link to the view.

## User profile enhancements

The user profile page is now organized into three tabs: **Overview**, **Monitoring**, and **Properties**.

### Overview tab

The overview tab contains key properties and insights about a user, such as:

- Properties like user principal name, object ID, created date/time, and user type
- Selectable aggregate values such as the number of groups that the user is a member of, the number of apps to which they have access, and the number of licenses that are assigned to them
- Quick alerts and insights about a user such as their current account enabled status, the last time they signed in, whether they can use multifactor authentication, and B2B collaboration options

![Screenshot of new user profile displaying the Overview tab contents.](media/users-search-enhanced/user-profile-overview.png)

Note

Some insights about a user may not be visible to you unless you have sufficient role permissions.

### Monitoring tab

The monitoring tab is the new home for the chart showing user sign-ins over the past 30 days.

### Properties tab

The properties tab now contains more user properties. Properties are broken up into categories including Identity, Job information, Contact information, Parental controls, Settings, and On-premises.

![Screenshot of new user profile displaying the Properties tab contents.](media/users-search-enhanced/user-profile-properties.png)

You can edit properties by selecting the pencil icon next to any category, which will then redirect you to a new editing experience. Here, you can search for specific properties or scroll through property categories. You can edit one or many properties, across categories, before selecting **Save**.

![Screenshot of user profile properties open for editing.](media/users-search-enhanced/user-properties-edit.png)

Note

Some properties won't be visible or editable if they are read-only or if you don’t have sufficient role permissions to edit them.