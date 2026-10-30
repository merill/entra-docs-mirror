---
layout: Conceptual
title: Memo 22-09 identity requirements overview - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/memo-22-09-meet-identity-requirements
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Get guidance on meeting requirements outlined in US government OMB memorandum 22-09.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2025-02-10T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: d0351f8c-045f-f948-c728-eed44c5a3da0
document_version_independent_id: 8d03fa12-3632-95b9-bd48-700c200180fb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/memo-22-09-meet-identity-requirements.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/memo-22-09-meet-identity-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/memo-22-09-meet-identity-requirements.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6b8a408f-40b4-ace8-bc38-287d9d627cfa
---

# Memo 22-09 identity requirements overview - Microsoft Entra | Microsoft Learn

The Executive Order on Improving the Nation’s Cybersecurity (14028), directs federal agencies to advance security measures that significantly reduce the risk of successful cyberattacks against federal government digital infrastructure. On January 26, 2022, in support of Executive Order (EO) 14028, the Office of Management and Budget (OMB) released the federal Zero Trust strategy in [M 22-09 Memorandum for Heads of Executive Departments and Agencies](https://bidenwhitehouse.archives.gov/wp-content/uploads/2022/01/M-22-09.pdf).

This article series has guidance to employ Microsoft Entra ID as a centralized identity management system when implementing Zero Trust principles, as described in Memo 22-09.

Memo 22-09 supports Zero Trust initiatives in federal agencies. It has regulatory guidance for federal cybersecurity and data privacy laws. The memo cites the [US Department of Defense (DoD) Zero Trust Reference Architecture](https://cloudsecurityalliance.org/artifacts/dod-zero-trust-reference-architecture/):

"*The foundational tenet of the Zero Trust Model is that no actor, system, network, or service operating outside or within the security perimeter is trusted. Instead, we must verify anything and everything attempting to establish access. It's a dramatic paradigm shift in philosophy of how we secure our infrastructure, networks, and data, from verify once at the perimeter to continual verification of each user, device, application, and transaction.*"

The memo identifies five core goals for federal agencies to reach, organized with the Cybersecurity Information Systems Architecture (CISA) Maturity Model. The CISA Zero Trust model describes five complementary areas of effort, or pillars:

- Identity
- Devices
- Networks
- Applications and workloads
- Data

The pillars intersect with:

- Visibility
- Analytics
- Automation
- Orchestration
- Governance

## Scope of guidance

Use the article series to build a plan to meet memo requirements. It assumes use of Microsoft 365 products and a Microsoft Entra tenant.

Learn more: [Quickstart: Create a new tenant in Microsoft Entra ID](../fundamentals/create-new-tenant).

The article series instructions encompass agency investments in Microsoft technologies that align with the memo's identity-related actions.

- For agency users, agencies employ centralized identity management systems that can be integrated with applications and common platforms
- Agencies use enterprise-wide, strong multifactor authentication (MFA)
    - MFA is enforced at the application layer, not the network layer
    - For agency staff, contractors, and partners, phishing-resistant MFA is required
    - For public users, phishing-resistant MFA is an option
    - Password policies don't require special characters or regular rotation
- When agencies authorize user access to resources, they consider at least one device-level signal, with identity information about the authenticated user