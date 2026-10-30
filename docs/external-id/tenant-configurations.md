---
layout: Conceptual
title: Tenant Configurations - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/tenant-configurations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about tenant configurations in Microsoft Entra External ID, including the differences between workforce and external tenants.
ms.topic: concept-article
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 5650ba1b-db39-8515-468e-9378c7c974f5
document_version_independent_id: 5650ba1b-db39-8515-468e-9378c7c974f5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/tenant-configurations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/tenant-configurations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/tenant-configurations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a734721d-cffb-a463-fe0e-f27f06d3bd0d
---

# Tenant Configurations - Microsoft Entra External ID | Microsoft Learn

A *tenant* is a dedicated and trusted instance of Microsoft Entra ID. It contains an organization's resources, including registered apps and a directory of users. There are two ways to configure a tenant, depending on how your organization intends to use the tenant and the resources that you want to manage:

- A *workforce* tenant configuration is for your employees, internal business apps, and other organizational resources. You can invite external business partners and guests to your workforce tenant.
- An *external* tenant configuration is exclusively for Microsoft Entra External ID scenarios where you want to publish apps to consumers or business customers. [Learn more about External ID in external tenants](customers/overview-customers-ciam).

Each tenant configuration represents a different scenario for working with users outside your organization.

[![Diagram that shows External ID tenant configurations.](media/tenant-configurations/tenant-configurations.png)](media/tenant-configurations/tenant-configurations.png#lightbox)

## Workforce tenants

A workforce tenant represents a single organization. You use it to manage your employees, business apps, and other internal resources. If you've worked with Microsoft Entra ID, you're already familiar with a workforce tenant. It's the standard tenant that's automatically created when your organization signs up for a Microsoft cloud service subscription, such as Microsoft Azure, Microsoft Intune, or Microsoft 365.

In a workforce tenant, the External ID feature [B2B collaboration](what-is-b2b) lets your employees collaborate with external business partners and guests.

You can create additional workforce tenants in either the Microsoft Entra admin center or the Azure portal.

## External tenants

When you want to use External ID to add customer identity and access management (CIAM) to your apps, you create a new tenant in an *external* configuration. This tenant is distinct and separate from your workforce tenant. It follows the standard Microsoft Entra tenant model, but it's configured for your consumer and business customer scenarios.

The external tenant is where you register your apps, create sign-up and sign-in user flows, and manage the users of your apps. The consumers and business customers who sign up for your apps are added to the tenant directory, but with [limited default permissions](customers/reference-user-permissions).

### When do I need to create an external tenant?

If you plan to use External ID for apps for consumers or business customers, the first resource that you need to create is a new tenant with an external configuration.

You can create an external tenant in a couple of ways:

- If you already have an Azure subscription, you can [create a new tenant](customers/how-to-create-customer-tenant-portal) in the Microsoft Entra admin center. When you create a tenant, choose the external configuration. You can't create external tenants via the Azure portal, which supports creation of workforce tenants only.
- If you don't already have a Microsoft Entra tenant and you want to try out External ID features in an external tenant, we recommend using the get-started experience to start a free trial.

When you create a tenant, you can set your correct geographic location and domain name. If you currently use Azure Active Directory B2C (Azure AD B2C), the new workforce and customer tenant model doesn't affect your existing Azure AD B2C tenants.

Important

Effective May 1, 2025, Azure AD B2C will no longer be available to purchase for new customers. To learn more, please see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

## Comparison of workforce and external tenants

Although workforce tenants and external tenants are built on the same underlying Microsoft Entra platform, there are some feature differences. For a detailed comparison of tenant features and capabilities, see [Supported features in workforce and external tenants](customers/concept-supported-features-customers).