---
layout: Conceptual
title: Customer data storage and processing for European customers in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/data-storage-eu
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about where Microsoft Entra ID stores identity-related data for its European customers.
ms.topic: concept-article
ms.date: 2026-04-27T00:00:00.0000000Z
ms.custom: it-pro, references-regions
ms.collection: M365-identity-device-management
locale: en-us
document_id: 0a2c8e98-6986-75fb-dc7e-6ea4a176c748
document_version_independent_id: bceb50c4-a803-1833-651a-a4ba3aff98e0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/data-storage-eu.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/data-storage-eu
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/data-storage-eu.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 952533f9-211b-15cd-a131-7b7ae09c888f
---

# Customer data storage and processing for European customers in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Microsoft Entra ID stores customer data in a geographic location based on how a tenant was created and provisioned. The following list provides information about how the location is defined:

- **Microsoft Entra admin center or Microsoft Entra API** - A customer selects a location from the predefined list.
- **Dynamics 365 and Power Platform** - A customer provisions their tenant in a predefined location.
- **EU Data Residency** - For customers who provided a location in Europe, Microsoft Entra ID stores most of the customer data in Europe, except where noted later in this article.
- **EU Data Boundary** - For customers who provided a location that is within the [EU Data Boundary](/en-us/privacy/eudb/eu-data-boundary-learn#eu-data-boundary-countries-and-datacenter-locations) (members of the EU and EFTA), Microsoft Entra ID stores and processes most of the customer data in the EU Data Boundary, except where noted later in this article.
- **Microsoft 365** - The location is based on a customer provided billing address.

The following sections provide information about customer data that doesn't meet the EU Data Residency or EU Data Boundary commitments.

## Services that will temporarily transfer a subset of customer data out of the EU Data Residency and EU Data Boundary

For some components of a service, work is in progress to be included in the EU Data Residency and EU Data Boundary, but completion of this work is delayed. The following sections in this article explain the customer data that these services currently transfer out of Europe as part of their service operations.

**EU Data Residency:**

- **Reason for customer data egress** - A few of the tenants are stored outside of the EU location due one of the following reasons:

    - The tenants were initially created with a country code that is NOT in Europe and later the tenant country code was changed to the one in Europe. The Microsoft Entra directory data location is decided during the tenant creation time and not changed when the country code for the tenant is updated. Starting March 2019, Microsoft has blocked updating the country code on a tenant to avoid such confusion.
    - There are 13 country codes (Countries include: Azerbaijan, Bahrain, Israel, Jordan, Kazakhstan, Kuwait, Lebanon, Oman, Pakistan, Qatar, Saudi Arabia, Türkiye, UAE) that were mapped to Asia region until 2013 and later mapped to Europe. Tenants that were created before July 2013 from this country code are provisioned in Asia instead of Europe.
    - There are seven country codes (Countries include: Armenia, Georgia, Iraq, Kyrgyzstan, Tajikistan, Turkmenistan, Uzbekistan) that were mapped to Asia region until 2017 and later mapped to Europe. Tenants that were created before February 2017 from this country code are provisioned in Asia instead of Europe.
- **Types of customer data being egressed** - User and device account data, and service configuration (application, policy, and group).
- **Customer data location at rest** - US and Asia/Pacific.
- **Customer data processing** - The same as the location at rest.
- **Services** - Directory Core Store

**EU Data Boundary:**

See more information on Microsoft Entra temporary partial customer data transfers from the EU Data Boundary [Services that temporarily transfer a subset of customer data out of the EU Data Boundary](/en-us/privacy/eudb/eu-data-boundary-temporary-partial-transfers#security-services).

## Services that will permanently transfer a subset of customer data out of the EU Data Residency and EU Data Boundary

Some components of a service will continue to transfer a limited amount of customer data out of the EU Data Residency and EU Data Boundary because this transfer is by design to facilitate the function of the services.

**EU Data Residency:**

[Microsoft Entra ID](what-is-entra): When an IP Address or phone number is determined to be used in fraudulent activities, they're published globally to block access from any workloads using them.

**EU Data Boundary:**

See more information on Microsoft Entra permanent partial customer data transfers from the EU Data Boundary [Services that will permanently transfer a subset of customer data out of the EU Data Boundary](/en-us/privacy/eudb/eu-data-boundary-permanent-partial-transfers#security-services).

## Other considerations

### Optional service capabilities that transfer data out of the EU Data Residency and EU Data Boundary

**EU Data Residency:**

Some services offer optional features. In some cases, you need a subscription to use them. As a customer administrator, you can choose to turn these features on or off for your service accounts. If made available and used by a customer's users, these capabilities will result in data transfers out of Europe as described in the following sections in this article.

- [Multitenant administration](../identity/multi-tenant-organizations/overview): An organization might choose to create a multitenant organization within Microsoft Entra ID. For example, a customer can invite users to their tenant in a B2B context. A customer can create a multitenant software as a service (SaaS) application that allows other third-party tenants to provision the application in the third-party tenant. A customer can link two or more tenants to work together as one in certain situations. These include forming a multitenant organization (MTO), syncing tenants, and sharing an email domain. Administrator configuration and use of multitenant collaboration might occur with tenants outside of the EU Data Residency and EU Data Boundary resulting in some customer data, such as user and device account data, usage data, and service configuration (application, policy, and group) being stored and processed in the location of the collaborating tenant.
- [Application Proxy](/en-us/entra/identity/app-proxy): Application proxy allows customers to access both cloud and on-premises applications through an external URL or an internal application portal. Customers might choose advanced routing configurations that would cause Customer Data to egress outside of the EU Data Residency and EU Data Boundary, including user account data, usage data, and application configuration data.

**EU Data Boundary:**

See more information on optional service capabilities that transfer customer data out of the EU Data Boundary [Optional service capabilities that transfer customer data out of the EU Data Boundary](/en-us/privacy/eudb/eu-data-boundary-transfers-for-optional-capabilities#microsoft-entra-id).

### Other EU Data Boundary online services

Services and applications that integrate with Microsoft Entra ID have access to customer data. Review how each service and application stores and processes customer data, and verify that they meet your company's data handling requirements.