---
layout: Conceptual
title: Determine your security posture for external access with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/1-secure-access-posture
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn about governance of external access and assessing collaboration needs, by scenario
ms.topic: how-to
ms.date: 2023-02-23T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: d664eb96-50ac-e5d4-6af7-73a956a241bd
document_version_independent_id: efcfe07c-7d8e-8fdf-f025-470c9767c1c8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/1-secure-access-posture.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/1-secure-access-posture
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/1-secure-access-posture.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 15ecb3fe-0566-84dd-7aa4-ba0fa16dba11
---

# Determine your security posture for external access with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

As you consider the governance of external access, assess your organization's security and collaboration needs, by scenario. You can start with the level of control the IT team has over the day-to-day collaboration of end users. Organizations in highly regulated industries might require more IT team control. For example, defense contractors can have a requirement to positively identify and document external users, their access, and access removal: all access, scenario-based, or workloads. Consulting agencies can use certain features to allow end users to determine the external users they collaborate with.

![Bar graph of the span from full IT team control, to end-user self service.](media/secure-external-access/1-overall-control.png)

Note

A high degree of control over collaboration can lead to higher IT budgets, reduced productivity, and delayed business outcomes. When official collaboration channels are perceived as onerous, end users tend to evade official channels. An example is end users sending unsecured documents by email.

## Before you begin

This article is number 1 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Scenario-based planning

IT teams can delegate partner access to empower employees to collaborate with partners. This delegation can occur while maintaining sufficient security to protect intellectual property.

Compile and assess your organizations scenarios to help assess employee versus business partner access to resources. Financial institutions might have compliance standards that restrict employee access to resources such as account information. Conversely, the same institutions can enable delegated partner access for projects such as marketing campaigns.

![Diagram of a balance of IT team governed access to partner self-service.](media/secure-external-access/1-scenarios.png)

### Scenario considerations

Use the following list to help measure the level of access control.

- Information sensitivity, and associated risk of its exposure
- Partner access to information about other end users
- The cost of a breach versus the overhead of centralized control and end-user friction

Organizations can start with highly managed controls to meet compliance targets, and then delegate some control to end users, over time. There can be simultaneous access-management models in an organization.

Note

Partner-managed credentials are a method to signal the termination of access to resources, when an external user loses access to resources in their own company. Learn more: [B2B collaboration overview](../external-id/what-is-b2b)

## External-access security goals

The goals of IT-governed and delegated access differ. The primary goals of IT-governed access are:

- Meet governance, regulatory, and compliance (GRC) targets
- High level of control over partner access to information about end users, groups, and other partners

The primary goals of delegating access are:

- Enable business owners to determine collaboration partners, with security constraints
- Enable partners to request access, based on rules defined by business owners

### Common goals

#### Control access to applications, data, and content

Levels of control can be accomplished through various methods, depending on your version of Microsoft Entra ID and Microsoft 365.

- [Microsoft Entra ID plans and pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing)
- [Compare Microsoft 365 Enterprise pricing](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans)

#### Reduce attack surface

- [What is Microsoft Entra Privileged Identity Management?](../id-governance/privileged-identity-management/pim-configure) - manage, control, and monitor access to resources in Microsoft Entra ID, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune
- [Data loss prevention in Exchange Server](/en-us/exchange/policy-and-compliance/data-loss-prevention/data-loss-prevention?view=exchserver-2019&amp;preserve-view=true)

#### Confirm compliance with activity and audit log reviews

IT teams can delegate access decisions to business owners through entitlement management, while access reviews help confirm continued access. You can use automated data classification with sensitivity labels to automate the encryption of sensitive content, easing compliance for end users.