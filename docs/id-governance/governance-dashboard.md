---
layout: Conceptual
title: Identity Governance dashboard - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/governance-dashboard
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article shows how to use the new identity governance dashboard
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 8710bfe3-5a0c-227e-9395-1c866fff5b63
document_version_independent_id: 75e59ca0-8484-8d9a-cc1e-94455cd8cd02
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/governance-dashboard.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/governance-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/governance-dashboard.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bd2c9554-e720-57f9-ea0e-c1a4989ef696
---

# Identity Governance dashboard - Microsoft Entra ID Governance | Microsoft Learn

In this article, we provide guidance on how to use the Microsoft Identity Governance dashboard.

## About the dashboard

Microsoft Identity Governance dashboard discovers usage information about various Identity Governance & Administration (IGA) features configured in your tenant. It then gives you at-a-glance view of your current state of Identity Governance, with actionable buttons and quickly accessible links to feature documentation.

## Using the dashboard

We understand that implementing Identity Governance is a journey, and you may be in different stages of this journey.

- If you are just getting started, use the dashboard to assess the complexity of your IT landscape. Identify the number of users and guests in your tenant. Discover business apps and privileged roles in your tenant and review capabilities provided by Microsoft Identity Governance to put together an implementation plan that addresses your security & compliance needs.
- If you have already deployed certain governance capabilities, use the dashboard to understand the coverage of your governance automations and find implementation gaps. For example, maybe you have automated birthright access using [entitlement management](https://go.microsoft.com/fwlink/?linkid=2210375), but you have not set up periodic [access reviews](https://go.microsoft.com/fwlink/?linkid=2211313). Use the call-to-action links in the dashboard to further improve your identity governance posture.

## Data displayed on the dashboard

You can access the dashboard by logging into the Microsoft Entra admin center and selecting the "Dashboard" blade under "Identity Governance". The dashboard experience is made up of the following main components:

- **Glanceable cards**: These cards provide high level insights into what’s happening in your tenant from the perspective of workforce users, guest users, privileged identities, and application access governance. The navigation links in the glanceable cards point to Identity Governance quick start guides and tutorials.
- **Identity Governance status**: This visual shows your identity landscape in terms of number of employees, guests, business apps, groups, and privileged roles. It then highlights the various Microsoft Identity Governance feature sets configured to better govern these entities. If a feature is not configured, you can use the "Configure Now" option to open the configuration landing blade for that feature.
- **Tutorials**: This section contains tutorials of popular Identity governance use cases for quick access.
- **Highlights**: Use the content in this section to stay informed about the latest Identity Governance features and learn how customers are using Identity Governance to improve their security and compliance posture.

Note

The Graph APIs on the dashboard will operate in the context of the logged in user using delegated permission model. To view the dashboard with full fidelity, we recommend at minimum using the Global Reader role.

## Troubleshooting dashboard errors

You may see two types of errors on the dashboard:

- **Service error**: This error indicates that the dashboard was unable to retrieve data due to a backend service error. The service error could be intermittent. Try refreshing the dashboard to see if the issue resolves automatically. If the issue persists, contact Microsoft support.
- **Permission error**: This error indicates that the dashboard was unable to retrieve data either due to insufficient permissions or data access issues or license issues. Check the role assigned to the logged in user and ensure your tenant has the right license. To view the dashboard with full fidelity, at a minimum we recommend assigning the Global reader role.