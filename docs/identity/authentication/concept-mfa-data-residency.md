---
layout: Conceptual
title: Microsoft Entra multifactor authentication data residency - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-data-residency
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn what personal and organizational data Microsoft Entra multifactor authentication stores about you and your users and what data remains within the country/region of origin.
ms.topic: concept-article
ms.date: 2025-06-06T00:00:00.0000000Z
ms.reviewer: inbarc
ms.custom: references_regions
locale: en-us
document_id: ba59950e-72c3-be82-4338-523f7369db7f
document_version_independent_id: dd17834a-6530-7e52-b392-84456652d25e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-mfa-data-residency.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-mfa-data-residency
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-mfa-data-residency.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e0ab2b99-f6f0-7c9d-b366-f1fb86a27658
---

# Microsoft Entra multifactor authentication data residency - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID stores customer data in a geographical location based on the address an organization provides when subscribing to a Microsoft online service such as Microsoft 365 or Azure. For information on where your customer data is stored, see [Where your data is located](https://www.microsoft.com/trust-center/privacy/data-location) in the Microsoft Trust Center.

Microsoft Entra multifactor authentication processes and stores personal data and organizational data. This article outlines what and where data is stored.

The Microsoft Entra multifactor authentication service has datacenters in the United States, Europe, and Asia Pacific. The following activities originate from the regional datacenters except where noted:

- Multifactor authentication SMS and phone calls originate from datacenters in the customer's region and are routed by global providers. **These providers may route the SMS or phone call outside of the user and company location.** Phone calls using custom greetings always originate from data centers in the United States.
- General purpose user authentication requests from other regions are currently processed based on the user's location.
- Push notifications that use the Microsoft Authenticator app are currently processed in regional datacenters based on the user's location. Vendor-specific device services, such as Apple Push Notification Service or Google Firebase Cloud Messaging, might be outside the user's location.

## Personal data stored by Microsoft Entra multifactor authentication

Personal data is user-level information that's associated with a specific person. The following data stores contain personal information:

- Bypassed users
- Microsoft Authenticator device token change requests
- Multifactor authentication activity reports—store multifactor authentication activity from the multifactor authentication on-premises components NPS Extension and AD FS adapter.
- Microsoft Authenticator activations

This information is retained for 90 days.

Microsoft Entra multifactor authentication doesn't log personal data such as usernames, phone numbers, or IP addresses. However, *UserObjectId* identifies authentication attempts to users. Log data is stored for 30 days.

### Data stored by Microsoft Entra multifactor authentication

For Azure public clouds, excluding Azure AD B2C authentication, the NPS Extension, and the Windows Server 2016 or 2019 Active Directory Federation Services (AD FS) adapter, the following personal data is stored:

| Event type | Data store type |
| --- | --- |
| OATH token | Multifactor authentication logs |
| One-way SMS | Multifactor authentication logs |
| Voice call | Multifactor authentication logsMultifactor authentication activity report data store |
| Microsoft Authenticator notification | Multifactor authentication logsMultifactor authentication activity report data storeChange requests when the Microsoft Authenticator device token changes |

For Microsoft Azure Government, Microsoft Azure operated by 21Vianet, Azure AD B2C authentication, the NPS extension, and the Windows Server 2016 or 2019 AD FS adapter, the following personal data is stored:

| Event type | Data store type |
| --- | --- |
| OATH token | Multifactor authentication logsMultifactor authentication activity report data store |
| One-way SMS | Multifactor authentication logsMultifactor authentication activity report data store |
| Voice call | Multifactor authentication logsMultifactor authentication activity report data store |
| Microsoft Authenticator notification | Multifactor authentication logsMultifactor authentication activity report data storeChange requests when the Microsoft Authenticator device token changes |

## Organizational data stored by Microsoft Entra multifactor authentication

Organizational data is tenant-level information that can expose configuration or environment setup. Tenant settings from the multifactor authentication pages might store organizational data such as lockout thresholds or caller ID information for incoming phone authentication requests:

- Account lockout
- Notifications
- Phone call settings