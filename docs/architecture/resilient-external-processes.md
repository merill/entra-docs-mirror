---
layout: Conceptual
title: Resilient interfaces with external processes using Azure AD B2C - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilient-external-processes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn about methods to build resilient interfaces with external processes.
ms.topic: how-to
ms.reviewer: gasinh
ms.date: 2025-05-20T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 461ed092-f970-d5b7-6726-bc325edaa0b3
document_version_independent_id: e00cfba8-6f4c-96bf-afc7-b1f3afd15d93
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilient-external-processes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilient-external-processes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilient-external-processes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3badd7de-47f5-053c-0a76-fa374e49b993
---

# Resilient interfaces with external processes using Azure AD B2C - Microsoft Entra | Microsoft Learn

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

In this article, find guidance on how to plan for and implement the RESTful APIs to make your application more resilient to API failures.

## Ensure correct API placement

Use identity experience framework (IEF) policies to call an external system using a [RESTful API technical profile](/en-us/azure/active-directory-b2c/restful-technical-profile). The IEF runtime environment doesn't control external systems, which is a potential failure point.

### Manage external systems using APIs

While calling an interface to access certain data, confirm the data drives the authentication decision. Assess whether the information is essential to the functionality of the application. For example, an e-commerce vs. a secondary functionality such as an administration. If the information isn't needed for authentication, consider moving the call to the application logic.

If the data for authentication is relatively static and small, and shouldn't be externalized, put it in the directory.

When possible, remove API calls from the preauthenticated path. If you can't, then enable protections for Denial of Service (DoS) and Distributed Denial of Service (DDoS) attacks for APIs. Attackers can load the sign-in page and try to flood your API with DoS attacks to disable your application. For example, use Completely Automated Public Turing Test To Tell Computers and Humans Apart (CAPTCHA) in your sign in and sign up flow.

Use [API connectors of sign-up user flows](/en-us/azure/active-directory-b2c/api-connectors-overview) to integrate with web APIs after federating with an identity provider, during sign-up, or before you create the user. Because user flows are tested, you don't have to perform user flow-level functional, performance, or scale testing. Test your applications for functionality, performance, and scale.

Azure AD B2C RESTful API [technical profiles](/en-us/azure/active-directory-b2c/restful-technical-profile) don't provide any caching behavior. Instead, RESTful API profile implements a retry logic and a timeout built into the policy.

For APIs that need to write data, use a task to have these actions executed by a background worker. Use services like [Azure queues](/en-us/azure/storage/queues/storage-queues-introduction). This practice makes the API return efficiently and increases the policy execution performance.

## API errors

Because the APIs live outside the Azure AD B2C system, enable error handling in the technical profile. Ensure users are informed and the application can deal with failure gracefully.

### Handle API errors

Because APIs fail for various reasons, make your application resilient. [Return an HTTP 4XX error message](/en-us/azure/active-directory-b2c/restful-technical-profile#returning-validation-error-message) if the API is unable to complete the request. In the Azure AD B2C policy, try to handle the unavailability of the API and perhaps render a reduced experience.

[Handle transient errors gracefully](/en-us/azure/active-directory-b2c/restful-technical-profile#error-handling). Use the RESTful API profile to configure error messages for various [circuit breakers](/en-us/azure/architecture/patterns/circuit-breaker).

Monitor and use continuous integration and continuous delivery (CICD). Rotate the API access credentials such as passwords and certificates used by the [technical profile engine](/en-us/azure/active-directory-b2c/restful-technical-profile).

## API management best practices

While you deploy the REST APIs and configure the RESTful technical profile, use the following best practices to avoid common errors.

### API Management

API Management (APIM) publishes, manages, and analyzes APIs. APIM handles authentication for secure access to back-end services and microservices. Use an API gateway to scale out API deployments, caching, and load balancing.

Our recommendation is to get the right token, instead of calling multiple times for each API and [secure an Azure APIM API](/en-us/azure/active-directory-b2c/secure-api-management?tabs=app-reg-ga).