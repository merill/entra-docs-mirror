---
layout: Conceptual
title: Configure Microsoft Entra ID for HIPAA compliance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/hipaa-configure-for-compliance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Introduction for guidance on how to configure Microsoft Entra ID for HIPAA compliance level.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, jricketts
ms.date: 2023-04-13T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 6e28462d-eb7b-5b6b-a367-ab928a3aeb8a
document_version_independent_id: de5d2f01-6a50-bf48-edb8-946995da442a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/hipaa-configure-for-compliance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/hipaa-configure-for-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/hipaa-configure-for-compliance.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2edfdcaf-bce0-3a39-5730-9777cef54f15
---

# Configure Microsoft Entra ID for HIPAA compliance - Microsoft Entra | Microsoft Learn

Microsoft services such as Microsoft Entra ID can help you meet identity-related requirements for the Health Insurance Portability and Accountability Act of 1996 (HIPAA).

The HIPAA Security Rule (HSR) establishes standards to protect individuals’ electronic personal health information that is created, received, used, or maintained by a covered entity. The HSR is managed by the U.S. Department of Health and Human Services (HHS) and requires appropriate administrative, physical, and technical safeguards to ensure the confidentiality, integrity, and security of electronic protected health information.

Technical safeguards requirements and objectives are defined in Title 45 of the Code of Federal Regulations (CFRs). Part 160 of Title 45 provides the general administrative requirements, and Part 164’s subparts A and C describe the security and privacy requirements.

Subpart § 164.304 defines technical safeguards as the technology and the policies and procedures for its use that protect electronic protected health information and control access to it. The HHS also outlines key areas for healthcare organizations to consider when implementing HIPAA technical safeguards. From [§ 164.312 Technical safeguards](https://www.ecfr.gov/current/title-45/section-164.312):

- **Access controls** - Implement technical policies and procedures for electronic information systems that maintain electronic protected health information to allow access only to those persons or software programs that have been granted access rights as specified in [§ 164.308(a)(4)](https://www.ecfr.gov/current/title-45/section-164.308).
- **Audit controls** - Implement hardware, software, and/or procedural mechanisms that record and examine activity in information systems that contain or use electronic protected health information.
- **Integrity controls** - Implement policies and procedures to protect electronic protected health information from improper alteration or destruction.
- **Person or entity authentication** - Implement procedures to verify that a person or entity seeking access to electronic protected health information is the one claimed.
- **Transmission security** - Implement technical security measures to guard against unauthorized access to electronic protected health information that is being transmitted over an electronic communications network.

The HSR defines subparts as standard, along with required and addressable implementation specifications. All must be implemented. The "addressable" designation denotes a specification is reasonable and appropriate. Addressable doesn't mean that an implementation specification is optional. Therefore, subparts that are defined as addressable are also required.

The remaining articles in this series provide guidance and links to resources, organized by key areas and technical safeguards. For each key area, there's a table with the relevant safeguards listed, and links to Microsoft Entra guidance to accomplish the safeguard.

## Learn more

- [HHS Zero Trust in Healthcare pdf](https://www.hhs.gov/sites/default/files/zero-trust.pdf)
- [Combined regulation text](https://www.hhs.gov/hipaa/for-professionals/privacy/laws-regulations/combined-regulation-text/index.html) of all HIPAA Administrative Simplification Regulations found at 45 CFR 160, 162, and 164
- [Code of Federal Regulations (CFR) Title 45](https://www.ecfr.gov/current/title-45) describing the public welfare portion of the regulation
- [Part 160](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-160?toc=1) describing the general administrative requirements of Title 45
- [Part 164](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164) Subparts A and C describing the security and privacy requirements of Title 45
- [HIPAA Security Risk Safeguard Tool](https://www.healthit.gov/topic/privacy-security-and-hipaa/security-risk-assessment-tool)
- [NIST HSR Toolkit](http://scap.nist.gov/hipaa/)