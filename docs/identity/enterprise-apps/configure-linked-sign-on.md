---
layout: Conceptual
title: Add linked single sign-on to an application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-linked-sign-on
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Add linked single sign-on to an application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-06-20T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: enterprise-apps
locale: en-us
document_id: 415d26ca-2a89-671f-04e3-d40d53e5bd38
document_version_independent_id: 0d62da94-efe8-75b6-f718-87547953e6cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-linked-sign-on.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-linked-sign-on
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-linked-sign-on.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3e04003a-7089-d86f-27be-c91332f78da5
---

# Add linked single sign-on to an application - Microsoft Entra ID | Microsoft Learn

This article shows you how to configure linked-based single sign-on (SSO) for your application in Microsoft Entra ID. Linked-based SSO enables Microsoft Entra ID to provide SSO to an application that is already configured for SSO in another service. The linked option lets you configure the target location when a user selects the application in your organization's My Apps or Microsoft 365 portal.

The term 'another service' refers to an external identity provider or service that has already configured SSO for the application. Microsoft Entra ID acts as a facilitator, linking users to the application without managing the sign-on process itself.

Linked-based SSO doesn't provide sign-on functionality through Microsoft Entra ID. The option simply sets the location that users are sent when they select the application on the My Apps or Microsoft 365 portal.

Some common scenarios where linked-based SSO is valuable include:

- Add a link to a custom web application that currently uses federation, such as Active Directory Federation Services (ADFS).
- Add deep links to specific web pages that you want to appear on your user's access pages.
- Add a link to an application that doesn't require authentication. The linked option doesn't provide sign-on functionality through Microsoft Entra credentials, but you can still use some of the other features of enterprise applications. For example, you can use audit logs and add a custom logo and application name.

## Prerequisites

To configure linked-based SSO in your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- One of the following roles: Cloud Application Administrator, Application Administrator, or owner of the service principal.
- An application that supports linked-based SSO.

## Configure linked-based single sign-on

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Search for and select the application that you want to add linked SSO.
4. Select **Single sign-on** and then select **Linked**.
5. Enter the URL for the sign-in page of the application.
6. Select **Save**.