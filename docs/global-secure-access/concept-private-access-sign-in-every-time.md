---
layout: Conceptual
title: Microsoft Entra Private Access sign-in every time (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-private-access-sign-in-every-time
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Understand sign-in every time for Microsoft Entra Private Access, its Conditional Access dependency, and its five-minute reauthentication window.
ms.topic: concept-article
ms.subservice: entra-private-access
ms.date: 2026-11-01T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1026
ai-usage: ai-generated
locale: en-us
document_id: 6f3e0ba2-7614-f37b-1655-0838f00b0742
document_version_independent_id: 6f3e0ba2-7614-f37b-1655-0838f00b0742
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-private-access-sign-in-every-time.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-private-access-sign-in-every-time
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-private-access-sign-in-every-time.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: dbc7b432-f971-61e0-e107-cd29dc5e5f3d
---

# Microsoft Entra Private Access sign-in every time (preview) - Global Secure Access | Microsoft Learn

Sign-in every time (preview) is a Microsoft Entra Private Access feature that uses Conditional Access to require reauthentication when users access sensitive private applications.

Use this overview to understand the supported client requirements, Conditional Access dependency, and reauthentication behavior before you plan your deployment.

Global Secure Access uses the Conditional Access **Every time strict (preview)** control for this feature. The Global Secure Access feature requires Conditional Access. You can use **Every time strict (preview)** in Conditional Access independently of Global Secure Access.

## Supported clients and platforms

Sign-in every time (preview) is currently supported only with the Global Secure Access client for Windows, version **2.34.222 or later**. Users with earlier Windows client versions or other operating systems are blocked from accessing applications where the feature is enforced.

## Scope enforcement by operating system

Depending on your requirements, you may want to allow access to these private applications from non-Windows devices, skipping sign in frequency requirements. You can use Conditional Access [device platform conditions](../identity/conditional-access/concept-conditional-access-conditions#device-platforms) to exclude non-Windows operating systems from policies that enforce sign-in every time.

## Reauthentication interval

Global Secure Access has a **five-minute reauthentication window**. It doesn't prompt the user to reauthenticate if it's been less than five minutes since the user signed in to a given private application. The following example illustrates sign-in prompt behavior and the user experience:

1. A Global Secure Access administrator configures a policy for the private application called 'SSH admin tools jump box' to use the **Every time strict (preview)** session control.
2. The user, a Linux administrator, opens the terminal on their Windows desktop and attempts to access the SSH admin tools application. Global Secure Access detects that more than five minutes have elapsed since the last sign-in and triggers an authentication prompt.
3. The user completes authentication at 09:01:15, accesses the application, runs one command, and closes the terminal at 09:01:55.
4. The user reopens the terminal at 09:03:45 and accesses the application again. Since it's been less than five minutes, a new sign-in prompt isn't triggered. The user completes the task and closes the terminal.
5. At 09:10:34, the user reopens the terminal. Since it's been more than five minutes since 09:01:15, the user is required to reauthenticate.