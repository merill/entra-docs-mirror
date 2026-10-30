---
layout: Conceptual
title: University multilateral federation decision tree - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multilateral-federation-decision-tree
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Use this decision tree to help design a multilateral federation solution for universities.
ms.topic: concept-article
ms.date: 2023-04-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: adc374f6-417c-b3bd-0d69-f827451fcb9c
document_version_independent_id: 0f4c074c-be71-e146-2926-76ab9f5c6fdd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multilateral-federation-decision-tree.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multilateral-federation-decision-tree
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multilateral-federation-decision-tree.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 523e304f-5519-8ad3-9a65-87119bb1bde0
---

# University multilateral federation decision tree - Microsoft Entra | Microsoft Learn

Use this decision tree to determine the multilateral federation solution that's best suited for your environment.

[![Diagram that shows a decision matrix with key criteria to help choose between three solutions.](media/multilateral-federation-decision-tree/tradeoff-decision-matrix.png)](media/multilateral-federation-decision-tree/tradeoff-decision-matrix.png#lightbox)

## Migration resources

The following resources can help with your migration to the solutions covered in this content.

| Migration resource | Description | Relevant for migrating to... |
| --- | --- | --- |
| [Resources for migrating applications to Microsoft Entra ID](../identity/enterprise-apps/migration-resources) | List of resources to help you migrate application access and authentication to Microsoft Entra ID | Solution 1, Solution 2, and Solution 3 |
| [Microsoft Entra custom claims provider](../identity-platform/custom-claims-provider-overview) | Overview of the Microsoft Entra custom claims provider | Solution 1 |
| [Custom security attributes](../fundamentals/custom-security-attributes-manage) | Steps for managing access to custom security attributes | Solution 1 |
| [Microsoft Entra single sign-on (SSO) integration with Cirrus Bridge](../identity/saas-apps/cirrus-identity-bridge-for-azure-ad-tutorial) | Tutorial to integrate Cirrus Bridge with Microsoft Entra ID | Solution 1 |
| [Cirrus Bridge overview](https://blog.cirrusidentity.com/documentation/azure-bridge-setup-rev-6.0) | Cirrus Identity documentation for configuring Cirrus Bridge with Microsoft Entra ID | Solution 1 |
| [Configuring Shibboleth as a Security Assertion Markup Language (SAML) proxy](https://shibboleth.atlassian.net/wiki/spaces/KB/pages/1467056889/Using+SAML+Proxying+in+the+Shibboleth+IdP+to+connect+with+Azure+AD) | Shibboleth article that describes how to use the SAML proxying feature to connect the Shibboleth identity provider (IdP) to Microsoft Entra ID | Solution 2 |
| [Microsoft Entra multifactor authentication deployment considerations](../identity/authentication/howto-mfa-getstarted) | Guidance for configuring Microsoft Entra multifactor authentication | Solution 1 and Solution 2 |