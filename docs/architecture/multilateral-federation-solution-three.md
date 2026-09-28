---
layout: Conceptual
title: 'Solution 3: Microsoft Entra ID with AD FS and Shibboleth - Microsoft Entra | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multilateral-federation-solution-three
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: This article describes design considerations for using Microsoft Entra ID with AD FS and Shibboleth as a multilateral federation solution for universities.
ms.topic: concept-article
ms.date: 2023-04-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: cb5bfed0-0b4e-32e7-c340-b4bcddb55c81
document_version_independent_id: 9f769519-92a8-7039-15a0-4bf9db87bdf2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multilateral-federation-solution-three.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multilateral-federation-solution-three
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multilateral-federation-solution-three.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3fd31205-2280-6832-baa6-16d0bb94da4c
---

# Solution 3: Microsoft Entra ID with AD FS and Shibboleth - Microsoft Entra | Microsoft Learn

In Solution 3, the federation provider is the primary identity provider (IdP). In this example, Shibboleth is the federation provider for the integration of multilateral federation apps, on-premises Central Authentication Service (CAS) apps, and any Lightweight Directory Access Protocol (LDAP) directories.

[![Diagram that shows a design integrating Shibboleth, Active Directory Federation Services, and Microsoft Entra ID.](media/multilateral-federation-solution-three/shibboleth-adfs-azure-ad.png)](media/multilateral-federation-solution-three/shibboleth-adfs-azure-ad.png#lightbox)

In this scenario, Shibboleth is the primary IdP. Participation in multilateral federations (for example, with InCommon) is done through Shibboleth, which natively supports this integration. On-premises CAS apps and the LDAP directory are also integrated with Shibboleth.

Student apps, faculty apps, and Microsoft 365 Apps are integrated with Microsoft Entra ID. Any on-premises instance of Active Directory is synced with Microsoft Entra ID. Active Directory Federation Services (AD FS) provides integration with third-party multifactor authentication. AD FS performs protocol translation and enables certain Microsoft Entra features, such as Microsoft Entra join for device management, Windows Autopilot, and passwordless features.

## Advantages

Here are some of the advantages of using this solution:

- **Customized authentication:** You can customize the experience for multilateral federation apps through Shibboleth.
- **Ease of execution:** The solution is simple to implement in the short term for institutions that already use Shibboleth as their primary IdP. You need to migrate student and faculty apps to Microsoft Entra ID and add an AD FS instance.
- **Minimal disruption:** The solution allows third-party multifactor authentication. You can keep existing multifactor authentication solutions, such as Duo, in place until you're ready for an update.

## Considerations and trade-offs

Here are some of the trade-offs of using this solution:

- **Higher complexity and security risk:** An on-premises footprint might mean higher complexity for the environment and extra security risks, compared to a managed service. Increased overhead and fees might also be associated with managing on-premises components.
- **Suboptimal authentication experience:** For multilateral federation and CAS apps, there's no cloud-based authentication mechanism and there might be multiple redirects.
- **No Microsoft Entra multifactor authentication support:** This solution doesn't enable Microsoft Entra multifactor authentication support for multilateral federation or CAS apps. You might miss potential cost savings.
- **No granular Conditional Access support:** The lack of granular Conditional Access support limits your ability to make granular decisions.
- **Significant ongoing staff allocation:** IT staff must maintain infrastructure and software for the authentication solution. Any staff attrition might introduce risk.

## Migration resources

The following resources can help with your migration to this solution architecture.

| Migration resource | Description |
| --- | --- |
| [Resources for migrating applications to Microsoft Entra ID](../identity/enterprise-apps/migration-resources) | List of resources to help you migrate application access and authentication to Microsoft Entra ID |