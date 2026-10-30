---
layout: Conceptual
title: Add an enterprise application - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-add-enterprise-application
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add enterprise applications to your Microsoft Entra external tenant using the admin center. Discover gallery apps, configuration steps, and deployment tips.
ms.topic: how-to
ms.date: 2025-07-17T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: e7d79c0b-8c7b-e2b5-f24a-d95a42513f4d
document_version_independent_id: e7d79c0b-8c7b-e2b5-f24a-d95a42513f4d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-add-enterprise-application.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-add-enterprise-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-add-enterprise-application.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 96c3a348-5dc3-e57c-79ec-b7d4a665798d
---

# Add an enterprise application - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Enterprise applications are software-as-a-service (SaaS) apps that are pre-integrated with Microsoft Entra ID. These apps support access management and single sign-on (SSO). You can find these apps in the Microsoft Entra application gallery, which includes a wide range of pre-integrated SaaS applications. This article uses the application named **Microsoft Entra SAML Toolkit** as an example, but the concepts apply for most [enterprise applications in the gallery](/en-us/entra/identity/saas-apps/tutorial-list).

## Prerequisites

To add an enterprise application to your external tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator).

## Add an enterprise application

To add an enterprise application to your Microsoft Entra external tenant, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select **New application** &gt; **Create your own application**.
4. Start typing the name of the application you want to add. If the application is already in the gallery, it appears in the list. In this article we use **Microsoft Entra SAML Toolkit** as an example.

    ![Screenshot showing how to add an enterprise application in the external tenant.](media/how-to-add-enterprise-application/add-enterprise-app.png)
5. Select the application from the list, and then select **Create**.
6. Select **Create**, you're taken to the application that you registered.
7. You should [assign owners to the application](/en-us/entra/identity/enterprise-apps/assign-app-owners?pivots=portal#assign-an-owner) as a best practice at this point.

## Clean up resources

You can keep the application in your tenant for future use, or you can [delete it](/en-us/entra/identity/enterprise-apps/delete-application-portal?pivots=portal) if you no longer need it. If you delete the application, all associated user assignments and configurations are also deleted.