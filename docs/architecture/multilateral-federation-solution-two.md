---
layout: Conceptual
title: 'Solution 2: Microsoft Entra ID with Shibboleth as a SAML proxy - Microsoft Entra | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multilateral-federation-solution-two
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: This article describes design considerations for using Microsoft Entra ID with Shibboleth as a SAML proxy as a multilateral federation solution for universities.
ms.topic: concept-article
ms.date: 2023-04-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 03af7943-16b7-c4c3-16bf-38df17a37ee9
document_version_independent_id: d18c12c8-a28b-c2a0-6be1-12f73d1ab86b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multilateral-federation-solution-two.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multilateral-federation-solution-two
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multilateral-federation-solution-two.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b1ae8ff3-fce3-ff86-9c3c-19538251c29b
---

# Solution 2: Microsoft Entra ID with Shibboleth as a SAML proxy - Microsoft Entra | Microsoft Learn

In Solution 2, Microsoft Entra ID acts as the primary identity provider (IdP). The federation provider acts as a Security Assertion Markup Language (SAML) proxy to the Central Authentication Service (CAS) apps and the multilateral federation apps. In this example, [Shibboleth acts as the SAML proxy](https://shibboleth.atlassian.net/wiki/spaces/KB/pages/1467056889/Using+SAML+Proxying+in+the+Shibboleth+IdP+to+connect+with+Azure+AD) to provide a reference link.

[![Diagram that shows Shibboleth used as a SAML proxy provider.](media/multilateral-federation-solution-two/azure-ad-shibboleth-as-sp-proxy.png)](media/multilateral-federation-solution-two/azure-ad-shibboleth-as-sp-proxy.png#lightbox)

Because Microsoft Entra ID is the primary IdP, all student and faculty apps are integrated with Microsoft Entra ID. All Microsoft 365 Apps are also integrated with Microsoft Entra ID. If Microsoft Entra Domain Services is in use, it also is synchronized with Microsoft Entra ID.

The SAML proxy feature of Shibboleth integrates with Microsoft Entra ID. In Microsoft Entra ID, Shibboleth appears as a non-gallery enterprise application. Universities can get single sign-on (SSO) for their CAS apps and can participate in the InCommon environment. Additionally, Shibboleth provides integration for Lightweight Directory Access Protocol (LDAP) directory services.

## Advantages

Advantages of using this solution include:

- **Cloud authentication for all apps:** All apps authenticate through Microsoft Entra ID.
- **Ease of execution:** This solution provides short-term ease of execution for universities that are already using Shibboleth.

## Considerations and trade-offs

Here are some of the trade-offs of using this solution:

- **Higher complexity and security risk:** An on-premises footprint might mean higher complexity for the environment and extra security risks, compared to a managed service. Increased overhead and fees might also be associated with managing on-premises components.
- **Suboptimal authentication experience:** For multilateral federation and CAS apps, the authentication experience for users might not be seamless because of redirects through Shibboleth. The options for customizing the authentication experience for users are limited.
- **Limited third-party multifactor authentication integration:** The number of integrations available to third-party multifactor authentication solutions might be limited.
- **No granular Conditional Access support:** Without granular Conditional Access support, you have to choose between the least common denominator (optimize for less friction but have limited security controls) or the highest common denominator (optimize for security controls at the expense of user friction). Your ability to make granular decisions is limited.

## Migration resources

The following resources can help with your migration to this solution architecture.

| Migration resource | Description |
| --- | --- |
| [Resources for migrating applications to Microsoft Entra ID](../identity/enterprise-apps/migration-resources) | List of resources to help you migrate application access and authentication to Microsoft Entra ID |
| [Configuring Shibboleth as a SAML proxy](https://shibboleth.atlassian.net/wiki/spaces/KB/pages/1467056889/Using+SAML+Proxying+in+the+Shibboleth+IdP+to+connect+with+Azure+AD) | Shibboleth article that describes how to use the SAML proxying feature to connect the Shibboleth IdP to Microsoft Entra ID |
| [Microsoft Entra multifactor authentication deployment considerations](../identity/authentication/howto-mfa-getstarted) | Guidance for configuring Microsoft Entra multifactor authentication |