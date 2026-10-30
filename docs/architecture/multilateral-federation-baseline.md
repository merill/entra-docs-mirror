---
layout: Conceptual
title: University multilateral federation baseline design - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multilateral-federation-baseline
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn about a baseline design for a multilateral federation solution for universities.
ms.topic: concept-article
ms.date: 2023-04-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: dd693117-0cc2-2302-3c8c-c4dd616575a0
document_version_independent_id: bc181284-a95f-eeb5-0339-80399dfd4444
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multilateral-federation-baseline.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multilateral-federation-baseline
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multilateral-federation-baseline.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 80fd6319-9602-f056-e817-468c96f86fe0
---

# University multilateral federation baseline design - Microsoft Entra | Microsoft Learn

Microsoft often speaks with research universities that operate in hybrid environments in which applications are either cloud-based or hosted on-premises. In both cases, applications can use various authentication protocols. In some cases, these protocols are reaching end of life or aren't providing the required level of security.

[![Diagram of a typical university architecture, including cloud and on-premises areas with trust, synchronization, and credential validation paths.](media/multilateral-federation-baseline/typical-baseline-environment.png)](media/multilateral-federation-baseline/typical-baseline-environment.png#lightbox)

Applications drive much of the need for different authentication protocols and different identity management (IdM) mechanisms.

In research university environments, research apps often drive IdM requirements. A university might use a federation provider, such as Shibboleth, as a primary identity provider (IdP). If so, Microsoft Entra ID is often configured to federate with Shibboleth. If Microsoft 365 Apps are also in use, Microsoft Entra ID enables you to configure integration.

Applications used in research universities operate in various parts of the overall IT footprint:

- Research and multilateral federation applications are available through InCommon and eduGAIN.
- Library applications provide access to electronic journals and other e-content providers.
- Some applications use legacy authentication protocols such as Central Authentication Service to enable single sign-on.
- Student and faculty applications often use multiple authentication mechanisms. For example, some are integrated with Shibboleth or other federation providers, whereas others are integrated with Microsoft Entra ID.
- Microsoft 365 applications are integrated with Microsoft Entra ID.
- Windows Server Active Directory might be in use and synchronized with Microsoft Entra ID.
- Lightweight Directory Access Protocol (LDAP) is in use at many universities that might have an external LDAP directory or identity registry. These registries are often used to house confidential attributes, role hierarchy information, and even certain types of users, such as applicants.
- On-premises Active Directory, or an external LDAP directory, is often used to enable single-credential sign-in for non-web applications and various non-Microsoft operating system sign-ins.

## Baseline architecture challenges

Baseline architectures often evolve over time, introducing complexity and rigidness to the design and the ability to update. Some of the challenges with using the baseline architecture include:

- **Hard to react to new requirements:** Having a complex environment makes it hard to quickly adapt and keep up with the most recent regulations and requirements. For example, if you have apps in lots of locations, and these apps are connected in different ways with different IdMs, you have to decide where to locate multifactor authentication services and how to enforce multifactor authentication.

    Higher education also experiences fragmented service ownership. The people responsible for key services such as enterprise resource planning, learning management systems, division, and department solutions might resist efforts to change or modify the systems that they operate.
- **Can't take advantage of all Microsoft 365 capabilities for all apps** (for example, Intune, Conditional Access, passwordless): Many universities want to move toward the cloud and use their existing investments in Microsoft Entra ID. However, with a different federation provider as their primary IdP, universities can't take advantage of all the Microsoft 365 capabilities for the rest of their apps.
- **Complexity of a solution:** There are many components to manage. Some components are in the cloud, and some are on-premises or in infrastructure as a service (IaaS) instances. Apps are operated in many places. From a user perspective, this experience can be disjointed. For example, users sometime see a Shibboleth sign-in page and other times see a Microsoft Entra sign-in page.

We present three solutions to solve these challenges, while also addressing the following requirements:

- Ability to participate in multilateral federations such as InCommon and eduGAIN
- Ability to support all types of apps (even apps that require legacy protocols)
- Ability to support external directories and attribute stores

We present the three solutions in order, from most preferred to least preferred. Each satisfies requirements but introduces tradeoff decisions that are expected in a complex architecture. Based on your requirements and starting point, select the one that best suits your environment. We also provide a decision tree to aid in this decision.