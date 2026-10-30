---
layout: Conceptual
title: NIST authenticator assurance levels with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/nist-about-authenticator-assurance-levels
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: An overview of authenticator assurance levels as applied to Microsoft Entra ID
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2022-11-23T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 8620cfc7-7318-46ac-7296-a34dd349c0a6
document_version_independent_id: 7e815906-9b80-5ae1-cec5-81ec7a06fc27
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/nist-about-authenticator-assurance-levels.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/nist-about-authenticator-assurance-levels
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/nist-about-authenticator-assurance-levels.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1dfa24d0-0f48-4593-a687-9f21a6d0ca2c
---

# NIST authenticator assurance levels with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

The National Institute of Standards and Technology (NIST) develops technical requirements for US federal agencies implementing identity solutions. [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html) has the technical guidelines for digital authentication implementation, using an authenticator assurance levels (AALs) framework. AALs characterize the authentication strength of a digital identity. You can also learn about authenticator lifecycle management, including revocation.

The standard includes AAL requirements for the following categories:

- Permitted authenticator types
- Federal Information Processing Standards 140 (FIPS 140) verification level. FIPS 140 requirements are satisfied by [FIPS 140-2](https://csrc.nist.gov/publications/detail/fips/140/2/final), or newer revisions.
- Reauthentication
- Security controls
- Man-in-the-middle (MitM) resistance
- Verifier-impersonation resistance (phishing resistance)
- Verifier-compromise resistance
- Replay resistance
- Authentication intent
- Records retention policy
- Privacy controls

## NIST AALs in your environment

In general, AAL1 isn't recommended because it accepts password-only solutions, the most easily compromised authentication. For more information, see the blog post, [Your Pa$$word doesn't matter](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984).

While NIST doesn't require verifier impersonation (credential phishing) resistance until AAL3, we advise you to address this threat at all levels. You can select authenticators that provide verifier impersonation resistance, such as requiring devices are joined to Microsoft Entra ID or hybrid Microsoft Entra ID. If you're using Office 365, you can use Office 365 Advanced Threat Protection, and its [anti-phishing policies](/en-us/microsoft-365/security/office-365-security/anti-phishing-policies-about).

As you evaluate the needed NIST AAL for your organization, consider whether your entire organization must meet NIST standards. If there are specific user groups and resources that can be segregated, you can apply NIST AAL configurations to those user groups and resources.

Tip

We recommend you meet at least AAL2 + phishing resistance. If necessary, meet AAL3 for business reasons, industry standards, or compliance requirements.

## Security controls, privacy controls, records retention policy

From the Joint Authorization Board, Azure and Azure Government have provisional authority to operate (P-ATO) at the [NIST SP 800-53 High Impact](https://nvd.nist.gov/800-53/Rev4/impact/high) level. This FedRAMP accreditation authorizes Azure and Azure Government to process highly sensitive data.

Important

Azure and Azure Government certifications satisfy the security controls, privacy controls, and records retention policy requirements for AAL1, AAL2, and AAL3.

The FedRAMP audit of Azure and Azure Government included the information security management system for infrastructure, development, operations, management, and support of in-scope services. When a P-ATO is granted, a cloud service provider requires an authorization (an ATO) from government agencies it works with. Government agencies, or organizations, can use the Azure P-ATO in their security authorization process, and use it as the basis for issuing an agency ATO that meets FedRAMP requirements.

Azure supports multiple services at FedRAMP High Impact. FedRAMP High in the Azure public cloud meets the needs of US government customers, however agencies with more stringent requirements use Azure Government. Azure Government safeguards include heightened personnel screening. In Azure Government, Microsoft lists available Azure public services, up to the FedRAMP High boundary, and services for the current year.

In addition, Microsoft is committed to [protecting and managing customer data](https://www.microsoft.com/trust-center/privacy/data-management) with clearly stated records retention policies. Microsoft has a large compliance portfolio. To see more, go to [Microsoft compliance offerings](/en-us/compliance/regulatory/offering-home).