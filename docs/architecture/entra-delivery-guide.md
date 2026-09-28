---
layout: Conceptual
title: Microsoft Entra Suite workshop delivery guide - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/entra-delivery-guide
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: This article is for use by the delivery expert that plans on delivering the Microsoft Entra Suite Workshop to customers. It aims to provide delivery experts with a comprehensive overview of the tasks that is required to successfully deliver the Microsoft Entra Suite Workshop to customers. It's structured chronologically following the standard and typical flow of a workshop delivery. It outlines how to use the Microsoft Entra Suite Workshop to deploy all the components of the suite. It gives organizations and IT admins a detailed plan to design and deploy Microsoft Entra ID Governance, Microsoft Entra Private Access, Microsoft Entra Internet Access, and Microsoft Entra Verified ID.
ms.date: 2025-08-01T00:00:00.0000000Z
ms.topic: concept-article
ms.reviewer: martinco
ms.subservice: architecture
locale: en-us
document_id: 743b4f55-af1b-d081-7f17-e37eaf480fb9
document_version_independent_id: 743b4f55-af1b-d081-7f17-e37eaf480fb9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/entra-delivery-guide.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/entra-delivery-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/entra-delivery-guide.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 628e29be-c18b-5152-80c7-f6bb58f03ee1
---

# Microsoft Entra Suite workshop delivery guide - Microsoft Entra | Microsoft Learn

## Overview

The [Microsoft Entra Suite workshop](https://aka.ms/EntraSuiteWorkshopdoc) helps customers to develop an actionable and orderly strategy for implementing the Microsoft Entra Suite. The workshop consists of five stages to help streamline all products and features in the suite. The first two stages are required to establish the correct foundation for deploying the products in the suite and should be completed before moving to the last three stages of the workshop. The following stages are available in the workshop:

- Establish a baseline
- Getting started
- Onboard your workforce
- Enable Remote Access
- Govern Internet Access

Customers can choose to deploy all the stages or just a subset of them depending on their priorities and resource availability. While the workshops are modular, customers are encouraged to start with Onboarding your workforce.

## Target customer

The ideal customer for this engagement:

- Understands and aligns to the Microsoft Identity security vision.
- Has the intent and resources to invest in projects to deploy Microsoft Security products

## Alignment with Microsoft recommendations

The content of the Microsoft Entra Suite Workshop will be updated when the Zero Trust Workshop gets updated, most recommendations are aligned with the Zero Trust Security Deployment Guidance:

- [Zero Trust Guidance Center](/en-us/security/zero-trust)
- [Zero Trust deployment for technology pillars overview](/en-us/security/zero-trust/deploy/overview)

## Customer stakeholders

In order to get the most out of these workshops, it's recommended to have people on the call from the customer’s side that can cover the following areas:

- Identity and Access Management (IAM)
- Security (Governance/CERT/SOC)
- Devices/Endpoint
- App Dev
- Networking

Recommendations for the customer stakeholders that should attend the workshop are as follows:

- Identity and Access Management (IAM) team
- Network Operations team
- Security Operations team
- Devices/Endpoint team
- ID Governance (IGA) team
- Enterprise Application Developers
- Applications / workloads stakeholders
- CISO (if possible)
- IT Director (if possible)

## Engagement model

| Phases | Key Objectives | Key Activities | Success Criteria |
| --- | --- | --- | --- |
| **Initial Scoping call with Customer Duration: 30 minutes** | • Arrange that the customer understands the technical review activity and ensure scope, objectives, format, and deliverables  • Confirm logistics and attendees  • Decide which of the stages the customer would like delivered | • Gather customer context and validate intent and readiness for Microsoft Entra Suite  • Conduct scoping meeting  • Agree on the assessment logistics and schedule time to deliver individual stages of the workshop  • Ensure customer understands prerequisites to run the assessment checks  • Validate required customer technical and operational stakeholders  • Validate that the customer understands their current Microsoft licensing arrangements for relevant services | • All required stakeholders understand the workshop engagement  • Logistics for the review are finalized  • Delivery Expert identified a way to share files with customer |
| **Roadmap Mapping Duration: 6 hours** | • Customer has a tailored adoption roadmap to implement the Microsoft Entra Suite | • Delivery expert leads working sessions to walk through the baseline adoption roadmap identified by Microsoft and fills it out based on customer requirements and constraints | • Customer has a customized deployment path with concrete deployment steps and decisions to make |
| **Closeout Duration: 1 hour** | • Gather customer feedback about the workshop  • Identify other stages to deliver | • Customer fills out [feedback survey](https://aka.ms/EntraSuiteWorkshop/feedback) | • Workshop feedback survey is completed |

During the roadmap mapping phase, each recommendation will include information on the implementation effort required and the impact on users.

The definitions for implementation effort are as follows:

- **High**: Customer IT and Security Operations teams must implement programs that require continuous time or resource investment.
- **Medium**: Customer IT and Security Operations teams need to drive projects.
- **Low**: Customer IT and Security Operations teams need to carry out specific tasks.

User impact levels are defined as:

- **High**: A large number of nonprivileged users need to take action or be informed of changes.
- **Medium**: A portion of nonprivileged users must take action or be informed of changes.
- **Low**: Actions can be performed by administrators, and users don't need to be notified.

## Workshop delivery time estimates

Below are the estimated delivery times for each section of the stage of the workshop:

- Establish a baseline: 1.5 hours
- Getting started: 1.5 hours
- Onboard your workforce: 1 hour
- Enable Remote Access: 1 hour
- Govern Internet Access: 1 hour **Total: 6 hours**

## Expected outcome

Upon completing this workshop, customers will:

- Gain a comprehensive understanding of the various scenarios supported by the Microsoft Entra Suite.
- Develop a clear overview of their organization's setup.
- Be well-equipped and ready to begin the planning process for deployment.