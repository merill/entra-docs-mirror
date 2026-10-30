---
layout: Conceptual
title: 'Quickstart: Add an enterprise application - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn to add pre-integrated apps to your Microsoft Entra tenant with clear, step-by-step instructions.
ms.topic: quickstart
ms.date: 2025-03-31T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: mode-other, enterprise-apps
locale: en-us
document_id: 74f69861-fd51-b4f0-e31e-fbe7b85c228d
document_version_independent_id: 121a0f4b-811a-ed2f-bb9d-e69e4fa22bcd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/add-application-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/add-application-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/add-application-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ca732fd6-29df-96ea-23a4-441fc0b148ba
---

# Quickstart: Add an enterprise application - Microsoft Entra ID | Microsoft Learn

In this quickstart, you use the Microsoft Entra admin center to add an enterprise application to your Microsoft Entra tenant. Microsoft Entra ID has a gallery that contains thousands of enterprise applications that are already preintegrated. Many of the applications your organization uses are probably already in the gallery. This quickstart uses the application named **Microsoft Entra SAML Toolkit** as an example, but the concepts apply for most [enterprise applications in the gallery](../saas-apps/tutorial-list).

We recommend that you use a nonproduction environment to test the steps in this quickstart.

## Prerequisites

To add an enterprise application to your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, or Application Administrator.

## Add an enterprise application

To add an enterprise application to your tenant:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select **New application**.
4. The **Browse Microsoft Entra Gallery** pane opens and displays tiles for cloud platforms, on-premises applications, and featured applications. Applications listed in the **Featured applications** section have icons indicating whether they support federated single sign-on (SSO) and provisioning. Search for and select the application. In this quickstart, **Microsoft Entra SAML Toolkit** is being used.

    [![Browse in the enterprise application gallery for the application that you want to add.](media/add-application-portal/browse-gallery.png)](media/add-application-portal/browse-gallery.png#lightbox)
5. Enter a name that you want to use to recognize the instance of the application. For example, `Microsoft Entra SAML Toolkit 1`.
6. Select **Create**, you're taken to the application that you registered.
7. You should [assign owners to the application](/en-us/entra/identity/enterprise-apps/assign-app-owners#assign-an-owner) as a best practice at this point.

If you choose to install an application that uses OpenID Connect based SSO, instead of seeing a **Create** button, you see a button that redirects you to the application sign-in or sign-up page depending on whether you already have an account there. For more information, see [Add an OpenID Connect based single sign-on application](add-application-portal-setup-oidc-sso). After sign-in, the application is added to your tenant.

## Clean up resources

If you're planning to complete the next quickstart, keep the enterprise application that you created. Otherwise, you can consider deleting it to clean up your tenant. For more information, see [Delete an application](delete-application-portal).

## Microsoft Graph API

To add an application from the Microsoft Entra gallery programmatically, use the [applicationTemplate: instantiate](/en-us/graph/api/applicationtemplate-instantiate) API in Microsoft Graph.