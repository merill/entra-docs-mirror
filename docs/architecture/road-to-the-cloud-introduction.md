---
layout: Conceptual
title: Road to the cloud - Introduction to moving identity and access management from AD to Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/road-to-the-cloud-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn how to plan a migration of IAM from Active Directory to Microsoft Entra ID.
documentationCenter: ''
ms.topic: how-to
ms.date: 2023-07-27T00:00:00.0000000Z
ms.custom: references_regions
ms.subservice: architecture
locale: en-us
document_id: e2b57dfb-d61f-2666-e9c6-a53a94f7de19
document_version_independent_id: b2778047-b4fd-afd7-302e-ed8d03fc7057
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/road-to-the-cloud-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/road-to-the-cloud-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/road-to-the-cloud-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 91afe1e3-9b7b-f221-ca4b-75a41b323d67
---

# Road to the cloud - Introduction to moving identity and access management from AD to Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Organizations are increasingly modernizing identity, access, and device management by reducing their dependence on on-premises Active Directory and adopting cloud-native capabilities in Microsoft Entra ID. Whether the goal is complete Active Directory retirement or a smaller, more secure on-premises footprint, this guidance helps you plan and execute that transformation.

This content provides guidance to move:

- *From* Active Directory and other non-cloud-based services, either on-premises or infrastructure as a service (IaaS), that provide identity management (IDM), identity and access management (IAM), and device management.
- *To* Microsoft Entra ID and other Microsoft cloud-native solutions for IDM, IAM, and device management.

Note

In this content, *Active Directory* refers to Windows Server Active Directory Domain Services.

Transformation must be aligned with and achieve business objectives, including increased productivity, reduced costs and complexity, and improved security posture. To better understand the costs versus value of moving to the cloud, see [Forrester TEI for Microsoft Entra ID](https://www.microsoft.com/security/business/forrester-tei-study) and [Cloud economics](https://azure.microsoft.com/overview/cloud-economics/).

## The AD minimization journey

Moving from Active Directory to Microsoft Entra ID progresses through five stages. Each stage describes where your environment is on the journey and is paired with a single strategic phase that describes the primary focus of work in that stage. Across every stage, three streams of progress (users and groups, applications, and devices) advance, and they can move independently of one another. 

1. **Cloud Attached (Identification):** Establish a baseline by discovering your current identity, application, and device landscape. Active Directory Domain Services remains authoritative while cloud identity is attached but not yet primary. The focus is on visibility and determining which workloads are ready to move.
2. **Hybrid (Modernization):** Move beyond synchronizing identities and begin using cloud identity to strengthen security, resilience, and user experience while on-premises environments remain in place. Identify dependent apps and services, and enable capabilities such as conditional access and self-service password reset.
3. **Cloud-First (Adoption):** Treat Microsoft Entra ID as the default authority for new investments and shift the identity control plane to the cloud. New users, groups, applications, and devices are provisioned as cloud-native by default.
4. **On-premises AD minimized (Reduction):** Reduce Active Directory from a default dependency to an exception. Actively shrink the on-premises footprint by replacing legacy workloads with cloud alternatives and migrating identity lifecycle workflows to Microsoft Entra ID.
5. **Cloud Only (Optimization):** Remove remaining on-premises identity dependencies and operate identity as a fully cloud-native service. All users, groups, and devices are managed in Microsoft Entra ID, enabling Active Directory to be decommissioned. Moving from Active Directory to Microsoft Entra ID progresses through five stages. Each stage describes where your environment is on the journey and is paired with a single strategic phase that describes the primary focus of work in that stage. Across every stage, three streams of progress (users and groups, applications, and devices) advance, and they can move independently of one another.