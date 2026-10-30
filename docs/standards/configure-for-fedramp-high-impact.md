---
layout: Conceptual
title: Configure Microsoft Entra ID to meet FedRAMP High Impact level - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/configure-for-fedramp-high-impact
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Overview of how you can meet a FedRAMP High Impact level for your organization by using Microsoft Entra ID.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2023-03-09T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 5557666d-8064-8962-4f60-fd5409c8d887
document_version_independent_id: 7eb49a66-0267-be4f-918f-0c109084773f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/configure-for-fedramp-high-impact.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/configure-for-fedramp-high-impact
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/configure-for-fedramp-high-impact.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7a6fe3b9-d125-e15d-f757-5374019b551e
---

# Configure Microsoft Entra ID to meet FedRAMP High Impact level - Microsoft Entra | Microsoft Learn

The [Federal Risk and Authorization Management Program](https://www.fedramp.gov/) (FedRAMP) is an assessment and authorization process for cloud service providers (CSPs). Specifically, the process is for CSPs that create cloud solution offerings (CSOs) for use with federal agencies. Azure and Azure Government have earned a [Provisional Authority to Operate (P-ATO) at the High Impact level](/en-us/compliance/regulatory/offering-fedramp) from the Joint Authorization Board, the highest bar for FedRAMP accreditation.

Azure provides the capability to fulfill all control requirements to achieve a FedRAMP high rating for your CSO, or as a federal agency. It's your organization’s responsibility to complete additional configurations or processes to be compliant. This responsibility applies to both CSPs seeking a FedRAMP high authorization for their CSO, and federal agencies seeking an Authority to Operate (ATO).

## Microsoft and FedRAMP

Microsoft Azure supports more services at [FedRAMP High Impact](/en-us/azure/azure-government/compliance/azure-services-in-fedramp-auditscope) levels than any other CSP. And while this level in the Azure public cloud meets the needs of many US government customers, agencies with more stringent requirements might rely on the Azure Government cloud. Azure Government provides additional safeguards, such as the heightened screening of personnel.

Microsoft is required to recertify its cloud services each year to maintain its authorizations. To do so, Microsoft continuously monitors and assesses its security controls, and demonstrates that the security of its services remains in compliance. For more information, see [Microsoft cloud services FedRAMP authorizations](https://marketplace.fedramp.gov/), and [Microsoft FedRAMP Audit Reports](https://aka.ms/MicrosoftFedRAMPAuditDocuments). To receive other FedRAMP reports, send email to [Azure Federal Documentation](mailto:AzFedDoc@microsoft.com).

There are multiple paths towards FedRAMP authorization. You can reuse the existing authorization package of Azure and the guidance here to significantly reduce the time and effort required to obtain an ATO or a P-ATO.

## Scope of guidance

The FedRAMP high baseline is made up of 421 controls and control enhancements from [NIST 800-53 Security Controls Catalog Revision 4](https://csrc.nist.gov/pubs/itlb/2015/01/release-of-nist-special-publication-80053a-revisio/final). Where applicable, we included clarifying information from the [800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final). This article set covers a subset of these controls that are related to identity, and which you must configure.

We provide prescriptive guidance to help you achieve compliance with controls you're responsible for configuring in Microsoft Entra ID. To fully address some identity control requirements, you might need to use other systems. Other systems might include a security information and event management tool, such as Microsoft Sentinel. If you're using Azure services outside of Microsoft Entra ID, there will be other controls you need to consider, and you can use the capabilities Azure already has in place to meet the controls.

The following is a list of FedRAMP resources:

- [Federal Risk and Authorization Management Program](https://www.fedramp.gov/)
- [Agency Guide for FedRAMP Authorizations](https://www.fedramp.gov/assets/resources/documents/Agency_Authorization_Playbook.pdf)
- [Managing compliance in the cloud at Microsoft](https://www.microsoft.com/trustcenter/common-controls-hub)
- [Microsoft Government Cloud](https://go.microsoft.com/fwlink/p/?linkid=2087246)
- [Azure Compliance Offerings](https://aka.ms/azurecompliance)
- [FedRAMP High Azure Policy built-in initiative definition](/en-us/azure/governance/policy/samples/fedramp-high)
- [Microsoft Purview portal](/en-us/purview/purview-portal)
- [Microsoft Purview Compliance Manager](/en-us/purview/compliance-manager)