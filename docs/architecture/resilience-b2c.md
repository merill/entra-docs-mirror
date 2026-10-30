---
layout: Conceptual
title: Build resilience in customer identity and access management with Azure AD B2C - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-b2c
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn methods to build resilience in customer identity and access management (CIAM) using Azure AD B2C.
ms.topic: how-to
ms.reviewer: gasinh
ms.date: 2025-05-20T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 2df4438d-1eba-51ec-30ed-8464acfe6971
document_version_independent_id: 8867a5a7-f78b-8eb7-f7e9-a4c4fb0709c7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-b2c.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-b2c
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-b2c.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 44e3408f-bf4a-f899-34cb-0b772b6fa7be
---

# Build resilience in customer identity and access management with Azure AD B2C - Microsoft Entra | Microsoft Learn

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

[Azure AD B2C](/en-us/azure/active-directory-b2c/overview) is a customer identity and access management (CIAM) platform that is designed to help you launch your critical customer facing applications. We have built-in features for [resilience](https://azure.microsoft.com/blog/advancing-azure-active-directory-availability/) to help our service scale to your needs and improve resilience in the face of potential outage situations. In addition, when launching a mission critical application, it's important to consider various design and configuration elements in your application. Consider how the application is configured in Azure AD B2C to ensure you see resilient behavior in response to outage or failure scenarios. In this article, we discuss some of the best practices to help you increase resilience.

A resilient service continues to function despite disruptions. To improve resilience:

- Understand all the components
- Eliminate single points of failures
- Limit effects by isolating failing components
- Provide redundancy with fast failover mechanisms and recovery paths

As you develop your application, we recommend you consider how to [increase resilience of authentication and authorization in your applications](resilience-app-development-overview) with the identity components of your solution. This article attempts to address enhancements for resilience for Azure AD B2C applications. We group our recommendations by CIAM functions.

In the subsequent sections, we guide you to build resilience in the following areas:

- [End-user experience](resilient-end-user-experience): Enable a fallback plan for your authentication flow and mitigate the potential impact from a disruption of Azure AD B2C authentication service.
- [Interfaces with external processes](resilient-external-processes): Build resilience in your applications and interfaces by recovering from errors.
- [Developer best practices](resilience-b2c-developer-best-practices): Avoid fragility because of common custom policy issues and improve error handling in the areas like interactions with claims verifiers, third-party applications, and REST APIs.
- [Monitoring and analytics](resilience-with-monitoring-alerting): Assess the health of your service by monitoring key indicators and detect failures and performance disruptions through alerting.
- [Build resilience in authentication infrastructure](resilience-in-infrastructure): Understand, contain, and mitigate the risk of disrupted authentication or authorization for resources.
- [Increase resilience of authentication and authorization in applications](resilience-app-development-overview): Use Microsoft identity platform to build apps your users and customers sign in to with Microsoft identities or social accounts.

Watch the following video to [build resilient and scalable flows](https://www.youtube.com/embed/8f_Ozpw9yTs). Learn how to design and configure resilient and scalable services using Azure AD B2C.