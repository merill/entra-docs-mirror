---
layout: Conceptual
title: University multilateral federation solution design - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multilateral-federation-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn how to design a multilateral federation solution for universities.
ms.topic: concept-article
ms.date: 2023-04-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: d240063a-2c38-10cf-b40e-063e8c6344a4
document_version_independent_id: 62794ce7-97ab-e051-921f-32b24aae50f2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multilateral-federation-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multilateral-federation-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multilateral-federation-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
platformId: c0627a82-ebb4-ebdb-66ae-ec619bcb0aa9
---

# University multilateral federation solution design - Microsoft Entra | Microsoft Learn

Research universities need to collaborate with one another. To accomplish collaboration, they require multilateral federation to enable authentication and access between universities globally.

## Challenges with multilateral federation solutions

Universities face many challenges. For example, a university might use one identity management system and a set of protocols. Other universities might use a different set of technologies, depending on their requirements. In general, universities can:

- Use different identity management systems.
- Use different protocols.
- Use customized solutions.
- Need support for a long history of legacy functionality.
- Need support for solutions that are built in different IT generations.

Many universities are also adopting the Microsoft 365 suite of productivity and collaboration tools. These tools rely on Microsoft Entra ID for identity management, which enables universities to configure:

- Single sign-on across multiple applications.
- Modern security controls, including passwordless authentication, multifactor authentication, and risk-based Conditional Access policies.
- Enhanced reporting and monitoring.

Because Microsoft Entra ID doesn't natively support multilateral federation, this content describes three solutions for federating authentication and access between universities with a typical research university architecture. These scenarios mention non-Microsoft products for illustrative purposes only and to represent the broader class of products. For example, this content uses Shibboleth as an example of a federation provider.