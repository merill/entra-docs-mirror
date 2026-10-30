---
layout: Conceptual
title: Understanding telephony fraud risk for Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-telephony-fraud
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Understanding International Revenue Share Fraud (IRSF) is crucial for implementing preventive measures for Microsoft Entra multifactor authentication telephony verification.
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: aloom3
ms.custom: references_regions
locale: en-us
document_id: c6b8272b-ad70-460b-3dff-f1a263cfedcb
document_version_independent_id: d965389e-1889-ea6c-5339-2a94d8b2ff2a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-mfa-telephony-fraud.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-mfa-telephony-fraud
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-mfa-telephony-fraud.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d4bcf245-955e-af25-82d0-e96b82992219
---

# Understanding telephony fraud risk for Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn

In today's digital landscape, telecommunication services seamlessly integrate into our daily lives. But technological progress also brings the risk of fraudulent activities like International Revenue Share Fraud (IRSF), which poses financial consequences and service disruptions. IRSF involves exploiting telecommunication billing systems by unauthorized actors. They divert telephony traffic and generate profits through a technique called *traffic pumping*. Traffic pumping targets multifactor authentication systems, and causes inflated charges, service unreliability, and system errors.

To counter this risk, a thorough understanding of IRSF is crucial for implementing preventive measures like regional restrictions and phone number verification, while our system aims to minimize disruptions and safeguard both our business, users, and your business we prioritize your security and as such we may sometimes take proactive measures.

## How we help fight telephony fraud

To protect our customers and vigilantly defend against bad actors who attempt fraud, we may engage in proactive remediation in the event of a fraud attack. Telephony fraud is a very dynamic space where even seconds can result in massive financial impact. To limit that impact, we may proactively engage temporary throttling when we detect excessive authentication requests from a particular region, phone, or user. These throttles normally clear after a few hours to a few days.

## How you can help fight telephony fraud

To help fight telephony fraud, B2C customers can take steps to improve security of authentication activities such as sign-in, MFA, password reset, and forgot username:

- Use the recommended versions of user flows
- Remove region codes that aren't relevant to your organization
- Use CAPTCHA to help distinguish between human users and automated bots
- Review your telecom usage to make sure it matches the expected behavior from your users

For more information, see [Securing phone-based MFA in B2C](/en-us/azure/active-directory-b2c/phone-based-mfa).

In addition, you may sometimes encounter throttles because you're requesting traffic from a region that requires an opt-in. For more information, see [Regions that need to opt in for MFA telephony verification](concept-mfa-regional-opt-in).

For Microsoft Entra External ID, the default SMS verification for external tenants is disabled. To enable telephony traffic for a specific country code in your application, see [Regional opt-in for MFA telephony verification with external tenants](/en-us/entra/external-id/customers/how-to-region-code-opt-in).