---
layout: Conceptual
title: 'Quickstart: View enterprise applications - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/view-applications-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Access Microsoft Entra admin center to effortlessly view and filter enterprise apps. Streamline tenant oversight and take charge now.
ms.topic: quickstart
ms.date: 2025-03-31T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: mode-other, enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 8620e16e-2440-1942-3d58-3ec08ee0030d
document_version_independent_id: d0b03ffe-a8d1-74b7-d983-017241271e35
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/view-applications-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/view-applications-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/view-applications-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 60263845-f7ab-4b2e-f77e-d07624a876e2
---

# Quickstart: View enterprise applications - Microsoft Entra ID | Microsoft Learn

In this quickstart, you learn how to use the Microsoft Entra admin center to search for and view the enterprise applications configured in your Microsoft Entra tenant.

We recommend that you use a nonproduction environment to test the steps in this quickstart.

## Prerequisites

To view applications registered in your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, or owner of the service principal.
- Completion of the steps in [Quickstart: Add an enterprise application](add-application-portal).

## View a list of applications

To view the enterprise applications registered in your tenant:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**. [![View the registered applications in your Microsoft Entra tenant.](media/view-applications-portal/view-enterprise-applications.png)](media/view-applications-portal/view-enterprise-applications.png#lightbox)
3. To view more applications, select **Load more** at the bottom of the list. If there are many applications in your tenant, it might be easier to search for a particular application instead of scrolling through the list.

## Search for an application

To search for a particular application:

1. Select the **Application Type** filter option. Select **All applications** from the **Application Type** drop-down menu, and choose **Apply**.
2. Enter the name of the application you want to find. If the application is already in your Microsoft Entra tenant, it appears in the search results. For example, you can search for the **Microsoft Entra SAML Toolkit 1** application that is used in the previous quickstarts.
3. Try entering the first few letters of an application name.

## Select viewing options

Select options according to what you're looking for:

1. The default filters are **Application Type** and **Application ID starts with**.
2. Under **Application Type**, choose one of these options:
    - **Enterprise Applications** shows non-Microsoft applications.
    - **Microsoft Applications** shows Microsoft applications.
    - **Managed Identities** shows applications that are used to authenticate to services that support Microsoft Entra authentication.
    - **Agent ID (Preview)** shows AI agent identities that are used by AI agents to authenticate to services that support Microsoft Entra authentication.
    - **All Applications** shows both non-Microsoft and Microsoft applications.
3. Under **Application ID starts with**, enter the first few digits of the application ID if you know the application ID.
4. After choosing the options you want, select **Apply**.
5. Select **Add filters**to add more options for filtering the search results. The other options include:
    - **Application Status**
    - **Application Visibility**
    - **Created on**
    - **Assignment required**
    - **Is App Proxy**
    - **Owner**
    - **Identifier URI (Entity ID)**
    - **Homepage URL**
6. To remove any of the filter options already added, select the **X** icon next to the filter option.

## Clean up resources

If you created a test application named **Microsoft Entra SAML Toolkit 1** that was used throughout the quickstarts, you can consider deleting it now to clean up your tenant. For more information, see [Delete an application](delete-application-portal).